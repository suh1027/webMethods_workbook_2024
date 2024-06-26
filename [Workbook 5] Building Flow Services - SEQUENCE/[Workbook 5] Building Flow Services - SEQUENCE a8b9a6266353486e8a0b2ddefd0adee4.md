# [Workbook 5] Building Flow Services - SEQUENCE

## Overview

이 연습에서는 **SEQUENCE** 문을 이해하고, **Flow service**에 **Sequence service**를 사용한 **Try/Catch** 로직을 구성하는 방법을 설명합니다.

(**10.x 버전 이후로 Try/Catch 문이 추가 되어 해당 로직을 사용해도 됩니다.**)

**Flow service**를 만들고 **Sequence** 문을 사용하여 **Try/Catch Sequence** 블록을 생성, TRY 블록에 **Exception** 이 발생하는 **Service** 를 구성합니다.


## Steps

#### STEP 0. IS 가 설치 된 서버 내 (Linux 기준) /webM/IS01/ 아래 test.txt 라는 파일을 미리 생성해 두었습니다.
![Untitled](%5BWorkbook%205%5D%20Building%20Flow%20Services%20-%20SEQUENCE%20a8b9a6266353486e8a0b2ddefd0adee4/Untitled.png))

#### STEP 1. 최상위 폴더 아래 IF0004와 IF0004.svc 폴더를 생성하고, 그 안에 svc_IF0004_riskOperation이라는 새 Flow service를 만듭니다. Input은 String으로 filename, Output은 String으로 result를 설정합니다. 
    
![Untitled](%5BWorkbook%205%5D%20Building%20Flow%20Services%20-%20SEQUENCE%20a8b9a6266353486e8a0b2ddefd0adee4/workbook5_step1.png)
    

#### STEP 2. **pub.file:getFile**를 **Service** 스탭에 추가하고 **filename**을 **filename**에 그대로 매핑합니다. (*Note. 이름이 동일한 필드의 경우 자동으로 매핑됩니다.*)   
    
![Untitled](%5BWorkbook%205%5D%20Building%20Flow%20Services%20-%20SEQUENCE%20a8b9a6266353486e8a0b2ddefd0adee4/Untitled%202.png)
    
![Untitled](%5BWorkbook%205%5D%20Building%20Flow%20Services%20-%20SEQUENCE%20a8b9a6266353486e8a0b2ddefd0adee4/workbook5_step2_2.png)
    

#### STEP 3. **string:bytesToString**를 **Service** 스탭에 추가합니다.
- **body/bytes**를 **bytes**로 연결하고 **string**을 **result**로 매핑합니다.
- **Pipeline Out**에서 다른 모든 변수를 **drop** 합니다.
    
![Untitled](%5BWorkbook%205%5D%20Building%20Flow%20Services%20-%20SEQUENCE%20a8b9a6266353486e8a0b2ddefd0adee4/Untitled%204.png)
    
![Untitled](%5BWorkbook%205%5D%20Building%20Flow%20Services%20-%20SEQUENCE%20a8b9a6266353486e8a0b2ddefd0adee4/workbook5_step3.png)
    

#### STEP 4. **Service**를 저장하고 실행합니다. **/webM/IS01/test.txt** 라는 값으로 **input 의 filename** 값을 입력합니다. (또는 존재하지 않는 다른 파일 명으로 입력 eg. /notthere.txt)  
    
![Untitled](%5BWorkbook%205%5D%20Building%20Flow%20Services%20-%20SEQUENCE%20a8b9a6266353486e8a0b2ddefd0adee4/Untitled%206.png)
![Untitled](%5BWorkbook%205%5D%20Building%20Flow%20Services%20-%20SEQUENCE%20a8b9a6266353486e8a0b2ddefd0adee4/Untitled%207.png)

---

#### STEP 5. IF0004.svc 폴더 아래 svc_IF0004_sequenceTryCatch 라는 이름으로 Flow service를 생성합니다. Input/Output은 위 서비스와 동일하게 구성합니다.   
    
![Untitled](%5BWorkbook%205%5D%20Building%20Flow%20Services%20-%20SEQUENCE%20a8b9a6266353486e8a0b2ddefd0adee4/workbook5_step5.png)
    

#### STEP 6. svc_IF0004_sequenceTryCatch에서 다음과 같이 세 개의 SEQUENCE를 추가하여 Flow try/catch 블록을 만듭니다.
- SEQUENCE Exit on SUCCESS 설정 (*Note. TRY-CATCH 블록으로 SEQUENCE 내부 로직이 SUCCESS 일 때 Exit*)
    - SEQUENCE가 Exit on FAILURE (*Note. TRY 블록으로 SEQUENCE 내부 로직이 FAILUER 일 때 Exit*)
    - SEQUENCE 가 Exit on DONE (*Note. CATCH 블록으로 SEQUENCE 내부 로직을 모두 수행 후 (DONE) Exit*)
        
    
    개별 **SEQUENCE** 문을 만들 때 **exit on** 의 조건에 따라 종료를 반영하도록 **Comments** 와 **Property** 를 반드시 설정합니다. 

![Untitled](%5BWorkbook%205%5D%20Building%20Flow%20Services%20-%20SEQUENCE%20a8b9a6266353486e8a0b2ddefd0adee4/Untitled%209.png)
    
#### STEP 7. **SEQUENCE**가 **FAILURE**일 때 종료 스탭 (Try 블록) 에서, **IF0004.svc:svc_IF0004_riskOperation** **Service**를 추가합니다.   
    
![Untitled](%5BWorkbook%205%5D%20Building%20Flow%20Services%20-%20SEQUENCE%20a8b9a6266353486e8a0b2ddefd0adee4/Untitled%2010.png)
    
- Pipeline 탭에서 다음과 같이 매핑합니다
    - **filename**에서 **filename**으로 매핑
    - **result**에서 **result**로 매핑
    
![Untitled](%5BWorkbook%205%5D%20Building%20Flow%20Services%20-%20SEQUENCE%20a8b9a6266353486e8a0b2ddefd0adee4/workbook5_step7_2.png)
    

#### STEP 8. **SEQUENCE**가 **DONE**일 때 종료에서, **pub.flow:getLastError** **Service**를 추가합니다 (**SEQUENCE** 아래에 **DONE**이 들여쓰기 되어있는지 확인).  
    
![Untitled](%5BWorkbook%205%5D%20Building%20Flow%20Services%20-%20SEQUENCE%20a8b9a6266353486e8a0b2ddefd0adee4/Untitled%2012.png)
    

#### STEP 9. **Pipeline** 탭에서 **lastError/error**와 **result**로 매핑
    
![Untitled](%5BWorkbook%205%5D%20Building%20Flow%20Services%20-%20SEQUENCE%20a8b9a6266353486e8a0b2ddefd0adee4/workbook5_step9.png)
    

#### STEP 10. **pub.flow:getLastError**의 호출 아래에 **pub.flow:debugLog**의 호출을 추가합니다. **lastError/error**를 **debugLog** 서비스의 **message** 입력 매개 변수에 매핑합니다. 
    
![Untitled](%5BWorkbook%205%5D%20Building%20Flow%20Services%20-%20SEQUENCE%20a8b9a6266353486e8a0b2ddefd0adee4/Untitled%2014.png)

![Untitled](%5BWorkbook%205%5D%20Building%20Flow%20Services%20-%20SEQUENCE%20a8b9a6266353486e8a0b2ddefd0adee4/workbook5_step10_2.png)


#### STEP 11. **Service**를 저장하고 실행합니다. **Results** 탭과 **IS Server log**를 확인합니다.
- **실패하려면 /notthere.txt를** **파일로** **입력합니다. IS Server log에 error message가** **있는지** **확인합니다.**
- **성공하려면 /webM/IS01/test.txt 를 입력합니다. 성공적으로 실행되면 파일 내용이 Results 탭에 표시되고 IS Server log에 error message가 표시되지 않습니다.**


## Check Your Understanding
#### QUIZ 1. 실패할 것을 알고 있는 서비스를 사용할 때 Flowservice 내부에서 어떻게 에러를 처리할 수 있습니까? (2가지 방법)
#### QUIZ 2. riskyOperation service 가 실행 되면 어떻게 되나요?


