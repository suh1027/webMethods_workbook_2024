# [Workbook 15]  JDBC Adapter Notifications

## Overview

이번 exercise 에서는, 데이터베이스 inserts 를 볼 수 있는 Notification Service 를 생성할 수 있습니다. 새로운 orders 이 ordering interface 의 데이터베이스에 입력 되면, 시스템과 서비스가 insertion(삽입) 을 인식 할 수 있도록 Notification document 를 게시해야 합니다.

## Steps
#### STEP 0. 상위 폴더 아래 IF0014 와 그 아래 adpt, noti, svc 폴더를 생성합니다.

#### STEP 1.IF0014.noti 폴더아래 IF0014_ORA_noti 라는 새 Adapter Notification 을 생성합니다. JDBC Adapter type 이 되도록 지정하고, InsertNotification template 선택, Adapter Connection Alias 는 CUDO_ConnORA:CUDO_SJH 를 사용하세요.
기본 Punblish Document 이름인 orderCanonicalNotifierPublishDocument 을 변경하지 말고 Finish를 클릭하세요.

![Untitled](%5BWorkbook%2015%5D%20JDBC%20Adapter%20Notifications%20366348d839fe499f9a7892f1bbd20595/Untitled.png1)

#### STEP 2. 다음과 같이 Adapter Notification 을 구성합니다:
- Notification Configure tab에서, Base Name 을 ORDER로 지정합니다.
    
![Untitled](%5BWorkbook%2015%5D%20JDBC%20Adapter%20Notifications%20366348d839fe499f9a7892f1bbd20595/Untitled%201.png2)
    
- Table tab에서, Table Name을 Acme.dbo.ORDER_HEADER으로 선택하세요.
    

![Untitled](%5BWorkbook%2015%5D%20JDBC%20Adapter%20Notifications%20366348d839fe499f9a7892f1bbd20595/Untitled%202.png3)

- **Joins** tab 은 skip 합니다.

- SELECT tab 에서, Insert Row 버튼을 한번 클릭, 다음 Fill in all rows to the table 버튼을
       클릭하세요.  

![Untitled](%5BWorkbook%2015%5D%20JDBC%20Adapter%20Notifications%20366348d839fe499f9a7892f1bbd20595/Untitled%203.png4)

- **WHEN** 및**Adapter Settings** tabs 을 skip 합니다. 
- 작업을 저장하세요.

#### STEP 3. [IS](http://3.IS) Administration Console에서, 
 **Adapters** →**JDBC Adapter → Polling Notifications** link. 
새로운 notification service  목록들을 볼 수 있습니다.   

![Untitled](%5BWorkbook%2015%5D%20JDBC%20Adapter%20Notifications%20366348d839fe499f9a7892f1bbd20595/Untitled%204.png5)

#### STEP 4.  Notification Schedule 편집은**Edit Schedule** 아이콘을 클릭하세요. 다음 parameters 를 지정한 다음 **Save Settings** 을 선택합니다:
- Interval =10
- Overlap=unchecked
- Immediate=unchecked

![Untitled](%5BWorkbook%2015%5D%20JDBC%20Adapter%20Notifications%20366348d839fe499f9a7892f1bbd20595/Untitled%205.png6)

- Notification Scheule 을 Enable합니다.

![Untitled](%5BWorkbook%2015%5D%20JDBC%20Adapter%20Notifications%20366348d839fe499f9a7892f1bbd20595/Untitled%206.png7)

#### STEP 5. Designer 에서 , **CUDO_SJH.**‌**IF0014.‌trigger:orderCanonicalInsertTrigger** 라는 새로운 Broker Local Trigger 을 생성합니다:   
![Untitled](%5BWorkbook%2015%5D%20JDBC%20Adapter%20Notifications%20366348d839fe499f9a7892f1bbd20595/Untitled%206.png8)
    
- 생성된 Drag ‌**PurchaseOrder.‌notifiers:IF0014_ORA_notiPublishDocumentt** 를 Trigger 의 Condition detail 패널에 있는 첫 번째 Document type 행에 추가합니다.
  
![Untitled](%5BWorkbook%2015%5D%20JDBC%20Adapter%20Notifications%20366348d839fe499f9a7892f1bbd20595/Untitled%206.png9)
    
- 기존 서비스 ‌**CUDO_SJH.IF0014.noti:‌processOrderCanonical** 를 drag 하여 새 trigger Condition detail 패널에 있는 Service field 에 입력합니다.  
    
*Hint*: 드래그된 **processOrderCanonical** 서비스는 **documentToXMLString** 서비스를 호출하여 수신 문서를 XML 표현을 포함하는 문자열로 변환합니다. 이건 XML document 를 IS Server log 에 나열하기 위해 **debugLog** 서비스를 호출합니다.
    
- Trigger definition 을 저장 합니다.
    
완성된 Trigger 는 다음과 같아야 합니다:
    

![Untitled](%5BWorkbook%2015%5D%20JDBC%20Adapter%20Notifications%20366348d839fe499f9a7892f1bbd20595/Untitled%207.png)

#### STEP 6. 이전 exercise 에서 **insertOrderCanonical** 서비스를 실행하여 작업을 테스트 합니다. 동일한 파일(**...\‌IntegrationServer\‌packages\‌AcmeSupport\‌pub\‌order_canonical_input.txt**)을 다시 로드할 수 있습니다.    **Include empty values for String Types** 을 체크하고 **OK** 를 클릭하세요. IS Server Log 에서 polling interval (10 seconds) 내에 orderHeader document 의 XML 표현이 표시되어야 합니다.         

![Untitled](%5BWorkbook%2015%5D%20JDBC%20Adapter%20Notifications%20366348d839fe499f9a7892f1bbd20595/Untitled%208.png)

#### STEP 7. IS Administration Console 을 사용하여 선택 :**Adapters** → **JDBC Adapter → Polling Notifications**

Polling Notification 을 Disable 합니다.   


## Check Your Understanding

#### QUIZ 1. JDBC Adapter Notification 로 작업할 때 자동으로 생성되고 업데이트 되는 항목은 무엇입니까?
#### QUIZ 2. JDBC Adapter Notification Schedule 이 enabled 되면 어떻게 됩니까?
#### QUIZ 3. JDBC Adapter Notification Schedule 이 administrative task 인 이유는 무엇입니까?
