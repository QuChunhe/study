

####Nginx

[warn] 190987#0: *469574 a client request body is buffered to a temporary file
调整conf/nginx.conf中的参数
client_body_buffer_size 2048K;
client_max_body_size 16m;
http://nginx.org/en/docs/http/ngx_http_core_module.html#client_body_buffer_size



[warn] 190991#0: *567085 an upstream response is buffered to a temporary file 
调整conf/nginx.conf中的参数
fastcgi_buffer_size 8k;
fastcgi_buffers 256 16k;
http://nginx.org/en/docs/http/ngx_http_fastcgi_module.html#fastcgi_buffers
