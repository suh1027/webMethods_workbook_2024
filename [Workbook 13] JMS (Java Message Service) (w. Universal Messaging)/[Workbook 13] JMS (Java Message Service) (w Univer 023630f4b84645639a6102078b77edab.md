# [Workbook 13] JMS (Java Message Service) (w. Universal Messaging)

**※ Overview**

 

이 연습에서는 JMS 을 사용, Universal Messaging 서버의 Queue 또는 Topic 으로 기존 문서를 게시하는 서비스를 만들고, 문서를 수신하기 위해 후속 핸들링 서비스와 JMS Trigger를 만듭니다.
기존 acme.PurchaseOrder.docs:Validation 문서 유형을 사용하고 JMS Publish 서비스를 이용하여 문서를 게시합니다. 

이 연습을 수행하기 위해서는 별도의 Universal Messaging 서버가 필요합니다.

Universal Messaging 은 공용, 개인 및 무선 인프라 전반에 걸쳐 메시지 전달을 보장하는 메시지 지향 미들웨어 제품으로 다음과 같은 별도의 설치 구성이 필요합니다. [**(참고)**](https://documentation.softwareag.com/universal_messaging/num10-15/webhelp/num-webhelp/)

![Universal Messaging 서버 구성 참고 - Universal Messaging Enterprise Manager 캡쳐 자료](%5BWorkbook%2013%5D%20JMS%20(Java%20Message%20Service)/Untitled.png)

Universal Messaging 서버 구성 참고 - Universal Messaging Enterprise Manager 캡쳐 자료

---

**※ Steps**

1. 다음 연습에 앞서 웹 관리 화면에서 다음과 같은 JNDI, JMS 설정이 필요합니다.
    1. JNDI provider alias 설정 (기존 DEFAULT_IS_JNDI_PROVIDER 수정 또는 신규 생성 사용)
        
        ![Untitled](%5BWorkbook%2013%5D%20JMS%20(Java%20Message%20Service)/Untitled%201.png)
        
        → Provider URL 을 UM 이 구성 된 Host : Port 로 설정 (ex. nsp://192.168.1.218:9000)
        
        ![Untitled](%5BWorkbook%2013%5D%20JMS%20(Java%20Message%20Service)/Untitled%202.png)
        
        → Test Lookup 결과 예시
        
    2. JMS Connection 설정 (기존 DEFAULT_IS_JMS_CONNECTION 수정 또는 신규 생성 사용)
        
        ![Untitled](%5BWorkbook%2013%5D%20JMS%20(Java%20Message%20Service)/Untitled%203.png)
        
        → 위에서 생성한 JNDI PROVIDER 내 Connection Factory Lookup Name 을 입력한다
        
        ![Untitled](%5BWorkbook%2013%5D%20JMS%20(Java%20Message%20Service)/Untitled%204.png)
        
        → Enable 하여 JMS Connection 활성화
        

1. acme.PurchaseOrder.work:publishValidationJMS 라는 플로우 서비스를 만듭니다. 이 서비스의 Input 에서 acme.PurchaseOrder.docs:Validation 문서 참조를 추가합니다.

![Untitled](%5BWorkbook%2013%5D%20JMS%20(Java%20Message%20Service)/Untitled%205.png)

1. Flowservice 서비스 내 jms:send 호출 단계를 추가합니다. 다음과 같이 매핑/설정을 수행 후 서비스를 저장합니다.
    
    ![Untitled](%5BWorkbook%2013%5D%20JMS%20(Java%20Message%20Service)/Untitled%206.png)
    
    1. **connectionAliasName** = **DEFAULT_IS_JMS_CONNECTION**
    2. **destinationName** = **TESTTOPIC**
    3. **destinationType** = **TOPIC**

1. 후속 핸들링 Flowservice 로 PurchaseOrder.work:handleValidationJMS 를 만듭니다. 이 서비스는 서비스를 처리하고 가입을 위해 트리거를 사용합니다. Input/Output 탭에서 Specification Reference 필드 오른쪽에 있는 버튼을 클릭합니다. WmPublic 패키지에서 pub.jms:triggerSpec을 찾아 선택합니다.

![Untitled](%5BWorkbook%2013%5D%20JMS%20(Java%20Message%20Service)/Untitled%207.png)

1. 서비스 편집기의 트리 탭에서 pub.xml:documentToXMLstring 단계를 추가하고 Service in 의 document 와 JMSMessage/body/data를 매핑합니다

![Untitled](%5BWorkbook%2013%5D%20JMS%20(Java%20Message%20Service)/Untitled%208.png)

1. 다음으로 flow:debugLog 호출을 서비스에 추가하고 xmldata 와 message 를 매핑합니다. 완료된 서비스는 다음과 같습니다.

![Untitled](%5BWorkbook%2013%5D%20JMS%20(Java%20Message%20Service)/Untitled%209.png)

1. acme.PurchaseOrder.work.trig 폴더에서 listenForValidationJMS 라는 새 JMS trigger를 만듭니다
    
    ![Untitled](%5BWorkbook%2013%5D%20JMS%20(Java%20Message%20Service)/Untitled%2010.png)
    
    1. 사전 단계에서 설정한 DEFAULT_IS_JMSCONNECTION 으로 JMS connection alias name 설정
        
        ![Untitled](%5BWorkbook%2013%5D%20JMS%20(Java%20Message%20Service)/Untitled%2011.png)
        
    2. Destination Name(대상 이름) 위 버튼 Insert Destinations 를 클릭하고 다음을 입력합니다
        
        ![Untitled](%5BWorkbook%2013%5D%20JMS%20(Java%20Message%20Service)/Untitled%2012.png)
        
        - **Destination name** = **TESTTOPIC**
        - **Destination Type** = **Topic**
        
    3. 아래 Messege routing 탭의 Insert routings 버튼을 클릭하여 메시지 라우팅을 구성합니다. 구성 된 Rule은 다음과 같이 설정하여 저장합니다.
        
        ![Untitled](%5BWorkbook%2013%5D%20JMS%20(Java%20Message%20Service)/Untitled%2013.png)
        
        - **Name** = **Rule1**
        - **Service** = **PurchaseOrder.work:handleValidationJMS**
        
2. publishValidationJMS 서비스를 실행합니다. 이 서비스의 입력에 대해 true 또는 false 값을 입력합니다. IS 관리 웹 페이지에서 해당 값이 서버 로그에 표시되는지 확인 합니다.

![Untitled](%5BWorkbook%2013%5D%20JMS%20(Java%20Message%20Service)/Untitled%2014.png)

![Untitled](%5BWorkbook%2013%5D%20JMS%20(Java%20Message%20Service)/Untitled%2015.png)

---

※ **Check Your Understanding**

1. Topic 과 Queue 의 차이는 무엇인가?

1. JMS 메시지 유형에는 어떤 것들이 있는지? (5가지)