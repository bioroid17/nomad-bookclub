# MISSION: 더러운 코드를 고쳐라

아래 가이드를 보고 총 3개의 더러운 코드를 깨끗하게 고쳐 보세요.

## QUIZ 01

- Hint❕ : 검색하기 쉬운 이름을 사용하세요.
- blastOFF는 로켓 발사를 의미. 86400000은 하루의 밀리초 (milliseconds) 의미.

```jsx
// What the heck is 86400000 for?
setTimeout(blastOff, 86400000);

// GOOD 😎
// 위 코드를 깨끗하게 다시 작성해 주세요.
const MILLISECNONDS_IN_A_DAY = 86400000;
setTimeout(blastOff, MILLISECONDS_IN_A_DAY);

// 어떻게 고쳤는지, 사례에서 무엇을 배워야 하는지 설명해주세요.
```

86400000이라는 숫자만으로는 이게 뭔지 알기 어렵다.

다행히 우리에겐 이 숫자가 ‘하루의 밀리초’라는 의미라는 것을 안다.

따라서 먼저 86400000을 `MILLISECONDS_IN_A_DAY`에 저장했다.

이를 `setTimeout`에서 호출해서 사용한다.

이렇게 하면 86400000의 의미도 이해하기 쉽고, 이후에 변수를 검색하기도 쉬워진다.

## QUIZ 02

- Hint❕ : 의미있는 이름을 사용해 주세요.

```jsx
const yyyymmdstr = moment().format("YYYY/MM/DD");

// GOOD 😎
// 위 코드를 깨끗하게 다시 작성해 주세요.
const timestamp = moment().format("YYYY/MM/DD");

// 어떻게 고쳤는지, 사례에서 무엇을 배워야 하는지 설명해주세요.
```

`yyyymmdstr`보다 의미가 명료한 `timestamp`라는 이름으로 변수를 만드는 것이 낫다.

또한 `yyyymmdstr`는 발음하기도 어려워서 동료들과의 커뮤니케이션에도 방해된다.

## QUIZ 03

- Hint❕ : 불필요하게 반복하지 마세요.

```jsx
const Car = {
  carMake: "Honda",
  carModel: "Accord",
  carColor: "Blue",
};

function paintCar(car, color) {
  car.carColor = color;
}

// GOOD 😎
// 위 코드를 깨끗하게 다시 작성해 주세요.
const Car = {
  make: "Honda",
  model: "Accord",
  color: "Blue",
};

function paint(car, color) {
  car.color = color;
}

// 어떻게 고쳤는지, 사례에서 무엇을 배워야 하는지 설명해주세요.
```

`Car` 객체 안에 있는 속성들은 이름 앞에 `car`라는 접두어를 일일이 붙이지 않아도 된다. 그런건 오히려 불필요한 중복 정보일 뿐이다.
