# douban-movie
### 关于如何将代码书写更具逻辑性
- 先写出核心代码，并将其封装，然后根据各核心代码作用，再分别写出相应的函数
``` App = {
init: function(){
this.bind()
this.start()
this.top250Page()
},
bind:function(){},
start:function(){},
tkop250Page(){}
}
```
### 相关注意：
- 在对象内部的this直接指代该对象
- 对于构建拉动条，在容器元素上面加上css样式 `  overflow:scroll;`即可
- 对于拉动拉动条触发的事件，可以使用函数节流，防止触发频率过高
``` 
$('main').on('scroll',function(){
    if(clock){
        clearTimeout
    }
    clock = setTimeout(function(){
        if($('main').height()+$('main').scrollTop() >= $('section').eq(0).height())
        _this.start()
    },300)
    }             
    ) 
   ```
    
-  对于ajax的请求，可以给ajax加上锁，防止在一次请求还没有完成的时候同步发生多次请求；
```
      $.ajax({
      url:'https:api.douban.com/v2/movie/top250',
      method:'GET',
      data:{
          start: _this.index,
          count: 20,
      },
      dataType:'JSONP',
  }).done(function(ret){
      console.log(ret)
      _this.setData(ret)
      _this.index += 20
      console.log(_this.index)
  }).fail(function(){
      console.log('error')
  }).always(function(){
      _this.isLoading = false
      $('.loading').fadeOut()
        console.log(_this.isLoading)
  })   
  ```
  
  - 将dom对象变成jQuery对象，可以使用如下方法，并使用jQuery方法中的find方法来查找jQuery中的相关元素
  ```
   var $node = $(tpl)
  $node.find('a').attr('href',movie.alt)
  ```
  
  - jQuery中的方法和dom对象中的方法有明显的不同：
  this与$(this)两者可以使用的方法差异很大，一种是dom对象一种是jQuery对象；在jQuery对象中遍历使用`each`方法，在dom 对象中使用`forEach`方法

