## Node.js 프로젝트 배포하기

#### 배포 준비

##### EC2 인스턴스 생성 절차

1. AWS Console에 접속하여 로그인한다.
   (https://console.aws.amazon.com/console/home)
2. 가장 가까운 Region을 선택한다.
3. EC2→인스턴스→인스턴스 시작을 누른다.
4. 사용할 운영체제와 인스턴스 유형을 선택한다.
5. 키 페어를 생성한다.
   “새 키 페어 생성” 선택→키 페어 이름 입력→키 페어 다운로드
6. 인스턴스 시작 버튼을 누른다.

##### AWS EC2에 접속하기

MacOS 터미널이나 git bash(Windows의 경우)에 아래 명령어를 입력한다.

```shell
ssh -i 키페어_경로 ubuntu@인스턴스_IP_주소
```

##### EC2 인스턴스에 Node.js 설치하기

```shell
curl -sL https://deb.nodesource.com/setup_16.x | sudo -E bash -

sudo apt-get install -y nodejs
```

##### EC2 인스턴스에 MongoDB 설치하기

```shell
wget -qO - https://www.mongodb.org/static/pgp/server-4.2.asc | sudo apt-key add -

echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu bionic/mongodb-org/4.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.2.list

sudo apt-get update

sudo apt-get install -y mongodb-org
```

##### EC2 인스턴스에서 MongoDB 실행하기

````shell
sudo service mongod start
````

#### 서버 프로그램 실행 및 웹사이트 접속

##### 포트 설정하기

EC2 터미널에 `git clone`을 이용해 프로젝트를 가져온 후, 생성된 프로젝트 폴더로 이동하여 `node app.js`로 프로젝트를 실행한 후 브라우저에 주소(`http://인스턴스_IP_주소:설정한_포트`)를 입력하면 접속이 되지 않는다. 이는 서버 방화벽에서 해당 포트로 접속하는 것을 막고 있기 때문이다.

→ 이를 해결하기 위해 접속할 포트를 설정해야 한다.

- 인스턴스→해당 인스턴스 선택→보안 탭→보안그룹 링크 클릭→인바운트 규칙 편집→규칙 추가→새 규칙 설정→규칙 저장
- 사용할 규칙
  - 유형: HTTP
  - 소스: Anywhere-IPv4

##### EC2 Instance 포트 설정

- **`iptables`**: AWS가 아닌 리눅스 운영체제 내부에서의 방화벽 역할을 하는 프로그램

iptables 규칙 변경 명령어

```shell
sudo iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 80 -j REDIRECT --to-port 3000
```

##### PM2

EC2 Instance에서 ssh 접속이 끊기거나 node.js 프로그램을 끄면 웹사이트에 접속할 수 없게 된다.

- 이를 해결하기 위해 PM2를 이용한다.

###### PM2 설치하기

```shell
# 관리자 계정 전환
sudo -s 
# npm으로 설치
npm install -g pm2
# 프로젝트 실행
pm2 start app.js
```

#### 서버와 도메인 연결하기

1. 가비아 페이지 접속: https://my.gabia.com/service#/
2. 연결하려는 도메인 칸의 관리 버튼 클릭
3. DNS 정보 칸의 도메인 연결 클릭
4. 해당 도메인 칸의 설정 버튼 클릭
5. 레코드 수정-수정 버튼 차례로 클릭
6. 호스트 이름에 @, IP주소에 EC2 Instance의 IP 입력

위 과정을 거친 후 10분 정도 기다리면 프로젝트와 도메인이 연결된다.