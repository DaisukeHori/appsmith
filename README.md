以下は、NginxおよびAppsmithの設定を含む完全な手順書です。




```
ip-172-31-37-255 (Ubuntu 24.04 64bit / Linux 6.8.0-1008-aws)                                                                                                                              Uptime: 0:31:37

AMD EPYC 7571                                                            CPU ↓     3.3%  idle    97.1%  ctx_sw    699         MEM -   42.0%  active   1.67G         SWAP -   0.0%         LOAD -  2core
CPU  [||                                                         3.3%]   user      1.7%  irq      0.0%  inter     501         total   3.76G  inacti   1.57G         total       0         1 min    0.71
MEM  [||||||||||||||||||||||||                                  42.0%]   system    0.5%  nice     0.0%  sw_int    165         used    1.58G  buffer   81.1M         used        0         5 min    0.47
SWAP [                                                           0.0%]   iowait    0.2%  steal    0.5%                        free    2.18G  cached   2.21G         free        0         15 min   0.33

NETWORK                  Rx/s   Tx/s   TASKS 136 (365 thr), 1 run, 82 slp, 53 oth Threads sorted automatically by CPU consumption
br-3ba0a75040fd            0b     0b
ens5                      5Kb   84Kb   CPU%   MEM%  VIRT  RES       PID USER          TIME+ THR  NI S  R/s W/s  Command ('e' to pin | 'k' to kill)
lo                         0b     0b   >3.4   1.2   202M  46.5M    8313 ubuntu         0:01 1     0 R    0 0    python3 /usr/bin/glances
veth8ca49de                0b     0b    1.0   3.7   1.71G 141M     5591 root           0:07 64    0 S    ? ?    mongod --port 27017 --dbpath . --logpath /appsmith-stacks/logs/mongodb/db.log --replSet m
                                        0.5   18.6  3.56G 717M     5593 root           1:29 61    0 S    ? ?    java --add-opens java.base/java.time=ALL-UNNAMED --add-opens java.base/java.nio=ALL-UNNAM
DefaultGateway                  12ms    0.5   1.2   1.79G 45.9M    2602 root           0:01 9     0 S    ? ?    containerd
                                        0.5   0.2   47.6M 6.12M    5590 root           0:00 4     0 S    ? ?    redis-server *:6379
DISK I/O                  R/s    W/s    0.5   0.1   81.0M 3.88M     648 root           0:00 2     0 S    ? ?    irqbalance
nvme0n1                     0   374K    0.0   3.4   635M  132M     7681 root           0:01 6     0 S    ? ?    fwupd
nvme0n1p1                   0   374K    0.0   2.4   2.11G 92.3M    2740 root           0:41 12    0 S    ? ?    dockerd -H fd:// --containerd=/run/containerd/containerd.sock
nvme0n1p14                  0      0    0.0   2.1   998M  80.2M    5592 root           0:00 7     0 S    ? ?    node server.js
nvme0n1p15                  0      0    0.0   1.1   1.21G 43.1M    5594 root           0:00 9     0 S    ? ?    caddy run --config /tmp/appsmith/Caddyfile
nvme0n1p16                  0      0    0.0   1.1   198M  42.7M    8097 root           0:00 1     0 S    ? ?    python3 /usr/bin/glances -s -B 127.0.0.1
                                        0.0   0.8   1.90G 30.2M     666 root           0:00 11    0 S    ? ?    snapd
FILE SYS                 Used  Total    0.0   0.7   209M  27.2M    5595 sshd           0:00 1     0 S    ? ?    postgres -D /appsmith-stacks/data/postgres/main -c listen_addresses=127.0.0.1
/ (nvme0n1p1)           5.84G  28.0G    0.0   0.7   282M  26.5M     176 root           0:00 7     0 S    ? ?    multipathd -d -s
                                        0.0   0.6   28.8M 23.8M    3750 root           0:01 1     0 S    ? ?    python3 /usr/bin/supervisord -n
SENSORS                                 0.0   0.6   107M  22.2M     704 root           0:00 2     0 S    ? ?    python3 /usr/share/unattended-upgrades/unattended-upgrade-shutdown --wait-for-signal
Composite                      -273C    0.0   0.5   31.7M 20.2M     654 root           0:00 1     0 S    ? ?    python3 /usr/bin/networkd-dispatcher --run-startup-triggers
                                        0.0   0.5   364M  20.0M    8272 root           0:00 4     0 S    ? ?    packagekitd
                                        0.0   0.5   1.75G 18.1M     987 root           0:01 9     0 S    ? ?    amazon-ssm-agent
                                        0.0   0.4   49.3M 13.9M     139 root           0:00 1     0 S    ? ?    systemd-journald
                                        0.0   0.3   22.2M 13.4M       1 root           0:06 1     0 S    ? ?    init
                                        0.0   0.3   458M  13.1M     670 root           0:00 6     0 S    ? ?    udisksd
                                        0.0   0.3   21.1M 12.5M     332 systemd-r      0:00 1     0 S    ? ?    systemd-resolved
                                        0.0   0.3   311M  12.1M     830 root           0:00 4     0 S    ? ?    ModemManager
                                        0.0   0.3   1.18G 11.9M    3729 root           0:00 11    0 S    ? ?    containerd-shim-runc-v2 -namespace moby -id 39a14c0e0a969f6d38c9404344094a992c00307c5a6db
                                        0.0   0.3   19.6M 10.9M    1412 ubuntu         0:00 1     0 S    ? ?    systemd --user
                                        0.0   0.2   21.9M 9.50M     531 systemd-n      0:00 1     0 S    ? ?    systemd-networkd
                                        0.0   0.2   209M  9.44M    5642 sshd           0:00 1     0 S    ? ?    postgres: walwriter 
                                        0.0   0.2   374M  9.18M     657 polkitd        0:00 4     0 S    ? ?    polkitd --no-debug
                                        0.0   0.2   12.6M 8.88M    5589 root           0:00 1     0 S    ? ?    python3 -m supervisor.appsmith_supervisor_stdout
                                        0.0   0.2   17.6M 8.50M     632 root           0:00 1    -1 S    ? ?    systemd-logind
                                        0.0   0.2   14.4M 8.24M    1065 root           0:00 1     0 S    ? ?    sshd: ubuntu [priv]
                                        0.0   0.2   210M  8.19M    5643 sshd           0:00 1     0 S    ? ?    postgres: autovacuum launcher 
                                        0.0   0.2   13.0M 8.12M    3524 www-data       0:00 1     0 S    ? ?    nginx: worker process
                                        0.0   0.2   13.0M 8.12M    3525 www-data       0:00 1     0 S    ? ?    nginx: worker process
                                        0.0   0.2   26.0M 8.07M     203 root           0:00 1     0 S    ? ?    systemd-udevd
                                        0.0   0.2   11.7M 7.75M    1064 root           0:00 1     0 S    ? ?    sshd: /usr/sbin/sshd -D -o AuthorizedKeysCommand /usr/share/ec2-instance-connect/eic_run_
                                        0.0   0.2   209M  7.31M    5639 sshd           0:00 1     0 S    ? ?    postgres: checkpointer 
                                        0.0   0.2   210M  7.31M    5646 sshd           0:00 1     0 S    ? ?    postgres: logical replication launcher 
                                        0.0   0.2   14.6M 6.78M    1517 ubuntu         0:00 1     0 S    ? ?    sshd: ubuntu@pts/0
                                        0.0   0.2   209M  6.56M    5640 sshd           0:00 1     0 S    ? ?    postgres: background writer 
                                        0.0   0.2   217M  5.88M     758 syslog         0:00 4     0 S    ? ?    rsyslogd -n -iNONE
                                        0.0   0.1   67.1M 5.44M    5644 sshd           0:00 1     0 S    ? ?    postgres: stats collector 
                                        0.0   0.1   9.68M 5.25M     638 messagebu      0:00 1     0 S    ? ?    @dbus-daemon --system --address=systemd: --nofork --nopidfile --systemd-activation --sysl
                                        0.0   0.1   8.85M 5.00M    1520 ubuntu         0:00 1     0 S    ? ?    -bash
                                        0.0   0.1   8.85M 5.00M    2935 ubuntu         0:00 1     0 S    0 0    bash
                                        0.0   0.1   1.59G 4.25M    3709 root           0:00 7     0 S    ? ?    docker-proxy -proto tcp -host-ip 0.0.0.0 -host-port 8080 -container-ip 172.18.0.2 -contai
                                        0.0   0.1   1.59G 3.75M    3715 root           0:00 7     0 S    ? ?    docker-proxy -proto tcp -host-ip :: -host-port 8080 -container-ip 172.18.0.2 -container-p
                                        0.0   0.1   18.9M 3.50M     765 _chrony        0:00 1     0 S    ? ?    chronyd -F 1
                                        0.0   0.1   20.6M 3.43M    1413 ubuntu         0:00 1     0 S    ? ?    (sd-pam)
                                        0.0   0.1   79.9M 2.80M    7726 root           0:00 1     0 S    ? ?    gpg-agent --homedir /var/lib/fwupd/gnupg --use-standard-socket --daemon
                                        0.0   0.1   7.05M 2.62M     637 root           0:00 1     0 S    ? ?    cron -f -P
                                        0.0   0.1   6.41M 2.38M    2934 ubuntu         0:00 1     0 S    ? ?    newgrp docker
                                        0.0   0.1   10.8M 2.14M     772 _chrony        0:00 1     0 S    ? ?    chronyd -F 1
                                        0.0   0.1   6.00M 2.00M    1002 root           0:00 1     0 S    ? ?    agetty -o -p -- \u --keep-baud 115200,57600,38400,9600 - vt220
                                        0.0   0.1   11.1M 1.99M    3523 root           0:00 1     0 S    ? ?    nginx: master process /usr/sbin/nginx -g daemon on; master_process on;
                                        0.0   0.0   2.66M 1.88M     633 root           0:00 1     0 S    ? ?    acpid
                                        0.0   0.0   5.96M 1.88M    1009 root           0:00 1     0 S    ? ?    agetty -o -p -- \u --noclear - linux
                                        0.0   0.0   0     0           2 root           0:00 1     0 S    ? ?    [kthreadd]
                                        0.0   0.0   0     0           3 root           0:00 1     0 S    ? ?    [pool_workqueue_release]
                                        0.0   0.0   0     0           4 root           0:00 1   -20 I    ? ?    [kworker/R-rcu_g]
                                        0.0   0.0   0     0           5 root           0:00 1   -20 I    ? ?    [kworker/R-rcu_p]
                                        0.0   0.0   0     0           6 root           0:00 1   -20 I    ? ?    [kworker/R-slub_]
                                        0.0   0.0   0     0           7 root           0:00 1   -20 I    ? ?    [kworker/R-netns]
                                        0.0   0.0   0     0          10 root           0:00 1   -20 I    ? ?    [kworker/0:0H-events_highpri]
                                        0.0   0.0   0     0          11 root           0:01 1     0 I    ? ?    [kworker/u4:0-flush-259:0]
                                        0.0   0.0   0     0          12 root           0:00 1   -20 I    ? ?    [kworker/R-mm_pe]
```

### NginxおよびAppsmith設定の完全な手順書

#### 1. 古いDocker関連パッケージの削除
```bash
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove -y $pkg || true; done
```

#### 2. 必要なパッケージのインストール
```bash
sudo apt-get update
sudo apt-get install -y ca-certificates curl git
```

#### 3. Dockerのインストール
```bash
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update
sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

#### 4. ユーザーをDockerグループに追加
```bash
sudo usermod -aG docker $USER
newgrp docker
```

#### 5. CertbotのインストールとSSL証明書の取得
```bash
sudo apt-get install -y certbot python3-certbot-nginx
```


#### 6. SSL証明書の取得
```bash
sudo certbot --nginx -d app.revol-one.com
```

#### 7. Nginxの設定ファイルを作成
```bash
sudo tee /etc/nginx/sites-available/appsmith.conf <<'EOF'
server {
    listen 80;
    server_name app.revol-one.com;

    location / {
        return 301 https://$host$request_uri;
    }
}

server {
    listen 443 ssl;
    server_name app.revol-one.com;

    ssl_certificate /etc/letsencrypt/live/app.revol-one.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/app.revol-one.com/privkey.pem;
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_prefer_server_ciphers on;
    ssl_ciphers "EECDH+AESGCM:EDH+AESGCM:AES256+EECDH:AES256+EDH";

    location / {
        proxy_pass http://localhost:8080;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
EOF



sudo ln -s /etc/nginx/sites-available/appsmith.conf /etc/nginx/sites-enabled/
sudo rm /etc/nginx/sites-enabled/default
```

#### 8. Nginxの既存プロセスの停止
```bash
sudo systemctl stop nginx
sudo killall nginx || true
```

#### 9. Nginxの再起動
```bash
sudo systemctl restart nginx
```

#### 10. Appsmithのインストール
```bash
mkdir ~/appsmith
cd ~/appsmith

sudo tee docker-compose.yml <<EOF
services:
  appsmith:
    image: index.docker.io/appsmith/appsmith-ce
    container_name: appsmith
    ports:
      - "8080:80"
    volumes:
      - ./stacks:/appsmith-stacks
    restart: unless-stopped
EOF

docker compose up -d
```

#### 11. ブラウザでアクセス確認
ブラウザで `https://app.revol-one.com` にアクセスし、Appsmithが正常に動作していることを確認します。

これで、NginxおよびAppsmithのセットアップが完了です。問題が発生した場合は、各コマンドの出力を確認して原因を特定してください。
