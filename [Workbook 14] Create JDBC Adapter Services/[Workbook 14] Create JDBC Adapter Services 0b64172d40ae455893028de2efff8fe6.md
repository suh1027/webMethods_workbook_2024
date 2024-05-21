# [Workbook 14] Create JDBC Adapter Services

**※ Overview**

이번 exercise 에서는, insert 와 select JDBC Adapter services 를 생성할 수 있습니다. 상위 Flow service 와 결합할 수 있습니다. 이들을 함께 사용하면 database 의 데이터로 쉽게 작업할 수 있습니다.

---

**※ Steps**

1. Designer 를 시작하고 acme.PurchaseOrder.adapters:insertOrderHeader 라는 새 Adapter Service를 생성합니다.
2. Adapter Service Type으로 JDBC Adapter를 선택합니다.

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%200b64172d40ae455893028de2efff8fe6/Untitled.png)

1. 다음  Adapter Connection Alias 로 commonSupport.adapters:acmeAdapter를 선택합니다.

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%200b64172d40ae455893028de2efff8fe6/Untitled%201.png)

1. 마지막으로 InsertSQL을 template으로 선택하고 Finish을 클릭합니다.

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%200b64172d40ae455893028de2efff8fe6/Untitled%202.png)

1. 생성된 JDBC Adapter Service insertOrderHeader를 다음과 같이 Configure(구성)합니다:
    1. Table tab에서, Table Name 컬럼의 첫 번째 행을 클릭하고  **Acme.dbo.ORDER_HEADER** 를 선택합니다. Click **OK.**   

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%200b64172d40ae455893028de2efff8fe6/Untitled%203.png)

        b.  **INSERT**tab 에서, 먼저 **Insert** 행 버튼을 한번 누릅니다**.**

       다음 **Fill in all rows to the Table** 버튼을 클릭 합니다.

       *참고:* 일부 JDBC Drivers 는 이 작업에 문제가 있습니다.

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%200b64172d40ae455893028de2efff8fe6/Untitled%204.png)

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%200b64172d40ae455893028de2efff8fe6/Untitled%205.png)

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%200b64172d40ae455893028de2efff8fe6/Untitled%206.png)

        c.     **Result** tab 에서, **Result Field:** **insertCount** / **Result Field Type**: **java.lang.String** 설정합니다.     

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%200b64172d40ae455893028de2efff8fe6/Untitled%207.png)

1. Package Navigator view 에서 Adapter Service 인 **insertOrderHeader** 를 저장하고 실행합니다.

      **OverrideCredentials** 및**$connectionName** 을 제외한 모든 입력 필드에 데이터를 삽입합니다.

![hit OK](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%200b64172d40ae455893028de2efff8fe6/Untitled%208.png)

hit OK

   

![    **insertCount** 가 ‘1’ 로 반환 되는지 확인홥니다.  ](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%200b64172d40ae455893028de2efff8fe6/Untitled%209.png)

    **insertCount** 가 ‘1’ 로 반환 되는지 확인홥니다.  

1. 1단계에서와 마찬가지로, acme.PurchaseOrder.adapters 폴더에 insertOrderDetails라는 또다른 Adapter Service를 생성합니다. **commonSupport.adapters:acmeAdapter** 를 사용하는 **JDBC Adapter type** 의 **Adapter Service 를 지정하고 InsertSQL** template 을 선택합니다.   

2. 생성된 JDBC Adapter Service **insertOrderDetails** 를 다음과 같이 구성합니다**:**   
    1. Table tab에서, Acme.dbo.ORDER_DETAILS를 선택합니다.
    2. INSERT tab에서, Fill in all rows 버튼을 클릭합니다. (참고: Fill in all rows in the Table 버튼을 활성화 하려면 adapter service를 저장해야 할 수 있습니다.)
    3. Result tab에서, Result Field:insertCount / Result Field Type: java.lang.String 설정하세요.
    
3. InsertOrderDetails service를 저장하고 실행합니다.
    
    OverrideCredentias 및 $connectionName 제외한 모든 입력 필드에 데이터를 삽입합니다.
    
    Hit OK. InsertCount 가 ‘1’로 반환 되는지 확인합니다.
    
4.   **acme.PurchaseOrder.adapters** 폴더에 **selectOrderHeader** 라는 새로운 Adapter Service 를 생성하세요.  **JDBC Adapter type** 의 **Adapter Service** 로       **commonSupport.adapters:acmeAdapter** 를 사용하고**, SelectSQL** template 를 선택하세요.   

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%200b64172d40ae455893028de2efff8fe6/Untitled%2010.png)

1. 생성된JDBC Adapter Service **selectOrderHeader** 를 다음과 같이 구성합니다:
    
    a. **Tables** tab 에서, in the first row 선택, **Table Name** 으로 **Acme.dbo.ORDER_HEADER** 을 선택 합니다.   
    
    ![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%200b64172d40ae455893028de2efff8fe6/Untitled%2011.png)
    
    b. Joins tab 을 skip하세요.
    
    c. SELECT tab에서 , select ALL. Insert Row 버튼을 먼저 클릭하고 , 다음 Fill in all rows to the Table 버튼을 클릭하세요.
    

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%200b64172d40ae455893028de2efff8fe6/Untitled%2012.png)

      d. WHERE tab 을 skip하세요.

e. Input/Output tab에서, 생성된 Document type을 검토하세요. results Document List 아래에 선택한 데이터 베이스 컬럼이 있어야 합니다.

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%200b64172d40ae455893028de2efff8fe6/Untitled%2013.png)

1. selectOrderHeader service를 저장하고 실행하세요. 이 Adapter Service는 input을 제공할 필요가 없습니다. Database table이 이 6단계의 데이터로 채워졌는지 확인합니다.

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%200b64172d40ae455893028de2efff8fe6/Untitled%2014.png)

1. **PurchaseOrder.adapters** 폴더에 **selectOrderDetails** 라는 마지막 Adapter Service 를 생성하세요. **JDBC Adapter** type 의 **Adapter Service** 로 **commonSupport.adapters:acmeAdapter** **를** **사용하고, SelectSQL** template 를 선택하세요. 
2. 생성된JDBC Adapter Service selectOrderDetails 를 다음과 같이 구성합니다:
    1. Table tab에서, Acme.dbo.ORDER_DETAILS선택하세요.
    2. Joins tab 을 skip하세요.
    3. Select tab 에서, select ALL. Insert Row 버튼을 한번 클릭 후 , Fill in all rows to the Table 버튼을 클릭하세요.
    4. WHERE tab 을 skip 하세요.
    5. **Input/Output** tab 에서, 생성된Document type 을 검토하세요. results Document List 아래에 선택한 데이터베이스 컬럼을 확인 할 수 있습니다.
3. selectOrderDetails service를 저장하고 실행하세요. 데이터베이스 테이블이 9단계의 데이터로 채워졌는지 확인하세요.

**다음 몇 단계에서는, 데이터베이스에 canonical order 을 저장하는데 필요한 service logic 을 생성합니다. 이건 order 에 속한 order header 와 order details 을 저장하는 것을 의미합니다.**

1. **PurchaseOrder.utils** 폴더에서, **insertOrderCanonical** 라는 새로운 Flow service 를 생성하세요**.** 이름이 **OrderCanonical** **인** **acme.PurchaseOrder.docs:OrderCanonical** document 에 대한 Document Reference(참조) 가 되도록 설정하세요.
    
    a. **Tree** tab 으로 전환하고 **acme.**‌**PurchaseOrder.‌adapters** 를 드래그 합니다
        **:‌insertOrderHeader** 를 서비스에 삽입합니다. Map all the fields from
        **OrderCanonical/Header** 의 모든 필드를 **insertOrderHeaderInput** 에서 비슷한 이름의 
        필드로 매핑합니다. Sender/ID 및 Receiver/ID 필드에서 매핑해야 합니다!   
       **overrideCredentials** 또는 **$connectionName** 매핑하지 마십시오.   
    

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%200b64172d40ae455893028de2efff8fe6/Untitled%2015.png)

         ****b. **LOOP** 단계를 추가하고 Input array property(속성) 을 **/OrderCanonical/Items** 로 설정합니다.

    c. **acme.PurchaseOrder.adapters:insertOrderDetails** 를 서비스로 드래그 하고 LOOP  단계 안으로 들여쓰기 합니다.   

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%200b64172d40ae455893028de2efff8fe6/Untitled%2016.png)

    Pipeline view 를 사용하여 insertOrderDetails 서비스 호출에서 **OrderCanonical/Items** 가 더 이상 array 가 아닌지 확인하십시오.     

다음 map을 따라오세요 :
 1.  **OrderCanonical/Header/OrderID**를 **insertOrderDetailsInput/ORDER_ID**로 매핑

 2. **OrderCanonical/Header/TransactionID**를 **insertOrderDetailsInput/TRANSACTION_ID**로 매핑

1. **OrderCanonical/Items/SKU**를 **insertOrderDetailsInput/SKU**로 매핑
2. **OrderCanonical/Items/Quantity**를 **insertOrderDetailsInput/Quantity**로 매핑   

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%200b64172d40ae455893028de2efff8fe6/Untitled%2017.png)

1.     **...\‌IntegrationServer\‌packages\‌AcmeSupport\‌pub\‌order_canonical_input.txt** 파일 데이터로 로드된 **acme.PurchaseOrder.utils:insertOrderCanonical** 서비스를 저장 하고 실행 합니다.   

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%200b64172d40ae455893028de2efff8fe6/Untitled%2018.png)

18. 두 개의 Select JDBC Adapter Services (**selectOrderHeader** 및 **selectOrderDetails**) 를 사용하여 테이터베이스 테이블을 확인하고 **insertOrderCanonical** 서비스가 올바르게 작동하는지 확인합니다.

---

**※ Check Your Understanding**

1. Adapter service templates 을 사용하기 전에 어떤 administrative activity (활동)을 수행해야 합니까 ?
2. insertOrderDetails 필드를 매핑하기 전에 LOOP input array 를 지정하는 것이 중요한 이유는 무엇입니까?