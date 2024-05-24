# [Workbook 8] Invoking Services

## Overview

이 장에서는 서비스를 호출하는 다양한 방법을 연습합니다.


## Steps
#### STEP 0. 최상위 폴더 아래 IF0007 과 svc 폴더를 생성합니다.
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/chapter8_1.png)

#### STEP 1. String 입력 2개를 받아 외부로 부터 호출 받는 서비스 svc_IF0007_addInts를 생성합니다:
- 서비스에 MAP을 설정하고 Input 값과 output 사이에 pub.math.addInts를 두어 a는 num1 과 b는 num2와 value는 output 값에 연결합니다.
  ![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/chapter8_2.png)
- HTTP를 사용하여 서비스를 호출하려면 Designer를 시작하고 CUDO_SJH 패키지의 IF0007.svc 폴더에서 addInts 서비스를 찾아 편집을 위해 잠금 설정합니다.HTTP URL별칭 속성을 찾아 확인하고 이 속성이 ‘addInput’로 설정되어 있는지 확인하세요.
  ![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/chapter8_4.png)
        
- 필요하다면 서비스를 저장하세요  
- 브라우저 탭을 열고 URL [http://192.168.1.100:5555/addInts?a=23&b=21](http://xn--localhost-p69d:5555/%E2%80%8CxmlAdd?%E2%80%8Ca=12&%E2%80%8Cb=23) 를 입력하세요.
- 인증을 요청하면 Administrator | manage를 입력하세요. 다른 부라우저 탭에서 대체 URL http://192.168.1.100:5555/invoke/CUDO_SJH.IF0007.svc/svc_IF0007_addInts?          a=123&b=13 를 입력하세요.

  두 결과를 비교하여 차이점을 확인하세요.
        
  ![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/chapter8_3.png)   
    

#### STEP 2. SMTP(메일)를 사용하여 서비스를 호출합니다:
  - SMTP 서버 설치 (CentOS7 기준)입니다.
  
  ```
  $ yum install sendmail sendmail-cf -y
  
  # sendmail 시작, 재시작, 중지 커맨드
  
  $ systemctl start sendmail
  $ systemctl restart sendmail
  $ systemctl stop sendmail
  ```
  - SMTP 서버 설정하세요.
    - /etc/mail/sendmail.mc
      - sendmail.cf 는 sendmail의 설정파일 입니다.
      - sendmail.mc는 설정을 조금더 용이하게 하기 위한 보조 파일 입니다.
      - m4 sendmail.mc > sendmail.cf 커맨드로 설정 적용합니다.
    - /etc/mail/access
      - IP, Domain, Email Address, 네트워크에 대해 Sendmail 에 접근하지 못하도록 제한 설정 파일입니다.
      - 스펨메일 방지나 스펨메일 릴레이 방지에 사용합니다.
      - makemap hash /etc/mail/access < /etc/mail/access 커맨드로 설정 적용합니다.
  
  - sendmail.mc를  설정하세요.
    ```
      $ cd /etc/mail

      $ vi sendmail.mc


    [수정 전]
    
    ...(중략)
    
    dnl TRUST_AUTH_MECH(`EXTERNAL DIGEST-MD5 CRAM-MD5 LOGIN PLAIN')dnl
    
    dnl define(`confAUTH_MECHANISMS', `EXTERNAL GSSAPI DIGEST-MD5 CRAM-MD5 LOGIN PLAIN')dnl
    
    ... (중략)
    
    DAEMON_OPTIONS(`Port=smtp, Addr=127.0.0.1, Name=MTA')dnl
    
    
    ## dnl 은 주석 처리문자이며 위 두 라인은 dnl 삭제 
    
    ## 외부 어디에서나 현재 서버의 메일 서비스를 사용할 수 있도록 루프백 주소를 (127.0.0.1 -> 0.0.0.0) 으로 변경
    
    
    [수정 후]
    
    
    ... (중략)
    
    
    define(`confAUTH_MECHANISMS', `EXTERNAL GSSAPI DIGEST-MD5 CRAM-MD5 LOGIN PLAIN')dnl 
    
    TRUST_AUTH_MECH(`EXTERNAL DIGEST-MD5 CRAM-MD5 LOGIN PLAIN')dnl
    
    
    ... (중략)
    
    
    DAEMON_OPTIONS(`Port=smtp, Addr=0.0.0.0, Name=MTA')dnl
    
    # 설정 적용 후 sendmail.mc 를 sendmail.cf에 반영
    
    $ m4 /etc/mail/sendmail.mc > /etc/mail/sendmail.cf
    
    # sendmail 재시작
    
    $ systemctl restart sendmail
    ```
  -  Telnet을 사용한 메일전송 테스트입니다. 로컬 SMTP 서버를 사용하여 hiworks 메일로 전송하기 입니다. 
      ```
        # 로컬 SMTP 서버를 사용 - hiworks 메일로 전송

        # telnet 으로 localhost 의 SMTP 서버 접속
        
        $ telnet localhost 25
        
        Trying ::1... 
        
        telnet: connect to address ::1: Connection refused 
        
        Trying 127.0.0.1... 
        
        Connected to localhost. 
        
        Escape character is '^]'. 
        
        220 192.168.1.51 ESMTP Sendmail 8.14.7/8.14.7; Mon, 21 Aug 2023 13:42:59 +0900
        
        
        EHLO smtps.hiworks.com  # hiworks SMTP 서버와 통신 시작
        												# 성공시 250 OK
        
        
        250-192.168.1.51 Hello localhost [127.0.0.1], pleased to meet you 
        
        250-ENHANCEDSTATUSCODES 
        
        250-PIPELINING 
        
        250-8BITMIME 
        
        250-SIZE 
        
        250-DSN 
        
        250-ETRN 
        
        250-AUTH GSSAPI DIGEST-MD5 CRAM-MD5 LOGIN PLAIN 
        
        250-DELIVERBY 
        
        250 HELP
        
        
        
        MAIL FROM:CUDO@Noreply.co.kr   #받는 SMTP 서버에 메시지 보낸 사람을 알리기 위한 명령
        
        250 2.1.0 CUDO@Noreply.co.kr... Sender ok
        
        
        RCPT TO:sjh@cudo.co.kr          #받는 SMTP 서버에 메시지 받는 사람을 알리기 위한 명령
        
        250 2.1.5 sjh@cudo.co.kr... Recipient ok
        
        
        DATA                             #데이터를 보낼 준비가 완료 되었음
        
        354 Enter mail, end with "." on a line by itself #성공
        
        Subject:sendmail test mail        #메일 제목 
        
        
        This is Test Message               
        
        .                                  #끝맺음    
        
        250 2.0.0 37L4oCHa015323 Message accepted for delivery 
        
        
        QUIT
        
        221 2.0.0 192.168.1.51 closing connection 
        
        Connection closed by foreign host.


      ```

  - mailx 사용한 메일 전송 테스트입니다.
    ```
    # mailx 설치

    $ yum install -y mailx
    
    $ mail sjh@cudo.co.kr
    
    Subject : test Mail!! 
    
    Test mail.....!!!!!
    
    
    # CTRL + D 명령으로 메일 끝맺음
    
    EOT
    ```


  - webMethods를 사용한 메일전송 테스트입니다.  CUDO_SJH.IF0007.svc 폴더에 svc_IF0007_smtp 서비스를 생성합니다.
    
    ![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/chapter8_5.png)
    

    mailhost 에는 [localhost](http://localhost) mailhostPort는 25로 설정합니다.

    Administration → Settings → Resources → Edit Resource Settings → Email Notification 을 설정하세요.
    ![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/chapter8_6.png)   
    
    
    





#### STEP 3. FTP를 사용하여 서비스를 호출합니다:
- FTP를 사용하기 전에 통합 서버에 활성화된 FTP포트가 있는지 확인하세요. Integration Server Administration Console을 열고 **Security** Æ **Ports** 하위 메뉴로 이동하세요. 포트 9021을 위한 FTP 포트가 있는지 확인하고 해당 액세스 모드 설정이 모든 서비스 실행을 허용하는지 확인하세요:   


 ![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/chapter8_14.png)  
 ![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/chapter8_15.png)  
 ![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/chapter8_16.png)  


 
        
       
 
    

#### STEP 4.  Java 를 사용하여 서비스를 Invoke(호출) 합니다: 
- IF0007.svc 폴더에서 svc_IF0007_addInts를 찾고 오른쪽 마우스클릭 후 Generate Code를 클릭합니다.

- 서비스를 우-클릭 하고 **Generate Code** 항목을 선택합니다. 열린dialog box 에서          **For calling this service from a client** 를 선택합니다.   
        
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/Untitled%2025.png)
        
- 다음 선택하세요. Language: **Java**   
        
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/Untitled%2026.png)
        
Code Generation 위한 directory로 **C:\TEMP** 를 사용합니다**.**   
        
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/Untitled%2027.png)
        
- 이제 Java project 를 생성하세요.
        
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/Untitled%2028.png)
        
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/Untitled%2029.png)
        
Dialog 안에서 **addInts** 를 프로젝트 이름으로 입력하세요. 기본값을 변경하지 말고 **Finish 버튼**을 누르십시오. Java perspective 변경을 허용하세요.
라이브러리는 JavaSE-1.6 선택 후 진행합니다

![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/chapter8_9.png)

        
- 이 프로젝트는 두 개의 추가적인 외부의 Jar 파일이 필요합니다. 추가하려면 **Properties** 항목을 선택하세요. 나타나는 dialog 에서 **Java Build Path** 를 선택하고**Libraries** tab 을 클릭하세요. 이 창에서 **Add external Jars** 를 선택하고 libraries **...\SoftwareAG\common\lib\wm-isclient.jar** 및 **...\SoftwareAG\common\lib\ext\mail.jar** 를 추가하세요. 완료가 되면, 창은 다음과 같습니다:   
        
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/chapter8-10.png)
        
**OK** 버튼을 클릭하여 dialog 를 닫습니다.   
        
- 이제 첫 번째 단계에서 생성된 Java 소스를 가져옵니다. 그렇게 하려면, right-click the **addInts** node 를 한 번 더 추가하고 menu  에서 **Import** option  옵션을 선택합니다. 선택: **General** Æ **File System** 후 click **Next**. 다음 창에서 directory 로 **C:\temp** 를 찾아보고 **svc_IF0007_addInts.java** 파일을 선택합니다. **Into Folder** field 에 **addInts\src** 를 입력합니다. Dialog 는 다음과 같아야 합니다:     
        
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/chapter8-11.png)
        
**Finish** 버튼을 클릭하세요.   
        
- **xmlAdd.java** 파일을 열고 행을 변경하십시오.   
        
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/Untitled%2032.png)
        
다음과 같이 자격 증명을 수정합니다:
        
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/Untitled%2033.png)
        
- 변경사항을 저장하세요. **svc_IF0007_addInts.java** 파일을 마우스 오른쪽 버튼으로 클릭하고 **Run As → Java Application**을 선택하여 프로그램을 실행하세요. 콘솔 뷰를 열어보세요:  
        
        
         
        
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/chapter8_12.png)
        
- **a =** 와 **b =** 프롬프트에 두 개의 작은 숫자를 입력하고 Enter 키를 누르세요. 결과를 확인하세요.

*참고* : 커서 키를 사용하여 커서를 ‘=’ 기호 뒤에 위치시키지 마세요. 커서위치 오류는 Eclipse IDE의 미세한 버그입니다. 커서가 올바른 위치에 있는 것처럼 숫자를 입력하세요.
        
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/chapter8_13.png)
        

## Check Your Understanding

#### QUIZ 1. 서비스에 HTTP URL 별칭을 사용하는 이유와 시기는 언제 입니까?
#### QUIZ 2. 서비스는 input 데이터는 어떻게 찾습니까?
#### QUIZ 3. 서비스는 결과를 어떻게 반환합니까?
