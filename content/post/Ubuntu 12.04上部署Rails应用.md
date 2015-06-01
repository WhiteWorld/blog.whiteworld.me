{
    "date": "2015-01-22",
    "description": null,
    "draft": false,
    "id": 6,
    "image": null,
    "meta_title": null,
    "slug": "deploy-rails-on-ubuntu",
    "tags": [
        "Ubuntu",
        "Deploy",
        "Rails",
        "Ruby"
    ],
    "title": "Ubuntu 12.04\u4e0a\u90e8\u7f72Rails\u5e94\u7528",
    "type": "post"
}


有几种方式可以把Rails程序部署在Linux系统上

+ 使用Nginx + Passenger方式
  - 步骤
    基本步骤参考: [Ubuntu 12.04 上使用 Nginx Passenger 部署 Ruby on Rails ](https://github.com/ruby-china/ruby-china/wiki/Ubuntu-12.04-%E4%B8%8A%E4%BD%BF%E7%94%A8-Nginx-Passenger-%E9%83%A8%E7%BD%B2-Ruby-on-Rails )
  - 注意
    - 如果提示没有安装JS运行环境，则可安装nodejs解决 `sudo apt-get install nodejs`
    - 默认Passenger以Production方式运行Rails程序，如果要以Development方式运行，在nginx的配置文件example.com.conf中加入一行，` rails_env development;`
    - 如果使用VPS，很可能VPS没有swap分区，导致Rails运行不了。我用的[阿里云](http://www.aliyun.com/ "阿里云")和[Digital Ocean](https://www.digitalocean.com/?refcode=ed2350733151 "Digital Ocean推荐注册链接") 。Ubuntu 12.04都没有使用swap分区，这时就需要创建swap分区，参考[How To Add Swap on Ubuntu 12.04](https://www.digitalocean.com/community/tutorials/how-to-add-swap-on-ubuntu-12-04)创建即可。
+ 待续


