# [Workbook 11] Create REST Service in Integration Server

## Overview


이번 exercise 에서는 Integration Server 에서 REST service 를 생성하고 Postman 을 사용하여 REST API service 를 호출합니다.


## Steps

#### STEP 1. **PurchaseOrder.work.REST** 라는 폴더와 getBook Flowservice 를 생성하세요.
#### STEP 2. REST 폴더 아래, **bookInformation** 라는 **REST Resource** 을 생성하세요.

![Untitled](%5BWorkbook%2011%5D%20Create%20REST%20Service%20in%20Integration%20S%20a83f4bcce6ee49c0a838556798b4e09c/Untitled.png)

![Untitled](%5BWorkbook%2011%5D%20Create%20REST%20Service%20in%20Integration%20S%20a83f4bcce6ee49c0a838556798b4e09c/Untitled%201.png)

#### STEP 3. REST Resource 의 Resource Configuration 탭에서 Resource 를 Add 하여 REST URL 을 추가합니다. 외부로부터 호출 받을 URL, HTTP Method, 실제 수행되는 서비스 (Flowservice) 를 매핑 하여 구성 후 저장합니다.

![Untitled](%5BWorkbook%2011%5D%20Create%20REST%20Service%20in%20Integration%20S%20a83f4bcce6ee49c0a838556798b4e09c/Untitled%202.png)

#### STEP 4. getBook Flowservice 를 구성합니다.
- https://github.com/benoitvallon/100-best-books/blob/master/books.json 파일을 사용하여 bookList 를 불러오는 서비스를 개발합니다. (/webM/IS01/books.json 을 생성하고 내용을 입력합니다.)
        
  ![Untitled](%5BWorkbook%2011%5D%20Create%20REST%20Service%20in%20Integration%20S%20a83f4bcce6ee49c0a838556798b4e09c/Untitled%203.png)
        
- getFile 서비스를 사용하여 서버에 위치한 file 데이터를 읽어 서비스를 구성합니다.
    
   ![Untitled](%5BWorkbook%2011%5D%20Create%20REST%20Service%20in%20Integration%20S%20a83f4bcce6ee49c0a838556798b4e09c/Untitled%204.png)
    
   ![Untitled](%5BWorkbook%2011%5D%20Create%20REST%20Service%20in%20Integration%20S%20a83f4bcce6ee49c0a838556798b4e09c/Untitled%205.png)
    

#### STEP 5. 생성 된 REST Resource 를 사용하여 bookInformation_RD 라는 Element Name 으로 REST API Descriptor 를 생성합니다.
    
   ![Untitled](%5BWorkbook%2011%5D%20Create%20REST%20Service%20in%20Integration%20S%20a83f4bcce6ee49c0a838556798b4e09c/Untitled%206.png)
    
- Specification Version 은 Swagger2.0 으로 선택 후 다음, Provider 로 설정하고 생성 된 REST Resource 를 사용한 생성을 선택합니다.
        
  ![Untitled](%5BWorkbook%2011%5D%20Create%20REST%20Service%20in%20Integration%20S%20a83f4bcce6ee49c0a838556798b4e09c/Untitled%207.png)
        
  ![Untitled](%5BWorkbook%2011%5D%20Create%20REST%20Service%20in%20Integration%20S%20a83f4bcce6ee49c0a838556798b4e09c/Untitled%208.png)
        
- REST API 의 Title 명, 사용할 REST Resource 를 선택 후 Finish

![Untitled](%5BWorkbook%2011%5D%20Create%20REST%20Service%20in%20Integration%20S%20a83f4bcce6ee49c0a838556798b4e09c/Untitled%209.png)

![Untitled](%5BWorkbook%2011%5D%20Create%20REST%20Service%20in%20Integration%20S%20a83f4bcce6ee49c0a838556798b4e09c/Untitled%2010.png)

#### STEP 6. REST API 호출 클라이언트인 [Postman 을 다운로드](https://www.postman.com/downloads/) 하여 설치 후, REST API Descriptor 에서 생성 된 정보를 사용하여 API 를 호출합니다.
    
   ![Untitled](%5BWorkbook%2011%5D%20Create%20REST%20Service%20in%20Integration%20S%20a83f4bcce6ee49c0a838556798b4e09c/Untitled%2011.png)
    
   ![Untitled](%5BWorkbook%2011%5D%20Create%20REST%20Service%20in%20Integration%20S%20a83f4bcce6ee49c0a838556798b4e09c/Untitled%2012.png)
    
- URL = [GET] ***http://{Host:Port}***/rad/acme.PurchaseOrder.work.REST:bookInformation_RD/getBook
- Authorization = Basic Auth
        - Username : Administrator
        - Password : manage
- Headers - Content-type : application/json
    
   ![Untitled](%5BWorkbook%2011%5D%20Create%20REST%20Service%20in%20Integration%20S%20a83f4bcce6ee49c0a838556798b4e09c/Untitled%2013.png)
    
#### 참고 STEP Flowservice 내 에서 API 를 호출 시 pub.client:http 서비스를 사용한 호출을 사용합니다.
    
   ![Untitled](%5BWorkbook%2011%5D%20Create%20REST%20Service%20in%20Integration%20S%20a83f4bcce6ee49c0a838556798b4e09c/Untitled%2014.png)
    
- url : ***http://{Host:Port}***/rad/acme.PurchaseOrder.work.REST:bookInformation_RD/getBook
- method : get
- auth/type : basic
- auth/user : Administrator
- auth/pass : manage
- headers/Content-type : application/json


## Check Your Understanding

#### QUIZ 1. HTTP Methods 인 GET, POST, PUT, DELETE 각 작업의 차이점은 무엇입니까?

#### QUIZ 2. book list 는 어디에서 불러옵니까?

#### QUIZ 3.  **pub.client.http** 를 호출할 때 자격 증명을 지정해야 하는 이유는 무엇입니까?
