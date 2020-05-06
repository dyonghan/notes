# RESTful API

## 概览

### method

|方法|描述|
|:---|:---|
|GET（SELECT）|从服务器取出资源（一项或多项）|
|POST（CREATE）|在服务器新建一个资源|
|PUT（UPDATE）|在服务器更新资源（客户端提供改变后的完整资源）|
|PATCH（UPDATE）|在服务器更新资源（客户端提供改变的属性）|
|DELETE（DELETE）|从服务器删除资源|

### path

|URL|Method|Description|
|:--|:-----|:----------|
|/users/|GET|Gives a list of all users|
|/users/|POST|Creates a new user|
|/users/<id>|GET|Shows a single user|
|/users/<id>|PUT|Updates a single user|
|/users/<id>|DELETE|Deletes a single user|

#### status code

|Code|Status|Method|Situation|
|:---|:-----|:-----|:--------|
||**Successful 2xx**|||
|200|OK|GET POST||
|201|Created|||
|204|No Content|POST PUT||
|205|Reset Content|DELETE||
||**Client Error 4xx**|||
|400|Bad Request|||
|401|Unauthorized|||
|403|Forbidden|||
|404|Not Found|||
|413|Request Entity Too Large|POST|Upload a file|
|415|Unsupported Media Type|POST|Upload a file|
||**Server Error 5xx**|||
|500|Internal Server Error|||
|502|Bad Gateway||Use a flow|

## url规则

URL rules that end with a slash are branch URLs, others are leaves. If you have strict_slashes enabled (which is the default), all branch URLs that are matched without a trailing slash will trigger a redirect to the same URL with the missing slash appended.

Take these two rules:
```python
@app.route('/projects/')
def projects():
    return 'The project page'

@app.route('/about')
def about():
    return 'The about page'
```
Though they look rather similar, they differ in their use of the trailing slash in the URL definition. In the first case, the canonical URL for the projects endpoint has a trailing slash. In that sense, it is similar to a folder on a file system. Accessing it without a trailing slash will cause Flask to redirect to the canonical URL with the trailing slash.

In the second case, however, the URL is defined without a trailing slash, rather like the pathname of a file on UNIX-like systems. Accessing the URL with a trailing slash will produce a 404 “Not Found” error.

This behavior allows relative URLs to continue working even if the trailing slash is ommited, consistent with how Apache and other servers work. Also, the URLs will stay unique, which helps search engines avoid indexing the same page twice.
