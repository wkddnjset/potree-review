---
marp: true
theme: uncover
---
<style>
h6 {
  text-align: right;
  font-size: 25px;
}
li {
  font-size: 30px;
}
img {
  max-width: 1000px;
}
</style>

# Potree 논문 세미나

> Rendering Large Point Clouds in Web Browsers

<br/>

###### `Markus Schuetz`<br/>`발표 - 서장원(Dooly)`

---

## 목차

1. Potree 개요
2. WebGL에 대한 기본적인 이해
3. Modifiable Nested Octree(MNO) 구조에 대한 정리

---

## ❗주의사항❗

---

## 라이센스

코드수정 가능!
재사용 가능!

***출처를 명시해야함**

---

![라이센스](/images/license.png)

---

## Motivation (동기)

---

## Motivation (동기)

- 거대한 양의 데이터를 웹으로 처리하기 위해

--- 

## Problem (문제)

---

## Problem (문제)


-  27조 개의 점으로 이뤄진 540 TB

```
https://pubs.er.usgs.gov/publication/cir1399
```

---

## How?

---

## How?

- WebGL
- out-of-core
- Modifiable Nested Octree(MNO)

---

### WebGL

- WebGL API
- Double Buffering
- Single JavaScript Callback

<!-- 단일 JavaScript 콜백 내에서 프레임의 WebGL 렌더링을 전체적으로 수행해야 한다는 것이다. -->

---

### WebGL API

```javascript
const gl = canvas.getContext("experimental-webgl");
```

<!-- 다음같이 선언된 gl Element를 통해 WebGL API 함수를 사용해 렌더링 할 수 있다. -->

---

### Double Buffering

![buffer](/images/buffer.png)

<!-- - Video Controller가 프론트버퍼의 내용을 출력하는 동안, GPU는 백버퍼에 백버퍼에 다음에 그려질 내용을 쓴다. 
- GPU가 전부 내용을 썼으면 비디오 컨트롤러가 백버퍼로 스위칭 후 새로운 내용을 화면에 그린다.
- 동시에 GPU는 프론트버퍼로 스위칭, 새로 화면에 그릴 내용을 버퍼에 쓴다. -->

---

### Single JavaScript Callback

![buffer](/images/buffer.png)

<!-- 브라우저가 자바스크립트의 실행 중을 제외하고 언제든지 백버퍼를 프런트버퍼에 복사할 수 있다는 것이다. 즉, 단일 JavaScript 콜백 내에서 프레임의 WebGL 렌더링을 전체적으로 수행해야 한다는 것이다. -->

---

## How?

- ~~WebGL~~
- out-of-core
- Modifiable Nested Octree(MNO)

---

### out-of-core 알고리즘

![out-of-core](/images/out-of-core.gif)

<!-- 머신러닝 관련 블로그에서는 외부메모리 학습 이라고 소개했지만, chuck로 데이터를 나눠서 프로그램을 실행할 수 있도록 만들어 성능을 향상시킨 느낌? -->

---

## How?

- ~~WebGL API~~
- ~~out-of-core~~
- Modifiable Nested Octree(MNO)

---

### Octree

![octree](/images/octree.png)

<!-- 탐색 모듈 이라고 부르는 듯 한데, Octree 말고도 다양한 방식이 있다. -->

---

### Octree

![octree-2](/images/octree-2.png)

<!-- 이미지 처럼 공간을 표현하는 방식으로 사용되며, 게임에서 충돌체크를 할 때 사용된다! -->

---


### MNO Structure

- subsamples : gird with $128^3$ cells
- 

![mno](/images/mno.png)

<!-- out-of-core 알고리즘으로 인한 부분적인 업데이트 반영에 대응하기 위해서 나온 개념으로 Octree와 다른 부분은   -->

--- 

### Potree’s Octree Structure

- subsamples : Poisson-Disk

![subsamples](/images/subsamples.png)

<!-- Poisson-Disk는 점과 점사이의 간격이 동일한 샘플링 방식   -->
