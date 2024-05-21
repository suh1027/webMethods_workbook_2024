# [Workbook 12] Pub/Sub (Local Queue)

**※ Overview**

 

이 연습에서는 Document type, 처리 서비스 (Flowservice) 및 Subscribing trigger 를 생성합니다. 그런 다음 문서를 Publish 하는 서비스를 만듭니다. 

---

**※ Steps**

1. Acme 패키지에서 Acme.PurchaseOrder.docs:Validation 이라는 Document type 을 생성 후 valid 라는 문자열 필드가 하나 포함된 유효성 확인 document type 을 생성합니다.

![Untitled](%5BWorkbook%2012%5D%20Pub%20Sub%20(Local%20Queue)%2032ecc07d34d54fc5980d37bf04e96ce5/Untitled.png)

1. document publishable 속성을 True로 설정하여 이 document를 Local Queue 에 Publish 할 수 있도록 만듭니다. Connection alias name 을 IS_LOCAL_CONNECTION 으로 설정 후 document type 을 저장하십시오.

![Untitled](%5BWorkbook%2012%5D%20Pub%20Sub%20(Local%20Queue)%2032ecc07d34d54fc5980d37bf04e96ce5/Untitled%201.png)

1. 새로운 Flowservice 로 acme.PurchaseOrder.work:handleValidation 을 생성합니다. 이 서비스의 input 을 Document로 생성한 acme.PurchaseOrder.docs:Validation 로 설정하세요. Document type 명을 문서 document type의 명과 동일하게 (acme.PurchaseOrder.docs:Validation) 으로 설정하세요.

![Untitled](%5BWorkbook%2012%5D%20Pub%20Sub%20(Local%20Queue)%2032ecc07d34d54fc5980d37bf04e96ce5/Untitled%202.png)

1. handleValidation 서비스 내 flow:debugLog 스탭을 추가하고 메시지를 매핑한 후 플로우 서비스를 저장합니다.

![Untitled](%5BWorkbook%2012%5D%20Pub%20Sub%20(Local%20Queue)%2032ecc07d34d54fc5980d37bf04e96ce5/Untitled%203.png)

1. PurchaseOrder.work 폴더 아래 trig 폴더를 생성하고, 새로운 webMethods Messeging Trigger 를 생성합니다. 이름은 listenForValidation로 지정합니다. 생성 한 Trigger 세부 정보는 다음과 같이 구성합니다
    
    ![Untitled](%5BWorkbook%2012%5D%20Pub%20Sub%20(Local%20Queue)%2032ecc07d34d54fc5980d37bf04e96ce5/Untitled%204.png)
    
    1. **Name** = **Condition1** (don’t change)
    2. **Service** = **PurchaseOrder.work:handleValidation**  (you may use copy and paste here as well)
    3. **Document type** = **PurchaseOrder.docs:Validation**
    4. **Filter** = ***leave this empty***
        
        ![Untitled](%5BWorkbook%2012%5D%20Pub%20Sub%20(Local%20Queue)%2032ecc07d34d54fc5980d37bf04e96ce5/Untitled%205.png)
        

1. 지금까지 작업을 테스트하려면 **PurchaseOrder.docs:Validation 으로 생성한 Document Type 을** 마우스 오른쪽 버튼 클릭 후, Run as > Publishable Document 을 선택합니다. Valid 필드에 일부 메시지를 입력하고 OK 를 눌러 실행합니다.

![Untitled](%5BWorkbook%2012%5D%20Pub%20Sub%20(Local%20Queue)%2032ecc07d34d54fc5980d37bf04e96ce5/Untitled%206.png)

1. IS 웹 관리 화면에서 메시지가 서버 로그에 나타나는지 확인 합니다.

![Untitled](%5BWorkbook%2012%5D%20Pub%20Sub%20(Local%20Queue)%2032ecc07d34d54fc5980d37bf04e96ce5/Untitled%207.png)

1. 다음 단계로 Flowservice 를 사용하여 Publish 서비스를 만듭니다. 
    1. acme.PurchaseOrder.work:publishValidation라는 이름의 Flowservice 를 생성, 서비스 내에서 pub.publish:publish 를 호출하는 단계를 추가 후 다음과 같이 매핑을 수행합니다
        
        ![Untitled](%5BWorkbook%2012%5D%20Pub%20Sub%20(Local%20Queue)%2032ecc07d34d54fc5980d37bf04e96ce5/Untitled%208.png)
        
    2. Input 에 acme.PurchaseOrder.docs:Validation 을 참조 설정 후, 이름을 동일하게 설정합니다.
        
        ![Untitled](%5BWorkbook%2012%5D%20Pub%20Sub%20(Local%20Queue)%2032ecc07d34d54fc5980d37bf04e96ce5/Untitled%209.png)
        
        ![Untitled](%5BWorkbook%2012%5D%20Pub%20Sub%20(Local%20Queue)%2032ecc07d34d54fc5980d37bf04e96ce5/Untitled%2010.png)
        
        - **Validation** - **document** 매핑
        - **documentTypeName :** acme.PurchaseOrder.docs:Validation 으**로 설정합니다.**

1. publishValidation Flow 서비스를 저장하고 실행합니다. 이 서비스를 입력할 때 true 또는 false 값을 입력하십시오. 이 값은 서버 로그에 표시되어야 합니다.

![Untitled](%5BWorkbook%2012%5D%20Pub%20Sub%20(Local%20Queue)%2032ecc07d34d54fc5980d37bf04e96ce5/Untitled%2011.png)

![Untitled](%5BWorkbook%2012%5D%20Pub%20Sub%20(Local%20Queue)%2032ecc07d34d54fc5980d37bf04e96ce5/Untitled%2012.png)

---

※ **Check Your Understanding**

1. Document 를 Publish 할 수 있게 되면 어떻게 되는지?

1. 스토리지 유형 = 보장된 경우 게시 가능한 속성 폐기 및 존속 시간에 대한 적절한 운영 설정은 무엇인지?

1. Publishing 을 위해서는 어떤 오브젝트들이 필요한지? (2개)

1. Subscribing 을 위해서는 어떤 오브젝트들이 필요한지? (3개)

1. handleValdiation 서비스에서 전체 document type 이름을 인수 이름으로 사용해야 하는 이유는 무엇인지?