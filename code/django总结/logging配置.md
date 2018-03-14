### logger的日志级别

* DEBUG：用于调试目的的底层系统信息

* INFO：普通的系统信息

* WARNING：表示出现一个较小的问题。

* ERROR：表示出现一个较大的问题。

* CRITICAL：表示出现一个致命的问题。

### logging的组成

* 记录器 ：loggers
* 处理程序：handlers
* 过滤器：filters
* 格式化：formatters

### admin\_log

* 表:`django\_admin\_log`
* 根据LogEntry log_action\(\)函数仿写一个admin\_log.py，重新定义各个函数:

  ```py
  source_code:

  ADDITION = 1
  CHANGE = 2
  DELETION = 3
  class LogEntryManager(models.Manager):
        use_in_migrations = True

  def log_action(self, user_id, content_type_id, object_id, object_repr, action_flag, change_message=''):
        e = self.model(
            None, None, user_id, content_type_id, smart_text(object_id),
            object_repr[:200], action_flag, change_message
        )
        e.save()
  ```

  ```py
  write admin_log.py

  from django.contrib.contenttypes.models import ContentType
  from django.contrib.admin.models import LogEntry, ADDITION, CHANGE, DELETION
  from django.utils.encoding import force_text
  # 将任何对象转成字符串

  LOGIN = 4
  LOGOUT = 5

  ACTION_FLAG = ((ADDITION, u'增加'),\
                 (CHANGE， u'修改'),\
                 (DELETION, u'删除'),\
                 (LOGIN, u'登录'),\
                 (LOGOUT, u'注销'))

  def get_content_type_for_model(obj):
      """
      Takes either a model class or an instance of a model, and returns the ContentType instance representing that model. for_concrete_model=False allows fetching the ContentType of a proxy mod
      """
      return ContentType.objects.get_for_model(obj, for_concrete_model=False)

  def log_change(request, object, message):
      """
      Log that an object has been successfully changed.

      The default implementation creates an admin LogEntry object.

      example:
      change_message = '描述信息'
      log_change(request, object, change_message)
      """
      ip = request.META['REMOTE_ADDR']
      LogEntry.objects.log_action(
          user_id=request.user.pk,
          content_type_id=get_content_type_for_model(object).pk,
          object_id=object.pk,
          object_repr=force_text(object),
          action_flag=CHANGE,
          change_message=u'%s IP:%s' % (message, ip)
      )
  ```
