# [Workbook 3] Building Flow Services - BRANCH

## Overview

이 연습에서는 **BRANCH 문**의 두 가지 다른 기능을 사용하여 Flow service 로직을 생성하는 방법을 설명합니다.

첫번째 예제는 **Switch 속성**의 변수 값을 사용한 분기 로직을 테스트하는 것이고, 

두번째는 **Evaluate labels** 속성을 사용해 **label** 의 정규표현식을 사용한 분기 처리 방식입니다. 


## Steps

#### STEP 1. 최상위 폴더 아래 IF0002 와 그 하위 폴더로 svc 를 생성합니다. svc 폴더 아래 svc_IF0002_branch1 이라는 새로운 Flow service를 새로 만듭니다.

#### STEP 2. svc_IF0002_branch1의 Input을 testValue라는 String을 정의하고 Output을 message라는 String 값으로 정의합니다.
    
![Untitled](%5BWorkbook%203%5D%20Building%20Flow%20Services%20-%20BRANCH%2016e22a6d373042f8b7c70b086784f6ca/Untitled.png)
    

#### STEP 3. testValue 변수 값에 따라 조건부 Server Log 메시지를 작성하는 BRANCH 문을 Flow service에 구성합니다. 예를 들어 testValue = true인 경우 IS Server 로그에 The value is TRUE 메시지를 작성합니다.
- service에 BRANCH문을 추가합니다. Switch 속성으로 /testValue를 지정합니다.    
        
![Untitled](%5BWorkbook%203%5D%20Building%20Flow%20Services%20-%20BRANCH%2016e22a6d373042f8b7c70b086784f6ca/Untitled%201.png)
        
- BRANCH 아래에 pub.flow:debugLog 문을 추가합니다 (BRANCH 논리의 일부가 되도록 BRANCH 아래에 들여쓰기). debugLog 속성에서 서비스의 Label을 true로 설정합니다(모두 소문자). 
        
![Untitled](%5BWorkbook%203%5D%20Building%20Flow%20Services%20-%20BRANCH%2016e22a6d373042f8b7c70b086784f6ca/Untitled%202.png)
        
- debugLog 문에 대한 Pipeline 탭에서 변수 메시지의 값을 “The value is TRUE”로 설정합니다. Server Log 에서 눈에 띄기 쉽게 Function 의 값은 ++++++로 설정합니다.
        
![Untitled](%5BWorkbook%203%5D%20Building%20Flow%20Services%20-%20BRANCH%2016e22a6d373042f8b7c70b086784f6ca/Untitled%203.png)
        
![Untitled](%5BWorkbook%203%5D%20Building%20Flow%20Services%20-%20BRANCH%2016e22a6d373042f8b7c70b086784f6ca/Untitled%204.png)
        

#### STEP 4. BRANCH 문 하위에 pub.flow:debugLog 문을 세 개 더 추가합니다 (모두 BRANCH 하위로 들여쓰기 하여 BRANCH 로직의 일부가 되도록 구성하십시오). 다음과 같이 각각의 Label 속성과 변수 메시지를 설정합니다.
- flow:debugLog (**Label = true**)
     - message = The value is TRUE
     - function = +++++

- flow:debugLog (**Label = false**)
     - message = The value is FALSE
     - function = +++++

- flow:debugLog (**Label = $default**)
     - message = The value is neither TRUE or FALSE
     - function = +++++
 
- flow:debugLog (**Label = $null**)
     - Message = The value was not provided
     - function = +++++
    
![Untitled](%5BWorkbook%203%5D%20Building%20Flow%20Services%20-%20BRANCH%2016e22a6d373042f8b7c70b086784f6ca/Untitled%205.png)
    

#### STEP 5. testValue 에 대해 매번 다른 값을 입력하며 Service를 여러 번 실행 테스트합니다. Output 이 IDE 하단의 Service Result(서비스 결과) 탭에 나타나야 하고 Integration Server 웹 관리 화면 > Server Log에서도 확인 가능해야 합니다.   
    
![Untitled](%5BWorkbook%203%5D%20Building%20Flow%20Services%20-%20BRANCH%2016e22a6d373042f8b7c70b086784f6ca/Untitled%206.png)
    
    
*참고: **service**가 작동하지 않거나 올바른 메시지가 출력되지 않으면 **debugger**을 사용해 **Service**를 실행하여 코드를 확인할 수 있습니다.*

---

#### STEP 6. IF0002.svc 폴더에 svc_IF0002_branch2 라는 다른 Flow Service를 만들어 String type의 Input값 2개 (account & cost) 와 String type의 Output값 (message)를 생성합니다.
    
![Untitled](%5BWorkbook%203%5D%20Building%20Flow%20Services%20-%20BRANCH%2016e22a6d373042f8b7c70b086784f6ca/Untitled%207.png)
    

#### STEP 7. 첫번 째 예제와 마찬가지로 **BRANCH**문과 **flow:debugLog** 를 사용하여 코드를 작성하며 **Server Log**에 남길 Message 값 을 입력하는 로직으로 구현합니다. 이 서비스에서는 **BRANCH 문 의 switch** 매개 변수를 비워두고 **Evaluate Labels** 을 **True**로 설정해야 합니다. 이 서비스 세부 로직은 다음과 같습니다.

![Untitled](%5BWorkbook%203%5D%20Building%20Flow%20Services%20-%20BRANCH%2016e22a6d373042f8b7c70b086784f6ca/Untitled%208.png)

- %cost% >= 100 : **cost** 변수의 값이 **>= 100**인 경우 **IS Server log**에 **Free Shipping** 로그를 남깁니다.
- %account% = /^PRE[0-9]/ : **Account** 의 값이 **PRE0 ~ PRE9**로 시작하는 경우 **IS Server log**에 **50% Shopping Discount**라고 로그를 남깁니다.
- $default : 위에 모두 해당되지 않을 경우 **IS Server log**에 **Full Shipping** 로그를 남깁니다.
        
![Untitled](%5BWorkbook%203%5D%20Building%20Flow%20Services%20-%20BRANCH%2016e22a6d373042f8b7c70b086784f6ca/Untitled%209.png)

정규 표현식은 다음 링크를 참고하세요. [**(참고)**](https://documentation.softwareag.com/webmethods/designer/sdf10-15/webhelp/sdf-webhelp/index.html#page/sdf-webhelp%2Fto-regular_expressions.html%23)

#### STEP 8. **Service**를 저장하고 테스트합니다. **IS Server log** 에서 결과를 확인합니다.     
    
![Untitled](%5BWorkbook%203%5D%20Building%20Flow%20Services%20-%20BRANCH%2016e22a6d373042f8b7c70b086784f6ca/Untitled%2010.png)
    
위 스크린샷은 다음과 같은 **input**값을 이용한 **service**를 실행하여 생성되었습니다.
    
![Untitled](%5BWorkbook%203%5D%20Building%20Flow%20Services%20-%20BRANCH%2016e22a6d373042f8b7c70b086784f6ca/Untitled%2011.png)

## Check Your Understanding
#### QUIZ 1. BRANCH에서 정규 표현식은 언제 유용합니까?
#### QUIZ 2. BRANCH 문의 속성인 switch 와 Evaluate labels=true 속성은 결합하여 사용할 수 있습니까?
