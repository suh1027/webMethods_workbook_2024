# [Workbook 14] Create JDBC Adapter Services

## Overview

이번 연습 에서는 JDBC Connection 을 활용하여 Adapter services 를 생성, Database 의 데이터를 쉽게 작업할 수 있습니다.

JDBC Adapter Service 는 일종의 Database 에 쿼리문을 수행하는 서비스로 

이번 연습에서는 **SELECT, UPDATE, INSERT, BATCH UPDATE** 네가지의 Adpater Service 를 연습합니다.


## Steps

#### STEP 1. 최상위 폴더 아래 IF0013 을 생성한 후 그 아래 svc, adpt 폴더를 생성합니다.

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/Untitled.png)

#### STEP 2. IS Server에서 Adapter Connection Alias를 생성합니다.

- IS 웹 관리자 화면에 접속하여 좌측 Adapters > webMethods Adapter for JDBC 클릭

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/15a2d6c8-9f90-49fd-b99b-960e2516f04b.png)

- webMethods Adapter for JDBC Connection 클릭하여 JDBC Conenction 을 생성합니다.

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/Untitled%201.png)

- 접속할 DB 접속 정보 입력 후 Test Connection 성공하면 Save Connection 을 클릭하여 커넥션을 저장합니다.  
      **DB 접속 정보**
    - Folder Name : CUDO_Conn.ORA
    - Connection Name : {회사명}_{이니셜} (ex. CUDO_SJH)
    - DataSource Class : oracle.jdbc.pool.OracleDataSource
    - Server Name : 192.168.1.54
    - User : {회사명}_{이니셜} 
    - password : {회사명}_{이니셜}
    - Database Name : XE
    - Port Number : 1521
    - Other Properties : driverType=Thin
      **계정 문제로 접속이 되지 않을 시 문의 부탁드립니다.**
![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/Untitled%202.png)


- Save Connection 을 눌러 생성 된 본인의 커넥션을 확인 후 Enbled 의 no 를 yes로 변경하여 커넥션을 활성화 합니다.

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/Untitled%203.png)

- Designer 로 돌아가 Package Navigator 서버에서 우클릭 Refresh 하여 커넥션 컴포넌트가 생성 되었는지 확인합니다.

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/Untitled%204.png)


---

#### STEP 3. Select 쿼리문을 수행하는 Select Adapter Service 를 생성하고, 실행 시켜 Database 로 부터 정상적인 데이터를 Select 할 수 있는지 확인합니다.

- IF0013.adpt 폴더 아래 새로운 Adapter Service 를 생성합니다.
- adpt 폴더 에서 우클릭 New > Adapter Service 를 클릭하여 새로운 Adapter Service 를 생성합니다.
![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/Untitled%205.png)

- Adapter Service 명은 IF0013_SRC_S_01 로 입력 후 Next를 클릭합니다.
![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new1.png)
**Note.** Adpater Service 의 네이밍 룰은 고객사별 상이하며, 일반적으로 IFID + SRC/TGT 시스템 명 + 로직 + 시퀀스 번호 로 구분하여 생성합니다.

- 다음 화면에서 설치된 Adapter 목록을 확인할 수 있습니다. 이번 연습에서는 JDBC Adpater 를 사용할 것이므로 JDBC Adpater 를 선택 후 Next 를 누릅니다.
![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new2.png)

- 다음 화면에서는 IS 관리자 웹 페이지에서 생성 한 JDBC 커넥션 리스트를 확인하실 수 있습니다. 본인이 생성한 Connection 명을 선택 하시고 Next 를 누릅니다.
![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new3.png)

- 실행 할 쿼리문의 템플릿을 선택합니다. JDBC Adapter 는 GUI 환경에서 개발 할 수 있도록 미리 생성 된 템플릿을 사용하여 쿼리문 서비스를 수행합니다. SelectSQL 을 선택 후 Finish 를 눌러 생성합니다.
![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new4.png)

**Note.** 생성 된 Adapter 서비스는 Flowservice 에서 서비스 단계로 추가하여 사용하거나, 단독으로 Service 를 수행하여 사용하실 수 있습니다.

- 다음은 생성 된 Adapter Service 개발 방법 입니다. 생성 된 Select Adpater 의 Table 탭에서는 Select 쿼리문을 수행 할 테이블을 선택할 수 있습니다. ... 아이콘을 클릭합니다.
![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new5.png)

- 개인별로 미리 생성 된 계정 (회사명_이니셜) 과 동일한 이름의 Schema 로 접속하여 SRC_EMPLOYEES_TABLE 을 선택 후 OK 를 누릅니다.
![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new6.png)
**스키마가 보이지 않거나, 테이블이 없는 경우 문의해주세요**

- Adapter Service 를 저장하고, SELECT 탭을 클릭합니다. 해당 탭에서는 SELECT 문에서 SELECT 할 필드들을 선택합니다. 선택한 테이블의 필드를 그대로 가져올 수 있습니다.
     - Insert Row 를 클릭하여 필드를 개별 등록 가능
     - Fill in all rows to the Table 을 클릭하여 모든 필드 한번에 등록 가능
![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new7.png)
![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new8.png)


- 다음은 SELECT 문의 세부 설정입니다. SELECT 할 Row 의 수, Timeout 설정, Result Field 를 설정 할 수 있습니다.
     - Maximum Row : 한번에 SELECT 할 Row 의 수 지정 (Default : 0, 전체 Row 한번에 SELECT)
     - Query Time out : -1 (Query 실행 Timeout 시간을 초단위로 지정, -1 은 별도의 Timeout 설정 없이 실행 됨)
     - Result Field : Select 레코드 수를 출력할 필드명 지정 (ex. record_count)
     - Result Field Type : Result Field 의 타입 지정 (Integer, String 으로 지정이 가능하며 String 을 권장)  
![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new9.png)

- WHERE 탭에서 SELECT 문의 조건을 설정할 수 있습니다. WHERE 조건에 EAI_FLAG 값을 기준으로 다음과 같이 설정합니다.
       - Insert Row 를 클릭하여 하나의 조건절을 추가하고, EAI_FLAG 컬럼을 지정, Input Field 에 'N' 을 입력하고 저장합니다.
![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new10.png)


- 저장 된 Adapter Service 를 우클릭하여 Run As > Run Service 를 눌러 서비스를 실행시켜 결과값을 확인합니다. 
![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new12.png)
![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new11.png)


---

#### STEP 4. Insert 쿼리문을 수행하는 Insert Adapter Service 를 생성하고, 실행 시켜 테이블에 데이터를 Insert 할 수 있는지 확인합니다.


---


### UPDATE




---

### BATCH UPDATE



---

#### STEP 3. IF0013.adpt 아래 IF0013_ORA_I_01 라는 새 Adapter Service 를 생성합니다.

- adpt 폴더 에서 우클릭 New > Adapter Service 를 클릭하여 새로운 Adapter Service 를 생성합니다.


- Adapter Service 명은 IF0013_ORA_I_01 로 지정합니다.
![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/Untitled%206.png)

- **Adapter Service Type** 은 **JDBC Adapter**를 선택합니다.
![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/Untitled%207.png)

- 다음 **Adapter Connection Alias** 로 **본인이 생성한 커넥션을**를 선택합니다.

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/Untitled%208.png)

- 마지막으로 **InsertSQL**을 template 을 선택하고 Finish을 클릭합니다.

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/Untitled%209.png)

- 생성된 JDBC Adapter Service "IF0013_ORA_I_01" 를 다음과 같이 Configure(구성)합니다.

    -  Table tab 에서 Insert 쿼리문을 수행 할 Table 을 선택합니다. Table Name 을 클릭하여 **본인의 스키마 명.ORDER_HEADER**을 선택합니다.
       

    ![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/Untitled%2010.png)

    **해당 ORDER_HEADER 테이블이 생성되어 있지 않은 경우 문의 부탁드립니다.**
  
    ![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/Untitled%2011.png)

    - 이제 Insert 쿼리문을 설정하기 위해 **INSERT** tab 을 클릭합니다. 다음 **Fill in all rows to the Table** 버튼을 클릭 합니다.
          **Note.** 해당 옵션은 테이블의 모든 행을 불러오는 기능입니다.

    ![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/Untitled%2012.png)

    ![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/Untitled%2013.png)

    ![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/Untitled%2014.png)

    - **Result tab** 에서 Insert 문의 성공 실패를 확인하기 위해 Result 필드를 선언합니다. **Result Field: results** / **Result Field Type: java.lang.String** 설정합니다

//// Insert Count 가 아니라 Insert 문은 Result 가 1(성공) 0(실패) 로 표현됩니다. 캡쳐 수정해주세요 results 로 변경////

    ![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/Untitled%2015.png)

    - Adapter Service 인 **IF0013_ORA_I_01**를 저장하고 우클릭 → Run As → Run Service를 눌러 실행합니다.

    ![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/Untitled%2016.png)

    - 모든 입력 필드에 데이터를 삽입합니다.
  
    ![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/Untitled%2017.png)

    - **results** 가 ‘1’ 로 반환되어 DB에 정상적으로 Insert 되었는지 확인합니다.
  
    ![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/Untitled%2018.png)

#### STEP 4. 위 단계와 마찬가지로, IF0013.adpt 폴더에 IF0013_ORA_I_02  라는 또 다른 Adapter Service를 생성합니다. CUDO_Conn.ORA:CUDO_SJH 를 사용하는 JDBC Adapter type 의 Adapter Service 를 지정하고 InsertSQL template 을 선택합니다. 

// 캡쳐 추가해 주세요 //

- 생성된 JDBC Adapter Service  **IF0013_ORA_I_02** 를 다음과 같이 구성합니다.
  
    - Table tab에서, **CUDO_SJH.ORDER_DETAILS**를 선택합니다.
  
    - INSERT tab에서, Fill in all rows 버튼을 클릭합니다.
  
    - Result tab에서, Result Field:insertCount / Result Field Type: java.lang.String 설정하세요.

- **IF0013_ORA_I_02** service를 저장하고 실행합니다.
    
    OverrideCredentias 및 $connectionName 제외한 모든 입력 필드에 데이터를 삽입합니다.
    
    InsertCount 가 ‘1’로 반환 되는지 확인합니다.

#### STEP 5. IF0013.adpt 폴더에 IF0013_ORA_S_01 라는 새로운 Adapter Service 를 생성하세요. JDBC Adapter type 의 Adapter Service 로  CUDO_Conn.ORA:CUDO_SJH 를 사용하고, SelectSQL template 를 선택하세요.  

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/Untitled%2019.png)

- 생성된 JDBC Adapter Service **IF0013_ORA_S_01** 를 다음과 같이 구성합니다.

    - **Tables tab** 에서, in the first row 선택, **Table Name** 으로 CODO_Conn.ORDER_HEADER 을 선택합니다.
 
      ![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/Untitled%2020.png)

    - Joins tab은 skip 하세요.
 
    - **SELECT tab**에서 , **select ALL**. **Insert Row** 버튼을 먼저 클릭하고 , **Fill in all rows to the Table** 버튼을 클릭하세요.
     
      ![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/Untitled%2021.png)

    - **Input/Output tab**에서, 생성된 Document type을 검토하세요. **results Document List** 아래에 선택한 데이터 베이스 컬럼이 있어야 합니다.
     
      ![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/Untitled%2022.png)

- **IF0013_ORA_S_01** service를 저장하고 실행하세요. 이 Adapter Service는 input을 제공할 필요가 없습니다. Database table이 이  **IF0013_ORA_I_01** service로 insert했던 데이터로 채워졌는지 확인합니다.

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/Untitled%2023.png)

#### STEP 6. IF0013.adpt 폴더에 IF0013_ORA_S_02 라는 마지막 Adapter Service 를 생성하세요. JDBC Adapter type 의 Adapter Service 로 CUDO_Conn.ORA:CUDO_SJH를 사용하고, SelectSQL template 를 선택하세요. 

- 생성된 JDBC Adapter Service  **IF0013_ORA_S_02** 를 다음과 같이 구성합니다:
    - Table tab에서 **CUDO_SJH.ORDER_DETAILS**선택하세요.
    - Select tab 에서, select ALL. Insert Row 버튼을 한번 클릭 후 , Fill in all rows to the Table 버튼을 클릭하세요..
    - **Input/Output** tab 에서, 생성된Document type 을 검토하세요. results Document List 아래에 선택한 데이터베이스 컬럼을 확인 할 수 있습니다.

- **IF0013_ORA_S_02**  service를 저장하고 실행하세요. 데이터베이스 **IF0013_ORA_I_02**  service로 insert했던  데이터로 채워졌는지 확인하세요.

다음 몇 단계에서는, 데이터베이스에 canonical order 을 저장하는데 필요한 service logic 을 생성합니다. 이건 order 에 속한 order header 와 order details 을 저장하는 것을 의미합니다.

#### STEP 7. CUDO_SJH.IF0013.svc 폴더에서, svc_IF0013_insertOrderCanonical 라는 새로운 Flow service 를 생성하세요. 이름이 TestOrderCanonical 인 acmeSupport.docs:TestOrderCanonical document 에 대한 Document Reference(참조) 가 되도록 설정하세요.

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/Untitled%2024.png)

- **Tree tab** 으로 전환하고 **CUDO_SJH.IF0013.adpt:IF0013_ORA_I_01**를 드래그 합니다.‌ **IF0013_ORA_I_01**를 서비스에 삽입합니다. Map all the fields from **testOrderCanonical/Header**의 모든 필드를 **IF0013_ORA_I_01Input** 에서 비슷한 이름의 필드로 매핑합니다. Sender/ID 및 Receiver/ID 필드에서 매핑해야 합니다! **overrideCredentials** 또는 **$connectionName** 매핑하지 마십시오.

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/Untitled%2025.png)

- **LOOP** 단계를 추가하고 Input array property(속성) 을 **/TestOrderCanonical/Items** 로 설정합니다.
 
![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/Untitled%2026.png)

- **CUDO_SJH.IF0013.adpt:IF0013_ORA_I_02** 를 서비스로 드래그 하고 **LOOP** 단계 안으로 들여쓰기 합니다. 
 
![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/Untitled%2027.png)

Pipeline view 를 사용하여 **IF0013_ORA_I_02** 서비스 호출에서 **TestOrderCanonical/Items** 가 더 이상 array 가 아닌지 확인하십시오.
    
![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/Untitled%2028.png)

다음 map 을 따라오세요.

- **TestOrderCanonical/Header/OrderID**를 **IF0013_ORA_I_02Input/ORDER_ID**로 매핑
  
- **TestOrderCanonical/Header/TransactionID**를 **IF0013_ORA_I_02Input/TRANSACTION_ID**로 매핑
  
- **TestOrderCanonical/Items/SKU**를 **IF0013_ORA_I_02Input/SKU**로 매핑
  
- **TestOrderCanonical/Items/Quantity**를 **IF0013_ORA_I_02Input/Quantity**로 매핑

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/Untitled%2029.png)

- **CUDO_SJH.IF0013.svc:svc_IF0013_insertOrderCanonical** 서비스를 저장 하고 실행 합니다.

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/Untitled%2030.png)

- 두 개의 Select JDBC Adapter Services (**IF0013_ORA_S_01** 및 **IF0013_ORA_S_02**) 를 사용하여 테이터베이스 테이블을 확인하고 **svc_IF0013_insertOrderCanonical** 서비스가 올바르게 작동하는지 확인합니다.

## Check Your Understanding

#### QUIZ 1. Adapter service templates 을 사용하기 전에 어떤 administrative activity (활동)을 수행해야 합니까 ?
#### QUIZ 2. insertOrderDetails 필드를 매핑하기 전에 LOOP input array 를 지정하는 것이 중요한 이유는 무엇입니까?
