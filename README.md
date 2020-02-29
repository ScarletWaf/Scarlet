# ScarletWaf 简要开发手册

## 0x00 前言

去年代码参考：

https://github.com/AnneviLL/So_FK_Vgtb

去年的项目由于管理端api也使用了lua编写，导致waf的核心功能与后端没有分离出来，因此今年需要将waf核心部分与主控部分完全分离开，这样更加利于维护和使用。

## 0x01 人员分工

waf核心：柳文浩 谭敬元 王邦耀

管理平台后端：王硕 张皓晨

管理平台前端：蔡祖润、李欣悦

具体工作可以摇摆

## 0x02 技术栈 开发环境

### waf核心模块

Ubuntu 18.04

openresty + lua + redis

##### 安装Openresty

```bash
# 安装导入 GPG 公钥时所需的几个依赖包（整个安装过程完成后可以随时删除它们）：
sudo apt-get -y install --no-install-recommends wget gnupg ca-certificates

# 导入 GPG 密钥：
wget -O - https://openresty.org/package/pubkey.gpg | sudo apt-key add -

# 安装 add-apt-repository 命令
# （之后可以删除这个包以及对应的关联包）
sudo apt-get -y install --no-install-recommends software-properties-common

# 添加官方 official APT 仓库：
sudo add-apt-repository -y "deb http://openresty.org/package/ubuntu $(lsb_release -sc) main"

# 更新 APT 索引：
sudo apt-get update

# 安装openrsty
sudo apt-get -y install openresty
```

##### 学习资料

https://github.com/openresty/lua-nginx-module

https://moonbingbing.gitbooks.io/openresty-best-practices/ngx_lua

### waf管理web端

#### 方案1 [Golang] 🌟

golang(gin) + vue.js

优势： 可编译为二进制程序运行 部署方便 运行更加安全

https://geektutu.com/post/quick-go-gin.html

#### 方案2 [php] ❌

php(ci) + vue.js

https://codeigniter.org.cn/user_guide/index.html

## 0x03 架构

### waf 核心

```
├── access.lua
├── conf
│   └── nginx.conf
├── config.lua
├── init.lua
├── log.lua
├── rules
│   ├── args.lua
│   ├── body.lua
│   ├── cc.lua
│   ├── cookie.lua
│   ├── ip.lua
│   ├── ua.lua
│   └── url.lua
└── waf_core.lua
```

日志记录需使用单独日志服务器

### waf 管理web端



###  一键部署

包括一键部署脚本 蜜罐一键部署 主要目的是尽可能的实现傻瓜式部署



## 0x04 接口文档 （初稿）

### 基础信息



### 修订记录

| 时间 | 原内容 | 修订后 |
| :--: | :----: | :----: |
|      |        |        |
|      |        |        |

### 接口信息 例如：

#### POST `admin/login` 管理员登陆

提交数据：

```json
{
  "username":"admin",
  "password":"admin123"
}
```

备注： 密码位数大于6位，必须大小写字母+数字....

返回：

```json
{
  "msg":"ok",
  "error":0,
  "data":"admin, Welcome to Scarlet waf system"
}
```

---

