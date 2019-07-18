var http = require('http')      //加载HTTP模块
var fs = require('fs')          //加载fs模块
var url = require('url')        //加载url模块



http.createServer(function(req, res){           //创建服务器

  var pathObj = url.parse(req.url, true)        //对用户请求的url进行处理

  switch (pathObj.pathname) {                   //匹配用户的url并进行对应输出
    case '/getWeather':
      var ret
      if(pathObj.query.city == 'beijing'){
        ret = {
          city: 'beijing',
          weather: '晴天'
        }
      }else{
        ret = {
          city: pathObj.query.city,
          weather: '不知道'
        }
      }
      res.end(JSON.stringify(ret))
      break;
    case '/user/123':

      res.end( fs.readFileSync(__dirname + '/static/user.tpl' ))          
      break;
    default:  
      res.end( fs.readFileSync(__dirname + '/static' + pathObj.pathname) )     //如果是静态，直接读取对应文件
  }
}).listen(8080)
