{
    "date": "2015-01-22",
    "description": "Virtualenv, Nginx, Gunicorn",
    "draft": false,
    "id": 2,
    "image": null,
    "meta_title": null,
    "slug": "flask-web-development",
    "tags": [
        "Flask",
        "Web"
    ],
    "title": "\u4f7f\u7528 Flask \u5f00\u53d1 Web \u9879\u76ee\u7684\u6b65\u9aa4",
    "type": "post"
}


### 建立 Virtualenv 环境
   
```bash
# install pip
sudo apt-get install python-pip
# install virtualenvwrapper
sudo pip install virtualenvwrapper
# Add to .bashrc/.zshrc
export WORKON_HOME=$HOME/.virtualenvs
export PROJECT_HOME=$HOME/Devel
source /usr/local/bin/virtualenvwrapper.sh
mkvirtualenv tmpenv
workon tmpenv
# install flask
pip install flask
```

### 本地开发&测试

### 部署

Flask 项目的部署方案有[很多种](http://flask.pocoo.org/docs/0.10/deploying/)，这里用的是`Nginx+Gunicorn+Supervisor`的组合
```bash
# install Nginx
sudo apt-get update
sudo apt-get install nginx
sudo update-rc.d nginx defaults

# install Gunicorn/Gevent
workon tmpenv
pip install gunicorn
sudo apt-get install python-dev
pip install gevent

# install Supervisor
sudo apt-get install supervisor
# edit /etc/supervisor/supervisord.conf
supervisorctl reread
supervisorctl update

# install MySQL
sudo apt-get install mysql-server
sudo mysql_install_db
sudo mysql_secure_installation

# set default character
# http://stackoverflow.com/questions/3513773/change-mysql-default-character-set-to-utf-8-in-my-cnf
[mysqld]
collation-server = utf8_unicode_ci
init-connect='SET NAMES utf8'
character-set-server = utf8
```
