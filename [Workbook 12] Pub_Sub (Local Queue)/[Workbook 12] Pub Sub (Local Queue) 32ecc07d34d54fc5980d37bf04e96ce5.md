# [Workbook 12] Pub/Sub (Local Queue)

## Overview

이 연습에서는 Document type, 처리 서비스 (Flowservice) 및 Subscribing trigger 를 생성합니다. 그런 다음 문서를 Publish 하는 서비스를 만듭니다. 



## Steps

#### STEP 1. IF0011 폴더를 생성하고 하위 폴더를 다음과 같이 구성합니다. 

![Untitled](%5BWorkbook%2012%5D%20Pub%20Sub%20(Local%20Queue)%2032ecc07d34d54fc5980d37bf04e96ce5/new1.png)

#### STEP 2. docs_IF0011_Validation 이라는 Document type 을 생성 후 valid 라는 String 필드가 하나 포함된 유효성 확인 document type 을 생성합니다.

![Untitled](%5BWorkbook%2012%5D%20Pub%20Sub%20(Local%20Queue)%2032ecc07d34d54fc5980d37bf04e96ce5/new2.png)

#### STEP 3. document publishable 속성을 True로 설정 후 저장합니다. 저장 후 이 document를 Local Queue 에 Publish 할 수 있도록 만듭니다. Connection alias name 을 IS_LOCAL_CONNECTION 으로 설정 후 document type 을 저장하십시오.

![Untitled](%5BWorkbook%2012%5D%20Pub%20Sub%20(Local%20Queue)%2032ecc07d34d54fc5980d37bf04e96ce5/new3.png)

#### STEP 4. 새로운 Flowservice 로 svc_IF0010_handleValidation 을 svc 폴더 아래 생성합니다. 

- input 은 Document로 생성한 CUDO_SJH.IF0011.docs:docs_IF0011_Validation 를 참조하세요.
- Document type 명을 문서 document type의 명과 동일하게 (CUDO_SJH.IF0011.docs:docs_IF0011_Validation) 으로 설정하세요.
**Note.** Document Type 컴포넌트를 클릭 후 CTRL + C 하여 Full Path 경로를 복사할 수 있습니다.

![Untitled](%5BWorkbook%2012%5D%20Pub%20Sub%20(Local%20Queue)%2032ecc07d34d54fc5980d37bf04e96ce5/new4.png)

#### STEP 5. handleValidation 서비스 내 flow:debugLog 스탭을 추가하고 메시지를 매핑한 후 플로우 서비스를 저장합니다.

![Untitled](%5BWorkbook%2012%5D%20Pub%20Sub%20(Local%20Queue)%2032ecc07d34d54fc5980d37bf04e96ce5/new5.png)

#### STEP 6.  trig 폴더 아래, 새로운 webMethods Messeging Trigger 를 생성합니다. 이름은 trig_listenForValidation로 지정합니다. 생성 한 Trigger 세부 정보는 다음과 같이 구성합니다
    
   ![Untitled](%5BWorkbook%2012%5D%20Pub%20Sub%20(Local%20Queue)%2032ecc07d34d54fc5980d37bf04e96ce5/new6.png)
    
- **Name** = **Condition1**
- **Service** = **CUDO_SJH.IF0011.svc:svc_IF0010_handleValidation** 
- **Document type** = **CUDO_SJH.IF0011.docs:docs_IF0011_Validation**
- **Filter** = ***leave this empty***
        
  ![Untitled](%5BWorkbook%2012%5D%20Pub%20Sub%20(Local%20Queue)%2032ecc07d34d54fc5980d37bf04e96ce5/new7.png)
        

#### STEP 7. 지금까지 작업을 테스트하려면 **docs_IF0011_Validation 으로 생성한 Document Type 을** 마우스 오른쪽 버튼 클릭 후, Run as > Publishable Document 을 선택합니다. valid 필드에 일부 메시지를 입력하고 OK 를 눌러 실행합니다.

![Untitled](%5BWorkbook%2012%5D%20Pub%20Sub%20(Local%20Queue)%2032ecc07d34d54fc5980d37bf04e96ce5/new8.png)

#### STEP 8. IS 웹 관리 화면에서 메시지가 서버 로그에 나타나는지 확인 합니다.

![Untitled](%5BWorkbook%2012%5D%20Pub%20Sub%20(Local%20Queue)%2032ecc07d34d54fc5980d37bf04e96ce5/Untitled%207.png)

---

#### STEP 9. 다음 단계는 Flowservice 를 사용한 Publish 서비스 생성 방법입니다. 
- svc_IF0010_publishValidation 라는 이름의 Flowservice 를 svc 폴더 아래 생성, 서비스 내에서 pub.publish:publish 를 호출하는 단계를 추가 합니다.
        
  ![Untitled](%5BWorkbook%2012%5D%20Pub%20Sub%20(Local%20Queue)%2032ecc07d34d54fc5980d37bf04e96ce5/new9.png)
        
- Input 에 CUDO_SJH.IF0011.docs:docs_IF0011_Validation 을 참조 설정 후, 이름을 아래와 동일하게 설정합니다.
        
  ![Untitled](%5BWorkbook%2012%5D%20Pub%20Sub%20(Local%20Queue)%2032ecc07d34d54fc5980d37bf04e96ce5/new10.png)

- pub.publish:publish 에서 다음과 같이 매핑 합니다.
        
  ![Untitled](%5BWorkbook%2012%5D%20Pub%20Sub%20(Local%20Queue)%2032ecc07d34d54fc5980d37bf04e96ce5/new11.png)
        
  - **Validation** - **document** 매핑
  - **documentTypeName : **CUDO_SJH.IF0011.docs:docs_IF0011_Validation 으**로 설정합니다.**

#### STEP 10. svc_IF0010_publishValidation Flow 서비스를 저장하고 실행합니다. 이 서비스를 입력할 때 true 또는 false 값을 입력하십시오. 이 값은 서버 로그에 표시되어야 합니다.

![Untitled](%5BWorkbook%2012%5D%20Pub%20Sub%20(Local%20Queue)%2032ecc07d34d54fc5980d37bf04e96ce5/new12.png)

![Untitled](%5BWorkbook%2012%5D%20Pub%20Sub%20(Local%20Queue)%2032ecc07d34d54fc5980d37bf04e96ce5/Untitled%2012.png)



## Check Your Understanding

#### QUIZ 1. Document 를 Publish 할 수 있게 되면 어떻게 되는지?

#### QUIZ 2. 스토리지 유형 = 보장된 경우 게시 가능한 속성 폐기 및 존속 시간에 대한 적절한 운영 설정은 무엇인지?

#### QUIZ 3. Publishing 을 위해서는 어떤 오브젝트들이 필요한지? (2개)

#### QUIZ 4. Subscribing 을 위해서는 어떤 오브젝트들이 필요한지? (3개)

#### QUIZ 5. handleValdiation 서비스에서 전체 document type 이름을 인수 이름으로 사용해야 하는 이유는 무엇인지?
