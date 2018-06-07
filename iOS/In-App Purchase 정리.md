# In-App Purchase 정리

### In-App 기능 활성화

최근 프로젝트에 인앱 구매 기능을 넣고 추후에 까먹을까봐 정리를 하려고한다.

먼저 인앱 기능을 넣고 싶은 프로젝트를 실행해서 Target > Capabillities 속성으로 이동한다.

OFF > ON으로 변경하면 이제부터 이 프로젝트에서는 인앱을 사용할 수 있다.

![Project-Capabillities](../Resource/Project-Capabillities.png)





그리고 애플 개발자 사이트에서 Certificates, Identifiers & Profiles로 이동한다.

좌측 메뉴에서 Identifiers > App IDs에서 현재 인앱을 ON시킨 프로젝트의 번들 아이디 값과 동일한

App IDs를 가진 프로젝트의 정보를 확인한다.

해당 프로젝트의 In-App Purchase 항목이 Enable로 되어 있으면 기본 설정은 끝났다.

![InAppPurchaseEnable](../Resource/InAppPurchaseEnable.png)







### In-App Source 구현

먼저 인앱을 구현하기 위해서는 StoreKit이라는 iOS SDK를 이용해야 한다.

Target > Build Phases으로 이동해서 StoreKit Framework 라이브러리를 링크 시킨다.

~~~~objc
#import <StoreKit/StoreKit.h>
~~~~





* itunesconnect
  * 사용자 및 역할
    * Sandbox 테스터





