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
> * (1) [编译 nginx](https://github.com/meetbill/op_practice_book/blob/master/doc/web/nginx.md)
> * (2) 将编译后的 nginx 放到 butterfly-admin/sbin 目录

# 2 帮助
> * [AMIS 示例](https://aisuda.bce.baidu.com/amis/examples/index)
> * [AMIS 可视化编辑器](https://aisuda.github.io/amis-editor-demo/#/hello-world) 页面数据保存在本地浏览器中

# 3 进阶
## 3.1 单点登录
https://meetbill.gitbook.io/butterfly-user-doc/fe/butterfly-admin/sso

## 3.2 页面管理
https://meetbill.gitbook.io/butterfly-user-doc/fe/butterfly-admin/pangu
