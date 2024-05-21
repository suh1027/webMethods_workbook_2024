# [Workbook 4] Building Flow Services - LOOP

## Overview

이 연습에서는 Flow service의 Loop 문을 사용하여 직원 목록을 처리하는 비즈니스 로직을 생성합니다.


## Steps

#### STEP 1. acme.PurchaseOrder.work 폴더에 loopTest라는 새로운 Flow service 을 만듭니다. 서비스의 input 은 acmeSupport.docs:Depart라는 Dept로 Document Reference(문서 참조)로 설정하고 output을 count라는 단일 String Type 으로 설정합니다.
    
    
*참고 :Input 또는 output 항목 field는 사용하지 마십시오. 이 항목의 목적에 대해서는 추후에 설명합니다.*
    
![Untitled](%5BWorkbook%204%5D%20Building%20Flow%20Services%20-%20LOOP%20adc3c2842c234df2ba93e2fcfb87669d/Untitled.png)
    

#### STEP 2. Service의 Input/Output 탭에서 Department 변수를 확장하여 Department/department/employee를 찾고 Copy를 마우스 오른쪽 버튼으로 클릭합니다.
#### STEP 3. Service에서 LOOP 문을 추가하고 Input array 속성에서 Department/employee에 붙여넣습니다. Enter 키를 누르면 LOOP에 Input array가 표시됩니다. 
    
![Untitled](%5BWorkbook%204%5D%20Building%20Flow%20Services%20-%20LOOP%20adc3c2842c234df2ba93e2fcfb87669d/Untitled%201.png)
    
![Untitled](%5BWorkbook%204%5D%20Building%20Flow%20Services%20-%20LOOP%20adc3c2842c234df2ba93e2fcfb87669d/Untitled%202.png)
    

#### STEP 4. LOOP 단계 아래에 MAP 문을 추가합니다(LOOP 아래에 들여쓰기를 확인하십시오). $iteration을 계산할 수 있도록 합니다.
    
    
![Untitled](%5BWorkbook%204%5D%20Building%20Flow%20Services%20-%20LOOP%20adc3c2842c234df2ba93e2fcfb87669d/Untitled%203.png)
    
![Untitled](%5BWorkbook%204%5D%20Building%20Flow%20Services%20-%20LOOP%20adc3c2842c234df2ba93e2fcfb87669d/Untitled%204.png)
    

#### STEP 5. Pub.flow:debugLog를 MAP 단계 아래에 추가합니다(LOOP 아래에 들여쓰기 되지 않았는지 확인). Count를 message에 매핑하고 function을 설정합니다. 
    
![Untitled](%5BWorkbook%204%5D%20Building%20Flow%20Services%20-%20LOOP%20adc3c2842c234df2ba93e2fcfb87669d/Untitled%205.png)
    
![Untitled](%5BWorkbook%204%5D%20Building%20Flow%20Services%20-%20LOOP%20adc3c2842c234df2ba93e2fcfb87669d/Untitled%206.png)
    
*참고: LOOP 문을 추가하면 $iteration이라는 새로운 변수가 Pipeline에 나타납니다. 이 변수는 루프의 반복 횟수를 추적합니다.* 
    
#### STEP 6. Service를 저장하고 실행합니다. Service가 input값을 요청하면 input box를 확장하고, employee를선택하고, 2명을 선택한 후 행을 추가합니다. 각 employee의 data를 입력합니다. 확인을 클릭합니다. Server log에서 2를 봐야 합니다. 
    
![Untitled](%5BWorkbook%204%5D%20Building%20Flow%20Services%20-%20LOOP%20adc3c2842c234df2ba93e2fcfb87669d/Untitled%207.png)
    
![Untitled](%5BWorkbook%204%5D%20Building%20Flow%20Services%20-%20LOOP%20adc3c2842c234df2ba93e2fcfb87669d/Untitled%208.png)
    

    
## Check Your Understanding
    
#### QUIZ 1. LOOP 아래에 MAP 단계를 들여놓지 않으면 어떻게 됩니까?
#### QUIZ 2. Employee를 몇 명 추가할 수 있습니까? LOOP에 제한이 있습니까?
#### QUIZ 3. Service input에 document를 작성하지 않고 document references를 사용하려는 이유는 무엇입니까?
