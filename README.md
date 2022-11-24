# ThymeleafStudy2
입력 폼 처리/체크박스/라디오버튼/셀렉트박스

스프링 통합으로 추가되는 기능들<br/>
스프링의 SpringEL 문법 통합<br/>
${@myBean.doSomething()} 처럼 스프링 빈 호출 지원<br/>
편리한 폼 관리를 위한 추가 속성<br/>
th:object (기능 강화, 폼 커맨드 객체 선택)<br/>
th:field , th:errors , th:errorclass<br/>
폼 컴포넌트 기능<br/>
checkbox, radio button, List 등을 편리하게 사용할 수 있는 기능 지원<br/>
스프링의 메시지, 국제화 기능의 편리한 통합<br/>
스프링의 검증, 오류 처리 통합<br/>
스프링의 변환 서비스 통합(ConversionService)<br/>
<br/><br/>
th:object : 커맨드 객체를 지정한다.<br/>
*{...} : 선택 변수 식이라고 한다. th:object 에서 선택한 객체에 접근한다.<br/>
th:field<br/>
HTML 태그의 id , name , value 속성을 자동으로 처리해준다.<br/>
렌더링 전<br/>
<input type="text" th:field="*{itemName}" /><br/>
렌더링 후<br/>
<input type="text" id="itemName" name="itemName" th:value="*{itemName}" /><br/>
<br/><br/>
th:object="${item}" : <form> 에서 사용할 객체를 지정한다. 선택 변수 식( *{...} )을 적용할 수
있다.<br/>
th:field="*{itemName}"<br/>
*{itemName} 는 선택 변수 식을 사용했는데, ${item.itemName} 과 같다. 앞서 th:object 로
item 을 선택했기 때문에 선택 변수 식을 적용할 수 있다.<br/>
th:field 는 id , name , value 속성을 모두 자동으로 만들어준다.<br/>
id : th:field 에서 지정한 변수 이름과 같다. id="itemName"<br/>
name : th:field 에서 지정한 변수 이름과 같다. name="itemName"<br/>
value : th:field 에서 지정한 변수의 값을 사용한다. value=""<br/>
<br/><br/>
HTML checkbox는 선택이 안되면 클라이언트에서 서버로 값 자체를 보내지 않는다.<br/> 수정의 경우에는
상황에 따라서 이 방식이 문제가 될 수 있다.<br/> 사용자가 의도적으로 체크되어 있던 값을 체크를 해제해도
저장시 아무 값도 넘어가지 않기 때문에, 서버 구현에 따라서 값이 오지 않은 것으로 판단해서 값을 변경하지
않을 수도 있다.<br/>
이런 문제를 해결하기 위해서 스프링 MVC는 약간의 트릭을 사용하는데, 히든 필드를 하나 만들어서,
_open 처럼 기존 체크 박스 이름 앞에 언더스코어( _ )를 붙여서 전송하면 체크를 해제했다고 인식할 수
있다. 히든 필드는 항상 전송된다.<br/> 따라서 체크를 해제한 경우 여기에서 open 은 전송되지 않고, _open 만
전송되는데, 이 경우 스프링 MVC는 체크를 해제했다고 판단한다.<br/>
체크 해제를 인식하기 위한 히든 필드<br/>
<input type="hidden" name="_open" value="on"/><br/>
<br/><br/>
@ModelAttribute의 특별한 사용법<br/>
등록 폼, 상세화면, 수정 폼에서 모두 서울, 부산, 제주라는 체크 박스를 반복해서 보여주어야 한다.<br/> 이렇게
하려면 각각의 컨트롤러에서 model.addAttribute(...) 을 사용해서 체크 박스를 구성하는 데이터를
반복해서 넣어주어야 한다.<br/>
@ModelAttribute 는 이렇게 컨트롤러에 있는 별도의 메서드에 적용할 수 있다.<br/>
이렇게하면 해당 컨트롤러를 요청할 때 regions 에서 반환한 값이 자동으로 모델( model )에 담기게 된다.<br/>
물론 이렇게 사용하지 않고, 각각의 컨트롤러 메서드에서 모델에 직접 데이터를 담아서 처리해도 된다.<br/>
<br/><br/>
HTML의 id 가 타임리프에 의해 동적으로 만들어지기 때문에 <label for="id 값"> 으로 label 의
대상이 되는 id 값을 임의로 지정하는 것은 곤란하다.<br/> 타임리프는 ids.prev(...) , ids.next(...) 을
제공해서 동적으로 생성되는 id 값을 사용할 수 있도록 한다.<br/>
