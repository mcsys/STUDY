# In-App Purchase 정리

### In-App 기능 활성화

최근 프로젝트에 인앱 구매 기능을 넣고 추후에 까먹을까봐 정리를 하려고한다.

먼저 인앱 기능을 넣고 싶은 프로젝트를 실행해서 Target > Capabillities 속성으로 이동한다.

OFF > ON으로 변경하면 이제부터 이 프로젝트에서는 인앱을 사용할 수 있다.

![Project-Capabillities](../Resource/Project-Capabillities.png)

<br />

그리고 애플 개발자 사이트에서 Certificates, Identifiers & Profiles로 이동한다.

좌측 메뉴에서 Identifiers > App IDs에서 현재 인앱을 ON시킨 프로젝트의 번들 아이디 값과 동일한

App IDs를 가진 프로젝트의 정보를 확인한다.

해당 프로젝트의 In-App Purchase 항목이 Enable로 되어 있으면 기본 설정은 끝났다.

![In-App Purchase Enable](../Resource/In-App Purchase Enable.png)













### In-App Source 구현



* itunesconnect
  * 사용자 및 역할
    * Sandbox 테스터





