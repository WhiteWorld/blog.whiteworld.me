{
    "date": "2015-01-22",
    "description": null,
    "draft": false,
    "id": 9,
    "image": null,
    "meta_title": null,
    "slug": "server-blog-with-github-and-gitcafe",
    "tags": [
        "Blog",
        "GitHub",
        "GitCafe",
        "Jekyll"
    ],
    "title": "\u540c\u65f6\u4f7f\u7528 GitHub \u548c GitCafe \u6258\u7ba1\u535a\u5ba2",
    "type": "post"
}


### 方案

使用Jektyll+GitHubPages方案，Markdown格式，Git管理，简单高效。缺点是GitHub服务器在国外，国内访问速度慢，以及有被墙的风险。参考网上的解决方案，把博客同时部署在GitHubPages和GitcafePages上。设置域名的DNS解析线路，让国内的线路访问国内的GitcafePages的IP，国外的线路访问国外的GitHubPages的IP，做到国内国外访问都很快。

### 步骤

1. 分别创建GitHub（[参考](https://pages.github.com/)）和Gitcafe（[参考](https://gitcafe.com/GitCafe/Help/wiki/Pages-%E7%9B%B8%E5%85%B3%E5%B8%AE%E5%8A%A9# wiki)）项目。GitHub如果选个人主页的话对应的分支名是master，如果选择项目主页对应的分支名是gh-pages;Gitcafe现在只有个人主页对应的分支名是gitcafe-pages。
2. 安装jekyll，参考[Jekyll 安装](http://jekyllrb.com/docs/installation/)和[Jekyllbootstrap](http://jekyllbootstrap.com/usage/jekyll-quick-start.html)。
3. 设置域名绑定
  - GitHub上绑定自定义域名。在项目根目录下创建CNAME文件，把自己的域名写进去。
  - Gitcafe上绑定自定义域名。在Gitcafe网站上的项目设置菜单中添加自己的域名。
4. 设置域名DNS。DNSPod上设置DNS记录，添加域名A记录，把域名的电信、联通、教育网线路指向GitCafe的IP地址，把默认线路指向GitHub的IP地址。
5. 设置项目的git remote url。GitHub和GitCafe的项目Git地址都作为remote url。在`.git/config`文件添加一个alias([参考](http://liberize.me/tech/host-your-blog-on-both-github-and-gitcafe.html))，让一条`git publish`命令就可以push到Github和GitCafe上。