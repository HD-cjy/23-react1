
<!-- 각 주차마다 새로운 수업 시작할때는 h2파일로 -->
<h2>최진용 10주차 05월11일(결석주차_실습코드만 했다고 함.) </h2>
#섭씨온도 화씨온도 표현

```react
const scaleNames = {
  c: "섭씨",
  f: "화씨",
};

function CtempFtemp(props){
  const handleChange = (event) => {
    props.onTemperatureChange(event.target.value);
  };

  return(
    <fieldset>
      <legend>
        온도를 입력해주세요(단위:{scaleNames[props.scale]});
      </legend>
      <input value={props.temperature} onChange={handleChange}/>
    </fieldset>
  );
}

export default CtempFtemp;
```


#물이 끓는가?
``` react
import React, {useState} from "react";
import TemperatureInput from "./TemperatureInput";

function BoilingVerdict(props){
  if(props.celsius >= 100){
    return <p>물이 끓습니다.</p>
  }
  return <p>물이 끓지 않습니다.</p>
}

function toCelsius(fahrenheit){
  return ((fahrenheit - 32) * 5) / 9;
}

function toFahrenheit(celsius){
  return (celsius * 9) / 5 + 32;
}

function tryConvert(temperature, convert){
  const input = parseInt(temperature);
  if(Number.isNaN(input)){
    return "";
  }
  const output = convert(input);
  const rounded = Math.round(output * 1000) / 1000;
  return rounded.toString();
}

function Calculator(props){
  const [temperature, setTemperature] = useState("");
  const [scale, setScale] = useState("c");

  const handleCelsiusChange = (temperature) => {
    setTemperature(temperature);
    setScale("c");
  };
  const handleFahrenheitChange = (temperature) => {
    setTemperature(temperature);
    setScale("f");
  };

  const celsius = scale === "f" ? tryConvert(temperature, toCelsius) : temperature;
  const fahrenheit = scale === "c" ? tryConvert(temperature, toFahrenheit) : temperature;

  return(
    <div>
      <TemperatureInput
        scale="c"
        temperature={celsius}
        onTemperatureChange={handleCelsiusChange}
      />
      <TemperatureInput
        scale="f"
        temperature={fahrenheit}
        onTemperatureChange={handleFahrenheitChange}
      />
      <BoilingVerdict celsius={parseFloat(celsius)}/>
    </div>
  );
}

export default Calculator;

```
<h2>최진용 10주차 05월04일 </h2>
실습 내용정리 
<ol>
<li>사용자 정보 입력받기.</li>
<li>받아온 정보(출석부) 출력.</li>
<li>Is Boiling? > 물이 끓는지 아닌지 알려주는 컴포넌트 </li>
<li>계산 컴포넌트 변경해보기</li>
</lo>

#Shared State
>shared state는 공유된 state를 의미
>어떤 컴포넌트의 state에 있는 데이터를 여러 하위 컴포넌트에서 공통적으로 사용하는 경우<br>
>하위 컴포넌트가 공통된 부모 컴포넌트의 state를 공유하여 사용하는 것을 shared state<br>
#폼이란? 
>폼은 일반적으로 사용자로부터 입력을 받기위한 양식에서 사용<br>

#폼 : Input Null Value
>value prop은 넣되 자유롭게 입력할 수 있도록 만들고 싶으면 값이 undefined 또는 null을 넣는다<br>
>제어 컴포넌트에 value prop을 정해진 값으로 넣으면 코드를 수정하지 않는 한 입력값 변경 불가능<br>
>여러개 입력하기.  
>>하나의 컴포넌트에서 여러개의 입력을 다루기 위해서는 여러 개의 state를 선언
#제어 컴포넌트
>제어 컴포넌트는 사용자가 입력한 값에 접근하고 제어할 수 있도록 해주는 컴포넌트<br>

#리스트와 키
>리스트에서는 키는 "리스트에서 아이템을 구별하기 위한 고유한 문자열" 이다. <br>
>이 키는 리스트에서 어떤 아이템을 변경, 추가 또는 제거되었는지 구분하기 위해 사용<br>
>키는 같은 리스트에 있는 엘리먼트 사이에서만 고유한 값이면 OK.<br>
>키값으로 인덱스를 사용하는 방법도 있음
인덱스 값도 고유한 값이기 때문에 키 값으로 사용해도 OK <em>BUT</em>배열에서 아이템의 순서가 바뀔 수 있어 키값을 인덱스에 사용하는 것을 권장하지 않음.<br>
>리액트에서는 키를 명시적으로 넣어 주지 않으면 기본적으로 인덱스 값을 키의 값으로 사용<br>

>HTML 폼-> 자체적으로 state를 관리<br>
>제어 컴포넌트 -> 모든 데이터를 state에서 관리<br>


#태그 정리
<ul>
	<li>File input :값이 읽기 전용임.리액트에선 비제어 컴포넌트
</li>
	<li>select :textarea와 비슷함,목록에서 다중으로 선택이 되도록 하려면 multiple속성 값을 true로 변경</li>
	<li> textarea : HTML에서는 textarea의 children으로 텍스트가 들어감.state를 통해 벨류의 attribute 변경하여 텍스트 표시 
	</li> 

</ul>

#제어 컴포넌트
>제어 컴포넌트는 사용자가 입력한 값에 접근하고 제어할 수 있도록 해주는 컴포넌트
<br>
>HTML 폼-> 자체적으로 state를 관리
<br>
>제어 컴포넌트 -> 모든 데이터를 state에서 관리
<h2>최진용 8주차 20일 시험// 27일 수업 </h2>
#이벤트 핸들링

>Dom 클릭 이벤트 처리, React 클릭 이벤트 처리가 있음
>React 클릭 이벤트는 이벤트의 이름이 onclick에서 onClick으로 변경
>React 클릭 이벤트는 젼댤하려는 함수는 문자열에서 함수 그대로 전달한다.

>이벤트 헨들러 추가 방법
>>버튼 클릭 시 이벤트 헨들러 함수인 handleClick()호출
>>bind 미사용시 this.handleClick은 클로벌 스코프에서 호출되어, undefined로 사용불가 하기 때문
>>bind 미사용 시 화살표 함수를 사용하여도 된다.(거의 사용하지는 않음)

>인라인 if-else
>>삼항 연산자를 사용한다.
>>문자열이나 엘리먼트를 넣어서 사용할 수도 있다.

>인라인 if-else
>>삼항 연산자를 사용한다.
>>문자열이나 엘리먼트를 넣어서 사용할 수도 있다.


>클래스형을 함수형으로 바꾸려면
>>함수 안에 함수로 정의
>>arrow function을 사용하여 정의
>>함수형에서는 this를 사용하지 않고, onClick에서 바로 HandleClick을 넘기면 된다.

>Arguments 전달하기
>>함수를 정의할 때는 파라미터(매개변수) 혹은 아귀먼트(인자) 라고 부른다.
>>이벤트 헨들러에 매개변수를 전달해야 하는 경우도 많다.
>>event라는 매개변수는 리액트의 이벤트 객체를 의미한다

<h2>최진용 7주차 4.13</h2>
리액트의 state와 생명주기 기능에 갈고리를 걸어 원하는 시점에 정해진 함수를 실행되도록 만든 것<br>

#훅이란?
>기존 함수 컴포넌트는 클래스 컴포넌트와는 다르게 코드도 간결함<br>
>클래스형 컴포넌트는 생성자에서 state를 정의하고, setState()함수를 통해 state를 업데이트 함<br>
>함수형 컴포넌트에서 state너 생명주기 함수의 기능을 사용하게 해주기 위해 추가됨.<br>

#useState()
>state를 사용하기 위한 훅<br>
>함수 컴포넌트에서는 기본적으로 state라는 것을 제공하지 않음<br>
>클래스 컴포넌트처럼 state를 사용하고 싶으면 useState() 훅을 사용해야함<br>
>>사용법<br>
>>const [변수명, set함수명] = useState (초깃값);<br>
>>변수 각각에 대해 set 함수가 따로 존재함<br>

#useEffect()
>정의:사이드 이펙트를 수행하기 위한 훅<br>
>사이드 이펙트란 서버에서 데이터를 받아오거나 수동으로 DOM을 변경하는 등의 작업<br>
>useEffect() 훅만으로 클래스 컴포넌트의 생명주기 함수들과 동일한 기능을 수행할 수 있음<br>
>>사용법<br>
>>useEffect(이펙트 함수, 의존성 배열);<br>
>>의존성 배열 안에 있는 변수 중에 하나라도 값이 변경되었을 때 이펙트 함수가 실행됨<br>
>>의존성 배열에 빈 배열([])을 넣으면 언마운트시에 단 한 번씩만 실행됨<br>
>>의존성 배열 생략 시 컴포넌트가 업데이트될 때마다 호출됨<br>
>>선언된 컴포넌트의 props와 state에 접근할 수 있음<br>
>>useEffect()에서 리턴하는 함수는 컴포넌트 마운트가 해제될 때 호출됨<br>

#useMemo()
>정의:Memoized value를 리턴하는 훅<br>
>연산량이 높은 작업이 매번 렌더링될 때마다 반복되는 것을 피하기 위해 사용<br>
>렌더링이 일어나는 동안 실행되므로 렌더링이 일어나는 동안 실행돼서는 안될 작업을 useMemo()에 넣으면 안 됨<br>
>>사용법<br>
>>const memoizedValue = useMemo(값 생성 함수, 의존성 배열);<br>
>>의존성 배열에 들어있는 변수가 변했을 경우에만 새로 값 생성 함수를 호출하여 결괏값을 반환함<br>
>>그렇지 않은 경우에는 기존 함수의 결괏값을 그대로 반환함<br>
>>의존성 배열을 넣지 않을 경우 렌더링이 일어날 때마다 매번 값 생성 함수가 실행되므로 의미가 없음<br>

#useCallback()
>정의:useMemo() 훅과 유사하지만 값이 아닌 함수를 반환한다는 점이 다름
>useCallback(콜백 함수, 의존성 배열);은 useMemo(() => 콜백 함수, 의존성 배열);과 동일 훅을 사용하여 불필요한 함수 재정의 작업을 없애는 것<br>
>>사용법<br>
>>const memoizedCallback = useCallback(콜백 함수, 의존성 배열);<br>
>>의존성 배열에 들어있는 변수가 변했을 경우에만 콜백 함수를 다시 정의해서 리턴함.<br>

#useRef()
>정의:레퍼런스를 사용하기 위한 훅<br>
>레퍼런스란 특정 컴포넌트에 접근할 수 있는 객체를 의미<br>
>매번 렌더링될 때마다 항상 같은 레퍼런스 객체를 반환<br>

>>사용법
>>const refContainer = useRef(초기값);<br>
>>current라는 속성을 통해서 접근<br>


#훅의 규칙
<li>무조건 최상위 레벨에서만 호출해야함</li>
<li>반복문이나 조건문 또는 중첩된 함수들 안에서 훅을 호출하면 안 됨</li>
<li>컴포넌트가 렌더링될 때마다 매번 같은 순서로 호출되어야 함</li>
<li>리액트 함수 컴포넌트에서만 훅을 호출해야 함</li>
<li>혹은 리액트 함수 컴포넌트에서 호출하거나 직접 만든 커스텀 훅에서만 호출할 수 있음</li><br>

#커스텀 훅
>이름이 use로 시작하고 내부에서 다른 훅을 호출하는 단순한 자바스크립트 함수.<br>
>파라미터로 무엇을 받을지, 어떤 것을 리턴해야 할지를 개발자가 직접 정할 수 있음.<br>
>중복되는 로직을 커스텀 훅으로 추출하여 재사용성을 높임<br>
>이름이 use로 시작하지 않으면 특정 함수의 내부에서 훅을 호출하는지를 알 수 없기 때문에 훅의 규칙 위반 여부를 자동으로 확인할 수 없음.<br>


<h2>최진용 6주차 4.6 </h2>
리액트 6주차

실습내용:
<br>추출과 실습에 이미지를 넣기, State에 대한 이해.
<br>댓글 컴포넌트 만들기
컴포넌트 추출<br>
>큰 컴포넌트에서 일부를 추출해서 새로운 컴포넌트를 만드는 것<br>
>기능 단위로 구분하는 것이 좋고, 나중에 곧바로 재사용이 가능한 형태로 추출하는 것이 좋음<br>

#State란?<br>
>리액트 컴포넌트의 변경 가능한 데이터<br>
>state가 변경될 경우 컴포넌트가 다시 렌더링됨<br>
>컴포넌트를 개발하는 개발자가 직접 정의해서 사용<br>
>렌더링이나 데이터 흐름에 사용되는 값만 state에 포함시켜야 함<br>
>State의 특징<br>
>>직접적인 변경이 불가능 함.(set 함수 사용하여 변경)<br>
>>자바스크립트 객체로 존재함.<br>

#클래스 컴포넌트<br>
>>생성자에서 모든 state를 한 번에 정의<br>
>>state를 변경하고자 할 때에는 꼭 setState()함수를 사용해야 함<br>

#함수 컴포넌트<br>
>useState()훅을 사용하여 각각의 state를 정의<br>
>각 state별로 주어지는 set함수를 사용하여 state 값을 변경<br>
>컴포넌트는 계속 존재하는 것이 아니라,시간의 흐름에 따라 생성,업데이트,소멸 반복<br>

#생명주기
>마운트<br>
>>componentDidMount()<br>
>>컴포넌트가 생성될 때<br>
>업데이트<br>
>>컴포넌트의 props가 변경시 업데이트<br>
>>setState() 함수 호출에 의해 state가 변경시 업데이트<br>
>언마운트<br>
>>componentWillUnmount()<br>
>>상위 컴포넌트에서 현재 컴포넌트를 덮을 때<br>
>컴포넌트는 생성,업데이트,소멸의 과정을 반복함.<br>

<h2>최진용 5주차 3.30 </h2>
리액트 5주차
DOM엘리먼트의 정의
엘리먼트는 리액트 앱을 구성하는 요소를 의미 
	ㄴ 엘리먼트는 리액트 앱의 가장 작은 블록들 
DOM엘리먼트이며 html요소를 뜻함

Virtual DOM의 엘리먼트 특징
리액트는 Virtual DOM의 형태를 가지고있으므
DOM 엘리먼트는 웹의 모든 정보를 들고 있어 무거움 ( 동기식에 유리 ) 



DOM 장 단점 
DOM은 트리 구조로 되어 있어서 이해하기 쉽지만, 
노드의 수가 많아질 수록 속도가 느려지고, 
DOM 업데이트에 잦은 오류를 발생시킬 수 있다.

| DOM vs VirtualDom| DOM 	| Virtual DOM   | 
| ------------- | ------------- | ------------- | 
| 업데이트	| 느리다	| 빠르다	|
|새로운 element 업데이트 방식|새로운 element가 업데이트된 경우 새로운 DOM 생성	 | 
| 메모리	| 메모리 낭비가 심함| 메모리 낭비가 덜함| 

#props의 특징.
>- 프로퍼티, props(properties의 줄임말) 라고 한다.
 >- 상위 컴포넌트가 하위 컴포넌트에 값을 전달할때 사용한다.
 >(단방향데이터흐름갖는다.)
 >- 프로퍼티는 수정할 수 없다는 특징이 있다.(자식입장에선 읽기 전용데이터이다.)
#pure 함수와 impure함수
>순수 함수(pure function)이란 함수형 프로그래밍에서 사용되는 언어로 함수가  
>수행하는 기능 외에 다른 효과가 나타나지 않는 것을 의미(부작용이 없다)합니다.  
>순수 함수가 아니고 기능 외에 다른 효과가 나타나는 함수를 불순 함수(impure  
>function)이라고 부릅니다.


<p>
<h2>최진용 4주차 3.23 </h2>
<p>
깃 레파지토리 재설정
<ol>
<li>README.md 백업</li>
<li>local에 있는 저장소 이름 바꾸기/삭제</li>
<li>새 프로젝트 생성(23-React1)</li>
<li>README.md 덮어쓰기</li>
<li>GitHub 저장소 삭제</li>
<li>로컬에서 23-React1 push</li>
<li>GitHub 저장소 확인</li>
</ol>

<br>명령어 정리 모음<br>
<ol>

<li>git init</li>
<li>git remote add origin https://github.com/HD-cjy/23-react1.git</li>
<li>git add .</li>
<li>git commit -m "test(코멘트 내용)"</li>
<li>git branch -M main </li>
<li>git push origin main</li>
----- 깃허브 초기화 후 폴더 연결.</li>
React 변수 선언 및 기초 문법</li>
	<!-- const element = <h1>hello,world</h1>    -->
		\{
		장단점:for문을 사용가능하여 작성 가능<br>
		React 는 UI를 구현하는 라이브러리<br>
		세계적으로 가장 관심도가 높고 웹 앱, <br>
		네이티브 모바일 앱 , 데스크톱 앱 등 <br>
		다양한 플랫폼에서 앱을 제작하는 공통 된<br>
		핵심 개발 방법을 제공합니다.<br>
		\}<br>
		xml에서단일태그 문법 사용시  \[<img>,<br>\] 등의 문법은 <img/> 라고 작성 해줘야 함.
</p>


<h2>최진용 3주차 3.16 </h2> 
<br>
리액트란?<br> 
사용자 인터페이스를 만들기 위한 자바스크립트 라이브러리<br>
<br>
리액트의 장점<br>
-동기식과 비동기식<br>
-DOM과 가상 DOM<br>
-컴포넌트 기반 구조<br>
-재사용성<br>

리액트의 단점<br>
-방대한 학습량<br>
-높은 상태 관리 복잡도<br>


1. 구글에 node 검색 후 https://nodejs.org 에 들어가 LTS버전 설치
2. cmd에 node -v 혹은 node --version으로 설치가 완료되었는지 확인<br>
(내 노트북에서의 유효명령어는 node -v ) 이다 . <br>
타 프로그램에서도 버전 확인 명령어 -v --version 를 사용하여 확인가능<br>
NPM의 정의<br>
Node Package Manager의 줄임말<br>
노드js에서 사용하는 패키지를 다운받을 수 있도록 해주는 프로그램<br>
( nodejs설치시 자동설치 )<br>
NPX의 정의<br>
Node Package Runner의 줄임말<br>
npm 5.2.0 버전부터 자동설치 프로그램,<br>
패키지를 설치하지않고 1회성 테스트로 실행 할 수 있게 해준다.<br> 
npm , yarn 등 글로벌 패키지를 설치하지 않고 사용가능.<br>
</P>


# 1주차 리액트 수업 03/09
0309 edit.
edit after class > Can I svae this ment?//

깃허브 쉘 명령어 정리
i)git -v
ii)git --version
iii)깃허브 레파지토리 클론하기: git clone <깃허브주소>

JS문법(js특이한 문법)
let a = 1   <정수 1
let b ='1'  <캐릭터 1 ( 문자1 ) 
a == b : TRUE가 나옴 
but 
a===b : false ( 자료형까지 판별하는 식별자 "===" 가 존재)
consol.log는 개발단계에서 확인용으로 자주 사용함.
개발 완료후 확인은 웹페이지 f12>consol창에서 확인.

commit comment는 50byte가 원칙( 통상적,한글 약 25자.) 
JAVA SCRIPT OBJECT NOTION의 줄임말 > JSON 
스크립트에서 KEY값과 KEY VALUE있는 스타일의 자료형을 가장 많이 사용하고 대중적임

패키지 메니저의 중요성> 어떤 프로그램을 깔았는지, 앱에 적용 되어야 할 부분이 어떤 부분인지 확인하기 위해서

commit의 이유 > 지금까지 했었던 작업을 잊지 않기 위해 ( 개발자 기준으로는 이것이 버전.)  
				 어떤시점에서 어느 파일을 adding했는가를 확인 하기 위해서 commit함.
commit작성 예시(나중에 찾아보세요... (커밋에 자주쓰는 뭐, 커밋작성법 )
간단한 요약으로 정리(엔터)
엔터 이후에는 글자수 제한없이 쭉 작성해줘도 괜찮다. ( 자주 커밋하는게 좋다) 

git저장소 :: remote<원격에있는 저장소 
로컬저장소 :: local<내 컴에 있는 저장소 
패키지 설치법 (2가지 있음., 하나는 통상적)
