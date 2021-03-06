MADE BY SOOMTI

문의는 soomti@likelion.org 

------

# HTTPS RAILS Production 모드로 배포하기

## 기본세팅

```bash
$ sudo apt-get update
```

```bash
$ sudo apt-get install git-core curl zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev libcurl4-openssl-dev python-software-properties libffi-dev nodejs
```

## 루비 설치

```bash
$ git clone https://github.com/rbenv/rbenv.git ~/.rbenv
```

```bash
$ echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
```

```bash
$ echo 'eval "$(rbenv init -)"' >> ~/.bashrc
```

```bash
$ exec $SHELL
```

```bash
$ git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build
```



#### 자신 로컬의 ruby -v 해서 버전 맞춰주세요!

```bash
$ rbenv install 2.x.x
```

```bash
$ rbenv global 2.x.x
```

```bash
$ rbenv rehash
```

```bash
$ ruby -v 
```

```bash
$ echo "gem: --no-document" > ~/.gemrc
```

```bash
$ gem install bundler
```



## Rails 설치

로컬에 있는 버전 맞춰주기! 

사실 안해도 밑에서 깔리는데 안되서 여기서 한번 더 해줬습니다..

```bash
$ gem install rails -v 5.x.x --no-ri --no-rdoc
$ rbenv rehash
$ rails -v
```



## NGINX 설치

```bash
$ sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 561F9B9CAC40B2F7
```

```bash
$ sudo apt-get install -y apt-transport-https ca-certificates
```

ubuntu xenial 여서 이 주소인데, 우분투가 아니거나 하면 찾아봐야한다! 

```bash
$ sudo sh -c 'echo deb https://oss-binaries.phusionpassenger.com/apt/passenger xenial main > /etc/apt/sources.list.d/passenger.list'
```

```bash
$ sudo apt-get update
```

```bash
$ sudo apt-get install -y nginx-extras passenger
```



## CertBot 설치

```bash
$ sudo add-apt-repository ppa:certbot/certbot # Enter를 눌러준다.
```

```bash
$ sudo apt-get update
```

```bash
$ sudo apt-get install python-certbot-nginx -y
```



## NGINX 설정

```bash
$ sudo vim /etc/nginx/sites-available/default
# 41번 행의 server_name _; 의 _ 부분을 # 자신의 도메인으로 수정해준다.
 server_name example.com www.example.com;
#ESC+:wq 로 저장 및 종료한다.
```

```bash
sudo nginx -t
# nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
# nginx: configuration file /etc/nginx/nginx.conf test is successful # 라는 메세지가 정상적으로 뜨는 지 확인한다.
```

```bash
sudo systemctl reload nginx # NGINX 리로드
```



## 방화벽 업데이트

```bash
$ sudo service nginx start
```

```bash
$ sudo ufw status
# Status: inactive 라고 뜰 것이다. active로 바꾸자. 
```

```bash
$ sudo ufw enable
# y 라고 입력
```

```bash
$ sudo ufw allow 'Nginx Full'
```

```bash
$ sudo ufw allow OpenSSH
```

## 인증서 받기

```bash
# AWS 인스턴스의 IP 주소를 example.com / www.example.com 에 연결해두고 시작. 
$ sudo certbot --nginx -d example.com -d www.example.com
# email 입력
# Agree / Yes 입력
# 2 (Redirect) 입력
# 접속해보면 자동으로 https로 연결됩니다. 적용되기까지 조금 시간이 걸립니다.
# 성공적으로 인증서가 설치되면 아래와 같은 메세지가 뜹니다.
```

결과메세지 

```bash
 - Congratulations! Your certificate and chain have been saved at:
   /etc/letsencrypt/live/heejae.site/fullchain.pem
   Your key file has been saved at:
   /etc/letsencrypt/live/heejae.site/privkey.pem
   Your cert will expire on 2018-01-05. To obtain a new or tweaked
   version of this certificate in the future, simply run certbot again
   with the "certonly" option. To non-interactively renew *all* of
   your certificates, run "certbot renew"
 - If you like Certbot, please consider supporting our work by:
   Donating to ISRG / Let's Encrypt:   https://letsencrypt.org/donate
   Donating to EFF:                    https://eff.org/donate-le
```



## 보안성 강화하기

```bash
$ sudo openssl dhparam -out /etc/ssl/certs/dhparam.pem 2048
```

```bash
$ sudo nginx -t
# nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
# nginx: configuration file /etc/nginx/nginx.conf test is successful 라고 떠 야 제대로 설정이 완료된 것입니다.
```

```bash
$ sudo systemctl reload nginx # NGINX 리로드
# 이제 A등급이 됩니다.
```



## 인증서 자동 갱신 설정

```bash
$ sudo crontab -e
# 텍스트 에디터를 자유롭게 선택합니다. 저는 3의 vim을 선택합니다.
# 마지막 줄에 다음을 추가하고 저장합니다.
15 3 * * * /usr/bin/certbot renew --quiet
# 매일 갱신 명령을 수행합니다. 이는 인증서가 만료 30일 이내에 자동 갱신되고 다시 로드되게 합니다.
```

## NGINX 추가 설정

```bash
# 환경설정 파일을 엽니다.
$ sudo vim /etc/nginx/nginx.conf
# 1번째 줄을 다음으로 수정합니다. user www-data => ubuntu
user ubuntu;
#63번째 줄의#을 지워 주석을 해제하여 다음과 같은 상태가 되게 한다. 
include /etc/nginx/passenger.conf;
```

```bash
sudo vim /etc/nginx/passenger.conf
# 모든 내용을 지우고 다음 내용으로 대체합니다.
passenger_root /usr/lib/ruby/vendor_ruby/phusion_passenger/locations.ini; passenger_ruby /home/ubuntu/.rbenv/shims/ruby;
# 서버를 재시작합니다.
sudo service nginx restart
```

## 프로젝트 추가

```bash
$ git config --global color.ui true
$ git config --global user.name "깃헙 이름을 입력하세요"
$ git config --global user.email "깃헙 이메일 주소를 입력하세요"
$ ssh-keygen -t rsa -b 4096 -C "github 이메일"
```

```bash
$ cat ~/.ssh/id_rsa.pub 
```

```bash
$ ssh -T git@github.com
$ yes
```

```bash
$ git clone 복사한 주소 
```

귀찮으면 ```$ git clone 주소``` 만 해도 된다

## 프로젝트폴더 NGINX에연결

```bash
$ sudo vim /etc/nginx/sites-enabled/default 
# 37번째  즈음에 있는 root를 수정합니다.
root /home/ubuntu/[프로젝트폴더명]/public;
#위에서 수정했던 41~42번째 줄쯤에 있는 server_name 아래에 다음을 추가합니다. 
passenger_enabled on;
rails_env production;
# 바로 아래의 location / { ... } 부분을 지우고 다음을 추가하고 저장합니다.
error_page 500 502 503 504 /50x.html;
location = /50x.html {
root html; }
```

## 프로젝트 설정

```bash
$ bundle install --without development test 
$ bundle exec figaro install 
$ echo "production:" >> ./config/application.yml 
$ echo "  SECRET_KEY_BASE: $(bundle exec rake secret RAILS_ENV=production)" >> ./config/application.yml 
$ cd ..
$ bundle exec rake db:create RAILS_ENV=production
$ bundle exec rake db:migrate RAILS_ENV=production
$ bundle exec rake assets:precompile RAILS_ENV=production
```



## 오류날때

1. nginx 오류 있는지 체크

   ```bash
   $ sudo nginx -t -c /etc/nginx/nginx.conf
   # nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
   # nginx: configuration file /etc/nginx/nginx.conf test is successful
   ```

   여기서 위 메세지가 안나오고 에러메세지를 뿜으면 , 구글에서 검색해서 에러를 찾으면 된다.

   로그 위치 

   ```bash
   $ tail -F /var/log/nginx/access.log
   ```

   ```bash
   $ tail -F /var/log/nginx/error.log
   ```


1. production 로그 확인

   만약에 some went wrong 이라는 빨간 박스? 가뜨면 그건 내 코드의 문제이다.

   프로젝트 페이지 안에서 명령어를 치면된다. 

   ```bash
   $ tail -F log/production.log 
   ```

   에서 오류를 확인해보자.

2. 서버 재시작

   ```bash
   $ sudo service nginx restart
   ```

   ​

##### 참고 사이트

- https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-14-04
- http://www.bsidesoft.com/?p=3340#main
- LIKELION X Korea Univ. Author - https 설정하기
- 멋쟁이 사자처럼 3기 갓재욱 - amazon ec2 Deploy
- https://certbot.eff.org/lets-encrypt/