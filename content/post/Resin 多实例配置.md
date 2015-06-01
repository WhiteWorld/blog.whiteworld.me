{
    "date": "2015-01-22",
    "description": null,
    "draft": false,
    "id": 5,
    "image": null,
    "meta_title": null,
    "slug": "resin-multiple-instance",
    "tags": [
        "Resin"
    ],
    "title": "Resin \u591a\u5b9e\u4f8b\u914d\u7f6e",
    "type": "post"
}


```xml
<cluster id="app-id"><!-- 保证这个id不与其他的cluster重复，建议用名字和业务的组合 -->
    <root-directory>.</root-directory>
        <server-default>
          <http address="*" port="9000"/><!-- 保证这个port没被使用 -->
          <jvm-arg>-Xms2048M</jvm-arg>
          <jvm-arg>-Xmx2048M</jvm-arg>
          <jvm-arg>-XX:MaxPermSize=128M</jvm-arg>
          <jvm-arg>-XX:PermSize=128M</jvm-arg>
        </server-default>
        <server id="app-id" address="127.0.0.1" port="6831"></server><!-- 保证id不与其他的server重复，这个id就是启动server的参数。保证port没被使用 -->
        <host id="" root-directory=".">
          <!-- root-directory 设置为自己的文件夹里webapps文件夹下的目录。 archie-path 设置为war下的目标war文件，war文件名要与root-directory目录一致 -->
          <web-app id="/" root-directory="/home/work/deploy/someone/webapps/miui-sec-api" archive-path="/home/work/deploy/someone/war/miui-sec-api.war" />
          <!-- 设置log存放路径 -->
          <stdout-log path="/home/work/deploy/someone/logs/app.stdout.log" rollover-period='1D' rollover-size='50mb'/>
          <stderr-log path="/home/work/deploy/someone/logs/app.stderr.log" rollover-period='1D' rollover-size='50mb'/>
    </host>
</cluster>
```