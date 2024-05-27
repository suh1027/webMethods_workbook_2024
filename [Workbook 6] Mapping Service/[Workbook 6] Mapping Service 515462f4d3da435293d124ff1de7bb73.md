# [Workbook 6] Mapping Service

## Overview

이 장에서는 미리 만들어진 Document Type 컴포넌트를 사용하여 한 데이터 형식에서 다른 데이터 형식으로 매핑하는 플로우 서비스를 생성합니다.


## Steps

#### STEP 1. 암묵적 매핑 서비스
    
- Designer는 하나의 flow내에 같은 이름, 데이터 타입이 적합한 변수들을 암묵적으로 연결하거나 매핑합니다. 

  a. 최상위 폴더 아래 IF0005 와 svc 폴더를 생성한 후, svc_IF0005_implicitMap라는 Flow service를 생성하세요. 
    
  ![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%2032520d2f4376462f83bb53b45e0694d8/Untitled.png)
    
  b. pub.math:divideInts 서비스를 호출합니다.

  ![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%2032520d2f4376462f83bb53b45e0694d8/Untitled%201.png)
    
  c. Input/Output 탭에서 input/output 변수를 각각 추가 해줍니다.

  ![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%2032520d2f4376462f83bb53b45e0694d8/Untitled%202.png)
    
  d. Service Out의 value 값을 Pipeline Out의 result에 명시적으로 매핑해줍니다.

  ![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%2032520d2f4376462f83bb53b45e0694d8/Untitled%203.png)
    
  암묵적 연결은 회색선으로 연결됩니다.
    
     

#### STEP 2. 조건적 Mapping

- Mapping 연결에 조건을 둘 수 있습니다.

  a. 최상위 폴더 아래 IF0005 와 svc 폴더를 생성한 후, svc_IF0005_conditionalMap라는 Flow service를 생성하세요. 
    
  ![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%2032520d2f4376462f83bb53b45e0694d8/Untitled%204.png)
    
  b. MAP 서비스를 추가 해줍니다.

  ![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%2032520d2f4376462f83bb53b45e0694d8/Untitled%205.png)
    
  c. Input/Output 변수를 추가 해줍니다.

  ![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%2032520d2f4376462f83bb53b45e0694d8/Untitled%206.png)
    
  d. Pipeline에서 Value1부터 차례로 outputString에 연결하고 Mapping 연결선을 클릭하여 Properties>Copy condition과 Indices를 채워줍니다.
    
  ![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%2032520d2f4376462f83bb53b45e0694d8/Untitled%207.png)
    
- 조건적 연결은 파란색으로 연결됩니다.
- Copy condition 값이 true일 때, 해당하는 값이 outputString에 복사됩니다.
    
  e. 서비스를 실행하여 결과값을 확인하세요.

  ![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%2032520d2f4376462f83bb53b45e0694d8/Untitled%208.png)

  ![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%2032520d2f4376462f83bb53b45e0694d8/Untitled%209.png)

  ![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%2032520d2f4376462f83bb53b45e0694d8/Untitled%2010.png)
    
**note! Mapping Indices**

- 배열의 개별 요소를 매핑할 수 있습니다. 이렇게 하려면, Indices property를 편집하고 입/출력값 변수를 설정합니다.
    
- 새로운 동작을 보여주기 위해 선이 파란색으로 바뀝니다.

  ![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%2032520d2f4376462f83bb53b45e0694d8/Untitled%2011.png)



#### STEP 3. Set Value를 사용한 Mapping

  a. 최상위 폴더 아래 IF0005 와 svc 폴더를 생성한 후,  svc_IF0005_setValueMap라는 Flow service를 생성하세요.
    
  ![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%2032520d2f4376462f83bb53b45e0694d8/Untitled%2012.png)
    
  b. pub.math:addInts 서비스를 호출 해줍니다.

  ![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%2032520d2f4376462f83bb53b45e0694d8/Untitled%2013.png)
    
  c. Input/Output 변수를 생성 해줍니다.

  ![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%2032520d2f4376462f83bb53b45e0694d8/Untitled%2014.png)
    
  d. Pipeline 에서 result변수 우클릭 후 set value클릭
    
  ![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%2032520d2f4376462f83bb53b45e0694d8/Untitled%2015.png)

  e. 출력하고자 하는 값을 Value에 넣어주고 “Perform Variable Substitution” 체크해줍니다.
    
  ![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%2032520d2f4376462f83bb53b45e0694d8/Untitled%2016.png)

  **파이프라인의 변수명= %변수명%**

  ![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%2032520d2f4376462f83bb53b45e0694d8/Untitled%2017.png)

  f. flow service를 실행하여 결과값을 확인해줍니다.
    
  ![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%2032520d2f4376462f83bb53b45e0694d8/Untitled%2018.png)

  ![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%2032520d2f4376462f83bb53b45e0694d8/Untitled%2019.png)  
  
**note! Mapping Indices**

- 양쪽 스크롤링이 가능합니다.
  - Transformers 은 확장된다면 , 싱글 스크롤링 모드는 Transformer가 collapse 될 때까지 사용됩니다.

    ![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%2032520d2f4376462f83bb53b45e0694d8/Untitled%2020.png)  

#### STEP 4. Transformer를 이용한 mapping

  a. 최상위 폴더 아래 IF0005 와 svc 폴더를 생성한 후 svc_IF0005_transformer 라는 서비스를 생성 하세요.

    ![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%2032520d2f4376462f83bb53b45e0694d8/Untitled%2021.png)  

  b. 서비스에 MAP을 추가 한 뒤, Transformer에 date:getCurrentDateString 서비스를 추가하세요.
  맵에서 다음 변수를

- **Transformer에서 MMMM dd, yyyy패턴으로** **설정하세요.**

- **Transformer의** **값을date로** **매핑하세요.**

    ![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%2032520d2f4376462f83bb53b45e0694d8/98514b54-25bd-45e5-876a-0b79e7c9a500.png)    

  c. MAP 단계에서 Transformer에 string:toUpper서비스를 추가하세요 . 다음 변수를 Transformer로 그리고 Transformer 에서pipeline out의 변수들로 매핑하세요.
  
    ![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%2032520d2f4376462f83bb53b45e0694d8/Untitled%2022.png)  

  d. 서비스를 저장하고 입력값을 넣어 실행 후 결과창을 확인하세요. 특히 현재 날짜 및 대문자로 바뀐 name값을 확인하십시오.
  
    ![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%2032520d2f4376462f83bb53b45e0694d8/Untitled%2023.png)  

## Check Your Understanding

#### QUIZ 1. Transformer와 일반 서비스 간의 차이는 무엇인가요?

#### QUIZ 2. 원하는 Transformer가 Transformer 드롭 다운 목록에 없는 경우 어떻게 해야하나요?
