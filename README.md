# 宝塔搭建个人自助云面板，支持Azure Aws Do、Linode等云厂商

 安装最新宝塔
```
https://bt.sy/bbs/forum-37-1.html
```
安装docker（请勿安装宝塔自带的Docker，存在问题，建议手动安装）
```
bash <(curl https://get.docker.com)
```
安装Mysql5.6或Mysql5.7
新建数据库

![image](https://user-images.githubusercontent.com/55003092/202548791-a1952113-9c2f-441a-acdc-9a69aea30013.png)

部署容器 (8111端口可改为任意，此处为实际对外端口)
```
docker run --name cloudpanel -d -it -p 8111:80 --restart=always cdntip/panel /bin/bash
```

 进入容器
```
docker exec -it cdntip /bin/bash
```
修改数据库信息
```
vi config/database.conf
```
![image](https://user-images.githubusercontent.com/55003092/202548258-b8efd278-c3df-484f-b6f9-14985742d139.png)

保存文件，Ctrl+D,退出容器，重启容器：
```
docker restart cloudpanel
```
查看容器日志
```
docker logs -f cloudpanel
```
![image](https://user-images.githubusercontent.com/55003092/202546952-c037ef4b-3c89-4e92-b0d7-64f2ebfa49d2.png)

创建管理员
```
docker exec -it cloudpanel /bin/bash #进入docker
python3 manage.py createsuperuser    # 创建管理员命令， 根据提示创建即可


添加aws镜像
```
python manage.py aws_update_images
```

# 其他功能
停止当前容器 
```
docker stop panel
```
删除当前容器
```
docker rm panel
```
# 演示效果
![image](https://user-images.githubusercontent.com/55003092/202330238-0ba46d1b-4e22-407f-b02f-bf4802a3f85e.png)

