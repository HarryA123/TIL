# GSAP

gsap 는 애니메이션 라이브러로, 아래와 같은 형식을 기본으로 사용한다. 첫 번재 인자로는 내가 타겟하는 엘리먼트의 클래스명이나 아이디명을 쓰고 두 번째 인자로는 보통 애니메이션 됐을 때의 효과를 쓴다.
<br/>

일반적으로 gsap.to(), gsap.from(), gsap.fromTo()가 있는데, gsap.fromTo()만 조금 다른 점은 from의 형태에서 To 로 애니메이션되는 기본식을 따로 작성해야 한다.

```r
gsap.fromTo(
  '.box_3',
  { x: 300, y: -200, duration: 1, scale: 0.8 },
  {
    x: 300,
    y: -200,
    duration: 1,
    scale: 3,
    backgroundColor: 'gold',
    scrollTrigger: {
      trigger: '.box_3',
      start: 'top center',
      end: 'bottom center',
      markers: true,
      toggleActions: 'play none none reverse',
    },
  },
);
```

<br/><br/>

## gsap 3.11.00 부터는...

스크롤 기능과 반응형을 동시에 구현하기 위해서 scrollTrigger.matchMedia 를 공부했다. 이게 GSAP 사용자들 사이에서 자주 유용하게 쓰이는 것 같았지만, 3.11.00 부터 사용할 수 없게 됐다. 그 대신 gsap.matchMedia 안에서 스크롤과 반응형을 둘 다 사용할 수 있게 만들어놨다.

[gsap.matchMedia 공식문서 참고링크](<https://greensock.com/docs/v3/GSAP/gsap.matchMedia()>)

<br/><br/>
2022.09.22
