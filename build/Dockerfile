FROM axizdkr/tengine:2.3.2
ADD nginx-upsync-module-master /usr/src/tengine-2.3.2/modules/nginx-upsync-module
ADD ngx_devel_kit-0.3.0.tar.gz /usr/src/tengine-2.3.2/modules/
ADD luajit2-2.1-agentzh /tmp/luajit2-2.1-agentzh/
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories && apk add --no-cache --virtual .build-deps gcc libc-dev  make  openssl-dev  pcre-dev  zlib-dev  linux-headers  curl  libxslt-dev  gd-dev  geoip-dev  
RUN cd /tmp/luajit2-2.1-agentzh/ && make && make install PREFIX=/usr/local/LuaJIT && rm -rf /tmp/luajit2-2.1-agentzh/
RUN export LUAJIT_LIB=/usr/local/LuaJIT/lib && export LUAJIT_INC=/usr/local/LuaJIT/include/luajit-2.1 && \
cd /usr/src/tengine-2.3.2/ && ./configure --prefix=/etc/nginx --sbin-path=/usr/sbin/nginx --modules-path=/usr/lib/nginx/modules --conf-path=/etc/nginx/nginx.conf --error-log-path=/var/log/nginx/error.log --http-log-path=/var/log/nginx/access.log --pid-path=/var/run/nginx.pid --lock-path=/var/run/nginx.lock --http-client-body-temp-path=/var/cache/nginx/client_temp --http-proxy-temp-path=/var/cache/nginx/proxy_temp --http-fastcgi-temp-path=/var/cache/nginx/fastcgi_temp --http-uwsgi-temp-path=/var/cache/nginx/uwsgi_temp --http-scgi-temp-path=/var/cache/nginx/scgi_temp --user=nginx --group=nginx --with-http_ssl_module --with-http_realip_module --with-http_addition_module --with-http_sub_module --with-http_dav_module --with-http_flv_module --with-http_mp4_module --with-http_gunzip_module --with-http_gzip_static_module --with-http_random_index_module --with-http_secure_link_module --with-http_stub_status_module --with-http_auth_request_module --with-http_xslt_module=dynamic --with-http_image_filter_module=dynamic --with-http_geoip_module=dynamic --with-threads --with-stream --with-stream_ssl_module --with-stream_ssl_preread_module --with-stream_realip_module --with-stream_geoip_module=dynamic --with-http_slice_module --with-mail --with-mail_ssl_module --with-compat  --with-http_v2_module \
--add-module=modules/ngx_http_upstream_check_module \
--add-module=modules/headers-more-nginx-module-0.33 \
--add-module=modules/ngx_http_upstream_session_sticky_module \
--add-module=/usr/src/tengine-2.3.2/modules/nginx-upsync-module \
--add-module=/usr/src/tengine-2.3.2/modules/ngx_http_lua_module \
--with-ld-opt="-Wl,-rpath,$LUAJIT_LIB" \
--add-module=/usr/src/tengine-2.3.2/modules/ngx_devel_kit-0.3.0 && \
make && make install

CMD ["nginx", "-g", "daemon off;"]