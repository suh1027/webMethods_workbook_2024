# [Workbook 9] Working With Flat Files

## Overview

이번 연습에서는 , 새로운 **Flat File Dictionary**을 생성하고, **Dictionary**에 재사용 가능한 **record definition**을 생성, 
새 **Flat File Schema**에서 **record definition**를 참조하고, **Flat File Schema**를 테스트 합니다.


## Steps

#### STEP 1. **Acme package** 에서 **acme.ff** 폴더를 생성하고, **schema**와 **dictionary** 라는 두 개의 새 폴더를 생성합니다. **acme.ff.dictionary:customer**라는 **Flat File Dictionary** 를 생성합니다.   
    
![Untitled](%5BWorkbook%209%5D%20Working%20With%20Flat%20Files%20bacbba872fe74e12adf97c424524e971/Untitled.png)
    

#### STEP 2. 열려 있는 **Flat File Dictionary customer**에서 **Record Definition**을 우-클릭 하여 **Address** (대소문자 구분)라는 **record definition**을 생성합니다. **Extractor Type** **of Fixed Position**을 사용하여, **Address** **record**에 새로운 **6**개의 **Field definitions**을 추가합니다. 아래와 같이 구성합니다.
    
![Untitled](%5BWorkbook%209%5D%20Working%20With%20Flat%20Files%20bacbba872fe74e12adf97c424524e971/Untitled%201.png)
    
![Untitled](%5BWorkbook%209%5D%20Working%20With%20Flat%20Files%20bacbba872fe74e12adf97c424524e971/Untitled%202.png)
    
**작업을 저장하세요**
    

#### STEP 3. **acme.ff.schema:addressFixed**라는 새로운 **Flat File Schema**를 생성하세요. **Record length**가 **79** **Fixed Length**로 지정합니다.    
    
![Untitled](%5BWorkbook%209%5D%20Working%20With%20Flat%20Files%20bacbba872fe74e12adf97c424524e971/Untitled%203.png)
    

  

#### STEP 4. **addressFixed schema**의 **Default Record** 속성에서, **Set** 행의 **Value** 열에 있는 버튼을 클릭 합니다.
    
![Untitled](%5BWorkbook%209%5D%20Working%20With%20Flat%20Files%20bacbba872fe74e12adf97c424524e971/Untitled%204.png)
    
**Dialog navigate**에서 **customer dictionary**으로 이동하여 선택합니다. **Click Next**.
    
![Untitled](%5BWorkbook%209%5D%20Working%20With%20Flat%20Files%20bacbba872fe74e12adf97c424524e971/Untitled%205.png)
    
**Select Default Record dialog**에서 **Address record**를 선택하고 **Finish** 버튼을 클릭 합니다.   
    
![Untitled](%5BWorkbook%209%5D%20Working%20With%20Flat%20Files%20bacbba872fe74e12adf97c424524e971/Untitled%206.png)
    

#### STEP 5. **Package Navigator에서 addressFixed Flat File Schema**를 우클릭 하여 작업을 저장하고 테스트 합니다. **Run As → Flat File Schema** 선택**. Input** 으로 **...\‌IntegrationServer\‌packages\‌AcmeSupport\‌pub\‌FlatFile\‌addressFixed.txt** 파일을 찾습니다**.**
    
**Flat File Results view**에서 테스트 결과를 검사하십시오.
    
![Untitled](%5BWorkbook%209%5D%20Working%20With%20Flat%20Files%20bacbba872fe74e12adf97c424524e971/Untitled%207.png)
    

#### STEP 6. **addressFixed schema**가 올바르게 작동하면, **Document Type** 아이콘을 선택 후 **addressFixedDT IS document type**을 생성합니다. 
    
**Create Document Type**을 활성화 하려면 **Flat File Structure tab**을 선택해야 합니다.
    
![Untitled](%5BWorkbook%209%5D%20Working%20With%20Flat%20Files%20bacbba872fe74e12adf97c424524e971/Untitled%208.png)
    


## Check Your Understanding
#### QUIZ 1. Flat files 을 XML 문서처럼 가져올 수 없는 이유는 무엇입니까?
#### QUIZ 2. N번째 필드의 의미는 무엇입니까?
#### QUIZ 3. Dictionary 와 schema 의 차이점은 무엇입니까?
#### QUIZ 4. Schema 가 완성되었을 때 IS document type 을 생성해야 하는 이유는 무엇입니까?
