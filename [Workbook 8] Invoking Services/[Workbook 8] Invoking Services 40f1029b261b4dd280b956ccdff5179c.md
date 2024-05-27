# [Workbook 8] Invoking Services

## Overview

이 장에서는 서비스를 호출하는 다양한 방법을 연습합니다.

1. 외부에서 Flowservice 호출 (Invoke 
2. SMTP Built-in 서비스 호출
3. FTP, SFTP Built-in 서비스 호출 


## Steps
#### STEP 0. 최상위 폴더 아래 IF0007 과 invoke, smtp, ftp 폴더를 생성합니다.

![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/new1.png)

#### STEP 1. invoke 아래 svc 폴더를 생성하고 String 입력 2개를 받아 외부로 부터 호출 받는 서비스 svc_IF0007_addInts를 생성합니다.
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/new2.png)

- 외부로 부터 호출 시 서비스에 대한 호출 실행 권한을 Anonymous 로 설정하여 누구나 호출이 가능하도록 설정합니다.
  - Flowservice 에서 우클릭 > properties > Permissions > Execute ACL 설정
  ![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/new22.png)

- 서비스에 MAP을 설정하고 Input 값과 output 사이에 pub.math.addInts를 두어 a는 num1 과 b는 num2와 value는 output 값에 연결합니다.
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/new3.png)


- 서비스에서 HTTP URL별칭 속성을 찾아 확인하고 이 속성을 addint_{이니셜} 로 설정후 저장하세요.
  ![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/new4.png)
        
- 브라우저 탭을 열고 URL http://192.168.1.100:5555/{설정한 HTTP URL Alias}?num1=23&num2=21 를 입력하세요.
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/new5.png)
  
- 인증을 요청하면 Administrator | manage를 입력하세요. 다른 브라우저 탭에서 http://192.168.1.100:5555/invoke/CUDO_SJH.IF0007.invoke.svc:svc_IF0007_addInts?num1=123&num2=13 를 입력하세요.

![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/new6.png)

    

#### STEP 2. SMTP Built-in 서비스 호출 방법입니다. (Mail 발송 서비스 구성 방안)

  - Local (IS 가 설치된 서버) 에 SMTP 서버가 구성되어 있는 환경 기준으로 테스트를 진행합니다.
    
  - IF0007 폴더 아래 smtp 폴더와 그 하위로 svc 폴더를 생성하고, 새로운 svc_IF0007_smtp Flowservice 를 생성합니다.
    ![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/new7.png)

  - 해당 서비스에 pub.client:smtp 서비스 단계를 추가하고 다음과 같이 설정합니다.
    - to : 받는 사람 메일 주소 (ex. sjh@cudo.co.kr)
    - subject : 메일 제목 (ex. TEST Mail)
    - from : 보내는 사람 메일 주소 (ex. IS_Admin@Admin.co.kr)
    - mailhost : SMTP 서버 주소 (ex. localhost 또는 192.168.1.100)
    - mailhostPort : SMTP 포트 (ex. 25)
    - body : 메일 전문 (ex. 테스트 메일 입니다.)
    ![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/new81.png)
    

  - 메일이 정상적으로 수신 되었는지 확인합니다.
    ![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/new9.png) 
     

    

  - **참고** IS 웹 관리자 화면으로 접속하여 SMTP Notification 설정을 확인 가능합니다. (Edit resource settings 를 클릭하여 해당 설정을 수정할 수 있습니다.)
    - 관리자 또는 개발자에게 메일 알람 구성을 위한 메일 서버 설정 화면입니다.
  ![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/new80.png)
  ![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/new8.png)



#### STEP 3. FTP, SFTP 전송을 위한 Built-in 서비스 호출 방법입니다. (FTP, SFTP 파일 전송 서비스 구성 방안)

  - Local 또는 각 PC에 FTP 서버, SFTP 서버가 사전 구성되어 있는 환경 기준으로 테스트를 진행합니다.
  - IF0007 폴더 아래 ftp 폴더와 그 하위로 svc 폴더를 구성합니다. 새로운 svc_IF0007_ftp, svc_IF0007_sftp 두개의 Flowservice 를 생성합니다.
  ![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/new10.png)

  - svc_IF0007_ftp 서비스 안에 다음과 같은 서비스 단계들을 구성 & 매핑합니다.
    - pub.client.ftp:login (ftp 서버 로그인, Session Key 생성)
      ![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/new11.png)
      - serverhost : localhost 또는 192.168.1.100
      - serverport : 21
      - username : sol
      - password : dhfQoal3883
      **Note .** FTP 서버의 접속을 위해서는 FTP 서버에 접근 가능한 OS 유저 정보와 패스워드가 필요합니다.
      **Note .** FTP 서버 접속 시 네트워크 이슈가 발생할 수 있으므로 REPEAT 문을 사용하여 여러번 FTP 서버에 login 하도록 구성하는 것을 권장합니다.  
         
    - pub.client.ftp:get (IS 서버로 getFile, pub.client.ftp:put 서비스를 이용하면 putFile 가능)
      ![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/new12.png)
      - transfermode : binary
      - remotefile : /webM/IS01/test.txt (테스트 용으로 생성해 둔 파일입니다.)
      
    - pub.string:bytesToString (get File 한 파일의 content 를 확인하기 위한 서비스)
      ![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/new13.png)
    - pub.client.ftp:logout (Session key 삭제, 세션 끊기)
      ![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/new14.png)

    - 서비스를 실행하여 다음과 같은 결과가 나오는지 확인합니다.
      ![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/new15.png)

  - 다음 단계로 sftp 서비스를 구성합니다. SFTP 설정은 IS 웹 관리자 화면에서 SFTP Server 의 Alais 설정과 User Alias 설정이 필요합니다.
    ![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/new16.png)
    - 다음과 같이 서버 설정을 구성 후 Get Host Key 를 누른 후 저장합니다. (Version 1.0, Alias 명을 SFTP_{이니셜} 로 설정, 서버는 192.168.1.100 사용)
    ![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/new17.png)
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/new18.png)

  - SFTP Server 설정 후 SFTP 서버에서 사용할 User Alias 를 생성합니다.
  ![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/new19.png)
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/new20.png)
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/new21.png)
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/new23.png)
    
  - 새로 생성한 svc_IF0007_sftp Flowservice 아래 다음과 같이 구성 & 매핑 합니다. (FTP 와 유사한 방식이나 Alias 를 사용합니다.)
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/new24.png)
    - pub.client.sftp:login
      - userAlias : 설정한 UserAlias 입력 (ex. SJH)
    ![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/new25.png)
    - pub.client.sftp:get
      - remotefile : /webM/IS01/test.txt
    ![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/new26.png)
    - pub.io.streamToString
    ![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/new27.png)
    - pub.client.sftp:logout
   ![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/new28.png)

  - 서비스 실행 후 다음과 같은 결과를 확인합니다.
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/new29.png)
    


## Check Your Understanding

#### QUIZ 1. 서비스에 HTTP URL 별칭을 사용하는 이유와 시기는 언제 입니까?
#### QUIZ 2. SMTP 서버는 어디에 구성되어 있습니까?
#### QUIZ 3. FTP 서비스를 사용한 get, put 명령은 무엇을 의미합니까?
