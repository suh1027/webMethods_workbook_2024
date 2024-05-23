# [Workbook 10] Web Service Descriptors and Custom Faults

## Overview

이 연습에서는 미리 생성한 sequenceTryCatch 라는 Flow 서비스를 웹 서비스 설명자(WSD)를 생성, 웹 서비스를 통해 호출 가능하게 만듭니다. 

누구든지 웹 서비스로 sequenceTryCatch를 호출할 수 있음을 증명하기 위해 공급자 WSD에서 생성 된 WSDL을 기반으로 소비자 WSD를 생성하고 자동 생성된 웹 서비스 커넥터를 사용하여 sequenceTryCatch를 호출합니다. 

마지막으로 일반 오류 문서를 만들어 사용자 정의 SOAP 오류가 반환될 수 있도록 지정하여 사용자 지정 오류가 예상대로 반환 되는지 테스트합니다.


## Steps

#### STEP 1. 최상위 폴더 아래 IF0009 폴더를 생성하고 다음과 같은 하위 폴더들을 생성합니다. 

![Untitled](%5BWorkbook%2010%5D%20Web%20Service%20Descriptors%20and%20Custom%20F%20b7ce5de1fb3a4023af5f789ba04b2676/Untitled%2011.png)

#### STEP 2. svc_IF0004_sequenceTryCatch Flowservice 내용을 복사하여 svc 아래 새로운 svc_IF0009_sequenceTryCatch 서비스 내 붙여넣습니다.

![Untitled](%5BWorkbook%2010%5D%20Web%20Service%20Descriptors%20and%20Custom%20F%20b7ce5de1fb3a4023af5f789ba04b2676/Untitled%2013.png)
![Untitled](%5BWorkbook%2010%5D%20Web%20Service%20Descriptors%20and%20Custom%20F%20b7ce5de1fb3a4023af5f789ba04b2676/Untitled%2012.png)

#### STEP 3. IF0009.ws.새 web service descriptor를 만듭니다. sequenceTryCatch를 Element name 으로 사용합니다. **Next>** 버튼을 클릭하세요. 

![Untitled](%5BWorkbook%2010%5D%20Web%20Service%20Descriptors%20and%20Custom%20F%20b7ce5de1fb3a4023af5f789ba04b2676/Untitled.png)

#### STEP 4. 모든 기본값(공급자, 기존 IS 서비스)을 선택하고 **Next>** 버튼을 클릭합니다.

![Untitled](%5BWorkbook%2010%5D%20Web%20Service%20Descriptors%20and%20Custom%20F%20b7ce5de1fb3a4023af5f789ba04b2676/Untitled%201.png)

#### STEP 5. 작업으로 사용할 서비스로 acme.PurchaseOrder.work:sequenceTryCatch 서비스를 선택하고 **Finish** 버튼을 클릭합니다. 

![Untitled](%5BWorkbook%2010%5D%20Web%20Service%20Descriptors%20and%20Custom%20F%20b7ce5de1fb3a4023af5f789ba04b2676/Untitled%202.png)

#### STEP 6. 새로운 Webservice Descriptor Provider 가 편집기에 나타나면 해당 속성 패널을 열고 WSDL URL 속성 값을 클릭한 후 클립보드에 복사합니다. 다음 단계에 해당 값이 필요합니다.

![Untitled](%5BWorkbook%2010%5D%20Web%20Service%20Descriptors%20and%20Custom%20F%20b7ce5de1fb3a4023af5f789ba04b2676/Untitled%203.png)

#### STEP 7. 브라우저 탭을 열고 주소 필드에 WSDL URL을 붙여넣은 후 Return 키를 누르세요. SequenceTryCatch 웹 서비스에 대한 WSDL이 표시되어야 합니다. 이는 웹서비스를 호출 하기 위해 Consumer (Client) 가 WSDL에 액세스하는 데 사용 하는 URL입니다.

![Untitled](%5BWorkbook%2010%5D%20Web%20Service%20Descriptors%20and%20Custom%20F%20b7ce5de1fb3a4023af5f789ba04b2676/Untitled%204.png)

#### STEP 8. 이제 PurchaseOrder.ws.consumer 폴더에 sequenceTryCatch 라는 다른 웹 서비스 설명자를 만듭니다.

![Untitled](%5BWorkbook%2010%5D%20Web%20Service%20Descriptors%20and%20Custom%20F%20b7ce5de1fb3a4023af5f789ba04b2676/Untitled%205.png)

#### STEP 9. Consumer 라디오 버튼을 선택하고 다른 모든 필드에 대해 기본 값을 적용합니다.

![Untitled](%5BWorkbook%2010%5D%20Web%20Service%20Descriptors%20and%20Custom%20F%20b7ce5de1fb3a4023af5f789ba04b2676/Untitled%206.png)

#### STEP 10. Select the WSDL Location 대화상자에서 File/URL을 선택하고 방금 복사한 WSDL URL을 텍스트 필드에 붙여 넣은 후 **Next >** 버튼을 클릭합니다.   

![Untitled](%5BWorkbook%2010%5D%20Web%20Service%20Descriptors%20and%20Custom%20F%20b7ce5de1fb3a4023af5f789ba04b2676/Untitled%207.png)

#### STEP 11. 기본 값을 모두 적용하고 **Finish** 버튼을 클릭합니다. 새로 생성된 모든 개체에 주목합니다.   

![Untitled](%5BWorkbook%2010%5D%20Web%20Service%20Descriptors%20and%20Custom%20F%20b7ce5de1fb3a4023af5f789ba04b2676/Untitled%208.png)

#### STEP 12. 웹 서비스 커넥터PurchaseOrder.ws.consumer.sequenceTryCatch_.connectors:sequenceTryCatch_PortType_sequenceTryCatch로 이동하여 엽니다.

![Untitled](%5BWorkbook%2010%5D%20Web%20Service%20Descriptors%20and%20Custom%20F%20b7ce5de1fb3a4023af5f789ba04b2676/Untitled%209.png)

#### STEP 13. 마우스 오른쪽 버튼을 클릭하여 시퀀스 TryCatch_PortType_SequenceTryCatch를 실행하고 Run As Flow Service를 선택합니다. 다음 값을 입력으로 제공합니다.
   1. **tns:sequenceTryCatch/fileName** = /webM/IS01/test.txt
   2. **auth/transport/type** = **BASIC**
   3. **auth/transport/user** = **Administrator**
   4. **auth/transport/pass = manage**

![Untitled](%5BWorkbook%2010%5D%20Web%20Service%20Descriptors%20and%20Custom%20F%20b7ce5de1fb3a4023af5f789ba04b2676/Untitled%2010.png)

#### STEP 14. 서비스 결과 보기에서 결과를 검토합니다.

![Untitled](%5BWorkbook%2010%5D%20Web%20Service%20Descriptors%20and%20Custom%20F%20b7ce5de1fb3a4023af5f789ba04b2676/Untitled%2011.png)

#### STEP 15. 이제PurchaseOrder.docs:Error 문서 유형에 문자열 필드 하나를 추가하고 이름을 Reason 으로 지정하고 저장합니다.

![Untitled](%5BWorkbook%2010%5D%20Web%20Service%20Descriptors%20and%20Custom%20F%20b7ce5de1fb3a4023af5f789ba04b2676/Untitled%2012.png)

#### STEP 16. 메인 Flow service 인 acme.PurchaseOrder.work.sequenceTryCatch를 열고 새 Error 문서를 사용하도록 수정합니다.
    
![Untitled](%5BWorkbook%2010%5D%20Web%20Service%20Descriptors%20and%20Custom%20F%20b7ce5de1fb3a4023af5f789ba04b2676/Untitled%2013.png)
    
1. 서비스에서 Tree 탭을 엽니다. 서비스를 확장하고 pub.flow:getLastError 를 선택합니다.
2. Pipeline 탭을 클릭하고 Pipeline Out 섹션을 선택한 다음 해당 섹션을 마우스 오른쪽 단추로 클릭하고 문서 참조 삽입을 선택한 다음 acme.PurchaseOrder.docs:Error 를 선택하여 생성 후 이름을 Error로 지정합니다. 
3. Service Out의 마지막 Error/Error 변수를 Error 문서 참조의 Reason 변수에 매핑 합니다. 수정 내용을 저장합니다.

#### STEP 17. Webservice Descriptor 인 acme.PurchaseOrder.ws.provider.sequenceTryCatch 를 클릭하여 sequenceTryCatch 작업을 확장한 후 응답 문서를 확장합니다. 
    
![Untitled](%5BWorkbook%2010%5D%20Web%20Service%20Descriptors%20and%20Custom%20F%20b7ce5de1fb3a4023af5f789ba04b2676/Untitled%2014.png)
    
1. 상단의 Add Header or Faullt 를 클릭합니다.
        
![Untitled](%5BWorkbook%2010%5D%20Web%20Service%20Descriptors%20and%20Custom%20F%20b7ce5de1fb3a4023af5f789ba04b2676/Untitled%2015.png)
        
2. 팝업 대화 상자에서 acme.PurchaseOrder.docs:Error Document Type 을 선택한 후 확인 단추를 클릭합니다. sequenceTryCatchProvider는 다음과 같이 나타납니다.
        
![Untitled](%5BWorkbook%2010%5D%20Web%20Service%20Descriptors%20and%20Custom%20F%20b7ce5de1fb3a4023af5f789ba04b2676/Untitled%2016.png)
        
3. 변경 내용을 저장합니다.
        
![Untitled](%5BWorkbook%2010%5D%20Web%20Service%20Descriptors%20and%20Custom%20F%20b7ce5de1fb3a4023af5f789ba04b2676/Untitled%2017.png)
        

#### STEP 18. 이제 Consumer WSD 를 재 생성하여 Provider WSD에 대한 변경 사항을 반영해야 합니다. Package Navigator 보기에서 consumer WSD를 마우스 오른쪽 버튼으로 클릭하고 웹 서비스 커넥터 새로 고침을 선택합니다

![Untitled](%5BWorkbook%2010%5D%20Web%20Service%20Descriptors%20and%20Custom%20F%20b7ce5de1fb3a4023af5f789ba04b2676/Untitled%2018.png)

![Untitled](%5BWorkbook%2010%5D%20Web%20Service%20Descriptors%20and%20Custom%20F%20b7ce5de1fb3a4023af5f789ba04b2676/Untitled%2019.png)

#### STEP 19. 위의 단계에 따라 재 생성된 consumer Connector Service 를 실행하되 fileName에는 /nofiles.txt를 입력합니다. 
    
![Untitled](%5BWorkbook%2010%5D%20Web%20Service%20Descriptors%20and%20Custom%20F%20b7ce5de1fb3a4023af5f789ba04b2676/Untitled%2020.png)
    


## Check Your Understanding

#### QUIZ 1. provider WSD는 언제, consumer WSD는 언제 만들어지는지?

#### QUIZ 2. 웹 서비스 커넥터(WSC)는 언제 어떻게 만들어지는지?

#### QUIZ 3. 둘 이상의 사용자 지정 SOAP 오류 문서를 가질 수 있는지?
