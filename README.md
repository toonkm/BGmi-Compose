#BGmi-Compose

使用docker-compose的BGmi一鍵包

使用鏡像:

toonkm/BGmi, Nginx, Transmission

## 特色

 - 開箱即用
 - 前端，後端和BT端獨立分開，有需要可以自行更換

## 安裝

服務啓動前記得先修改docker-compose.yml內的ADMIN_TOKEN，這個是前端管理用的

```
ADMIN_TOKEN=你的密碼
```

然後在運行
```
docker-compose up -d
```

有需要請自行修改docker-compose.yml的端口

|端口|用途|
|---|---|
|80|前端網頁|
|9091|Transmission管理頁面|
|51413|Torrent Port TCP，不建議修改|
|51413/udp|Torrent Port UDP，不建議修改|

其他事項：

Transmission前端自帶幾個主題的，有需要更換可以將修改TRANSMISSION_WEB_HOME，包括:

/combustion-release/, /transmission-web-control/ 或者 /kettu/

默認BGmi的資料會保存在./app裏，而影片和封面會保存在./data裏面，假如有需要修改位置記得把bgmi及web的路徑也修改

## 使用

由於BGmi需要使用命令行操作，使用docker-compose需要自行進入BGmi的運行環境

找到相關container id
```
$ docker container ls
d85d712274ff      bgmi-compose_bgmi       "/script/run.sh start"
```

進入相關container
```
$ docker exec -it d85 bash (假如前面幾個字符沒有重複可以不用輸入完整字句)
```

然後就可以使用bgmi的相關指令
```
bash-5.1# bgmi -h
```

相關資料可以參考[BGmi主git](https://github.com/BGmi/BGmi/blob/master/README.cn.md#使用)

## 注意事項

 - BT端會在下載完成後繼續做種，需要自行暫停或刪除
 - 訂閲後默認只會下載之後的集數，假如整套下載請在filter上調整episode參數