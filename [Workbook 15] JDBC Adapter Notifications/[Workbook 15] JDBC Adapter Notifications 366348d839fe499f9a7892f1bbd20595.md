# [Workbook 15]  JDBC Adapter Notifications

## Overview

이번 연습에서는 JDBC Adapter Notification 을 생성합니다.

JDBC Adapter Notification 은 Database 의 특정 테이블을 모니터링 하며 Insert, Update 와 같이 특정 로직 (데이터 변경)등 로직이 수행 되었을 때

변경된 데이터가 EAI 서버로 자동으로 흘러 변경 된 데이터에 따른 적절한 후속 Flowserivce, 특정 로직을 수행 시키도록 자동화 할 수 있습니다.

이번 연습에서는 InsertNotification 을 생성하여 Database 테이블에 Insert 로직이 수행되는 것을 모니터링 & 변경 데이터를 이용한 후속 서비스가 수행 되는 것을 테스트 합니다.


## Steps

#### STEP 0. 상위 폴더 아래 IF0014 와 그 아래 adpt, noti, svc 폴더를 생성합니다.

![Untitled](%5BWorkbook%2015%5D%20JDBC%20Adapter%20Notifications%20366348d839fe499f9a7892f1bbd20595/new1.png)

- 미리 svc 폴더 아래 svc_IF0014_insertNoti 라는 새로운 Flowservice 를 생성해 둡니다.

![Untitled](%5BWorkbook%2015%5D%20JDBC%20Adapter%20Notifications%20366348d839fe499f9a7892f1bbd20595/new13.png)


#### STEP 1. IF0014.noti 폴더아래 IF0014_SRC_noti 라는 새 Adapter Notification 을 생성합니다. 

- noti 폴더에서 우클릭 > New > Adapter Notification 선택

![Untitled](%5BWorkbook%2015%5D%20JDBC%20Adapter%20Notifications%20366348d839fe499f9a7892f1bbd20595/new2.png)

- IF0014_SRC_noti 입력 후 Next 

![Untitled](%5BWorkbook%2015%5D%20JDBC%20Adapter%20Notifications%20366348d839fe499f9a7892f1bbd20595/new3.png)

- Adatper 타입은 JDBC 로 선택

![Untitled](%5BWorkbook%2015%5D%20JDBC%20Adapter%20Notifications%20366348d839fe499f9a7892f1bbd20595/new4.png)

- InsertNotification 을 선택 후 Next

![Untitled](%5BWorkbook%2015%5D%20JDBC%20Adapter%20Notifications%20366348d839fe499f9a7892f1bbd20595/new5.png)

- 다음 본인이 생성한 Connection Alias 명을 선택합니다.
  
![Untitled](%5BWorkbook%2015%5D%20JDBC%20Adapter%20Notifications%20366348d839fe499f9a7892f1bbd20595/new6.png)

- 생성 될 Publish Document Name 을 확인 후, Finish 를 눌러 Notification 생성 완료

![Untitled](%5BWorkbook%2015%5D%20JDBC%20Adapter%20Notifications%20366348d839fe499f9a7892f1bbd20595/new7.png)


- 생성 된 Insert Notification 에서 Notification Configure 탭을 확인합니다.
    - Insert, Update, Delete 등의 Notification 은 트리거, 버퍼 테이블의 조합을 사용하여 특정 테이블에서 발생하는 이벤트들을 모니터링 합니다.
    - Notification Configure 탭에서는 기존에 생성한 Connection Alias, Schema 내부에 해당 테이블을 생성합니다. (**연결 된 JDBC Connection 계정은 TABLE, TRIGGER 생성 권한 필요**)
    - Base Name 을 지정하여 관리 가능

![Untitled](%5BWorkbook%2015%5D%20JDBC%20Adapter%20Notifications%20366348d839fe499f9a7892f1bbd20595/new8.png)

- Tables 탭에서 모니터링 할 Database 내 테이블을 선택합니다. 기존에 생성해 두었던 SRC_EMPLOYEES_TABLE 을 선택 합니다.

![Untitled](%5BWorkbook%2015%5D%20JDBC%20Adapter%20Notifications%20366348d839fe499f9a7892f1bbd20595/new9.png)

- SELECT 탭에서 모니터링할 상세 컬럼들을 지정합니다. 모든 컬럼을 지정하고 ID 의 Output Field Type 을 java.lang.String 으로 지정합니다.

![Untitled](%5BWorkbook%2015%5D%20JDBC%20Adapter%20Notifications%20366348d839fe499f9a7892f1bbd20595/new10.png)

- 다음 Adapter Settings 탭으로 넘어가 Messaging Provider 를 IS_LOCAL_CONNECTION 으로 선택 후 저장합니다.
    - 변경 된 데이터는 IS_LOCAL_CONNECTION (local queue) 로 전송되어 적재됩니다.
  
![Untitled](%5BWorkbook%2015%5D%20JDBC%20Adapter%20Notifications%20366348d839fe499f9a7892f1bbd20595/new11.png)
 
 - Trigger 를 사용하여 Local Queue 에 적재 되어있는 데이터를 처리하는 후속 Flowserivce 를 연결합니다.
    - trig 폴더 아래 trig_IF0014_insertNoti 명칭의 새로운 webMethods Messaging Trigger 를 생성합니다.
      
![Untitled](%5BWorkbook%2015%5D%20JDBC%20Adapter%20Notifications%20366348d839fe499f9a7892f1bbd20595/new12.png)


- 생성 된 Trigger 는 다음과 같이 설정합니다.
    - Service : 미리 생성 한 svc_IF0014_insertNoti 연결
    - Properties > Enabled = True 로 변경 후 저장

![Untitled](%5BWorkbook%2015%5D%20JDBC%20Adapter%20Notifications%20366348d839fe499f9a7892f1bbd20595/new15.png)

    - Document 는 Notification 을 생성하면서 자동 생성 된 Publish Document 지정 후 저장

![Untitled](%5BWorkbook%2015%5D%20JDBC%20Adapter%20Notifications%20366348d839fe499f9a7892f1bbd20595/new14.png)


- 이제 svc 폴더 아래 svc_IF0014_insertNoti 서비스를 개발합니다.
    - Input/Output 탭으로 이동하여 Input 필드를 다음과 같이 구성합니다.
  
![Untitled](%5BWorkbook%2015%5D%20JDBC%20Adapter%20Notifications%20366348d839fe499f9a7892f1bbd20595/new16.png)

    - pub.json:documentToJSONString 서비스 스탭을 추가하고 다음과 같이 매핑합니다.

![Untitled](%5BWorkbook%2015%5D%20JDBC%20Adapter%20Notifications%20366348d839fe499f9a7892f1bbd20595/new17.png)

    - 그 아래 pub.flow:debugLog 서비스를 추가 jsonString 을 message 에 매핑 후 서비스를 저장합니다.

![Untitled](%5BWorkbook%2015%5D%20JDBC%20Adapter%20Notifications%20366348d839fe499f9a7892f1bbd20595/new18.png)


- 서비스 저장 후 IF0013 에서 테스트 했던 IF0013.adpt:IF0013_SRC_I_01 서비스를 실행시켜 결과를 확인합니다.

![Untitled](%5BWorkbook%2015%5D%20JDBC%20Adapter%20Notifications%20366348d839fe499f9a7892f1bbd20595/new19.png)





- Notification 의 여러 Type 에 대한 자세한 정보는 이곳을 참고 부탁드립니다.
https://documentation.softwareag.com/webmethods/adapters_estandards/Adapters/JDBC/JDBC_10-3/10-3_Adapter_for_JDBC_webhelp/index.html#page/jdbc-webhelp%2Fco-notif_types.html%23


## Check Your Understanding

#### QUIZ 1. JDBC Adapter Notification 로 작업할 때 자동으로 생성되고 업데이트 되는 항목은 무엇입니까?
#### QUIZ 2. JDBC Adapter Notification Schedule 이 enabled 되면 어떻게 됩니까?
#### QUIZ 3. JDBC Adapter Notification Schedule 이 administrative task 인 이유는 무엇입니까?
