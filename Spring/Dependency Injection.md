## Spring MVC

---


### Spring에서 가장 핵심 이라고 생각하는 것은 의존성 주입 DI이다.

![의존성주입.png](img%2F%EC%9D%98%EC%A1%B4%EC%84%B1%EC%A3%BC%EC%9E%85.png)

저는 이 사진이 DI를 이해하는데 가장 큰 도움이 되었던 것 같습니다.       
위 그림같이 메인 모듈이 직접 의존성을 주는것 보다는  중간에 의존성 주입자가 간접적으로 의존성을 주입하는 것이 메인모듈이 하위모듈에 대한 의존성이 떨어지게 됩니다. 참고로 이를 “디커플링” 이라고도 합니다

---

### Spring MVC 흐름과 의존 관계

Spring MVC 흐름과 의존 관계를코드로 예를 들어 보겠습니다.

### 1. Dao 추상화 레이어 정의.       
![CalendarDao.png](img%2FCalendarDao.png)
### 2. Dao 구현체를 만든다.
![CalendarDaoImpl.png](img%2FCalendarDaoImpl.png)
### 3. Service 추상화 레이어 정의.
![CalendarService.png](img%2FCalendarService.png)
### 4. Service 구현체를 만든다.
![CalendarServiceImpl.png](img%2FCalendarServiceImpl.png)
### 5. Controller 에서 주입하고 사용.
![CalendarController.png](img%2FCalendarController.png)
