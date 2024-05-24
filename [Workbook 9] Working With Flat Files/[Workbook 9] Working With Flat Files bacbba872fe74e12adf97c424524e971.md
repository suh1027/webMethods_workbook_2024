# [Workbook 9] Working With Flat Files

## Overview

이번 연습에서는 Flatfile 을 다루는 서비스를 연습합니다.

webMethods 에서 Flatfile 을 다루기 위해서는 **Flat File Dictionary** 와 **Flat File Schema** 두 개의 컴포넌트 가 필요합니다.

**Flat File Dictionary** 에는 재사용 가능한 **record definition**을 생성하고,

**Flat File Schema** 에서는 생성 된 **record definition**를 참조하여 스키마를 구성합니다. 

구성 된 컴포넌트를 사용하여 서비스를 생성 & 테스트 합니다.


## Steps

#### STEP 1. 최상위 폴더 아래 IF0008 과 svc, ff 폴더를 생성합니다. (ff 폴더는 flatfile 컴포넌트 저장용 폴더입니다.)    

#### STEP 2. 생성 된 IF0008.ff 폴더 아래, schema와 dictionary 두 개의 폴더를 생성합니다. IF0008.ff.dictionary:customer 라는 Flat File Dictionary 를 생성합니다.

![Untitled](%5BWorkbook%209%5D%20Working%20With%20Flat%20Files%20bacbba872fe74e12adf97c424524e971/Untitled.png)
    

#### STEP 3. 열려 있는 **Flat File Dictionary customer**에서 **Record Definition**을 우클릭 하여 **Address** (대소문자 구분)라는 **Record definition**을 생성합니다. **Extractor Type** **of Fixed Position**을 사용하여, **Address** **record**에 새로운 **6**개의 **Field definitions**을 추가합니다. 아래와 같이 구성합니다.
    
![Untitled](%5BWorkbook%209%5D%20Working%20With%20Flat%20Files%20bacbba872fe74e12adf97c424524e971/Untitled%201.png)

- Record Definition 생성
  
![Untitled](%5BWorkbook%209%5D%20Working%20With%20Flat%20Files%20bacbba872fe74e12adf97c424524e971/Untitled%202.png)
    
- Record 생성 후 Composite 또는 Field 생성
  
![Untitled](%5BWorkbook%209%5D%20Working%20With%20Flat%20Files%20bacbba872fe74e12adf97c424524e971/Untitled%203.png)    
생성은 Definition/Reference로 생성 가능 (정의 또는 기존 Element 재사용)
- Field 정의
  
![Untitled](%5BWorkbook%209%5D%20Working%20With%20Flat%20Files%20bacbba872fe74e12adf97c424524e971/Untitled%204.png)    

![Untitled](%5BWorkbook%209%5D%20Working%20With%20Flat%20Files%20bacbba872fe74e12adf97c424524e971/Untitled%205.png)    

**작업을 저장하세요**
    

#### STEP 4. IF0008.ff.schema:addressFixed라는 새로운 Flat File Schema를 생성하세요. Record length가 79자인 Fixed Length로 지정합니다.        
    
![Untitled](%5BWorkbook%209%5D%20Working%20With%20Flat%20Files%20bacbba872fe74e12adf97c424524e971/Untitled%206.png)
    

  

#### STEP 5. **addressFixed schema**의 **Default Record** 속성에서, **Set** 행의 **Value** 열에 있는 버튼을 클릭 합니다.
    
![Untitled](%5BWorkbook%209%5D%20Working%20With%20Flat%20Files%20bacbba872fe74e12adf97c424524e971/Untitled%207.png)
    
**Dialog navigate**에서 **customer dictionary**으로 이동하여 선택합니다. **Click Next**.
    
![Untitled](%5BWorkbook%209%5D%20Working%20With%20Flat%20Files%20bacbba872fe74e12adf97c424524e971/Untitled%208.png)
    
**Select Default Record dialog**에서 **Address record**를 선택하고 **Finish** 버튼을 클릭 합니다.   
    
![Untitled](%5BWorkbook%209%5D%20Working%20With%20Flat%20Files%20bacbba872fe74e12adf97c424524e971/Untitled%209.png)
    

#### STEP 6. Package Navigator에서 addressFixed Flat File Schema를 우클릭 하여 작업을 저장하고 테스트 합니다. Run As → Flat File Schema 선택. Input 으로 ...\‌IntegrationServer\‌packages\‌AcmeSupport\‌pub\‌FlatFile\‌addressFixed.txt 파일을 찾습니다.
    
**Flat File Results view**에서 테스트 결과를 검사하십시오.
    
![Untitled](%5BWorkbook%209%5D%20Working%20With%20Flat%20Files%20bacbba872fe74e12adf97c424524e971/Untitled%2010.png)
    

#### STEP 7. **addressFixed schema**가 올바르게 작동하면, **Document Type** 아이콘을 선택 후 **addressFixedDT IS document type**을 생성합니다. 
    
**Create Document Type**을 활성화 하려면 **Flat File Structure tab**을 선택해야 합니다.
    
![Untitled](%5BWorkbook%209%5D%20Working%20With%20Flat%20Files%20bacbba872fe74e12adf97c424524e971/Untitled%2011.png)

    
#### STEP 8. 1. **pub.file:getFIle, pub.flatFile:convertToValues** 서비스를 사용한 예시.  **IF0008.svc** 아래 **svc_IF0008_receive** 서비스 ****생성합니다.
    
**Input/Output**에 **fileName** 추가합니다.

![Untitled](%5BWorkbook%209%5D%20Working%20With%20Flat%20Files%20bacbba872fe74e12adf97c424524e971/Untitled%2012.png)

**pub.file:getFIle**, **pub.string:bytesToString**, **pub.flatFile:convertToValues** 서비스를 위치 시킵니다.

![Untitled](%5BWorkbook%209%5D%20Working%20With%20Flat%20Files%20bacbba872fe74e12adf97c424524e971/Untitled%2013.png)

**string**과 **ffData**를 매핑하고, **ffSchema**에 생성했던 **schema**인 **addressFixed** 입력합니다.

![Untitled](%5BWorkbook%209%5D%20Working%20With%20Flat%20Files%20bacbba872fe74e12adf97c424524e971/Untitled%2014.png)

실행 결과 값 예시 (**Input**에 **addressFixed.txt** 파일 경로 넣고 실행) 

![Untitled](%5BWorkbook%209%5D%20Working%20With%20Flat%20Files%20bacbba872fe74e12adf97c424524e971/Untitled%2015.png)

## Check Your Understanding
#### QUIZ 1. Flat files 을 XML 문서처럼 가져올 수 없는 이유는 무엇입니까?
#### QUIZ 2. N번째 필드의 의미는 무엇입니까?
#### QUIZ 3. Dictionary 와 schema 의 차이점은 무엇입니까?
#### QUIZ 4. Schema 가 완성되었을 때 IS document type 을 생성해야 하는 이유는 무엇입니까?
