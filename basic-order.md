####Docker?
##다양한 운영체제와 시스템 환경 상에서, 서버 셋업을 위한 작업이 각각 다르고 복잡함.
##도커는 컨테이너 기반의 가상화 플랫폼으로, 컨테이너 상에 서버를 셋업해 놓을 수 있음
##따라서 기반 환경이 다르더라도, 언제든 해당 컨테이너를 실행만 하면, 동일한 서버 셋업이 가능함

####도커 설치 
##curl은 커멘드라인 기반의 웹 요청도구
##root권한 필요
##sudo apt-get install curl
##curl -fsSL https://get.docker.com/ | sudo sh

####docker는 root 권한이 필요함
##sudo usermod -aG docker $USER
##usermod : 사용자가 사용하는 ID가 속하는 그룹외에 추가 그룹으로 docker 그룹을 추가할 수 있음
##-G 옵션 : 사용자 계정에 관련된 설정을 변경할 수 있는 명령어
##-a 옵션 : -G옵션과 같이 사용하는 옵션으로 현재 사용자가 가지고 있는 2차그룹 외에 추가로	2차그룹을 지정할 때 사용

####docker는 서버/클라이언트 구조로 이루어짐 
##서버는 docker daemon process형태로 동작함
##데몬이란 보통 계속 실행중인 프로그램

####docker command 는 일종의 클라이언트
##내부적으로 rest API를 이용해 docker 데몬 프로세스를 호출함

####docker image
##도커에서 서비스 운영에 필요한 서버프로그램, 코드, 라이브러리, 컴파일된 실행파일을 묶는 형태
##도커 컨테이너를 생성하기 위한 명령들을 가진 템플릿

####docker container 
##이미지를 리눅스 컨테이너 형태로 실행한 상태, 응용프로그램의 종속성과 함께 응용프로그램 자체를 
##패키징 캡슐화하여 격리된 공간에서 프로세스를 동작시키는 기술

####도커 이미지 받기
##docker pull ubuntu

####도커 이미지 별로 받기
##docker pull ubuntu:20.10

####도커 다운로드 이미지 삭제하기
##docker rmi 이미지id

####도커 컨테이너 관련 중요 명령어
##컨테이너 생성
##각 이미지는 컨테이너로 만들어줘야 실행가능함
##이미지와 컨테이너는 각각 관리해주어야함
##컨테이너 생성시, docker 프로그램에서 이름이 자동 부여됨

####컨테이너 생성
##docker create ubuntu

####모든 컨테이너 확인
##docker ps -a
##docker ps -a -q //실행중이지 않은 컨테이너 포함해서, 전체 컨테이너의 ID만 출력하기

####컨테이너 삭제
##docker rm 삭제컨테이너 이름

####컨테이너 이름 변경
##docker create --name 내가원하는컨테이너이름 이미지이름

####컨테이너 실행
##docker start 컨테이너이름

##docker run -it ubuntu //컨테이너 실행 후, 해당 ubuntu내로 들어가서 터미널로 명령을 내릴 수 있음
##docker run -it --name myubuntu ubuntu //컨테이너 실행 후 이름을 원하는 이름으로 변경 시
##docker run -it --rm --name myubuntu2 ubuntu//컨테이너 종료시 자동으로 컨테이너까지 삭제하는 옵션
##docker run -it -d --name myubuntu3 ubuntu //백그라운드로 실행하기

####컨테이너 종료하기
##docker stop myubuntu3

####종료컨테이너 재실행하기
##docker start

####apache 웹서버 공식 docker 찾기
##docker search httpd

####이미지 다운받고 바로 컨테이너로 만들어 실행시키기
##docker run -d --name apacheweb httpd

##docker run -d -p 9999:80 --name apacheweb2 httpd

####나만의 웹서비스 만들기 
##docker run -v 호스트_pc의 절대경로:도커_컨테이너의 절대경로 httpd
##ex)
##docker run -d -p 9999:80 -v "/users/이조순/바탕화면:/usr/local/apache2/htdocs --name apcheweb2 httpd

####docker가 사용하고 있는 저장매체 현황 확인하기 
##docker system df

####대부분의 docker 이미지에 가장 기본이 되는 이미지는 ubuntu가 아닌 alpine 알파인 실행해보기
##docker run -d -p 9999:80 -v "/users/이조순/바탕화면:/usr/local/apache2/htdocs --name apcheweb2 httpd:alpine 

####실행중인 컨테이너 사용 리소스 확인하기 
##docker container stats

####exec : 해당 컨테이너에 신규명령을 실행함
####attach : 컨테이너에 연결하는 명령
####실행중인 컨테이너에 명령 실행하기
##docker exec -it apacheweb2 /bin/sh 
##/bin/sh 쉘프로그래밍을 사용하면 터미널에 연결되므로, 컨테이너 안으로 들어갈 수 있음

####실행중인 컨테이너에 연결하기
##docker run -it -d --name 실행중인컨테이너이름 본래이미지

####다음과 같이 실행하면, 해당 컨테이너에 연결되어, 컨테이너 내에서 쉘프로그램을 사용하여, 명령을 내릴 수 있음
##docker attach myubuntu3 

####삭제명령어
##docker stop $(docker ps -a -q) 모든 컨테이너 중지
##docker rm $(docker ps -a -q) 모든 컨테이너 삭제
##docker rmi -f $(docker images -q) 모든 이미지 삭제





