# ThymeleafStudy2
입력 폼 처리/체크박스/라디오버튼/셀렉트박스

스프링 통합으로 추가되는 기능들
스프링의 SpringEL 문법 통합
${@myBean.doSomething()} 처럼 스프링 빈 호출 지원
편리한 폼 관리를 위한 추가 속성
th:object (기능 강화, 폼 커맨드 객체 선택)
th:field , th:errors , th:errorclass
폼 컴포넌트 기능
checkbox, radio button, List 등을 편리하게 사용할 수 있는 기능 지원
스프링의 메시지, 국제화 기능의 편리한 통합
스프링의 검증, 오류 처리 통합
스프링의 변환 서비스 통합(ConversionService)

th:object : 커맨드 객체를 지정한다.
*{...} : 선택 변수 식이라고 한다. th:object 에서 선택한 객체에 접근한다.
th:field
HTML 태그의 id , name , value 속성을 자동으로 처리해준다.
렌더링 전
<input type="text" th:field="*{itemName}" />
렌더링 후
<input type="text" id="itemName" name="itemName" th:value="*{itemName}" />

