---
title: "CentOS 설치부터 WEB(Apache)와 WAS(Wildfly) 연동까지"
excerpt: "post"

categories:
- company-work

tags:
- centos
- apache
- wildfly
---

# 온-나라 AP 설치 메뉴얼

## 운영체제 설치 및 세팅

### 1. 운영체제 설치
1. CentOS 7.x 이상 다운로드 [(CentOS 7.x)](http://isoredirect.centos.org/centos/7/isos/x86_64/)
2. 설치 가이드 [(가이드)](https://docs.centos.org/en-US/centos/install-guide/)  
   \*주의사항으로는 `Fedora Media Writer`를 공홈에서는 추천하지만 `exe`에 문제가 있어서 `rufus`로 설치하는 것을 추천
3. 설치 후 CentOS 업데이트
   ```shell
   yum -y update  # YellowDog Updater, Modified의 약자
   ```
4. 필요한 드라이버
   1. wget - 웹 상에서 파일 다운로드 시 필요
   2. net-tools - ifconfig 필요 시 (`ip addr`로도 가능)
   3. gcc - `tar.gz` 설치 시 필요
   4. gcc-c++ - `tar.gz` 설치 시 필요
   5. make - `tar.gz`파일을 압축 해제한 후 빌드 시 필요
   6. perl - 무지성으로 설치해서 몰랐으나 pcre 때문에 필요할 듯?
   7. libtool - apr이였나 apache였나 설치하다가 이거 뭐시기 에러 뜸;
   8. unzip - Wildfly 다운로드 후 zip 압축 해제 시 필요
   9. expat-devel - 이거 없으면 apr-util에서 에러 난다.
   ```shell
   yum -y install wget  # 이렇게 설치할 수 있으니 원하는 드라이버 설치
   ```

### 2. JDK 설치
1. 기존에 설치된 jdk 확인
    ```shell
    rpm -qa *jdk  # Red Hat Package Manager의 약자
    ```
   1. 설치된 jdk가 있다면
      ```shell
      yum remove [해당 jdk명]
      ```
2. openjdk-devel 1.7 설치
    ```shell
    yum -y install java-1.7.0-openjdk-devel.x86_64
    ```
3. 환경변수 설정
   1. 자바 경로 확인 후 /etc/profile 진입
      ```shell
      which java  # 자바를 호출하면 어디서 불러오는지 경로 확인
      >>[자바 경로]
      readlink -f [자바 경로]  # 바로가기 경로가 아니라 원본 경로 확인
      >>[원본 자바 경로]
  
      vi /etc/profile
      ```
   2. /etc/profile 에서 수정
      ```shell
      export JAVA_HOME=[원본 자바 경로에서 /bin/java 제외한 경로]  # /usr/lib/jvm/java-1.7.0-openjdk-1.7~~~.el7_8.x86_64/jre
      export PATH=$PATH:$JAVA_HOME/bin
      ```
      이후 `:wq`로 save &amp; quit
4. 환경변수 등록 확인
   ```shell
   echo $JAVA_HOME
   ```
5. 자바 버전 확인
   ```shell
   java -version
   javac -version
   ```


### 3. 방화벽 설정
개발 환경에서는 방화벽을 비활성화 하여 진행하며 필요에 따라 서비스용 포트 허용
- 비활성화
  ```shell
  service firewalld stop
  ```


### 4. 네트워크 설정
- 가상화 경우 :  
  vmware의 Manage - Virtual Machine Settings - Network Adapter에서 Custom 선택 후 VMnet() (Auto-bridging) 선택
- 다른 PC에 설치되어있을 시 :
  `/etc/sysconfig/network-scripts/`안에 해당 PC ip 인터페이스 장치명과 똑같은 파일 내부 변경
  - 필자 설정
    ```shell
    TYPE=Ethernet
    PROXY_METHOD=none
    BROWSER_ONLY=no
    BOOTPROTO=none  # dhcp에서 none으로 변경 시 고정 아이피
    DEFROUTE=yes
    IPV4_FAILURE_FATAL=no
    IPV6INIT=no  # IPV6 사용 여부 설정
    IPV6_AUTOCONF=no  # IPV6 사용 시 yes로 변경
    IPV6_DEFROUTE=no  # 위와 동일
    IPV6_FAILURE_FATAL=no
    IPV6_ADDR_GEN_MODE=stable-privacy
    NAME=enp1s0
    UUID=d9ad7f1c-51b4-4bee-9c73-6ce4a5e4895d
    DEVICE=enp1s0
    ONBOOT=yes  # 부팅/네트워크 재시작 시 자동으로 인터페이스 활성화 여부
    IPADDR=192.168.0.24  # 고정 아이피 설정
    PREFIX=24  #  NETMASK=255.255.255.0 과 동일 설정
    GATEWAY=192.168.0.1  # 게이트웨이 설정
    DNS1=8.8.8.8  # google 네임서버
    DNS2=8.8.4.4  # google 네임서버
    IPV6_PRIVACY=no
    ```
  - 설정 이후 네트워크 재시작
    ```shell
    systemctl restart network
    ```


## Apache WEB서버 설치

### 1. 설치 전 환경 세팅 (root 유저로 수행)
1. 아파치 설치 및 로그 디렉토리 생성
   ```shell
   mkdir /apache/src /ap_log  # make directory의 약자
   ```
2. `apache`유저 생성 및 패스워드 설정
   ```shell
   useradd apache
   passwd apache
   ```
3. `apache`에 `1`에서 만든 디렉토리 권한 부여
   ```shell
   chown apache:apache /apache /ap_log  # changes user ownership of의 약자
   ```

### 2. 소스 파일 다운로드 및 빌드 (apache 유저로 수행)
1. 유저 전환
   ```shell
   su - apache  # substitute user 라는 뜻
   ```
2. 다운로드 경로
   ```shell
   cd /apache/src/  # change directory의 약자
   ```
3. 다운로드 리스트 (wget으로 다운로드를 하거나 ftp 사용해서 다운로드)
  - httpd-2.x.xx.tar.gz : 아파치 HTTP Server (WEB 서버)
  - tomcat-connectors-1.x.xx-src.tar.gz : 다른 WAS와 WEB을 연결시켜주는 플러그인 
  - pcre-8.xx.tar.gz : Perl Compatible Regular Expressions
  - apr-1.x.x.tar.gz : Apache Portable Runtime
  - apr-util-1.x.x.tar.gz : Apache Portable Runtime Util
3. 압축해제 (`/apache/src/` 에서)
   ```shell
   tar xvzf httpd-2.x.xx.tar.gz  # tape archive의 약자
   tar xvzf tomcat-connectors-1.x.xx-src.tar.gz
   tar xvzf pcre-8.xx.tar.gz
   tar xvzf apr-1.x.x.tar.gz
   tar xvzf apr-util-1.x.x.tar.gz
   ```
4. 압축해제한 폴더별로 들어가서 빌드
  - pcre
    ```shell
    cd /apache/src/pcre-8.xx
    ./configure --prefix=/apache/pcre  # /apache/pcre에 설치하겠다는 것
    make && make install  # 만약 뭔가 불길한 색깔(빨강&주황)이 보인다면 make check를 해볼 것
    ```
  - apr
    ```shell
    cd /apache/src/apr-1.x.x
    ./configure --prefix=/apache/apr
    make && make install
    ```
  - apr-util
    ```shell
    cd /apache/src/apr-util-1.x.x
    ./configure --prefix=/apache/apr-util --with-apr=/apache/apr  # --with는 특정 패키지 이용하여 설치 시
    make && make install
    ```
  - apache
    ```shell
    cd /apache/src/httpd-2.x.xx
    ./configure --prefix=/apache/apache2 \  # minor 버전까지 적어도 됨
    --with-apr=/apache/apr \
    --with-apr-util=/apache/apr-util \
    --with-pcre=/apache/pcre \
    --enable-mpms-shared=all  # event, worker, prefork 방식을 모두 사용 가능(???). all로 하고 conf파일 수정하는게 정신건강상 좋다고 함
    make && install
    ```
  - tomcat-connector (이건 꼭 `cd` 부분 확실하게 잘 보기)
    ```shell
    cd /apache/src/tomcat-connectors-1.x.xx-src/native
    ./configure --with-apxs=/apache/apache2/bin/apxs
    make && install
    ```

### 3. 아파치 설정 수정
1. 아차피 설정 파일 경로 및 편집기 실행
   ```shell
   cd /apache/apache2/conf
   vi httpd.conf
   ```
2. 설정 내용
  - Listen : IP 주소 &amp; 포트 또는 포트만 설정
  - User / Group : 웹서버를 기동할 유저/그룹 (apache / apache)
  - ServerName : 등록된 DNS 이름. 없다면 IP:포트 적기

### 4. 아파치 기동 및 정지
```shell
# 기동
/apache/apache2/bin/apachectl start

# 정지
/apache/apache2/bin/apachectl stop
```

### 5. 아파치 설치 및 기동 확인
```shell
ps -ef | grep httpd  # processes status와 global regular expression print의 약자
```


## Wildfly WAS 설치
`standalone`모드와 `domain`모드 중 `standalone`모드 설치 방법

### 1. Wildfly 다운로드 디렉토리 생성
```shell
cd /
mkdir jboss
```

### 2. 해당 경로에 Wildfly 다운로드 및 압축해제
1. 다운로드
   ```shell
   cd /jboss
   wget https://download.jboss.org/wildfly/9.0.2.Final/wildfly-9.0.2.Final.zip
   ```
2. 압축해제
   ```shell
   unzip wildfly-9.0.2.Final.zip
   ```

### 3. Wildfly standalone 설정
1. standalone.xml 파일 경로 및 편집기 실행
   ```shell
   cd /jboss/wildfly-9.0.2.Final/standalone/configuration
   vi standalone.xml
   ```
2. standalone.xml 수정 부분
    ```xml
    <server xmlns="urn:jboss:domain:3.0">
    <!-- 생략 -->
        <interface name="management">
            <inet-address value="${jboss.bind.address.management:192.168.0.24}"/>  <!-- 원하는 관리자용 IP적기 -->
        </interface>
        <interface name="public">
            <inet-address value="${jboss.bind.address:192.168.0.24}"/>  <!-- 원하는 공개용 IP적기 -->
        </interface>
    <!-- 생략 -->
        <socket-binding-group name="standard-sockets" default-interface="public" port-offset="${jboss.socket.binding.port-offset:0}">
            <socket-binding name="management-http" interface="management" port="${jboss.management.http.port:9990}"/>  <!-- 관리자 포트번호 -->
            <socket-binding name="management-https" interface="management" port="${jboss.management.https.port:9993}"/>
            <socket-binding name="ajp" port="${jboss.ajp.port:8009}"/>  <!-- (중요)추후 WEB서버 연동 포트 -->
            <socket-binding name="http" port="${jboss.http.port:8080}"/>  <!-- WAS 포트 -->
            <socket-binding name="https" port="${jboss.https.port:8443}"/>
            <socket-binding name="txn-recovery-environment" port="4712"/>
            <socket-binding name="txn-status-manager" port="4713"/>
            <outbound-socket-binding name="mail-smtp">  <!-- 이메일 관련 -->
                <remote-destination host="localhost" port="25"/>
            </outbound-socket-binding>
        </socket-binding-group>
    </server>
    ```
3. 관리자 계정 생성
    ```shell
    cd /jboss/wildfly-9.0.2.Final/bin
    ./add-user.sh  # Management User로 생성할 것
    ```

### 4. Wildfly 기동 및 정지
```shell
# 기동
nohup /jboss/wildfly-9.0.2.Final/bin/standalone.sh &

# 정지
/jboss/wildfly-9.0.2.Final/bin/jboss-cli.sh --controller=192.168.0.24:9990 --connect --command=:shutdown
```

### 5. Wildfly 설치 및 기동 확인
- 포트 확인
    ```shell
    netstat -an | grep 9990
    ```
- 생성한 관리용 계정으로 웹브라우저 접속 (192.168.0.24:9990)


## WEB-WAS 연동

### 1. WAS 연동 설정
1. 경로 및 편집기 실행
    ```shell
    cd /jboss/wildfly-9.0.2.Final/standalone/configuration
    vi standalone.xml
    ```
2. standalone.xml 수정 부분
    ```xml
    <!-- 생략 -->
    <subsystem xmlns="urn:jboss:domain:undertow:2.0">
        <buffer-cache name="default"/>
            <server name="default-server">
                <ajp-listener name="ajp" socket-binding="ajp" scheme="http"/>  <!-- 해당 부분 추가하기 -->
                <http-listener name="default" socket-binding="http" redirect-socket="https"/>
                <host name="default-host" alias="localhost">
                    <location name="/" handler="welcome-content"/>
                    <filter-ref name="server-header"/>
                    <filter-ref name="x-powered-by-header"/>
                </host>
            </server>
            <servlet-container name="default">
                <jsp-config/>
                <websockets/>
            </servlet-container>
            <handlers>
                <file name="welcome-content" path="${jboss.home.dir}/welcome-content"/>
            </handlers>
        <filters>
            <response-header name="server-header" header-name="Server" header-value="WildFly/9"/>
            <response-header name="x-powered-by-header" header-name="X-Powered-By" header-value="Undertow/1"/>
        </filters>
    </subsystem>
    <!-- 생략 -->
    ```

### 2. WEB 연동 설정
1. httpd.conf 파일 경로 및 편집기 실행
    ```shell
    cd /apache/apache2/conf
    vi httpd.conf
    ```
2. httpd.conf 수정 부분
    ```shell
    LoadModule jk_module modules/mod_jk.so  # mod_jk.so 파일 불러옴 (tomcat-connectors를 설치할때 생김)
    JkWorkersFile conf/workers.properties  # WEB서버와 연동할 WAS의 정보
    JkLogFile /ap_log/jk/mod_jk.log  # 로그 파일 경로
    JkLogLevel info  # error/debug/info 로 나누어서 설정 가능
    JkLogStampFormat "[%a %b %d %H:%M:%S %Y]"  # 시간을 어떻게 표시할 건지
    JkMount /* wlb  # 모든 형식의 파일들을 wlb라는 workers(WAS)이 작업하도록 설정
    ```
3. workers.properties 파일 경로 및 편집기 실행
    ```shell
    cd /apache/apache2/conf
    vi workers.properties
    ```
4. workers.properties 설정
    ```shell
    worker.list=wlb
    worker.wlb.type=ajp13
    worker.wlb.port=8009  # standalone.xml의 ajp 포트번호와 동일해야함
    worker.wlb.socket_timeout=180
    worker.wlb.reply_timeout=180000
    worker.wlb.host=192.168.0.24
    ```
   로드밸런싱 작업은 링크 참고  
   [링크](https://taetaetae.github.io/2019/08/04/apache-load-balancing/)