1. 해당 키 입력시 효과음 추가하는 함수 생성
```
function playSound(e) {
    const audio = document.querySelector(`audio[data-key="${e.keyCode}"]`)
    const key = document.querySelector(`.key[data-key="${e.keyCode}"]`)
    if(!audio) return;
    audio.currentTime = 0;
    audio.play();
    key.classList.add('playing');
  }
```
audio, key에 각각 누른 자판의 KeyCode와 일치하는 요소들을 담아주고<br>
일치하는 audio가 없다면 return(실행x), 일치한다면 누른 key 요소에 playing클래스를 추가해주고<br>
음악파일을 play하는 playSound()함수를 생성



2. 키 재입력 시간 설정(연속 입력 가능하도록)
```
audio.currentTime = 0;
audio.play();
```
오디오 재생의 현재 위치를 0초로 이동하게 하여 delay없이 연속으로 입력이 가능해진다.


3. 효과 종료시 변화하는 함수 생성
```
function removeTransition(e) {
    if(e.propertyName !== 'transform') return;
    this.classList.remove('playing');
    // console.log(this);
  }
```
누른 키의 속성명 중 transform이 이 없으면 return(실행x),<br>
있다면 playing이란 클래스를 지우도록하는 removeTransition()함수를 생성<br>
=> 눌렀을 때 작용하는 애니메이션이 모두 끝난 후 그 상태의 playing이란 클래스를 삭제


4. 효과음 출력 및 종료 설정
```
const keys = document.querySelectorAll('.key');
keys.forEach(key => key.addEventListener('transitionend', removeTransition));

window.addEventListener('keydown', playSound);
```
key 클래스를 가진 모든 요소를 keys에 배열로 담고<br>
forEach를 사용해 각각의 요소에 변화가 끝나면(transitionend) removeTransition 함수를 실행하고,<br>
keydown 이라는 이벤트가 실행되면 playSound함수가 작동함

> 찾아본 것 | 알게된 점<br>
HTML DOM classList Property<br>
HTML kbd tag
