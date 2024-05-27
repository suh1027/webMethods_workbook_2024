# [Workbook 1] Packages and Folders

**※ Overview**

이 연습에서는 향후 연습에서 수행할 Integration Server 개발 작업을 저장할 package 및 folders 를 만듭니다.

---

**※ Steps**

개발을 시작하기 위해서는 향후 개발 작업을 보관할 package 및 folder 조직이 필요합니다.

1. Software AG Designer 를 열고 기본 workspace을 유지한 다음 Use this as the default and do not ask again 옆의 상자를 선택합니다.

![Untitled](%5BWorkbook%201%5D%20Packages%20and%20Folders%20a9de6bc1f42049a79e829dda34f176e7/Untitled.png)

1. 서버 연결을 위해 Package Navigator 우측 상단에서 Add or modifiy Integration Severs를 선택 후 연결 정보를 입력합니다. 

![Untitled](%5BWorkbook%201%5D%20Packages%20and%20Folders%20a9de6bc1f42049a79e829dda34f176e7/167b22ea-9c09-4378-bb90-dc947074fcd2.png)

![Untitled](%5BWorkbook%201%5D%20Packages%20and%20Folders%20a9de6bc1f42049a79e829dda34f176e7/Untitled%201.png)

접속정보 

Host: 192.168.1.100

Port:5555

User : SJH(이니셜)

Password: SJH(이니셜)

1. Designer에서 기본 시작 화면을 표시하는 경우

![Untitled](%5BWorkbook%201%5D%20Packages%20and%20Folders%20a9de6bc1f42049a79e829dda34f176e7/Untitled%202.png)

![Untitled](%5BWorkbook%201%5D%20Packages%20and%20Folders%20a9de6bc1f42049a79e829dda34f176e7/Untitled%203.png)

1. 본 연습에서는 실습자 본인의 소속회사+이니셜을 사용하여 New package를 만듭니다. (ex. CUDO_SJH) 패키지는 Package Navigator 에서 우클릭 New > Package 를 클릭하여 생성 할 수 있습니다.

![Untitled](%5BWorkbook%201%5D%20Packages%20and%20Folders%20a9de6bc1f42049a79e829dda34f176e7/Untitled%204.png)

![Untitled](%5BWorkbook%201%5D%20Packages%20and%20Folders%20a9de6bc1f42049a79e829dda34f176e7/Untitled%205.png)

    **Note.** Package 와 Folder의 네이밍 룰은 고객사 별로 상이하게 관리하며, 일반적으로 IFID을 포함하여 생성합니다. (ex. {IFID)_{소스시스템명}_{타겟시스템명} )   

1. 생성 된 package에서 “소속 + 이니셜” 동일한 명칭의 Folder를 만듭니다.

![Untitled](%5BWorkbook%201%5D%20Packages%20and%20Folders%20a9de6bc1f42049a79e829dda34f176e7/Untitled%206.png)

![Untitled](%5BWorkbook%201%5D%20Packages%20and%20Folders%20a9de6bc1f42049a79e829dda34f176e7/Untitled%207.png)

**Note.** Integration Server 는 Folder 구조에 의해 컴포넌트들이 고유하게 식별되므로 Package 바로 하위 폴더는 Package 명과 동일하게 구성할 것을 권장 드립니다. (Namespace 충돌 방지)

1. 생성 된 하위폴더에서 IF0001이라는 폴더를 만듭니다.
2. IF0001폴더에서는 다음과 같은 6개의 폴더를 생성합니다.
    1. adpt (Adapter Service용 폴더)
    2. docs (Document Type용 폴더)
    3. noti (Notification용 폴더)
    4. ws (WebService용 폴더)
    5. api (REST API용 폴더)
    6. svc (Flow Service용 폴더)
    
    ![Untitled](%5BWorkbook%201%5D%20Packages%20and%20Folders%20a9de6bc1f42049a79e829dda34f176e7/Untitled%208.png)
    

    참고: 이 폴더들을 모두 정확한 위치에 놓으려면 매번 **폴더를 생성할 상위 폴더에**  마우스 오른쪽 단추로 클릭하고 **New -> Folder**를 선택합니다. 만약 이름을 잘못 입력한 경우에는 마우스 오른쪽 단추로 클릭하고 **Rename**을 선택합니다.

1. **IF0001.ws** 와 **IF0001.api** 폴더에서는 다음과 같은 하위 폴더 두개를 새로 만듭니다.
    1. **consumer (Consumer 용** **폴더)**
    2. **provider (Provider 용** **폴더)**
    
    ![Untitled](%5BWorkbook%201%5D%20Packages%20and%20Folders%20a9de6bc1f42049a79e829dda34f176e7/Untitled%209.png)
    

**※ Check Your Understanding**

1. 만약 folder을 잘못된 상위 폴더에 배치할 경우, 어떻게 수정할 수 있습니까?
2. 모든 package에서 일관 된 folder 구조가 중요한 이유는 무엇입니까?