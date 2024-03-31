---
# layout : single
title: "ClickerGame 포트폴리오3"

# author_profile: true
categories:
  - ClickerGame
toc: true
toc_sticky: true
# sidebar:
#     nav: "sidebar-category"
---
### 시작화면
<img src="/assets/images/TitleMain.png" width="40%" height="40%" title="TitleMain" alt="TitleMain"/> <br/>

바인딩을 위해 enum Texts{...}, Buttons{...} 설정 및 바인딩 (오브젝트 이름과 같아지게 해야 함)   
`Managers`를 통해 `SoundManager` 클래스에서 음악 BGM실행
``` cs
    enum Texts
    {
        StartButtonText,
        StartButtonText2,
    }

    enum Buttons
    {
        StartButton,
        StartButton2,
        ExitButton,
    }

    public override bool Init()
    {
      
      BindText(typeof(Texts));
      BindButton(typeof(Buttons));

      Managers.Sound.Play(Define.Sound.Bgm, "Sound_MainTitle", 0.25f);
      ...
    }
```
<img src="/assets/images/TitleHierarchy.png" width="60%" height="60%" title="TitleHierarchy" alt="TitleHierarchy"/> <br/>

### 세이브파일 확인
<hr/>

GameManager에서 로드파일이 있는지확인 없으면 로드 버튼 안 보이게 함

### 버튼 클릭 이벤트
<hr/>

`StartButton` : GameData초기화 `UIManager`를 통해 현재팝업 닫고 이름입력 프리팹(`UI_NamePopup`) 호출   
effect소리 실행   

``` cs
  void OnClickStartButton()
  {
      Managers.Game.Despawn(knight);
      Managers.Sound.Play(Define.Sound.Effect, "Sound_MainButton");
      
      Managers.Game.Init();
      Managers.Game.SaveData.Reset = true;
      
      Managers.UI.ClosePopupUI(this);
      Managers.UI.ShowPopupUI<UI_NamePopup>();
  }
```

`OnClickLoadButton` : 현재팝업 닫기 -> `UI_PlayPopup`프리팹 호출

```cs
  void OnClickLoadButton()
  {
      Managers.Game.Despawn(knight);
      Managers.Sound.Play(Define.Sound.Effect, "Sound_MainButton");
      Managers.UI.ClosePopupUI(this);
      Managers.UI.ShowPopupUI<UI_PlayPopup>();
  }
```
`OnClickLoadButton` : 게임을 종료 
```cs
  void OnExitButton(){Application.Quit();}
```
