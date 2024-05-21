# [Workbook 7] Create a Java Service

**※ Overview**

이 장에서는 **Designer**를 사용하여 **Java** 서비스를 생성, 컴파일하고 실행합니다. 특정 문자열이 두 번째 문자열로 끝나는지 테스트하는 특별한 서비스가 필요하다고 상상해보세요. **pub.string**  폴더에는 이와 같은 서비스가 없지만 **Java** 런타임 환경에서 **String.endsWith()** 메서드를 사용하려고 합니다. 

---

**※ Steps**

1. **acme.PurchaseOrder.work** 폴더에 **endsWith라는 새 Java 서비스를 생성하세요**. 이 서비스에는 **string** 및 **suffix**라는 두 개의 문자열 입력 및 **value**라는 문자열 출력이 있어야 합니다.   
    
    ![Untitled](%5BWorkbook%207%5D%20Create%20a%20Java%20Service%20dbc34d756ea943a2a8c1a6aaf20da91c/Untitled.png)
    

1. 서비스를 저장한 다음 패키지 네비게이터 뷰에서 해당 서비스를 마우스 오른쪽 버튼으로 클릭하고 **Generate Code…** -> **For implementing this service**를 선택한 다음 **Finish** 버튼을 클릭하세요. 이렇게 하면 템플릿 코드가 클립보드에 복사됩니다. **Java** 서비스의 소스 탭을 열고 생성된 코드를 빈 메서드 본문에 붙여 넣으세요. 그리고 다음과 같이 코드를 편집하세요:     
    
    ![Untitled](%5BWorkbook%207%5D%20Create%20a%20Java%20Service%20dbc34d756ea943a2a8c1a6aaf20da91c/Untitled%201.png)
    
    *참고*: **Eclipse IDE**에서 익숙한 코드 완성과 같은 모든 **Java** 개발 기능을 사용할 수 있습니다.   
    

1. 샘플 입력값으로 서비스를 저장하고 실행하세요. 반환된 값이 올바른지 확인하세요. 

---