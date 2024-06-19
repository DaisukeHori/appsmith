以下は、NginxおよびAppsmithの設定を含む完全な手順書です。

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

#### 6. Nginxの既存プロセスの停止
```bash
sudo systemctl stop nginx
sudo killall nginx || true
```

#### 7. Nginxの設定ファイルを作成
```bash
sudo tee /etc/nginx/sites-available/appsmith.conf <<EOF
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


sudo ln -s /etc/nginx/sites-available/appsmith.conf /etc/nginx/sites-enabled/
sudo rm /etc/nginx/sites-enabled/default
```

#### 8. SSL証明書の取得
```bash
sudo certbot --nginx -d app.revol-one.com
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
