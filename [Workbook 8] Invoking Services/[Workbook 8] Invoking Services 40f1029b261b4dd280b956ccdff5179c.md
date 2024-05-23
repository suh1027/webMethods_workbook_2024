# [Workbook 8] Invoking Services

## Overview

이 장에서는 서비스를 호출하는 다양한 방법을 연습합니다.


## Steps
#### STEP 0. 최상위 폴더 아래 IF0007 과 svc 폴더를 생성합니다. 

#### STEP 1. String 입력 2개를 받아 외부로 부터 호출 받는 서비스 svc_IF0007_addInts를 생성합니다:
- 서비스에 MAP을 설정하고 Input 값과 output 사이에 pub.math.addInts를 두어 a는 num1 과 b는 num2와 value는 output 값에 연결합니다.
- 


#### STEP 2. HTTP를 사용하여 서비스를 호출합니다:

- HTTP를 사용하여 서비스를 호출하려면 Designer를 시작하고 CUDO_SJH 패키지의 IF0007.svc 폴더에서 addInts 서비스를 찾아 편집을 위해 잠금 설정합니다.HTTP URL별칭 속성을 찾아 확인하고 이 속성이 ‘addInts’로 설정되어 있는지 확인하세요.
        
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/Untitled.png)
        
- 필요하다면 서비스를 저장하세요  
- 브라우저 탭을 열고 URL [http://192.168.1.100:5555/addInts?a=23&b=21](http://xn--localhost-p69d:5555/%E2%80%8CxmlAdd?%E2%80%8Ca=12&%E2%80%8Cb=23) 를 입력하세요.
- 인증을 요청하면 Administrator | manage를 입력하세요. 다른 부라우저 탭에서 대체 URL [http://‌localhost:5555/‌invoke/‌acmeSupport.xml/‌xmlAdd‌?‌a=12‌&b=23](http://xn--localhost-p69d:5555/%E2%80%8Cinvoke/%E2%80%8CacmeSupport.xml/%E2%80%8CxmlAdd%E2%80%8C?%E2%80%8Ca=12%E2%80%8C&b=23) 를 입력하세요

두 결과를 비교하여 차이점을 확인하세요.
        
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/Untitled%201.png)    
    
#### STEP 2. XML 입력값을 사용하여 서비스를 호출하세요.
- **acmeSupport.xml:xmlAdd** 서비스를 마우스 오른쪽 버튼으로 클릭하고 **Debug As** > **Debug Configurations** 선택하세요. 다음 대화 상자에서 IS Service를 선택하세요:   
        
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/Untitled%202.png)
        
- 새로운 런치 구성을 만들기 위해 New 버튼을 클릭하세요. **acmeSupport.xml:xmlAdd**를 찾아 선택하세요. 그런다음 런치 구성의 이름을 New_configuration에서 **xmlAddWithXMLInput** 과 같이 의미 있는 이름으로 변경하고 **Apply**를 누르세요.   
        
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/Untitled%203.png)
        
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/Untitled%204.png)
        
- 이제 **Input** 탭을 선택하고 **Use XML** 라디오 버튼을 선택하세요. **Browse를 클릭하여** XML File **...\‌IntegrationServer\‌packages\‌AcmeSupport\‌pub\‌addInput.xml**로 이동하고 ‘Open’을 누르세요. 그런 다음 다시 ‘Apply’를 클릭하세요.     
        
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/Untitled%205.png)
        
- 이제 **Common** 탭을 선택하고 **Display in favorites menu** 확인란을 선택하세요. 다시 **Apply**를 클릭하고 **Debug**를 누르세요   
        
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/Untitled%206.png)
        
- Perspective switch에 관한 다이얼로그가 나타나면 Yes를 클릭하여 확인하세요. 선택적으로 Remember my decision확인란을 선택하여 이 다이얼로그의 추가적인 표시를 억제할 수 있습니다.
        
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/Untitled%207.png)
        
- Debugger가 시작되고 파이프라인에 이미 있는 Object 유형의 단일 입력 변수 노드를 디버깅하고 있습니다. 이것이 어떻게 변환되고 추가되는지 확인하기 위해 서비스를 단계별로 진행하세요.
        
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/Untitled%208.png)
        
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/Untitled%209.png)
        
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/Untitled%2010.png)
        

#### STEP 3. SMTP(메일)를 사용하여 서비스를 호출합니다

- Designer에서 다시 Service Development Perspective로 전환하세요. 패키지 네비게이터 뷰에서 문서**acmeSupport.xml:addDocument를 엽니다**. 해당 문서에는 a와 b라는 두 변수를 포함하는 간단한 루트 노드가 있는 것을 발견해야 합니다.   
        
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/Untitled%2011.png)
        
- 이제 동일한 폴더에 있는 **xmlAdd** 서비스를 열고 해당 서비스가 무엇을 수행하는지 알아보세요. 또한 파일 **...\‌IntegrationServer\‌packages\‌AcmeSupport\‌pub\‌xml**의 내용을 확인하세요.이 파일을 xmlAdd 서비스의 입력으로 제공할 경우 어떤 결과를 기대할 것인가요?
- 기본적으로 비활성화된 Integration Server의 이메일 포트를 활성화하세요. 이를 위해 Integration Server 관리 콘솔을 열고 **Security** Æ **Ports** 메뉴로 이동하세요. **integration-server@company.com@localhost** 항목을 클릭하세요.   
        
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/Untitled%2012.png)

           
        
그리고 **Edit Email Client Configuration을 선택하세요:**   
        
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/Untitled%2013.png)
        
**비밀번호로manage를 입력하세요**. 서비스가 처리되기를 기다리는 시간을 줄이기 위해 구성된 값인**Time Interval (seconds)**매개변수를 300에서 **10**초로 변경하세요. 그리고 **Save Changes**를 클릭하세요.
        
**팁: 연습이 끝난 후에는 이 값을 300으로 다시 변경하는 것을 잊지 마세요.**
        
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/Untitled%2014.png)
        
그런 다음 메일 포트를 활성화해야 합니다. 이를  위해 Enabled 열의 No를 클릭하여 이 포트를 활성화하세요. 화면 상단에 성공 메시지를 볼 수 있어야 합니다:
        
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/Untitled%2015.png)
        
- Mozilla Thunderbird를 시작하세요. 왼쪽에 있는 **[customer@company.com](mailto:customer@company.com)** 계정을 클릭하세요. 이제 **customer@company.com** 에서 **integration-server@company.com** 으로 빈 본문과 주제를**acmeSupport.xml:xmlAdd로 설정한 메일 메시지를 작성하세요.** 파일 첨부를 추가하고 **addInput.xml**문서를 선택하세요.   
        
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/Untitled%2016.png)
        
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/Untitled%2017.png)
        
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/Untitled%2018.png)
        
메일 작성을 완료하면 **Send**버튼을 눌러 전송하세요.
        
참고: 가상 머신에서는 메일 서비스와 Thunderbird가 모든 메일을 로컬로 처리하도록 설정되어 있습니다. 외부 메일 시스템과의 연결이 없습니다. Thunderbird 와 hMail Server ‘company.com’ 도메인을 제공하도록 설정되어 있습니다. 구성 설정을 변경하지 마세요.
        
메일을 보낸 후 약 15초 동안 기다린 다음 Thunderbird에서 **Get Mail**
        
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/Untitled%2019.png)
        
버튼을 클릭하면 Integration Server로부터 메시지 처리 결과가 포함된 답장을 받게 됩니다.
        
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/Untitled%2020.png)
        
    
- 이 부분의 연습을 마친 후에는 리소스의 낭비를 방지하기 위해 Integration Serve에서 이메일 포트를 비활성해야 합니다.
    

#### STEP 4. FTP를 사용하여 서비스를 호출합니다:
- FTP를 사용하기 전에 통합 서버에 활성화된 FTP포트가 있는지 확인하세요. Integration Server Administration Console을 열고 **Security** Æ **Ports** 하위 메뉴로 이동하세요. 포트 9021을 위한 FTP 포트가 있는지 확인하고 해당 액세스 모드 설정이 모든 서비스 실행을 허용하는지 확인하세요:   
        
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/Untitled%2021.png)
        
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/Untitled%2022.png)
        
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/Untitled%2023.png)
        
- 이제 Windows 명령 프롬프트 창을 열고 아래와 같이 표시된 명령을 실행하세요. 입력부분은굵게 표시되었습니다. 각 명령이 수행하는 작업을 입력하기 전에 이해하세요.                C:\>**cd /d C:\SoftwareAG\IntegrationServer\packages\AcmeSupport\pub**
        
        C:\SoftwareAG\IntegrationServer\packages\AcmeSupport\pub>**dir addInput.xml** 
        
        Volume in drive C has no label.
        
        Volume Serial Number is 9C80-4210 
        
        Directory of C:\SoftwareAG\IntegrationServer\packages\AcmeSupport\pub  
        
        03/09/2010 03:54 PM           181  addInput.xml 
        
                                   1 File(s)         181 bytes 
        
                                   0 Dir(s)    42,108,518,400 bytes free  
        
        C:\SoftwareAG\IntegrationServer\packages\AcmeSupport\pub>**ftp** 
        
        ftp> **open localhost 9021** 
        
        Connected to sagbase.eur.ad.sag. 
        
        220 sagbase:9021 FTP server (webMethods Integration Server version 8.2.1.0) 
        
        ready. 
        
        User (sagbase.eur.ad.sag:(none)): **Administrator** 
        
        331 Password required for Administrator.
        
         Password: **manage**
        
        230 User Administrator logged in. 
        
        ftp> **cd ns** 
        
        250 CWD command successful.
        
        ftp> **cd acmeSupport** 
        
        250 CWD command successful. 
        
        ftp> **cd xml** 
        
        250 CWD command successful.
        
        ftp> **cd xmlAdd** 
        
        250 CWD command successful.
        
         ftp> **send addInput.xml** 
        
        200 PORT command successful. 
        
        150 ASCII mode data connection for addInput.xml (127.0.0.1,2366).
        
        226 ASCII transfer complete.
        
        ftp: 181 bytes sent in 0.00Seconds 181000.00Kbytes/sec. 
        
        ftp> **dir** 200 PORT command successful. 
        
        150 ASCII mode data connection for /bin/ls (127.0.0.1,2368). 
        
        total 1 
        
        dr-xr-xr-x 3 root root 1 Mar 09 16:44 . 
        
        dr-xr-xr-x 3 root root 1 Mar 09 16:44 .. 
        
        -r--r--r-- 1 tx tx 106 Mar 09 16:44 addInput.xml.out 
        
        226 ASCII transfer complete. 
        
        ftp: 232 bytes received in 0.02Seconds 14.50Kbytes/sec. 
        
        ftp> **get addInput.xml.out -** 
        
        200 PORT command successful. 
        
        150 ASCII mode data connection for addInput.xml.out (127.0.0.1,2370) (106 bytes). 
        
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/Untitled%2024.png)
        
        226 ASCII transfer complete.
        
        ftp: 106 bytes received in 0.00Seconds 106000.00Kbytes/sec.
        
        ftp> **quit**
        
        221 Goodbye.  
        
    

#### STEP 5.  Java 를 사용하여 서비스를 Invoke(호촐) 합니다: 
- Designer 에서 위의 **xmlAdd** 서비스를 찾으십시오**.**
- 서비스를 우-클릭 하고 **Generate Code** 항목을 선택합니다. 열린dialog box 에서          **For calling this service from a client** 를 선택합니다.   
        
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/Untitled%2025.png)
        
- 다음 선택하세요. Language: **Java**   
        
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/Untitled%2026.png)
        
Code Generation 위한 directory로 **C:\TEMP** 를 사용합니다**.**   
        
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/Untitled%2027.png)
        
- 이제 Java project 를 생성하세요.
        
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/Untitled%2028.png)
        
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/Untitled%2029.png)
        
Dialog 안에서 **xmlAdd** 를 프로젝트 이름으로 입력하세요. 기본값을 변경하지 말고 **Finish 버튼**을 누르십시오. Java perspective 변경을 허용하세요.
        
- 이 프로젝트는 두 개의 추가적인 외부의 Jar 파일이 필요합니다. 추가하려면, project node () 를 우-클릭하고 pop up 버튼 아래에 있는 **Properties** 항목을 선택하세요. 나타나는 dialog 에서 **Java Build Path** 를 선택하고**Libraries** tab 을 클릭하세요. 이 창에서 **Add external Jars** 를 선택하고 libraries **...\SoftwareAG\common\lib\wm-isclient.jar** 및 **...\SoftwareAG\common\lib\ext\mail.jar** 를 추가하세요. 완료가 되면, 창은 다음과 같습니다:   
        
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/Untitled%2030.png)
        
**OK** 버튼을 클릭하여 dialog 를 닫습니다.   
        
- 이제 첫 번째 단계에서 생성된 Java 소스를 가져옵니다. 그렇게 하려면, right-click the **xmlAdd** node 를 한 번 더 추가하고 menu  에서 **Import** option  옵션을 선택합니다. 선택: **General** Æ **File System** 후 click **Next**. 다음 창에서 directory 로 **C:\temp** 를 찾아보고 **xmlAdd.java** 파일을 선택합니다. **Into Folder** field 에 **xmlAdd\src** 를 입력합니다. Dialog 는 다음과 같아야 합니다:     
        
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/Untitled%2031.png)
        
**Finish** 버튼을 클릭하세요.   
        
- **xmlAdd.java** 파일을 열고 행을 변경하십시오.   
        
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/Untitled%2032.png)
        
다음과 같이 자격 증명을 수정합니다:
        
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/Untitled%2033.png)
        
- 변경사항을 저장하세요. **xmladd.java** 파일을 마우스 오른쪽 버튼으로 클릭하고 **Run As → Java Application**을 선택하여 프로그램을 실행하세요. 콘솔 뷰를 열어보세요:  
        
        
         
        
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/Untitled%2034.png)
        
- **a =** 와 **b =** 프롬프트에 두 개의 작은 숫자를 입력하고 Enter 키를 누르세요. 결과를 확인하세요.

*참고* : 커서 키를 사용하여 커서를 ‘=’ 기호 뒤에 위치시키지 마세요. 커서위치 오류는 Eclipse IDE의 미세한 버그입니다. 커서가 올바른 위치에 있는 것처럼 숫자를 입력하세요.
        
![Untitled](%5BWorkbook%208%5D%20Invoking%20Services%2040f1029b261b4dd280b956ccdff5179c/Untitled%2035.png)
        

## Check Your Understanding

#### QUIZ 1. 서비스에 HTTP URL 별칭을 사용하는 이유와 시기는 언제 입니까?
#### QUIZ 2. 서비스는 input 데이터는 어떻게 찾습니까?
#### QUIZ 3. 서비스는 결과를 어떻게 반환합니까?
