### null与blank的区别

> `blank`、`null`默认都是`False`

#### `null` is for the DataBase column value

`null=True` sets `NULL` (versus `NOT NULL`) on the column in your DB. Blank values for Django field types such as `DateTimeField` or `ForeignKey` will be stored as `NULL` in the DB.

#### `blank` is for the field requirement in forms

`blank=True` determines whether the field will be required in forms. This includes the admin and your own custom forms. If `blank=True` then the field will not be required, whereas if it's `False` the field cannot be blank.

The combo of the two is so frequent because typically if you're going to allow a field to be blank in your form, you're going to also need your database to allow `NULL` values for that field. The exception is `CharField`s and `TextField`s, which in Django are never saved as NULL. Blank values are stored in the DB as an empty string (`''`).

A few examples:
```python
models.DateTimeField(blank=True) # raises IntegrityError if blank
models.DateTimeField(null=True) # NULL allowed, but must be filled out in a form
```
Obviously those two options don't make logical sense to use (though, there might be a use case for `null=True, blank=False` if you want a field to always be required in forms, but optional when dealing with an object through something like the shell.)
```python
models.CharField(blank=True) # No problem, blank is stored as ''
models.CharField(null=True) # NULL allowed, but will never be set as NULL
```
`CHAR` and `TEXT` types are never saved as `NULL` by Django, so `null=True` is unnecessary. However, you can manually set one of these fields to `None` to force set it as `NULL`. If you have a scenario where that might be necessary, you should still include `null=True`.

---

### db层次的null与空字符串的区别

如果打算搜索列值为`NULL`的列，不能使用`expr = NULL`测试。下述语句不返回任何行，这是因为，对于任何表达式，`expr = NULL`永远不为“真”： `mysql> SELECT * FROM my_table WHERE phone = NULL;` 。

要想查找`NULL`值，必须使用`IS NULL`测试。在下面的语句中，介绍了查找NULL电话号码和空电话号码的方式：

```sql
    mysql> SELECT * FROM my_table WHERE phone IS NULL; 
    mysql> SELECT * FROM my_table WHERE phone = '';
```