# TypeScript

typescript 공식에서는 타입 지정에 있어서 Type 보다는 interface 사용을 권장한다. Type은 특정한 때에만 사용하라고 한다.

Type과 interface는 대부분의 경우 비슷하거나 같게 작동한다.

```js
type BirdType = {
  wings:2;
};

interface BirdInterface {
  wings: 2;
}

const bird1 : BirdType = {wings:2}
const bird2 : BirdInterface = {wings:2}

```
<br><br>
type 을 쓰냐 interface를 쓰냐의 차이는 'error 메세지'에 있다.

```js

type Owl = { nocturnal: true } & BirdType;
type Robin = { nocturnal: false } & BirdInterface;

interface Peacock extends BirdType {
  colourful: true;
  flies: false;
}
interface Chicken extends BirdInterface {
  colourful: false;
  flies: false;
}

let owl: Owl = { wings: 2, nocturnal: true };
let chicken: Chicken = { wings: 2, colourful: false, flies: false };

owl = chicken;
//Type 'Chicken' is not assignable to type 'Owl'.
//Property 'nocturnal' is missing in type 'Chicken' but required in type '{ nocturnal: true; }'.(2322)

chicken = owl;
//Type 'Owl' is missing the following properties from type 'Chicken': colourful, flies(2739)
```
<br><br>
그리고 interface는 재선언이 가능하지만 type은 재선언이 불가하다.

```js

interface Kitten {
  purrs: boolean;
}

interface Kitten {
  colour: string;
}


type Puppy = {
  color: string;
};

type Puppy = {
  toys: number;
};
// Duplicate identifier 'Puppy'.(2300)
```

