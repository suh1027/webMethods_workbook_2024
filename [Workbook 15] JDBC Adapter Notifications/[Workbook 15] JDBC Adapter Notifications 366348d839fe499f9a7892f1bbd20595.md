# [Workbook 15]  JDBC Adapter Notifications

**※ Overview**

이번 exercise 에서는, 데이터베이스 inserts 를 볼 수 있는 Notification Service 를 생성할 수 있습니다. 새로운 orders 이 ordering interface 의 데이터베이스에 입력 되면, 시스템과 서비스가 insertion(삽입) 을 인식 할 수 있도록 Notification document 를 게시해야 합니다.

---

**※ Steps**

1. acme.PurchaseOrder.notifiers 폴더에 orderCanonicalNoifier 라는 새 Adapter Notification을 생성합니다. 
JDBC Adapter type이 되도록 저장하고, InsertNotification template 선택, Adapter Connection Alias는 commonSupport.adapters:acmeAdapter를 사용하세요.
기본 Punblish Document 이름인 orderCanonicalNotifierPublishDocument 을 변경하지 말고 Finish를 클릭하세요.

![Untitled](%5BWorkbook%2015%5D%20JDBC%20Adapter%20Notifications%20366348d839fe499f9a7892f1bbd20595/Untitled.png)

1. 다음과 같이 Adapter Notification 을 구성합니다:
    1. Notification Configure tab에서, Base Name 을 ORDER로 지정합니다.
    
    ![Untitled](%5BWorkbook%2015%5D%20JDBC%20Adapter%20Notifications%20366348d839fe499f9a7892f1bbd20595/Untitled%201.png)
    
     b. Table tab에서, Table Name을 Acme.dbo.ORDER_HEADER으로 선택하세요.
    

![Untitled](%5BWorkbook%2015%5D%20JDBC%20Adapter%20Notifications%20366348d839fe499f9a7892f1bbd20595/Untitled%202.png)

         c. **Joins** tab 은 skip 합니다.

   d. SELECT tab 에서, Insert Row 버튼을 한번 클릭, 다음 Fill in all rows to the table 버튼을
       클릭하세요.  

![Untitled](%5BWorkbook%2015%5D%20JDBC%20Adapter%20Notifications%20366348d839fe499f9a7892f1bbd20595/Untitled%203.png)

    e. **WHEN** 및**Adapter Settings** tabs 을 skip 합니다. 

    f.작업을 저장하세요.

1. [IS](http://3.IS) Administration Console에서, 
 **Adapters** →**JDBC Adapter → Polling Notifications** link. 
새로운 notification service  목록들을 볼 수 있습니다.   

![Untitled](%5BWorkbook%2015%5D%20JDBC%20Adapter%20Notifications%20366348d839fe499f9a7892f1bbd20595/Untitled%204.png)

1.  Notification Schedule 편집은**Edit Schedule** 아이콘을 클릭하세요. 다음 parameters 를 지정한 다음 **Save Settings** 을 선택합니다:
- Interval =10
- Overlap=unchecked
- Immediate=unchecked

![Untitled](%5BWorkbook%2015%5D%20JDBC%20Adapter%20Notifications%20366348d839fe499f9a7892f1bbd20595/Untitled%205.png)

b.Notification Scheule 을 Enable합니다.

![Untitled](%5BWorkbook%2015%5D%20JDBC%20Adapter%20Notifications%20366348d839fe499f9a7892f1bbd20595/Untitled%206.png)

1. Designer 에서 , **acme.**‌**PurchaseOrder.‌notifiers:‌orderCanonicalInsertTrigger** 라는 새로운 Broker Local Trigger 을 생성합니다:   
    
    a.생성된 Drag ‌**PurchaseOrder.‌notifiers:‌orderCanonicalNotifierPublishDocument** 를 Trigger 의 Condition detail 패널에 있는 첫 번째 Document type 행에 추가합니다.
    
    b.기존 서비스 ‌**PurchaseOrder.‌notifiers:‌processOrderCanonical** 를 drag 하여 새 trigger Condition detail 패널에 있는 Service field 에 입력합니다.  
    
    *Hint*: 드래그된 **processOrderCanonical** 서비스는 **documentToXMLString** 서비스를 호출하여 수신 문서를 XML 표현을 포함하는 문자열로 변환합니다. 이건 XML document 를 IS Server log 에 나열하기 위해 **debugLog** 서비스를 호출합니다.
    
    c. Trigger definition 을 저장 합니다.
    
        완성된Trigger 는 다음과 같아야합니다:
    

![Untitled](%5BWorkbook%2015%5D%20JDBC%20Adapter%20Notifications%20366348d839fe499f9a7892f1bbd20595/Untitled%207.png)

1. 이전 exercise 에서 **insertOrderCanonical** 서비스를 실행하여 작업을 테스트 합니다. 동일한 파일(**...\‌IntegrationServer\‌packages\‌AcmeSupport\‌pub\‌order_canonical_input.txt**)을 다시 로드할 수 있습니다.    **Include empty values for String Types** 을 체크하고 **OK** 를 클릭하세요. IS Server Log 에서 polling interval (10 seconds) 내에 orderHeader document 의 XML 표현이 표시되어야 합니다.         

![Untitled](%5BWorkbook%2015%5D%20JDBC%20Adapter%20Notifications%20366348d839fe499f9a7892f1bbd20595/Untitled%208.png)

1. IS Administration Console 을 사용하여 선택
: **Adapters** → **JDBC Adapter → Polling Notifications**
 Polling Notification 을 Disable 합니다.   

---

**※ Check Your Understanding**

1. JDBC Adapter Notification 로 작업할 때 자동으로 생성되고 업데이트 되는 항목은 무엇입니까?
2. JDBC Adapter Notification Schedule 이 enabled 되면 어떻게 됩니까?
3. JDBC Adapter Notification Schedule 이 administrative task 인 이유는 무엇입니까?