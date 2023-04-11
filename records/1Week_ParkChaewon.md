## Title: [1Week] 박채원

### 미션 요구사항 분석 & 체크리스트

---
[ ] 1. 삭제 기능 구현 
- [x] 삭제 기능 테스트 케이스
- [x] 해당 항목에 대한 소유권이 본인(로그인한 사람)에게 있는지 체크
- [x] 삭제 후, 다시 호감목록 페이지로 돌아오기
- [x] rq.redirectWithMsg 함수 사용

### N주차 미션 요약

---

호감목록 페이지에서 특정 항목에서 삭제버튼을 누르면, 해당 항목은 삭제되어야 한다.

**[접근 방법]**

**1.LikeablePersonControllerTests.java**

  - @Secured("user3") : Spring Security 어노테이션을 사용하여 해당 요청에 대한 인가를 수행하기 위해
  - .andExpect(redirectedUrl("/likeablePerson/list**")); : 리다이렉션 URL이 /likeablePerson/list로 시작해야하는지를 검증하기 위함

  - 테스트 코드 작성 시 참고 자료 : https://codecrafting.tistory.com/2


**2. LikeablePersonController.java**

전체적인 프로세스
  - @PreAuthorize 어노테이션 : 인증된 사용자만 접근 가능하도록 설정한 컨트롤러 메소드
  - @GetMapping("/delete/{id}") : GET 요청에 대한 매핑을 수행하고, {id} 경로 변수를 통해 삭제할 호감상대의 id를 전달받습니다.

  - likeablePersonService.deleteLikeablePerson(id, rq.getMember().getInstaMember()) : 해당 id에 대한 호감상대를 삭제

  - 삭제가 실패할 경우 : rq.historyBack(deleteRsData)를 호출하여 이전 페이지로 이동
  - 삭제가 성공한 경우 : rq.redirectWithMsg("/likeablePerson/list", deleteRsData)를 호출하여 호감목록으로 이동하고, 성공 메시지를 전달

  - 코드 작성 시 참고 자료 : 점프 투 스프링부트, 구글링

**3. LikeablePersonService.java**

호감상대(LikeablePerson)를 삭제하고 조회하는 기능을 구현한 메소드입니다.

전체적인 프로세스
  - deleteLikeablePerson(): 주어진 id와 instaMember를 이용하여, 해당하는 LikeablePerson을 삭제하는 메소드
  - getLikeablePerson(id): 주어진 id를 이용하여, 해당하는 LikeablePerson을 조회하는 메소드를 호출합니다. RsData(반환 결과)에서 LikeablePerson(호감상대)을 가져옵니다.
  - 해당 유저가 호감 상대를 삭제할 권한이 있는지 확인하는 기능을 구현하기 위해  'IF문을 사용하여 F-1 에러 코드를 가진 RsData를 반환'하였습니다.
  - 인자로 받은 instaMember와, 조회된 LikeablePerson의 fromInstaMember(호감상대의 작성자)를 비교하여, 삭제 권한이 없으면 실패 결과(RsData)를 반환합니다.
  - 인자로 받은 LikeablePerson을 삭제하고, 삭제된 LikeablePerson을 포함한 성공 결과(RsData)를 반환합니다.

  - getLikeablePerson(): 주어진 id를 이용하여, 해당하는 LikeablePerson을 조회하는 메소드입니다.
  - likeablePersonRepository.findById(id): 주어진 id를 이용하여, LikeablePerson을 데이터베이스에서 조회합니다.
  - 조회된 결과가 없으면, 실패 결과(RsData)를 반환합니다.
  - 조회된 결과가 있으면, 성공 결과(RsData)를 반환합니다. 이 때, 데이터로 조회된 LikeablePerson 객체를 포함합니다.

  - 코드 작성 시 참고 자료 : 점프 투 스프링부트, 구글링

**[특이사항]**

구현 과정에서 아쉬웠던 점 : rq에 대해 조금 더 공부가 필요할 것 같습니다.

궁금했던 점 : 기능 구현은 되는데, 테스트케이스 실행에서 계속 오류가 발생합니다. 
             그 이유를 모르겠어서 추후 리팩토링 시 해결해보겠습니다.

[ ] 리팩토링 : 테스트케이스 오류 해결




 