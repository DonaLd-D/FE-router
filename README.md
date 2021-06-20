# frontend_router 前端路由

  1. **hash**  **hashchange**事件
  ```
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>router</title>
  </head>
  <body>
      <div>
          <ul>
              <li><a data-url='/aa'>aaa</a></li>
              <li><a data-url='/bb'>bbb</a></li>
              <li><a data-url='/cc'>ccc</a></li>
          </ul>
      </div>
      <div id="content">内容</div>
  </body>
  <script>
      let _routerData=[{
          path:'/aa',pathData:'aaa页面'
      },{
          path:'/bb',pathData:'bbb页面'
      },{
          path:'/cc',pathData:'ccc页面'
      }]

      let _aBtn=document.getElementsByTagName('a')
      let _content=document.querySelector('#content')

      let _path
      for(let i=0;i<_aBtn.length;i++){
          _aBtn[i].addEventListener('click',function(){
              _path=this.getAttribute('data-url')
              window.location.hash=_path
          })
      }

      window.addEventListener('hashchange',()=>{
          _routerData.map(item=>{
              if(_path===item.path){
                  _content.innerHTML=item.pathData
              }
          })
      })
  </script>
  </html>
  ```

  2. **history**  **popstate**事件
  ```
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>router</title>
  </head>
  <body>
      <div>
          <ul>
              <li><a data-url='/aa'>aaa</a></li>
              <li><a data-url='/bb'>bbb</a></li>
              <li><a data-url='/cc'>ccc</a></li>
          </ul>
      </div>
      <div id="content">内容</div>
  </body>
  <script>
      let _routerData=[{
          path:'/aa',pathData:'aaa页面'
      },{
          path:'/bb',pathData:'bbb页面'
      },{
          path:'/cc',pathData:'ccc页面'
      }]

      function refreshFn(_path){
          _routerData.map(item=>{
              if(_path==item.path){
                  _content.innerHTML=item.pathData
              }
          })
      }

      let _aBtn=document.getElementsByTagName('a')
      let _content=document.querySelector('#content')
      let _path
      for(let i=0;i<_aBtn.length;i++){
          _aBtn[i].addEventListener('click',function(){
              _path=this.getAttribute('data-url')

              history.pushState(null,null,_path)
              refreshFn(_path)
          })
      }

      window.addEventListener('popstate',()=>{
          console.log(location.pathname)
          refreshFn(location.pathname)
      })
  </script>
  </html>
  ```
