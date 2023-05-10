## Title: [4Week] 박채원

### 미션 요구사항 분석 & 체크리스트

---

 1. 필수 미션 - 내가 받은 호감리스트

- [ ] 내가 받은 호감리스트(/usr/likeablePerson/toList)에서 성별 필터링기능 구현
- [ ] 네이버클라우드플랫폼을 통한 배포, 도메인, HTTPS 까지 적용


  2. 선택 미션

- [ ] 내가 받은 호감리스트(/usr/likeablePerson/toList)에서 호감사유 필터링기능 구현
- [ ] 내가 받은 호감리스트(/usr/likeablePerson/toList)에서 정렬기능
- [ ] 젠킨스를 통해서 리포지터리의 main 브랜치에 커밋 이벤트가 발생하면 자동으로 배포가 진행되도록

### 4주차 미션 요약

---

**[접근 방법]**
호감리스트를 성별에 따라, 호감사유에 따라 필터링하는 기능을 구현

**[접근 방법]**

- 호감사유변경 시에 modifyUnlockDate 갱신

**- 호감리스트에서 성별에 따라 필터링 기능 구현**
  - gender가 null이 아니고 빈 문자열이 아닐 경우, 
    filter() 메서드를 이용하여 likeablePeopleStream 스트림을 gender로 필터링합니다.
  - lp는 likeablePeopleStream 스트림의 요소를 나타내는 매개변수이며, 
    해당 요소에서 FromInstaMember 객체를 가져와 getGender() 메서드로 성별 정보를 가져옵니다. 
  - 그리고 Objects.equals() 메서드를 사용하여 가져온 성별 정보와 gender 변수의 값을 비교합니다. 
    두 값이 동일한 경우에만 filter() 메서드는 true를 반환하고, 
    해당 요소를 likeablePeopleStream 스트림에 유지합니다.
  
**- 호감리스트에서 호감사유에 따라 필터링하는 기능을 구현**
  - attractiveTypeCode가 null이 아니고, gender 변수가 빈 문자열이 아닐 경우,
    filter() 메서드를 이용하여 likeablePeopleStream 스트림을 attractiveTypeCode로 필터링합니다. 
  - lp는 likeablePeopleStream 스트림의 요소를 나타내는 매개변수이며, 
    해당 요소에서 getAttractiveTypeCode() 메서드로 호감사유 코드를 가져옵니다. 
  - 그리고 Integer.parseInt() 메서드를 사용하여 attractiveTypeCode를 정수형으로 변환한 후, 
    가져온 호감사유 코드와 비교합니다. 두 값이 동일한 경우에만 filter() 메서드는 true를 반환하고, 
    해당 요소를 likeablePeopleStream 스트림에 유지합니다.


**[특이사항]**
- toList 에서 구현하는 것을 아직 못하였습니다.
- 코드 오류가 떠서 리팩토링 시 수정하겠습니다.