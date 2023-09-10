# ubuntu_NodeApp_sysytemctl

## Ubuntu20.04 Node.js アプリケーションのデーモン化方法

【事前事項】 //好きな場所好きな名前で大丈夫だけど今回はこの設定で行きます
ディレクトリーの位置: /opt
ディレクトリー名: service
メインファイル: index.js


1. Git clone <URL> などでファイルを用意する
2. vi /etc/systemd/system/{serviceName}.service  
iを押して編集モードへ
```
[Unit]
Description=Node.js App
After=network.target

[Service]
User= {実行ユーザー名}
WorkingDirectory=/opt/{fileName} // ファイルの場所を指定
ExecStart=/usr/local/bin/node /opt/{fileName}/index.js //メインファイルを指定
Restart=always

[Install]
WantedBy=multi-user.target
```
例
```
[Unit]
Description=Node.js App
After=network.target

[Service]
User=yuyutti
WorkingDirectory=/opt/service
ExecStart=/usr/local/bin/node /opt/service/index.js
Restart=always

[Install]
WantedBy=multi-user.target
```
編集し終わったら  
Esc :wq で保存して退出

3. systemctl enable {serviceName}.service
4. systemctl start {serviceName}.service

以上！
