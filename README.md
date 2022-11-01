#基于Fabric的农产品溯源系统  

## 介绍
    
基于区块链的农产品溯源系统，分为pc端，h5端，后台采用SpringBoot，前端Vue，
区块链网络采用Fabric，一共分为六个组织节点，农户，原料厂商，生产厂商，物流厂商，零售商，消费者 .

## 软件架构

此系统有四个模块，已上传Gitee， blockchain-trace-bcnetwork ，blockchain-trace-applets ，blockchain-trace-pc ，blockchain-trace-basic-data。

    blockchain-trace-bcnetwork：区块链网络，可直接将文件上传至服务器，然后启动里面的脚本

    blockchain-trace-applets：小程序端溯源，做得十分简单

    blockchain-trace-pc：PC端,使用的是RuoYi-Vue

    blockchain-trace-basic-data：系统基础数据后台，使用的是RuoYi

    前端：Vue.js , Element UI , mpvue

    后端：SpringBoot , Mybatis , FastDFS , Node.js , Redis , MySQL

    区块链：Fabric1.2

    智能合约：Golang语言编写

    环境：Ubuntu16.04 64位(2核 4G以上)，Docker 18.09.7 , Docker-compose 1.29.1 , 

## 安装教程


1.先部署好区块链网络（blockchain-trace-bcnetwork,这里需要先拉取好所需的docker镜像，fabric-orderer,fabric-peer,fabric-couchdb,fabric-tools,
fabric-ca，然后tag为latest([拉取docker镜像命令点击此处去复制](install-fabric-env/pull-fabric-images.md)）：
将traceNetwork上传至服务器（也可自己搭建），进入basic-network目录中，启动start.sh脚本（./start.sh）,
启动成功后进入webapp目录，启动start.sh脚本（此脚本是安装智能合约，它里面包含了其他几个脚本，可以自己观看），
启动成功后看一下docker容器，不出意外的话会安装了6个chaincode,安装成功后执行node enrollAdmin.js 
和 node registerUser.js(这里如果没有生成成功，执行npm install fabric-client后再试) 生成对应的密钥文件后，
最后启动node服务，命令为 node app.js ， 
如果需要让其常驻后台，需要安装pm2，然后执行启动 pm2 start app.js  , 停止  pm2 stop app.js ， 
（环境变量需要有node，npm , golang）
    
2.系统基础数据后端 （blockchain-trace-basic-data）
配置好Redis，MySQL , FastDFS(FastDFS的地址需要修改yml文件里面的地址和代码里面，不然访问不了) , 端口为8088，（本系统全部所有服务都采用Docker部署）

3.PC端（blockchain-trace-pc）

    npm install --registry=https://registry.npm.taobao.org

    npm run dev

    npm run build:prod

4.小程序（blockchain-trace-applets）
自己使用开发者工具打开
    



    
