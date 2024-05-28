# [Workbook 6] Mapping Service

## Overview

이 장에서는 한 데이터 형식에서 다른 데이터 형식으로 매핑, 특정 변수 값을 지정하거나 변환하는 서비스 기능을 설명합니다.

1. 암묵적 / 명시적 매핑
2. 조건적 매핑
3. Set Value 를 사용한 매핑
4. Transformer 기능


## Steps

#### STEP 0. 최상위 폴더 아래 IF0005와 그 하위 폴더로 svc 와 docs 폴더를 생성합니다. 

#### STEP 1. 암묵적/명시적 매핑 기능을 확인합니다.
    
- Designer는 하나의 서비스 단계 내에서 같은 이름, 데이터 타입이 동일한 변수들을 암묵적으로 연결하거나 매핑합니다. 

  - 최상위 폴더 아래 IF0005 와 svc 폴더를 생성한 후, svc_IF0005_implicitMap라는 Flow service를 생성하세요. 
    
  ![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%2032520d2f4376462f83bb53b45e0694d8/Untitled.png)
    
  - pub.math:divideInts 서비스 단계를 추가합니다.

  ![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%2032520d2f4376462f83bb53b45e0694d8/Untitled%201.png)
    
  - Input/Output 탭에서 다음과 같이 input/output 변수(num1, num2, result) 를 각각 추가 후 서비스를 저장합니다.

  ![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%2032520d2f4376462f83bb53b45e0694d8/Untitled%202.png)
    
  - 이제 pub.math:divideInts 단계에서 암묵적 매핑이 되어 있는것을 확인합니다. Service Out 의 value 는 Drag & Drop 하여 result 와 명시적으로 매핑을 합니다.
  
  **Note.** num1 과 num2 는 동일한 타입, 동일한 명칭의 변수로 암묵적으로 매핑 되어 있는 것을 확인할 수 있습니다.
  **Note.** 암묵적 연결은 회색선으로 연결됩니다. (ex. num1, num2, value)
  
  ![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%2032520d2f4376462f83bb53b45e0694d8/Untitled%203.png)

    
     

#### STEP 2. 조건적 매핑 기능을 확인합니다.

- MAP 단계에서 변수간 매핑 연결에 조건을 둘 수 있습니다.

  - IF0005.svc 폴더 아래 새로운 svc_IF0005_conditionalMap 이라는 Flow service를 생성하세요. 
    
  ![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%2032520d2f4376462f83bb53b45e0694d8/Untitled%204.png)
    
  - MAP 서비스를 단계를 추가 합니다.

  ![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%2032520d2f4376462f83bb53b45e0694d8/Untitled%205.png)
    
  - Input/Output 변수는 다음과 같이 구성합니다.

  ![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%2032520d2f4376462f83bb53b45e0694d8/Untitled%206.png)
    
  - Pipeline에서 Value1 를 outputString 에 연결하고 우측 Properties > Copy Condition 의 조건 값을 입력하여 매핑 조건을 설정합니다.
    - **Value1 - ouputString**
   
        Copy condition: %Source/switchValue%==1
      
        Indices: /Source/Elements/Value1 --> /outputString

    - **Value2 - ouputString**
    
        Copy condition: %Source/switchValue%==2
      
        Indices: /Source/Elements/Value2 --> /outputString

    - **Value3 - ouputString**
    
        Copy condition: %Source/switchValue%==3
      
        Indices: /Source/Elements/Value3 --> /outputString

  ![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%2032520d2f4376462f83bb53b45e0694d8/Untitled%207.png)
    
  **Note.** 조건적 매핑의 선은 파란색으로 연결됩니다.
  
  **Note.** Copy Condition 값은 정규표현식을 사용해 입력하며 위 값은 /Source/switchValue 값이 1일 경우를 표현합니다.
  
    
  - 서비스를 실행하여 결과값을 확인하세요.

  ![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%2032520d2f4376462f83bb53b45e0694d8/Untitled%208.png)

  ![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%2032520d2f4376462f83bb53b45e0694d8/Untitled%209.png)

  ![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%2032520d2f4376462f83bb53b45e0694d8/Untitled%2010.png)
    




#### STEP 3. Set Value 를 사용한 매핑

  - 최상위 폴더 아래 IF0005 와 svc 폴더를 생성한 후,  svc_IF0005_setValueMap라는 Flow service를 생성하세요.
    
  ![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%2032520d2f4376462f83bb53b45e0694d8/Untitled%2012.png)
    
  - pub.math:addInts 서비스를 호출 해줍니다.

  ![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%2032520d2f4376462f83bb53b45e0694d8/Untitled%2013.png)
    
  - Input/Output 변수를 생성 해줍니다.

  ![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%2032520d2f4376462f83bb53b45e0694d8/Untitled%2014.png)
    
  - Pipeline 에서 result변수 우클릭 후 set value클릭
    
  ![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%2032520d2f4376462f83bb53b45e0694d8/Untitled%2015.png)

  - 출력하고자 하는 값을 Value에 넣어주고 “Perform Variable Substitution” 체크해줍니다.
    
  ![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%2032520d2f4376462f83bb53b45e0694d8/Untitled%2016.png)

  **파이프라인의 변수명= %변수명%**

  ![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%2032520d2f4376462f83bb53b45e0694d8/Untitled%2017.png)

  - flow service를 실행하여 결과값을 확인해줍니다.
    
  ![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%2032520d2f4376462f83bb53b45e0694d8/Untitled%2018.png)

  ![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%2032520d2f4376462f83bb53b45e0694d8/Untitled%2019.png)  
  


#### STEP 4. Transformer 를 이용한 mapping

  - 최상위 폴더 아래 IF0005 와 svc 폴더를 생성한 후 svc_IF0005_transformer 라는 서비스를 생성 하세요.

![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%2032520d2f4376462f83bb53b45e0694d8/Untitled%2021.png)  

  - 서비스에 MAP을 추가 한 뒤, Transformer에 date:getCurrentDateString 서비스를 추가하세요.
      - Transformers 에 생성 된 서비스를 확장하여 pattern = MMMM dd,yyyy 로 설정하고, value 는 Pipeline Out 의 date 변수와 매핑하세요.

    ![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%2032520d2f4376462f83bb53b45e0694d8/98514b54-25bd-45e5-876a-0b79e7c9a500.png)    

  - MAP 단계에서 Transformer에 string:toUpper서비스를 추가하세요 . 다음 변수를 Transformer 로 그리고 Transformer 에서 pipeline out의 변수 outputName 으로 매핑하세요.
  
    ![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%2032520d2f4376462f83bb53b45e0694d8/Untitled%2022.png)  

  - 서비스를 저장하고 입력값을 넣어 실행 후 결과창을 확인하세요. 특히 현재 날짜 및 대문자로 바뀐 name 값을 확인하십시오.
  
    ![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%2032520d2f4376462f83bb53b45e0694d8/Untitled%2023.png)  

## Check Your Understanding

#### QUIZ 1. Transformer와 일반 서비스 간의 차이는 무엇인가요?

#### QUIZ 2. 원하는 Transformer가 Transformer 드롭 다운 목록에 없는 경우 어떻게 해야하나요?
