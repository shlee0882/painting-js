### painting-js(그림판)
- JS만 사용해 그림판을 구현하였습니다.
- html canvas 태그를 사용했습니다.
- 마우스 이벤트 메서드(mousemove, mousedown, mouseup, mouseleave, click, contextmenu)를 사용했습니다.
- mousemove시 event.offsetX, event.offsetY로 값을 구합니다.
- canvas.getContext("2d");로 context를 통해 paint메서드를 호출합니다.
- 좌표값을 얻어 
	- 마우스가 클릭 되지 않았을때 beginPath();, moveTo(x,y) 호출합니다. 
	- 마우스가 클릭 되었을때 lineTo(x,y), stroke(); 호출합니다.
- default값 설정 이후 이벤트 발생 시 값(strokeStyle, fillStyle, fillRect, lineWidth, innerText)을 새로 set합니다.
- 펜모드, 펜 두께조절, 채우기 모드가 있으며 캔버스 안에서 마우스 오른쪽 버튼을 막았습니다.(event.preventDefault()) 
- 그림을 저장할수 있습니다.(canvas.toDataURL())

#### 분할정복 방식으로 공통된 값은 상수를 사용하며, 각각 함수를 쪼개어 호출합니다. 

```js

// 상수 정의
const canvas = document.getElementById("canvas");
const save = document.getElementById("save");
const CANVAS_SIZE = 700;

// 공통 값 셋팅
canvas.width = CANVAS_SIZE;
canvas.height = CANVAS_SIZE;

// 함수 정의
function onMouseMove(evnet){
    const x = event.offsetX;
    const y = event.offsetY;
    console.log(x,y);
}

function handleSaveClick(){
    const image = canvas.toDataURL();
    const link = document.createElement("a");
    link.href = image;
    link.download = "myPainting";
    link.click();
}

// 이벤트 정의 및 함수호출
if(canvas){
    canvas.addEventListener("mousemove", onMouseMove);
}

if(save){
    save.addEventListener("click", handleSaveClick);
}

/*
const - canvas      > canvas.addEventListener("mousemove", onMouseMove) > function onMouseMove(evnet)
      - save        > save.addEventListener("click", handleSaveClick)   > function handleSaveClick()
      - CANVAS_SIZE > set canvas.width, height
*/

```

배포된 url :
  - deploy url : https://shlee0882.github.io/painting-js/
