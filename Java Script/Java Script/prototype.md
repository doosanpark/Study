# prototype

## prototype이란?

JavaScript는 **프로토타입 기반 언어(prototype-based language)**라 불린다. 모든 객체들이 메소드와 속성들을 상속 받기 위한 템플릿으로써 **프로토타입 객체(prototype object)**를 가진다는 의미다. 프로토타입 객체도 또 다시 상위 프로토타입 객체로부터 메소드와 속성을 상속 받을 수 있고 그 상위 프로토타입 객체도 마찬가지이기에 이를 **프로토타입 체인(prototype chain)**이라 부른다. 

엄밀히 말해 상속되는 속성과 메소드들은 **객체의 생성자의 prototype**이라는 속성에 정의되어 있다.

JavaScript에서는 객체 인스턴스와 프로토타입 간에 연결이 구성되며 이 연결을 따라 **프로토타입 체인을 타고 올라가며 속성과 메소드를 탐색**한다.

다음 코드를 보면 o.ultraProp에 관여한 Sub라는 함수와 Super라는 함수에는 ultraProp이라는 속성이 없는 것을 볼 수 있다. 이 ultraProp은 Ultra 함수에 들어 있다. Sub는 Super을 상속받고, Super는 Ultra를 상속받는다. Sub에 접근했을 때 이 ultraProp이 없는 것을 확인하면 JS는 부모 함수인 Super에 접근한다. 그리고 이와 같은 과정을 다시 진행해서 Ultra 함수까지 접근할 수 있게 되는 것이다.

```jsx
function Ultra(){}
Ultra.prototype.ultraProp = true;
 
function Super(){}
Super.prototype = new Ultra();
 
function Sub(){}
Sub.prototype = new Super();
 
var o = new Sub();
console.log(o.ultraProp);  //true 출력
```

### 생성자

생성자는 기본적으로 함수다.

var o = new Sub()와 같이 new를 붙였을 경우 함수는 생성자라는 함수가 된다. 이렇게 해서 실행된 결과는 새로운 객체를 만들어서 o라는 변수에 객체가 들어간다. 이게 생성자의 역할이다. 이렇게 했을 때 변수 o에는 얻고자 하는 객체의 속성들까지 획득 가능하다.