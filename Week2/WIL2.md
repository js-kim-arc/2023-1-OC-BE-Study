# GDSC 과제연

1.컨트롤러, 서비스, 리포지토리의 역할

Controller란?

Controller은 MVC에서 C에 해당 하며 주로 사용자의 요청을 처리 한 후 지정된 뷰에 모델 객체를 넘겨주는 역할을 합니다.

즉 사용자의 요청이 진입하는 지점이며 요청에 따라 어떤 처리를 할지 결정을 Service에 넘겨줍니다. 그후 Service에서 실질적으로 처리한 내용을 View에게 넘겨줍니다.

Service란?

1. Client가 Request를 보낸다.(Ajax, Axios, fetch등..)
2. Request URL에 알맞은 Controller가 수신 받는다. (@Controller , @RestController)
3. Controller 는 넘어온 요청을 처리하기 위해 Service 를 호출한다.
4. Service는 알맞은 정보를 가공하여 Controller에게 데이터를 넘긴다.
5. Controller 는 Service 의 결과물을 Client 에게 전달해준다.

Service가 알맞은 정보를 가공하는 과정을 '비즈니스 로직을 수행한다.' 라고 합니다.Service가 비즈니스 로직을 수행하고 데이터베이스에 접근하는 DAO를 이용해서 결과값을 받아 옵니다.

→일반적으로 리포지토리와 비교했을 때 비즈니스적인 이름을 많이 사용한다.

Repository

Entity에 의해 생성된 DB에 접근하는 메서드 들을 사용하기 위한 인터페이스입니다.

쉽게 말해 DB 연결, 해제, 자원을 관리하고 CRUD 작업을 처리한다.

→ 데이터베이스에 가장 근접해 있다.

1. TDD란?

test driven development -테스트 주도 개발

main 함수를 따로 만들어서 컴파일러로 실행을 해서 에러를 찾는 것이 아닌 테스트 코드를 짜서 바로 바로 에러 유무를 확인할 수 있게 해주는 시스템이다.

왜 하는가?→ 

1. 기능에 집중을 할 수 있다.

코드 구현→ 서버 실행 → 수동 입력→ 실행→ 에러→ 에러 분석→ 해결 테스트를 작성하지 않고 하면 이렇게 많은 시간을 투자해서 에러를 알아내야 하지만

테스트 코드를 작성하게 되면 불필요한 시간들을 생략할 수 있게 된다.

1. 작성한 코드만 필요함

db연동, 서버 연결없이 테스트가 가능하다. 

```jsx
@Test
    void 회원가입() {
        //given
        Member member=new Member();
        member.setName("hello");
        //when
        Long saveId=memberService.join(member);
        //then
        Member findMember=memberService.findOne(saveId).get();
        Assertions.assertThat(member.getName()).isEqualTo(findMember.getName())

    }
```

```jsx
public Long join(Member member){
        validateDuplicateMember(member);
        memberRepository.save(member);
        return member.getId();
    }
```

이런 식으로 바로 바로 테스트 할 수 있다.