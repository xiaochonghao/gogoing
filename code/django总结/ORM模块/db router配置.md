## settings.py

1. 配置`DATABASES`
    ```python
    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.mysql',
            'HOST': os.environ.get('FLOW_HOST', '101.251.234.164'),
            'PORT': 3306,
            'NAME': os.environ.get('FLOW_DB_NAME', 'flow_snmp'),
            'USER': os.environ.get('FLOW_DB_USER', 'root'),
            'PASSWORD': os.environ.get('FLOW_DB_PASSWORD', '4CbPsJJo'),
            'CHARSET': 'utf-8'
        },
        'cloud': {
            'ENGINE': 'django.db.backends.mysql',
            'HOST': os.environ.get('CLOUD_HOST', '101.251.234.164'),
            'USER': os.environ.get('CLOUD_DB_USER', 'root'),
            'PASSWORD': os.environ.get('CLOUD_DB_PASSWORD', '4CbPsJJo'),
            'NAME': os.environ.get('CLOUD_DB_NAME', 'cdscp_trunk'),
            'PORT': 3306,
            'CHARSET': 'utf-8',
        }
    }
    ```

    default必须配置，如果不需要可以配成：`'default': {}`

    但是，为了避免调试错误（莫名原因），尽量给`default`设置值。

2. 配置数据库路由
    ```python
    # 该变量必须配，指明router类
    DATABASE_ROUTERS = ["db.db_routers.DatabaseRouter"]
    # 下面的变量用在model的Meta子类下的app_label，非必需
    DB_LABEL_FLOW = 'flow'
    DB_LABEL_CLOUD = 'cloud'
    # 用在router类中映射app_label->db name关系
    DATABASE_MAPPING = {
        # 'app_name': 'database_name'
        'flow': 'default',
        'cloud': 'cloud'
    }
    ```

## 配置路由类

```python
from django.conf import settings

DATABASE_MAPPING = settings.DATABASE_MAPPING


class DatabaseRouter(object):
    """
    配置数据库路由
    """
    def db_for_read(self, model, **hints):
        """
        Attempts to read flow_app models go to flow DB.
        :param model:
        :param hints:
        :return: settings配置的database节点名称，并非db name
        """
        if model._meta.app_label in DATABASE_MAPPING:
            return DATABASE_MAPPING[model._meta.app_label]
        return None

    def db_for_write(self, model, **hints):
        """
        Attempts to write flow_app models go to flow DB.
        :param model:
        :param hints:
        :return:
        """
        if model._meta.app_label in DATABASE_MAPPING:
            return DATABASE_MAPPING[model._meta.app_label]
        return None

    # def allow_relation(self, obj1, obj2, **hints):
    #     pass

    def allow_migrate(self, db, app_label, model_name=None, **hints):
        """Make sure that apps only appear in the related database."""
        if db in DATABASE_MAPPING.values():
            return DATABASE_MAPPING.get(app_label) == db
        elif app_label in DATABASE_MAPPING:
            return False
        return None

    # def allow_syncdb(self, db, model):
    #     return False
```