# [Workbook 7] Create a Java Service

## Overview

이 장에서는 **Designer**를 사용하여 **Java** 서비스를 생성, 컴파일하고 실행합니다.

특정 문자열이 두 번째 문자열로 끝나는지 테스트하는 특별한 서비스가 필요하다고 상상해보세요. 

webMethods 내 Built-in 된 **pub.string** 폴더 아래는 이와 같은 서비스가 없지만 **Java** 런타임 환경의 **String.endsWith()** 메서드를 사용하려고 합니다. 


## Steps

#### STEP 1. 최상위 폴더 아래 IF0006 와 svc 폴더를 생성한 후 폴더에 svc_IF0006_endsWith라는 새 Java Service를 생성하세요. 이 서비스에는 string 및 suffix 두 개의 문자열 입력 및 value 라는 문자열 출력이 있어야 합니다.       
   ![Untitled](%5BWorkbook%207%5D%20Create%20a%20Java%20Service%20dbc34d756ea943a2a8c1a6aaf20da91c/Untitled.png)
    

#### STEP 2. 서비스를 저장한 다음 패키지 네비게이터 뷰에서 해당 서비스를 마우스 오른쪽 버튼으로 클릭하고 **Generate Code…** -> **For implementing this service**를 선택한 다음 **Finish** 버튼을 클릭하세요. 이렇게 하면 템플릿 코드가 클립보드에 복사됩니다. **Java** 서비스의 소스 탭을 열고 생성된 코드를 빈 메서드 본문에 붙여 넣으세요. 그리고 다음과 같이 코드를 편집하세요.
   ![Untitled](%5BWorkbook%207%5D%20Create%20a%20Java%20Service%20dbc34d756ea943a2a8c1a6aaf20da91c/Untitled%201.png) 
   ![Untitled](%5BWorkbook%207%5D%20Create%20a%20Java%20Service%20dbc34d756ea943a2a8c1a6aaf20da91c/Untitled%202.png)
    
   *참고*: **Eclipse IDE**에서 익숙한 코드 완성과 같은 모든 **Java** 개발 기능을 사용할 수 있습니다.   
    

#### STEP 3. 샘플 입력값으로 서비스를 저장하고 실행하세요. 반환된 값이 올바른지 확인하세요. 
![Untitled](%5BWorkbook%207%5D%20Create%20a%20Java%20Service%20dbc34d756ea943a2a8c1a6aaf20da91c/Untitled%203.png)

## Check Your Understanding

#### QUIZ 1. endsWith 서비스의 Java 코드 각 라인이 정확히 어떤 역할을 하나요?
#### QUIZ 2. 이 서비스는 스레드가 안전한가요? 그렇지 않다면 어떻게 해야 하나요?
#### QUIZ 3. 커서 처리를 어떻게 개선할 수 있을까요?
