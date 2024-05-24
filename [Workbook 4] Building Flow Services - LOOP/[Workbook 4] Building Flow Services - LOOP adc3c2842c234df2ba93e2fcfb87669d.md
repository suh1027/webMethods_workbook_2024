# [Workbook 4] Building Flow Services - LOOP

## Overview

이 연습에서는 Flow service의 Loop 문을 사용하여 직원 목록을 처리하는 비즈니스 로직을 생성합니다.


## Steps

#### STEP 0. 최상위 폴더 아래 IF0003 와 svc 와 docs 폴더를 생성합니다. docs 폴더 아래 Depart 라는 명칭으로 다음과 같은 새로운 Document Type 을 생성합니다.

![Untitled](%5BWorkbook%204%5D%20Building%20Flow%20Services%20-%20LOOP%20adc3c2842c234df2ba93e2fcfb87669d/new1.png)   

**Note.** Document List Type은 다건의 Document 를 처리하는데 사용하는 타입 입니다.


#### STEP 1. 생성 한 svc 폴더 아래 svc_IF0003_loopTest 라는 새 빈 Flow service 을 만듭니다. 
![Untitled](%5BWorkbook%204%5D%20Building%20Flow%20Services%20-%20LOOP%20adc3c2842c234df2ba93e2fcfb87669d/new2.png)   

- 서비스의 input 은 Document Reference(문서 참조)로 설정하며, 명칭도 그대로 사용합니다.
    - docs 폴더 아래 생성 한 **docs_IF0003_Depart** Document Type 을 그대로 복사하여 Input 에 붙여넣습니다.
    - 생성 된 Document Type 을 CTRL + C & V 하여 편리하게 붙여 넣을 수 있습니다.
- output 은 **count** 라는 단일 String field 로 설정합니다.

![Untitled](%5BWorkbook%204%5D%20Building%20Flow%20Services%20-%20LOOP%20adc3c2842c234df2ba93e2fcfb87669d/new3.png)
    

#### STEP 2. 생성 한 Input/Output 탭에서 Input Document Type 을 확장하여 ... .docs_IF0003_Depart/department/employee 를 찾고 클릭 후 CTRL + C 하여 Copy 합니다.
![Untitled](%5BWorkbook%204%5D%20Building%20Flow%20Services%20-%20LOOP%20adc3c2842c234df2ba93e2fcfb87669d/new4.png)


#### STEP 3. 이제 tree 탭으로 돌아가 서비스 내 LOOP 문을 추가하고 Input array 속성에 ... .docs:docs_IF0003_Depart/department/employee 을 붙여 넣고 Enter 를 눌러 입력합니다.
    
![Untitled](%5BWorkbook%204%5D%20Building%20Flow%20Services%20-%20LOOP%20adc3c2842c234df2ba93e2fcfb87669d/new5.png)
        

#### STEP 4. LOOP 단계 아래에 MAP 문을 추가합니다 (LOOP 아래에 들여쓰기로 MAP 이 들어가 있는지 확인하십시오).
- MAP 단계에서 pipeline in 의 employee 가 DocumentList 타입에서 Document 로 변경 되어 있는지 확인하세요.
- MAP 단계에서 새로 생겨난 $iteration 필드는 LOOP 문의 반복 횟수를 나타냅니다.
  
**참고: LOOP 문을 추가하면 $iteration 이라는 새로운 변수가 Pipeline 에 생성됩니다. 이 변수는 LOOP 의 반복 횟수를 나타냅니다.**
    
![Untitled](%5BWorkbook%204%5D%20Building%20Flow%20Services%20-%20LOOP%20adc3c2842c234df2ba93e2fcfb87669d/new6.png)

- $iteration 필드와 count 값을 매핑하여 LOOP 문이 반복된 횟수를 count 변수에 매핑합니다.
![Untitled](%5BWorkbook%204%5D%20Building%20Flow%20Services%20-%20LOOP%20adc3c2842c234df2ba93e2fcfb87669d/new7.png)
    

#### STEP 5. pub.flow:debugLog 를 MAP 단계 아래에 추가합니다 (LOOP 아래에 들여쓰기 되지 않았는지 확인하십시오). 

- pub.flow:debugLog 단계에서 count 변수를 message 에 매핑하고 function 은 눈에 띄기 쉽게 ++++ 로 설정합니다. 
    
![Untitled](%5BWorkbook%204%5D%20Building%20Flow%20Services%20-%20LOOP%20adc3c2842c234df2ba93e2fcfb87669d/new8.png)
    

    
#### STEP 6. 이제 해당 Flowservice를 저장하고 실행합니다. 

- Service가 input값을 요청하면 input 필드를 확장하고, employee 를 선택 후, 2개의 행을 추가합니다. (아이콘 중 아래 행을 추가하는 아이콘을 클릭합니다.)
![Untitled](%5BWorkbook%204%5D%20Building%20Flow%20Services%20-%20LOOP%20adc3c2842c234df2ba93e2fcfb87669d/new9.png)

- 추가 한 employee 에 두 개의 data 를 입력 후 확인을 클릭합니다.
![Untitled](%5BWorkbook%204%5D%20Building%20Flow%20Services%20-%20LOOP%20adc3c2842c234df2ba93e2fcfb87669d/new10.png)
  
- 실행 후 Result 탭을 확인 하고, IS 서버 웹 관리 페이지 Logs > Server Log 에서 로그를 확인합니다. 
    
![Untitled](%5BWorkbook%204%5D%20Building%20Flow%20Services%20-%20LOOP%20adc3c2842c234df2ba93e2fcfb87669d/new11.png)
    
![Untitled](%5BWorkbook%204%5D%20Building%20Flow%20Services%20-%20LOOP%20adc3c2842c234df2ba93e2fcfb87669d/new12.png)
    

    
## Check Your Understanding
    
#### QUIZ 1. LOOP 아래에 MAP 단계를 들여놓지 않으면 어떻게 되나요?
#### QUIZ 2. Employee를 몇 명 추가할 수 있습니까? LOOP에 제한이 있습니까?
#### QUIZ 3. Service input에 document를 작성하지 않고 document references를 사용하는 이유는 무엇입니까?
