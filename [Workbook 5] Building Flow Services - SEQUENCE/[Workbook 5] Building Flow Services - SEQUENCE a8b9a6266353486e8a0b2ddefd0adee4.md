# [Workbook 5] Building Flow Services - SEQUENCE

**※ Overview**

이 연습에서는 **Flow service**에 **Sequence service**를 사용하여 **Try/Catch**를 사용하여 시도합니다. **Exception**로 반환되는 **service**를 만들고 **Try/Catch Sequence**에서 **service**를 내장합니다. 

---

**※ Steps**

1. **acme.PurchaseOrder.work** 폴더에서 **riskOperation**이라는 새 **Flow service**를 만듭니다. **input**은 **fileName**이라는 **String**으로, **output**은 **String**이라는 **result**로 설정합니다. 
    
    ![Untitled](%5BWorkbook%205%5D%20Building%20Flow%20Services%20-%20SEQUENCE%20a8b9a6266353486e8a0b2ddefd0adee4/Untitled.png)
    

1. **pub.file:getFile**를 **service**에 추가하고 **fileName**을 **filename**에 매핑합니다.   
    
    ![Untitled](%5BWorkbook%205%5D%20Building%20Flow%20Services%20-%20SEQUENCE%20a8b9a6266353486e8a0b2ddefd0adee4/Untitled%201.png)
    
    ![Untitled](%5BWorkbook%205%5D%20Building%20Flow%20Services%20-%20SEQUENCE%20a8b9a6266353486e8a0b2ddefd0adee4/Untitled%202.png)
    

1. **string:bytesToString**를 **service**에 추가합니다.
    1. **body/bytes**를 **bytes**로 연결하고 **string**을 **result**로 연결합니다. .
    2. **Pipeline Out**에서 다른 모든 변수를 **drop** 합니다.
    
    ![Untitled](%5BWorkbook%205%5D%20Building%20Flow%20Services%20-%20SEQUENCE%20a8b9a6266353486e8a0b2ddefd0adee4/Untitled%203.png)
    
    ![Untitled](%5BWorkbook%205%5D%20Building%20Flow%20Services%20-%20SEQUENCE%20a8b9a6266353486e8a0b2ddefd0adee4/Untitled%204.png)
    

1. **Service**를 저장하고 실행합니다. **c:\notthere.txt**의 **input fileName**을 제공합니다**.** (또는 존재하지 않는 다른 파일) 어떤 **result**를 받나요? **c:\autoexec.bat** 같은 기존 파일로 **service** 해보세요. 그럼 어떤 결과를 받나요?    
    
    ![Untitled](%5BWorkbook%205%5D%20Building%20Flow%20Services%20-%20SEQUENCE%20a8b9a6266353486e8a0b2ddefd0adee4/Untitled%205.png)
    
2. 이제 **sequenceTryCatch**라고 불리는 **acme.PurchaseOrder.work**  새로운 **service**를 만듭니다. 파일 이름이 올바르지 않는 경우 작업을 **riskyOperation**에서 발생하는 **exception**를 파악할 수 있습니다. **fileName**이라는 서비스에 대한 단일 입력 **String**과 **result**라는 단일 출력 **String**을 정의합니다.   
    
    ![Untitled](%5BWorkbook%205%5D%20Building%20Flow%20Services%20-%20SEQUENCE%20a8b9a6266353486e8a0b2ddefd0adee4/Untitled%206.png)
    

1. **sequenceTryCatch** **service**에서 다음과 같이 세 개의 **SEQUENCE**를 추가하여 **Flow try/catch** 블록을 만듭니다. :
    1. **SEQUENCE가 SUCCESS일** **때** **종료로** **설정됨**
        1. **SEQUENCE가 FAILURE일** **때** **종료** (첫 번째 **SEQUENCE** 아래에 움푹 들어간 상태인지 확인)
        2. **SEQUENCE 가 DONE일** **때** **종료** (첫 번째 **SEQUENCE** 아래에 움푹 들어간 상태인지 확인)
        
    
    개별 **SEQUENCE**문을 만드는 동안에 **exit on**의 조건에 따라 종료를 반영하도록 **comment property**를 설정합니다. 
    
2. **SEQUENCE**가 **FAILURE**일 때 종료에서, **acme.PurchaseOrder.work:riskyOperation** **service**를 추가합니다 (실패 시 시퀀스 종료).   
    
    ![Untitled](%5BWorkbook%205%5D%20Building%20Flow%20Services%20-%20SEQUENCE%20a8b9a6266353486e8a0b2ddefd0adee4/Untitled%207.png)
    
    Pipeline 탭에서 다음과 같이 매핑합니다 :
    
    1. **fileName**에서 **fileName**으로 매핑
    2. **result**에서**result**로 매핑
    
    ![Untitled](%5BWorkbook%205%5D%20Building%20Flow%20Services%20-%20SEQUENCE%20a8b9a6266353486e8a0b2ddefd0adee4/Untitled%208.png)
    

1. **SEQUENCE**가 **DONE**일 때 종료에서, **pub.flow:getLastError** **service**를 추가합니다 (**SEQUENCE** 아래에 **DONE**이 들여쓰기 되어있는지 확인).  
    
    ![Untitled](%5BWorkbook%205%5D%20Building%20Flow%20Services%20-%20SEQUENCE%20a8b9a6266353486e8a0b2ddefd0adee4/Untitled%209.png)
    

Pipeline 탭에서 다음과 같이 매핑합니다:

1. **lastError/error**에서 **result**로 매핑
    
    ![Untitled](%5BWorkbook%205%5D%20Building%20Flow%20Services%20-%20SEQUENCE%20a8b9a6266353486e8a0b2ddefd0adee4/Untitled%2010.png)
    

1. **pub.flow:getLastError**의 호출 아래에 **pub.flow:debugLog**의 호출을 추가합니다. **lastError/error**를 **debugLog** 서비스의 **message** 입력 매개 변수에 매핑합니다. **Function**을 설정합니다.   
    
    ![Untitled](%5BWorkbook%205%5D%20Building%20Flow%20Services%20-%20SEQUENCE%20a8b9a6266353486e8a0b2ddefd0adee4/Untitled%2011.png)
    

1. **service**를 저장하고 실행합니다. **Results** 탭과 **IS Server log**를 확인합니다.
    1. **실패하려면 c:\notthere.txt를** **파일로** **입력합니다. IS Server log에 error message가** **있는지** **확인합니다.**
    2. **성공하려면 c:\autoexec.bat를 입력합니다. 성공적으로 실행되면 파일 내용이 Results 탭에 표시되고 IS Server log에  error message가 표시되지 않습니다.**

---