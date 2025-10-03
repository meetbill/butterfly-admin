# butterfly-admin
基于 amis 并适配 butterfly 的后台模板
![pangu-list](https://github.com/meetbill/meetbill_static/blob/master/butterfly_admin/pangu-list.png?raw=true)

# 1 部署
```
butterfly-admin
├── conf                                    // nginx 配置文件
│   ├── mime.types
│   └── nginx.conf
├── logs                                    // nginx 日志
├── run.sh
├── sbin
│   └── nginx
├── static                                  // butterfly-admin static
│   ├── logo
│   └── pages
└── templates                               // butterfly-admin templates
    ├── favicon.ico
    ├── index_sso.html                      // 用于单点登录场景
    ├── index_pangu.html                    // 可页面管理，页面 json 存储在数据库中
    └── index.html
```

## 1.1 编译 nginx
[编译 nginx](https://github.com/meetbill/op_practice_book/blob/master/doc/web/nginx.md)
```
$ # 通过 CC 环境变量指定 GCC(可选)，如果在低版本的 Centos 上编译，可以指定下 GCC
$ CC=/opt/compiler/gcc-8.2/bin/gcc

$ # 下载 pcre(让 Nginx 支持 Rewrite 功能)
$ wget https://github.com/PCRE2Project/pcre2/releases/download/pcre2-10.46/pcre2-10.46.tar.gz
$ tar -zxf pcre2-10.46.tar.gz

$ wget http://nginx.org/download/nginx-1.29.1.tar.gz
$ tar -zxf nginx-1.29.1.tar.gz
$ ./configure --prefix=../nginx_output --with-pcre=../pcre2-10.46 --with-http_auth_request_module --with-http_stub_status_module
$ make
$ make install
```
将编译后的 ../nginx_output/sbin/nginx 放到 butterfly-admin/sbin 目录

## 1.2 下载 amis jssdk(可选)
```
$ cd butterfly-admin/static
$ mkdir jssdk && cd jssdk
$ wget https://github.com/baidu/amis/releases/download/6.13.0/jssdk.tar.gz
$ tar -zxf jssdk.tar.gz
```
如下载 amis jssdk，需要将 templates 中依赖的 6.13.0 相关部分替换为 `static/jssdk/xxx`

# 2 帮助
> * [AMIS 示例](https://aisuda.bce.baidu.com/amis/examples/index)
> * [AMIS 可视化编辑器](https://aisuda.github.io/amis-editor-demo/#/hello-world) 页面数据保存在本地浏览器中

# 3 进阶
## 3.1 单点登录
https://meetbill.gitbook.io/butterfly-user-doc/fe/butterfly-admin/sso

## 3.2 页面管理
https://meetbill.gitbook.io/butterfly-user-doc/fe/butterfly-admin/pangu
