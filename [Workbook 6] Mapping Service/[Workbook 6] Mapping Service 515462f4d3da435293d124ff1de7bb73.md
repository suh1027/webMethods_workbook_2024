# [Workbook 6] Mapping Service

## Overview

이 장에서는 미리 만들어진 Document Type 컴포넌트를 사용하여 한 데이터 형식에서 다른 데이터 형식으로 매핑하는 플로우 서비스를 생성합니다.


## Steps

#### STEP 1.  PurchaseOrder.maps 폴더에서 orderRequestToCanonical라는 Flow 서비스를 생성하세요. 

#### STEP 2. **isValid라는** **문자열** **변수를** **입력값으로** **하고** **PurchaseOrder.docs.request:OrderRequest** 문서를 참조하는 ‘**OrderRequest’로** **설정하세요**.
#### STEP 3. 출력값으로 **PurchaseOrder.docs:OrderCanonical 문서를** **참조하는 ‘OrderCanonical’로** **설정하세요**.

![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%20515462f4d3da435293d124ff1de7bb73/Untitled.png)


#### STEP 4.서비스에 MAP을** **추가하세요. MAP문에서** **다음** **변수를 Pipeline 탭에서** **왼쪽에서** **오른쪽으로** **매핑하세요.**
- **OrderRequest/PurchaseOrderRequest/PurchaseOrder/totalCost** 를 **OrderCanonical/Header/TotalCost로** **매핑하세요.**
- **isValid** 를 **OrderCanonical/Header/IsValid로** **매핑하세요.**
- **OrderRequest/PurchaseOrderRequest/fromRole/PartnerRoleDescription/DUNS** 를 **OrderCanonical/Header/Sender/ID로** **매핑하세요.**
- **OrderRequest/PurchaseOrderRequest/toRole/PartnerRoleDescription/DUNS** 를 **OrderCanonical/Header/Receiver/ID 매핑하세요.**

#### STEP 5.  **MAP 단계에서** **Transformer에** **string:toUpper서비스를** **추가하세요 . 다음** **변수를** **OrderRequest 에서 Transformer로** **그리고 Transformer 에서OrderCanonical로** **매핑하세요:**

- **OrderRequest/‌PurchaseOrderRequest/‌thisDocumentIdentifier/‌ProprietaryDocumentIdentifer에서 Transformer의 inString으로** **매핑하세요.**
    - Transformer**의** **값을** **OrderCanonical/‌Header/‌OrderID로** **매핑하세요.**
    - Transformer의 값을**OrderCanonical/‌Header/‌TransactionID로** **매핑하세요.**

#### STEP 6. **MAP 단계에서 Transformer에** **date:getCurrentDateString 서비스를** **추가하세요.맵에서** **다음** **변수를 Transformer에서 OrderCanonical문서** **사이로** **매핑하세요.**.
- **Transformer에서 MMMM dd, yyyy패턴으로** **설정하세요.**
- **Transformer의** **값을 OrderCanonical/‌Header/‌OrderDate로** **매핑하세요.**

![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%20515462f4d3da435293d124ff1de7bb73/Untitled%201.png)

#### STEP 7. 서비스에 **LOOP**단계를 추가하세요. 입력값 배열을/**OrderRequest/‌PurchaseOrderRequest/‌PurchaseOrder/‌ProductLineItem로 설정하세요**. 출력값 배열을 /**OrderCanonical/‌Items로 설정하세요.**   

![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%20515462f4d3da435293d124ff1de7bb73/Untitled%202.png)

#### STEP 8. **LOOP내에 MAP 단계를 추가하세요 (반드시 LOOP문 아래 들여쓰기 되어야 합니다). OrderRequest 변수에서 OrderCanonical의 /OrderCanonical/‌Items/‌Quantity 멤버로 /OrderRequest/‌PurchaseOrderRequest/‌PurchaseOrder/‌ProductLineItem/‌ProductQuantity를 매핑하세요.  팁: 이렇게 깊게 중첩된 구조를 매핑할 때는 두 단계로 매핑 라인을 만드는 것이 종종 더 쉽습니다. 먼저 마우스로 클릭하여 from 및 to 필드를 선택한 다음, 두 선택한 필드를 연결하려면 ‘Create a Link...’을 클릭하세요.**

![ **이** **버튼은 Pipeline 창의** **타이틀** **바에** **위치합니다**.](%5BWorkbook%206%5D%20Mapping%20Service%20515462f4d3da435293d124ff1de7bb73/e5a43352-d551-4200-8212-24d0cbd28aee.png)

 **이** **버튼은 Pipeline 창의** **타이틀** **바에** **위치합니다**.

#### STEP 9. **MAP단계에서 Transformer에 string:toUpper서비스를** **추가하세요. 다음** **변수를** **매핑하세요:**
    
- /OrderRequest/‌PurchaseOrderRequest/‌PurchaseOrder/‌ProductLineItem/‌productUnit/‌ProductPackageDescription/‌ProductIdentification/‌GlobalProductIdentifier 를 Transformer의 InString으로 매핑하세요.
- Transformer의 값을/OrderCanonical/‌Items/‌SKU로 매핑하세요
    
![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%20515462f4d3da435293d124ff1de7bb73/Untitled%203.png)
    
#### STEP 10. **서비스를** **저장하고** **실행하세요. 입력** **파일로** **…\IntegrationServer\‌packages\‌AcmeSupport\‌pub\‌txt을** **사용하세요 (테스트할** **때 isValid를 true 또는 false로** **설정하는** **것을** **잊지** **마세요!**).
    
    **결과창을 확인하세요. OrderRequest 축소하고 OrderCanonical을 살펴보세요. 이 변수는 완전히 채워져 있어야 합니다. 특히 날짜 및 대문자로 된 OrderID, TransactionID 및 SKU값들을 확인하십시오.**
    
![Untitled](%5BWorkbook%206%5D%20Mapping%20Service%20515462f4d3da435293d124ff1de7bb73/Untitled%204.png)
    

## Check Your Understanding

#### QUIZ 1. Transformer와 일반 서비스 간의 차이는 무엇인가요?
#### QUIZ 2. 원하는 Transformer가 Transformer 드롭다운 목록에 없는 경우 어떻게 해야하나요?
#### QUIZ 3. 왜 ProductLineItems를 LOOP하여 처리해야 했나요? ProductLineItems에서 Items로 직접 매핑하지 않는 이유는 무엇인가요?
