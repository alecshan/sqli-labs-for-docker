# Sqli labs for Docker

---
使用 docker 建立学习 sqli-labs 的虚拟环境，无需 docker 知识，运行简单命令即可。

## sqli-labs简介

对于想要学习web安全的同学, 这是一个非常好的学习有关SQL注入的学习资料。类似于闯关的模式, 每一个关卡都有非常多的思路和利用方式。这些关卡包含了各种常见的SQL注入姿势:
 * 明注
 * 盲注
 * 基于bool
 * 基于时间
 * 基于报错

> [sqli-labs 地址](https://github.com/Audi-1/sqli-labs)

## 安装 docker-compose

在 arch linux 下安装 docker / docker-compose:

```bash
curl -s https://bootstrap.pypa.io/get-pip.py | python3

# 安装最新版 docker
curl -s https://get.docker.com/ | sh

# 启动 docker 服务
systemctl start docker.service

# 安装 docker-compose
pip install docker-compose
```
其他操作系统安装 docker 和 docker-compose 请参考 Docker 文档进行安装。
安装 docker-compose 时，建议使用 aliyun 的 docker 镜像服务，大学的 docker 镜像服务可能没有包含 docker-compose。

## Usage

1. clone this repository.
```bash
git clone https://github.com/alecshan/sqli-labs-for-docker
```

2. edit config in `.env`. (optional)

3. run it!
```bash
docker-compose up -d
```

4. 然后在浏览器中访问 : http://127.0.0.1:8080/ , 就可以看到启动的页面了

5. 点击 “Setup/reset Database for labs” 进行数据库初始化，返回再点击各个关卡即可开始解题。

6. 测试完成后，停止环境
```bash
docker-compose down
```

## docker-compose 代码说明

1. 从github上克隆sqli-labs仓库
```bash
git clone https://github.com/Audi-1/sqli-labs.git
```

2. 进入sqli-labs目录, 修改数据库配置文件 `code/sqli-labs/sql-connections/db-creds.inc`.
```php
<?php
//give your mysql connection username n password
$dbuser ='root';
$dbpass ='root';
$dbname ="security";
$host = 'db';
$dbname1 = "challenges";
?>
```

3. 拉起一个 mysql 数据库实例

4. sqli-labs 代码目录会挂载到 apache 的 web 目录(默认为: /var/www/html/)
```dockerfile
volumes:
      - ./code/sqli-labs:/var/www/html
```

5. 启动 apache web 服务器

## Tip
1. You can view/edit valnerable code in `code/sqli-labs`.
2. You can connect mysql server on port `8989`.

## 参考资料 :
1. [WangYihang/sqli-labs](https://github.com/WangYihang/sqli-labs)
2. [gr4vit0n/sqli-labs-solution](https://github.com/gr4vit0n/sqli-labs-solution)
3. [0xs1riu5/sqli-writeup](https://github.com/0xs1riu5/sqli-writeup)
