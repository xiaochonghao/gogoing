## 装饰器

* list\_route与detail\_route的区别就是 list\_route 的参数不包含 pk（对应 list），而 detail\_route 包含pk（对应 retrieve）。看一段代码就懂了：

  ```py
  @list_route(methods=['post', 'delete'], url_path='')
  def custom_handler(self, request):
      pass
  ```

  ```py
  @detail_route(methods=['get'], url_path='')
  def custom_handler(self, request, pk=None):
      pass
  ```
