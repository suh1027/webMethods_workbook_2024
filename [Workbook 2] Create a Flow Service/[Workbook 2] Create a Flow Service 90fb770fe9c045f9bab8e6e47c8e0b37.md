# [Workbook 2] Create a Flow Service

## Overview

이 연습에서는 Flow service를 만들고 실행합니다.


## Steps

#### 1. Acme package 의 acme.PurchaseOrder.work folder 에서 customWriteToLog 라는 새로운 Flow service을 만듭니다.:
    
    ![Untitled](%5BWorkbook%202%5D%20Create%20a%20Flow%20Service%2090fb770fe9c045f9bab8e6e47c8e0b37/Untitled.png)
    
    ![Untitled](%5BWorkbook%202%5D%20Create%20a%20Flow%20Service%2090fb770fe9c045f9bab8e6e47c8e0b37/Untitled%201.png)
    

#### 2. **inMsg1, inMsg2**로 불리는 두 개의 String 타입의 input 값을 새로운 service에 추가합니다. 아래 메뉴를 보려면 Input/Output 탭을 선택하고 왼쪽에 있는 Input 패널에서 마우스 오른쪽 버튼을 클릭합니다. input Document 를 지정할 수 있는 text field과 혼동하지 마십시오.:   
    
    ![Untitled](%5BWorkbook%202%5D%20Create%20a%20Flow%20Service%2090fb770fe9c045f9bab8e6e47c8e0b37/Untitled%202.png)
    
    ![Untitled](%5BWorkbook%202%5D%20Create%20a%20Flow%20Service%2090fb770fe9c045f9bab8e6e47c8e0b37/Untitled%203.png)
    
    ![Untitled](%5BWorkbook%202%5D%20Create%20a%20Flow%20Service%2090fb770fe9c045f9bab8e6e47c8e0b37/Untitled%204.png)
    

#### 3. 새로운 service에 다음과 같이 세 가지 서비스 단계를 추가합니다.:
    - **flow:debugLog**
    - **string:toUpper**
    - **string:concat**
    
    이러한 service 단계를 추가하는 가장 쉬운 방법은 우측 Palette 에서 invoke... 을 클릭하여 서비스를 검색하거나 Package Navigatior 에서 WmPublic package 를 찾아 해당 services 을 끌어오는 것입니다.
    
    ![Untitled](%5BWorkbook%202%5D%20Create%20a%20Flow%20Service%2090fb770fe9c045f9bab8e6e47c8e0b37/Untitled%205.png)
    
#### 4. 위로 이동 및 아래로 이동 화살표 아이콘을 사용하여 서비스 순서를 다음과 같이 바꿉니다. 
    1. **string:concat**
    2. **string:toUpper**
    3. **flow:debugLog**
        
        
        ![Untitled](%5BWorkbook%202%5D%20Create%20a%20Flow%20Service%2090fb770fe9c045f9bab8e6e47c8e0b37/Untitled%206.png)
        
        (현재 비활성화된) 왼쪽 이동 아이콘과 오른쪽 이동 아이콘은 위로 이동 및 아래로 이동 아이콘 옆에 있으므로 나중에 연습할 경우 필요할 것입니다.
        
        ![Untitled](%5BWorkbook%202%5D%20Create%20a%20Flow%20Service%2090fb770fe9c045f9bab8e6e47c8e0b37/Untitled%207.png)
        
    
#### 5. 다음과 같이 services를 통해 입력한 데이터 흐름을 매핑합니다:
    1. **pub.string:concat** 
        1. **Msg1에서 String1에** **매핑해야** **합니다.**
        2. **Msg2에서 String2에** **매핑해야** **합니다.**
        
        ![Untitled](%5BWorkbook%202%5D%20Create%20a%20Flow%20Service%2090fb770fe9c045f9bab8e6e47c8e0b37/Untitled%208.png)
        
        이 단계를 완료하려면 IDE 하단의 pipeline view 로 전환하고 customWriteToLog의  editor view에서 pub.string:concat을 선택해야 합니다. 그런 다음 inMsg1 인수를 concat 서비스의 inString1 매개 변수로 끕니다. inMsg2 및 inString2에서 동일하게 수행합니다.
        
    2. **pub.string:toUpper**
        1. **value**에서 **inString에** **매핑해야** **합니다.**
        
        ![Untitled](%5BWorkbook%202%5D%20Create%20a%20Flow%20Service%2090fb770fe9c045f9bab8e6e47c8e0b37/Untitled%209.png)
        
    3. **pub.flow:debugLog**
        1. **value**에서 **message에 매핑해야 합니다.**
        
           
        
        ![Untitled](%5BWorkbook%202%5D%20Create%20a%20Flow%20Service%2090fb770fe9c045f9bab8e6e47c8e0b37/Untitled%2010.png)
        

#### 6. service를 저장하고 실행합니다. service 을 처음 실행하려면 service 메뉴에서 R **Run As** → **Run Flow Service** 를 선택해야 합니다. 
    
    ![Untitled](%5BWorkbook%202%5D%20Create%20a%20Flow%20Service%2090fb770fe9c045f9bab8e6e47c8e0b37/Untitled%2011.png)
    
    추가적인 방법으로 상단 도구 모음의 녹색 화살표 버튼을 누르면 됩니다:  
    
    ![Untitled](%5BWorkbook%202%5D%20Create%20a%20Flow%20Service%2090fb770fe9c045f9bab8e6e47c8e0b37/Untitled%2012.png)
    
    그런 다음 string 타입의 inputs 값을 입력합니다.
    
    ![Untitled](%5BWorkbook%202%5D%20Create%20a%20Flow%20Service%2090fb770fe9c045f9bab8e6e47c8e0b37/Untitled%2013.png)
    

#### 7. Designer에서 Service Result 보기를 확인한 다음 브라우저 기반 Integration Server Administration Console에서 Server log를 확인하여 service 가 성공적으로 executed 되었는지 확인합니다.
    
    ![Untitled](%5BWorkbook%202%5D%20Create%20a%20Flow%20Service%2090fb770fe9c045f9bab8e6e47c8e0b37/Untitled%2014.png)
    
    ![Untitled](%5BWorkbook%202%5D%20Create%20a%20Flow%20Service%2090fb770fe9c045f9bab8e6e47c8e0b37/Untitled%2015.png)
    

#### 8.	이 service에 대한 개발이 완료된 대로 service 잠금을 해제합니다.

![Untitled](%5BWorkbook%202%5D%20Create%20a%20Flow%20Service%2090fb770fe9c045f9bab8e6e47c8e0b37/Untitled%2016.png)

---

##  Check Your Understanding

1. Service의 순서가 중요한 이유는 무엇입니까?
2. string:toUpper service는 몇 개의 input값을 받을 수 있습니까?
3. server 가 명령 프롬프트를 통해 실행되지 않는 경우 server log는 어디에 표시됩니까?
4. Upper service의 output값을 매핑할 필요가 없었던 이유는 무엇입니까?
