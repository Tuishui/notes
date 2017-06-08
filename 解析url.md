##通过创建链接标签实现url解析@https://www.lyblog.net/category/webfront.html
  通常在处理url解析，前端会创建一个a标签m，通过浏览器解析url。实现代码如下：  
  ```
  function parseUrl(url){
    var anchor = document.createElement('a');
      anchor.href = url;
    var path = anchor.pathname,
        search = anchor.search,
        query = null;
        if(search){
          var keyValue = search.replace(/^\?/,'').split('&'),
              tempValue ;
          query = {};
            for(var i = 0, j = keyValue.length; i < j; i++){
              tempvalue = keyValue[i].split('=');
              query[tempValue[0]] = tempValue[1];
            }
        }
        var defaultPort = {
          'http:':80,
          'https:':433,
          'ftp:':21,
          'gopher:':70,
          "ws:":80,
          "wws:":443
        };
        return{
          href:anchor.href,
          protocol:anchor.protocol,
          host:anchor.host,
          hostname:anchor.hostname,
          path:path + search,
          port:anchor.port || defaultPort[anchor.protocol] || "",

          pathname:path,
          hash:anchor.hash,
          search:search,
          query:query
        };
  }
  ```

##DOM节点的增、删、改、查  
（1）创建新的节点  
```
creatDocumentFragment()  //创建一个DOM片段
createElement_x()  //创建一个具体的元素
creatTextNode（）  //创建一个文本节点
```
（2）增添、删除、替换、插入
```
appendChild()
removeChild()
replaceChild()
insertBefore()
```
(3) 查找
getElementsByTagName() // 通过标签名称
getElementsByName()  //通过元素的Name属性值
getElementById()  //通过元素id，唯一性


Root element  <--------------------------  
<site>                                  |  
   |            firstChild                ------------  
   |-------------------------------  element:        |  
   |                                 <camnpr>        |  
   |                                     |           |  
   |                     nextSibling     |           |  
   |                                                 |  
   |--------------------------------  element:       |  
   |                                  <camnpr>       |  childNodes to  
   |                                                 |  <site> and siblings  
   |                  previousSibling    |           |  to each other  
   |                                     |           |  
   |---------------------------------  element:      |  
   |                                   <camnpr>      |  
   |                                                 |  
   |             lastChild                           |  
   |---------------------------------  element:      |  
   |                                   <camnpr>      |  
                                            ----------
