---
title: "Linux_deploy"
date: 2021-04-05 
categories: Deploy
---
AWS에 배포를 하기 위해서 
1. EC2 인스턴스 생성
2. JAVA/JDK 설치
3. tomcat 설치
4. war파일 업로드(추후 git으로 자동배포 해보기)

위의 과정이 필요하다

Linux환경에서 설치를 하기 때문에 다음과 같은 과정을 거쳐야 한다
<strong>문제점 해결과 각 명령어의 의미는 추후에 다시 정리할 것!!</strong>
- 자바 설치
  - jre설치: $ sudo apt-get install openjdk-8-jre입력 
  - jdk설치: $ sudo apt-get install openjdk-8-jdk입력 
  - 설치후 버전확인 : java -version, javac -version
  - 자바 위치 확인하기:  which javac
  - 자바위치 풀경로 확인 : readlink -f /usr/bin/javac
  - 환경변수 설정 : $sudo nano /etc/profile
  - 환경변수
    - export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
    - export PATH=$JAVA_HOME/bin/:$PATH
    - export CLASS_PATH=$JAVA_HOME/lib:$CLASS_PATH
    - 저장 ctrl+O, 나가기 ctrl+X       
      - 환경변수  오류시 명령어를 입력해도 오류가 발생하는 경우가 있다 이떄 PATH="$PATH:/usr/local/bin:/usr/bin:/bin" export PATH 를 하면 해결된다
  - reload: $source/etc/profile
  - 환경변수 확인: 
    - $echo $JAVA_HOME
    - $JAVA_HOME/bin/javac -version
  
- 톰캣설치
  - wget [톰캣 다운로드 주소]
  - 압축해제: #tar xvfz apache-tomcat-8.5.57.tar.gz
  - tomcat8.5 라는 폴더를 만들고, 이동시킴
  - sudo mv apache-tomcat-8.5.57 /usr/local/tomcat8.5
    - 권한으로 인해 sudo를 사용하며 해당 디렉토리생성이 안될시 cd /usr/local로 이동해 mkdir tomcat8.5를 직접해주고 이동한다
    - 이때 되돌알때 경로는 /home/ubuntu이다
    - 파일명 변경: mv [파일명] [변경할 파일명]
  - 환경변수 설정
    - export CATALINA_HOME=/usr/local/tomcat8.5 
    - source /etc/profile
    - echo $CATALINA_HOME
  - 톰캣설정
    - 특정 디렉토리의 파일목록보기: ls 디렉토리 경로
    - ls /usr/local/tomcat8.5/conf (mv가 잘못될경우 tomcat8.5 안에 또 폴더가 있을 수 있다)
    - sudo nano /usr/local/tomcat8.5/conf/server.xml
    - <Connector prot="8080" ~~부분을 찾아서 인코딩을 추가한다  URIEncoding="UTF-8"  
  - 톰캣실행: /usr/local/tomcat8.5/bin/startup.sh
  - 정상여부 체크: ps -ef | grep tomcat
  - 8080포트가 열려있는지 확인: netstat -tln  혹은 netstat -anp | grep 8080
  - AWS의 인스턴스 ip주소:8080으로 접속하면 된다
  - 이 떄 접속이안되는 경우 인바운드 보안설정으로 8080포트가 접속가능하게 설정한다
    - 사용자 지정 TCP TCP 8080 0.0.0.0/0
    - 사용자 지정 TCP TCP 8080 ::/0 
- 참고
  - [https://jiwontip.tistory.com/45](https://jiwontip.tistory.com/45)
  - [https://blog.naver.com/shjce93/220311546942](https://blog.naver.com/shjce93/220311546942)
  - [https://gaemi606.tistory.com/entry/AWS-EC2에-톰캣Tomcat-설치하기](https://gaemi606.tistory.com/entry/AWS-EC2%EC%97%90-%ED%86%B0%EC%BA%A3Tomcat-%EC%84%A4%EC%B9%98%ED%95%98%EA%B8%B0)
  - [https://jiwontip.tistory.com/45](https://jiwontip.tistory.com/45)
  - [https://gaemi606.tistory.com/entry/AWS-EC2에-JAVA설치-및-환경변수-설정](https://gaemi606.tistory.com/entry/AWS-EC2%EC%97%90-JAVA%EC%84%A4%EC%B9%98-%EB%B0%8F-%ED%99%98%EA%B2%BD%EB%B3%80%EC%88%98-%EC%84%A4%EC%A0%95) 
  - [war 업로드](https://13akstjq.github.io/aws/2019/05/29/how-to-deploy-spring-lagacy-project-ec2-aws.html)
