---
title: "Django 서버 AWS EC2에 배포하기"
excerpt: "aws ec2"
categories:
  - aws
last_modified_at: 2021-01-24
toc: true
toc_sticky: true
---

## Django 서버 AWS EC2에 배포하기

### IAM Setting

1. aws console에 로그인
2.  서비스 -> `IAM` 선택
3. 왼쪽 탭에서 `사용자` 선택 후 `사용자 추가` 선택

![image-20210124011132634](https://user-images.githubusercontent.com/17541671/105611080-98184f00-5df6-11eb-9342-a422b712f606.png)

4.  이름 지정하고 `프로그래밍 방식` 액세스 클릭

![image-20210124011312431](https://user-images.githubusercontent.com/17541671/105611071-8df65080-5df6-11eb-8bf3-94afba936e83.png)

5. 기존 정책 직접 연결 -> `AmazonEC2FullAccess` 클릭

![image-20210124011510591](https://user-images.githubusercontent.com/17541671/105611056-7cad4400-5df6-11eb-87b7-bcf041be80e4.png)

6.  우측 하단의 `사용자 만들기` 선택 후 `.csv 다운로드`로 액세스 키 저장

   (액세스 키ID, 비밀 액세스 키는 다시 확인 할 수 없으므로 저장해두는 게 좋음!)

![image-20210124011714865](https://user-images.githubusercontent.com/17541671/105611031-5c7d8500-5df6-11eb-87d8-7f6b6b5d4176.png)



### EC2 Setting

1.  서비스 -> `EC2` 선택
2.  왼쪽 탭에서 `키 페어` 선택후 `키 페어 생성` 해서 `ppk` 파일 저장
3. `인스턴스 시작`

![image-20210124005000155](https://user-images.githubusercontent.com/17541671/105611107-bed68580-5df6-11eb-82bd-33d010c84c1a.png)

4. ubuntu Server 18.04 선택 (원하시는 버전 `선택`하시면 됩니다.)

![image-20210124005115965](https://user-images.githubusercontent.com/17541671/105611389-55f00d00-5df8-11eb-95a1-c04ec68e3779.png)

5. t2.micro (프리티어 사용 가능) 선택하시고 `다음 `

6. 단계 5까지는 default 설정, 단계 6. 보안 그룹 설정

![image-20210124010131669](https://user-images.githubusercontent.com/17541671/105611088-a2d2e400-5df6-11eb-8db5-163f0767b360.png)

7.  기존 키 페어 선택해서 위에서 생성한 키 선택

![image-20210124012753538](https://user-images.githubusercontent.com/17541671/105611019-5091c300-5df6-11eb-9d58-325edc4770c3.png)

8. 인스턴스 실행중 확인



### SSH에 접속해서 EC2서버 실행

1. putty 설치 후 실행
2. `Connection` -> `SSH` -> `Auth` 이동 후 저장했던 key file을 `Browse`

![image-20210124013440708](https://user-images.githubusercontent.com/17541671/105611006-42dc3d80-5df6-11eb-880d-cb412e72efc0.png)

3. `Session`으로 돌아와 `Host Name`에 실행 중인 인스턴스의 pubic DNS를 복사해서 붙여 넣고 `Open` 클릭해서 실행

![image-20210124013728551](https://user-images.githubusercontent.com/17541671/105610993-36f07b80-5df6-11eb-9b61-f59bf0ce478a.png)

4. Putty 경고창이 뜨면 `예` 선택 후 EC2  에 로그인 하기위해 `ubuntu` 입력

![image-20210124013943477](https://user-images.githubusercontent.com/17541671/105610989-2b9d5000-5df6-11eb-9536-e8cb4e9d50c5.png)

5.  서버에 접속 후 설정 기본 세팅

   `sudo vi /etc/default/locale`

   ```
   LC_CTYPE=en_US.UTF-8
   LC_ALL=en_US.UTF-8
   LANG=en_US.UTF-8
   ```

6. 1.  패키지 정보 업데이트`sudo apt-get update`
   2.  패키지 의존성 업그레이드`sudo apt-get dist-upgrade`
   3.  파이썬 패키지 매니저 설치 `sudo apt-get install python-pip`
   4. `sudo apt-get install -y make build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev xz-utils tk-dev`

7.  pyenv 설치
   1. `curl -L https://github.com/pyenv/pyenv-installer/raw/master/bin/pyenv-installer | bash`

   2. `vi ~/.bashrc`

   3. 파일 맨 아래에 내용 추가

      ```
      export PATH="~/.pyenv/bin:$PATH"
      eval "$(pyenv init -)"
      eval "$(pyenv virtualenv-init -)"
      ```

   4.  Reload the *bashrc*  `source ~/.bashrc`

8.  git 설치

   `sudo apt-get install libcurl4-gnutls-dev libexpat1-dev gettext libz-dev libssl-dev`

9.  srv 폴더 유저 변경

   `sudo chown -R ubuntu:ubuntu /srv/`

10.  프로젝트 `clone` 및 `pyenv` 설정

    1. `git clone 레포지토리.git`
    2. `cd 파일명`
    3. `pyenv install 3.7.0`  장고서버 실행했던 파이썬 버전 설치
    4. `pyenv virtualenv 3.7.0 가상환경명`
    5. `pyenv local 가상환경명`
    6. `pip install -r requriements.txt`





#### pip install mysqlclient 오류시

`sudo apt-get install libmysqlclient-dev`

