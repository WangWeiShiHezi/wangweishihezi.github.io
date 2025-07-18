```
docker run -d \
  --name libretv \
  --restart unless-stopped \
  -p 8899:8080 \
  -e PASSWORD=your_password \
  -e ADMINPASSWORD=your_adminpassword \
  bestzwei/libretv:latest

``` 



对接影视接口
饭团影视  `https://www.fantuan.tv/api.php/provide/vod/`
影视工厂  `https://cj.lziapi.com/api.php/provide/vod/`
七七资源  `https://www.qiqidys.com/api.php/provide/vod/`
