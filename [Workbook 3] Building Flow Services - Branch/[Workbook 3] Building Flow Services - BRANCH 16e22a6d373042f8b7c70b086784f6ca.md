# [Workbook 3] Building Flow Services - BRANCH

**※ Overview**

이 연습에서는 두 가지 다른 **Branch** 단계를 사용하여 비즈니스 로직을 생성합니다. 하나는 변수의 내용을 테스트하는 것이고 하나는 로직과 관련된 **label**을 평가하는 것입니다. 

---

**※ Steps**

1. **acme.PurchaseOrder.work** 하위 폴더에 **branch1**이라는 빈 **Flow service**를 새로 만듭니다.

1. **branch1**의 **input**을 **testValue**라는 단일 **String**으로 정의하고 **output**을 **testValue**라는 단일 **String** 메시지로 정의합니다.
    
    ![Untitled](%5BWorkbook%203%5D%20Building%20Flow%20Services%20-%20BRANCH%2016e22a6d373042f8b7c70b086784f6ca/Untitled.png)
    

1. 다음 단계에서 **testValue** 변수의 내용을 기반으로 조건부로 **Server Log**에 메시지를 작성하는 **BRANCH** 문을 **Flow** **service**에 추가합니다. 예를 들어 **testValue = true**인 경우 **IS Server** 로그에 **The value is TRUE** 메시지를 작성합니다.
    1. **service**에 **BRANCH**문을 추가합니다. **Switch** 속성으로 **/testValue**를 지정합니다.    
        
        ![Untitled](%5BWorkbook%203%5D%20Building%20Flow%20Services%20-%20BRANCH%2016e22a6d373042f8b7c70b086784f6ca/Untitled%201.png)
        
    2. **Branch** 아래에 **pub.flow:debugLog** 문을 추가합니다(**BANCH** 논리의 일부가 되도록 **BANCH** 아래에 들여쓰기). **debugLog** 속성에서 서비스의 **Label**을 **true**로 설정합니다(모두 소문자). 
        
        ![Untitled](%5BWorkbook%203%5D%20Building%20Flow%20Services%20-%20BRANCH%2016e22a6d373042f8b7c70b086784f6ca/Untitled%202.png)
        
    3. **debugLog** 문에 대한 **Pipeline** 탭에서 변수 메시지의 값을 “**The value is TRUE”**로 설정합니다. **eye-catcher**로서 함수의 값을 **+++ +++**로 설정합니다.
        
        ![Untitled](%5BWorkbook%203%5D%20Building%20Flow%20Services%20-%20BRANCH%2016e22a6d373042f8b7c70b086784f6ca/Untitled%203.png)
        
        ![Untitled](%5BWorkbook%203%5D%20Building%20Flow%20Services%20-%20BRANCH%2016e22a6d373042f8b7c70b086784f6ca/Untitled%204.png)
        

1. 다음 섹션에서 **branch**에 **pub.flow:debugLog** 문을 세 개 더 추가합니다(모두 **Branch** 아래로 들여쓰기하여 **Branch** 로직의 일부가 되도록 하십시오). 다음과 같이 각각의 **Label** 속성과 변수 메시지를 설정합니다.
    1. **flow:debugLog** (**step 3**에서 이미 완료되었으며, 예시로 나열하였습니다.)
        1. **Label = true**
        2. **message = The value is TRUE**
        3. **function = +++++**
    2. **flow:debugLog**
        1. **Label = false**
        2. **message = The value is FALSE**
        3. **function = +++++**
    3. **flow:debugLog**
        1. **Label = $default**
        2. **message = The value is neither TRUE or FALSE**
        3. **function = +++++**
    4. **flow:debugLog**
        1. **Label = $null**
        2. **Message = The value was not provided**
        3. **function = +++++**
    
    ![Untitled](%5BWorkbook%203%5D%20Building%20Flow%20Services%20-%20BRANCH%2016e22a6d373042f8b7c70b086784f6ca/Untitled%205.png)
    

1. 여러 번 실행하고 **testValue**에 대해 매번 다른 값을 제공하여 **service**를 테스트합니다. **output**가 **Service Result**(서비스 결과) 보기에 나타나야 하고 **Server Log**(서버 로그)에서 확인할 수 있습니다.   
    
    ![Untitled](%5BWorkbook%203%5D%20Building%20Flow%20Services%20-%20BRANCH%2016e22a6d373042f8b7c70b086784f6ca/Untitled%206.png)
    
    위 스크린샷은 **input** 값이 **true, false, maybe** 및 메시지 입력 값을 기입하지 않은 상태에서 **service**를 실행하여 생성되었습니다.
    
    *참고: **service**가 작동하지 않거나 올바른 메시지가 출력되지 않으면 **debugger**을 사용해 **service**를 실행하여 코드를 확인할 수 있습니다.*
    
2. **acme.PurchaseOrder.work** 폴더에서 **String type**의 **input**값**2**개 **(account & cost)** 및 **String type**의 **output**값 **(message)**가 있는 **branch2**라는 다른 **Flow Service**를 만듭니다.
    
    ![Untitled](%5BWorkbook%203%5D%20Building%20Flow%20Services%20-%20BRANCH%2016e22a6d373042f8b7c70b086784f6ca/Untitled%207.png)
    

1. 다음 섹션에서는 **BRANCH**와 **flow:debugLog** 코드를 작성하여 (**input field** 값을 기준으로) **Server Log**에 메시지를 작성합니다. 이 서비스에서는 **label**을 평가하려고 하므로 **BRANCH switch** 매개 변수를 비워두고 **Evaluate Labels**를 **True**로 설정해야 합니다. 이 서비스의 구조는 다음과 같습니다.
    1. ****cost** 변수의 **contents**가 **>= 100**인 경우 **IS Server log**에 **Free Shipping**이라고 적습니다. *참고* : **%cost% >= 100** 는 **run-time**에 **cost**의 **contents**를 평가합니다.
    2. **Account**가 **PRE0 ~ PRE9**로 시작하는 경우 **IS Server log**에 **50% Shopping Discount**라고 적습니다. *참고*: **%account% = /^PRE[0-9]/**와 같은 정규식을 사용하여 한 단계로 테스트할 수 있습니다.
    3. 그렇지 않으면 **IS Server log**에 **Full Shipping**을 기록합니다.
        
        ![Untitled](%5BWorkbook%203%5D%20Building%20Flow%20Services%20-%20BRANCH%2016e22a6d373042f8b7c70b086784f6ca/Untitled%208.png)
        
2. **service**를 저장하고 테스트합니다. **IS Server log**에서 결과를 확인합니다.     
    
    ![Untitled](%5BWorkbook%203%5D%20Building%20Flow%20Services%20-%20BRANCH%2016e22a6d373042f8b7c70b086784f6ca/Untitled%209.png)
    
    위 스크린샷은 다음과 같은 **input**값을 이용한 **service**를 실행하여 생성되었습니다.
    
    ![Untitled](%5BWorkbook%203%5D%20Building%20Flow%20Services%20-%20BRANCH%2016e22a6d373042f8b7c70b086784f6ca/Untitled%2010.png)
    

---