# Tween

Tween 이란 애니메이션이 작동하도록 하는 setter라고 보면 된다. 애니메이션이 몇 초동안 동작하는 지, 동작하면서 어떤 속성을 갖는 지를 다양하게 설정할 수 있다.

Tween을 만드는 일반적이고 가장 간단한 방법으로는 아래와 같은 메소드가 있다. 아래의 메소드들은 Tween instance를 반환한다.

```
gsap.to()
gsap.from()
gsap.fromTo()
```

```r
gsap.to(".box", {rotation: 27, x: 100, duration: 1});
```
위에서는 gsap.to() 를 사용해서 클래스명이 '.box'인 것을 1초동안 x축으로 100,을 가면서 27도를 돌린다. 중괄호 안에 Tween이 사용되었다.


<br/><br/>

## 인스턴스 제어를 위한 변수 할당
여러가지 복잡한 애니메이션을 구현하고 싶을 때 delay라는 속성을 사용할 수 있지만, 이보다 timeline을 사용하는 것이 더 직관적이고 쉽다.

그리고 자주 사용하는 속성들을 통합해 하나의 변수로 할당하기도 한다.

```r
let tween = gsap.to(".class", {rotation: 360, duration: 5, ease: "elastic"});

tween.pause();
tween.seek(2);
tween.progress(0.5);
tween.play();
...
```
<br/><br/>

## 랜덤값

랜덤 값을 'random(-100, 100)' 또는 'random([red, blue, yellow])' 같이 정의해서 타겟이 랜덤으로 동작하게 할 수도 있다.


```r
gsap.to(".class", {
  x:"random(-100, 100, 5)"
}); 
```
위는 .class의 x축 위치를 -100과 100사이의 랜덤한 숫자를 선택하여 5에 가까운 것을 반올림한다.


```r
gsap.to(".class", {
  x:"random([0, 100, 200, 500])" 
}); 
```
아니면 위와 같은 식으로 x축 위치를 0, 100, 200, 500 중 하나를 랜덤하게 선정한다.

<br/><br/>

2022.09.24