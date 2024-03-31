---
# layout : single
title: "ClickerGame 포트폴리오"

# author_profile: true
categories:
  - ClickerGame
toc: true
toc_sticky: true
# sidebar:
#     nav: "sidebar-category"
---

### 방치형 게임 만들기
<hr/>

* 개발 기간 : 2024.02.26 ~ 2024.03.25 (약 1달)
* 개발 인원 : 1명
* 개발 환경 
    * unity (2021.3.33f)
    * 윈도우 11
    * 화면비율 1280 * 720 portrait 

### 시연영상
[![Video Label](http://img.youtube.com/vi/BnNjLPQfcCs/0.jpg)](https://www.youtube.com/watch?v=BnNjLPQfcCs)

### Socrce Code 
<hr/>

[소스코드 보기](https://github.com/Theta08/growGame)

### 게임구조
<img src="/assets/images/전체구조도.png" width="90%" height="90%" title="전채구조도" alt="전채구조도"/> <br/>

{: .notice}
게임 시작 시 `saveData`가 있는지 확인 있으면 불러오기 버튼 생성 없으면 이름 생성 후 게임 시작이 된다.   
게임 시작 시 `saveData`에 기본 능력치가 세팅된다. 몬스터를 잡으면 돈이 들어오고 하단에 스탯 증가로 능력치가 강화된다.   
하단 뽑기 버튼으로 능력치 무작위 스탯(공격력, 체력, 방어력) 중 하나와 랭크 1~3중 하나 생성해서 선택 가능하다.


<!-- ## 기능
1. 타이틀화면 세이브데이터 체크 
    1. 세이브데이터 O : 불러오기 버튼 활성화
    2. 세이브데이터 X : 새로하기 버튼 -> 이름입력 팝업 실행
2. 플레이화면
    1. 스탯증가 버튼
    2. 뽑기버튼 -->

### 스탯 설정
캐릭터오브젝트 호출 후 `BaseController`와 `Stat`를 GetComponent한다.
<hr/>

## BaseController
캐릭터 애니메이션 : 오브젝트상태에따라 애니메이션 생성
공격타겟 설정 : 오브젝트 콜로이더로 `LayerMask`(player, monster)기준으로 오브젝트를 찾아 `target`으로 설정 

``` cs
Collider2D collider = Physics2D.OverlapBox(transform.position, new Vector2(3,3), 0, targetLayer);
_lockTarget = collider.gameObject;
```
## Stat
<hr/>

캐릭터오브젝트에 `Stat`를 넣어 캐릭터 스탯 설정
OnAttacked : 공격자 `Stat`.Attack를 가져와 Hp감소
``` cs
 public void OnAttacked(Stat attacker)
  {
        int damage = Mathf.Max(0, attacker.Attack - Def);
        Hp -= damage;
  }
``` 

OnDead: Hp < 0일때 `UI_DeadPopup`팝업 호출 