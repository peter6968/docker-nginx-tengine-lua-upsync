# docker-nginx-tengine-lua-upsync

基于tengine 2.3.2 
安装了
- luajit 2.1
- nginx-upsync-module 
- ngx_devel_kit-0.3.0 
- lua-nginx-module


镜像：
- docker pull peter6968/nginx-tengine-lua-upsync

使用：
- git clone https://github.com/peter6968/docker-nginx-tengine-lua-upsync.git
- cd example/tengine 
- docker-compose up -d