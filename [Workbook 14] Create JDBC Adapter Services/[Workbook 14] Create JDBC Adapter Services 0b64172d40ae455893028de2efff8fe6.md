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

### SELECT

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

### INSERT

#### STEP 4. Insert 쿼리문을 수행하는 Insert Adapter Service 를 생성하고, 실행 시켜 테이블에 데이터를 Insert 할 수 있는지 확인합니다.

- 새로운 Adapter Service 를 생성합니다.

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/Untitled%205.png)

- Adapter Service 명은 IF0013_SRC_I_01 로 입력 후 이후 본인이 생성한 동일한 커넥션을 선택합니다.

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new13.png)

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new14.png)

- InsertSQL 을 선택 후 Finish

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new15.png)

- 생성 된 Insert Adapter Service 를 클릭합니다. SELECT 와 동일하게 TABLE 탭에서 INSERT 쿼리를 수행할 테이블을 선택합니다.

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new16.png)

- 테이블은 동일하게 본인 스키마 안에 있는 SRC_EMPLOYEES_TABLE 테이블을 선택합니다.

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new17.png)

- Adapter Service 저장 후 INSERT 탭으로 가서 테이블에 INSERT 할 필드들을 선택합니다.

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new18.png)

- EAI_FLAG 필드의 Expression 부분에 'N' 으로 설정하여 특정 고정값이 INSERT 되도록 설정할 수 있습니다.

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new19.png)

- Result 탭으로 이동하여 Insert Adapter Service 의 성공/실패 여부를 판단할 필드 Result Field 를 설정할 수 있습니다.

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new20.png)

**Note.** Insert Adapter 의 Result Field 는 Adapter Service 의 실행 성공 유무에 따라 1 또는 0 으로 반환되며, 서비스 성공 시 1, 실패 시 0 이 반환됩니다.

- 해당 서비스를 저장하고 다음과 같이 쿼리문을 실행시켜 결과값을 확인합니다.
    - 해당 테이블의 PK 값은 ID 로 1~1000 까지는 더미 데이터가 생성되어 있습니다.

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new21.png)    

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new22.png)    

- STEP 3 에서 생성 한 Select Adapter Service 를 수정 & 재 실행 하여 테이블에 데이터가 정상적으로 Insert 되었는지 확인합니다.

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new23.png)   

---

### UPDATE

#### STEP 4. Insert 쿼리문을 수행하는 Insert Adapter Service 를 생성하고, 실행 시켜 테이블에 데이터를 Insert 할 수 있는지 확인합니다.

- 새로운 Adapter Service 를 생성합니다.

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/Untitled%205.png)

- Adapter Service 명은 IF0013_SRC_U_01 로 입력 후 이후 본인이 생성한 동일한 커넥션을 선택, UpdateSQL 템플릿을 선택후 Finish 를 눌러 생성합니다.

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new24.png)

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new25.png)   

- 생성 된 Update Adapter Service 의 Table 탭에서도 동일하게 SRC_EMPLOYEES_TABLE 을 선택합니다.

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new26.png)

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new27.png)  

- UPDATE 탭에서 Update 를 수행할 필드를 선택합니다. EAI_FLAG 값을 선택 후 Expression 에 'Y' 로 입력합니다.

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new28.png)


- WHERE 탭으로 이동, ID(PK 값)을 조건으로 선택 한 후 다음과 같이 설정합니다.
    - Input Field Type 을 java.lang.String 으로 설정, Input Field 를 ID 로 입력 후 저장

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new29.png)

- Result 탭으로 이동하여 Insert Adapter 와 동일하게, Update Adapter Service 의 성공/실패 여부를 판단할 필드 Result Field 를 설정할 수 있습니다.

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new30.png)

**Note.** Update Adapter 의 Result Field 는 Adapter Service 의 실행 성공 유무에 따라 1 또는 0 으로 반환되며, 서비스 성공 시 1, 실패 시 0 이 반환됩니다.

- 서비스를 저장하고, 우클릭 하여 다음과 같이 입력 후 결과를 확인해 봅니다.

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new31.png)

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new32.png)

- Select Adapter 를 실행시켜 Select 가 되지 않으면 성공입니다, 또는 조건절을 변경시켜 EAI_FLAG 값이 'Y' 인 데이터가 있는지 조회하여 확인하실 수 있습니다.

---

### BATCH UPDATE

#### STEP 5. 다 건의 데이터를 일괄 Update 수행하는 Batch Update Adapter 서비스를 생성하고, 테이블 내 데이터에 일괄 Update 되는지 확인합니다.

- 새로운 Adapter Service 를 생성합니다.

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/Untitled%205.png)

- Adapter Service 명은 IF0013_SRC_BU_01 로 입력 후 이후 본인이 생성한 동일한 커넥션을 선택, BatchUpdateSQL 템플릿을 선택후 Finish 를 눌러 생성합니다.

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new34.png)

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new35.png)   

- 생성 된 Update Adapter Service 의 Table 탭에서 동일하게 SRC_EMPLOYEES_TABLE 을 선택합니다.

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new36.png) 

- UPDATE 탭으로 이동하여 Update 할 필드를 지정합니다. Field 를 하나 추가 후 EAI_FLAG = 'Y' 로 설정합니다.

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new37.png)

- WHERE 탭으로 이동, EAI_FLAG 값이 'N' 인 값들을 조건으로 설정합니다.

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new38.png)


- 서비스를 저장 후 실행시켜 봅니다.

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new39.png)

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new40.png)

- Select Adapter Service 를 재 실행 하여 Select 되는 값들이 있는지 확인합니다.
   - SELECT 절 조건에 EAI_FLAG = 'N' 인 값이 없어 결과 값이 0 건 결과가 리턴 됩니다.

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new41.png)

- Batch Update 의 WHERE 탭을 다음과 같이 수정 후 저장합니다.
    - WHERE 조건에 기존 EAI_FLAG 컬럼 제거
    - 필드 하나 추가 후 ID = ? 로 설정 (PK 값을 조건으로 사용)
    - 아래 부분에 Insert Row 하여 EAI 서비스 에서 ID 컬럼에 매핑될 Field 설정
        - JDBC Type : VARCHAR
        - Input Field Type : java.lang.String
        - Input Field : ID

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new42.png)


---


### UPDATE + INSERT (UPSERT)

#### STEP 6. Update Adapter Service 와 Insert Adapter Service 를 하나의 로직으로 수행하는 서비스(UPSERT)를 개발합니다.

- adpt 폴더 아래 두 개의 Adapter Serivce 를 새로 생성합니다. IF0013_TGT_I_01, IF0013_TGT_U_01 로 생성, 각 템플릿은 InsertSQL, UpdateSQL 문으로 생성합니다.

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new43.png)

- Insert Adapter Serivce 설정입니다.
   - TABLE 탭에서 TGT_EMPLOYEES_TABLE 테이블로 설정 

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new44.png)

 - INSERT 탭에서 모든 필드 (컬럼) 선택 후 저장 (**ID 값의 Input Field Type 을 java.lang.String 으로 변경 주의**)

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new45.png)

- Update Adapter Serivce 설정입니다.
   - TABLE 탭에서 TGT_EMPLOYEESTABLE 테이블로 설정

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new46.png)
   - UPDATE 탭에서 ID(PK값) 를 제외한 모든 필드 선택

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new47.png)
          
 - WHERE 탭에서 다음과 같이 PK 값 기준으로 Update 로직이 수행되도록 조건을 설정 (**Input Field Type, Input Field 설정 주의**)

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new48.png)
          
 - Update Adapter Service 의 성공/실패 여부를 판단하는 Results Field 설정

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new51.png)

- IF0013.svc 폴더 아래 svc_IF0013_upsert 라는 새 Flowservice 를 생성 후 다음과 같이 구성합니다.

  - 위에서 생성한 Select Adpater Service 를 맨 위 스탭에 생성하고 TRY-CATCH Sequence 블록을 생성 (Success - Failure - Done)

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new32.png)
          
 - TRY 블록에서 LOOP 단계 추가, Select Output 의 Results DocumentList 를 Input Array 에 입력합니다.

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new49.png)
         
 - LOOP 문 안에 위에서 새로 생성한 IF0013_TGT_U_01 Adapter Service 단계를 추가하고 다음과 같이 매핑합니다. EAI_RESULTS 필드는 Set value 기능 또는 더블클릭하여 Success 를 입력합니다.

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new50.png)    
 
 - Update 아래 BRANCH 문을 추가 후 Switch 속성애 다음 필드를 입력합니다.

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new52.png)    
          
 - BRANCH 문 안에 생성한 Insert Adapter Service 단계를 추가 합니다. Label 엔 0 (Update 로직이 실패했을 때 Insert 로직 수행), 매핑은 다음과 같이 매핑합니다.

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new53.png)    

 - Batch Update Adapter Service 를 Loop 밖 아래 단계에 추가하고 다음과 같이 매핑 합니다. **들여쓰기 주의**

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new54.png)     
          
 - 서비스를 저장 후 실행시켜 결과를 확인해봅니다. (Select Adapter 를 생성하여 TGT_EMPLOYEES_TABLE 에 데이터가 저장 되었는지 확인하세요)

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new55.png)           


**추가 참고 Note. 트랜잭션 처리는 pub.art.transaction:startTransaction, pub.art.transaction:commitTransaction, pub.art.transaction:rollbackTransaction 세개의 서비스를 사용하여 트랜잭션을 묶어 구성합니다.** 

- 개발 예시

![Untitled](%5BWorkbook%2014%5D%20Create%20JDBC%20Adapter%20Services%20de5383e748184e9dbd34a7cff5d5864d/new56.png)


---

## Check Your Understanding

#### QUIZ 1. Adapter service 를 생성 하기 전에 IS 관리자 페이지에서 어떤 설정들이 선행되어야 합니까?
#### QUIZ 2. Select Adapter Service 의 Results Field 와 Insert Adapter Service 의 Results Field 의 차이점은 무엇입니까?
