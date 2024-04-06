---
# layout : single
title: "ClickerGame 포트폴리오2"

# author_profile: true
categories:
  - ClickerGame
toc: true
toc_sticky: true
# sidebar:
#     nav: "sidebar-category"
---
### 매니저 설정
<img src="/assets/images/Manager.png" width="90%" height="90%" title="Manager" alt="Manager"/> <br/>

프로젝트를 만들면서 공통적으로 쓸거를 만들어야 재사용이 덜 되서 Manager오브젝트에 만듬   
게임시작시 게임오브젝트(@Manager)에 AddComponent한다.

```cs
public static Managers s_instance = null;

private static void Init()
{
  if (s_instance == null)
  {
      GameObject go = GameObject.Find("@Managers");
      if (go == null)
          go = new GameObject { name = "@Managers" };

      s_instance = Utils.GetOrAddComponent<Managers>(go);
      DontDestroyOnLoad(go);
      
  }
}
```

다른 매니저들을 매니저에 호출해서 쓸 수 있게 설정

``` cs
private static ResourceManager s_resourceManager = new ResourceManager();
private static PoolManager s_poolManager = new PoolManager();
private static UIManager s_uiManager = new UIManager();
private static SoundManager s_soundManager = new SoundManager();
private static GameManager s_gameManager = new GameManager();

public static ResourceManager Resource { get { Init(); return s_resourceManager; }}
public static PoolManager Pool { get { Init(); return s_poolManager; }}
public static UIManager UI { get { Init(); return s_uiManager; }}
public static SoundManager Sound { get { Init(); return s_soundManager; }}
public static GameManager Game { get { Init(); return s_gameManager; }}
```

{: .notice}
`ReSourceManager`: ReSource폴더의 프리펩을 `Load`, `Instantiate`, `Destory`하는 함수 생성   
`SoundManager` : Audio관리 GameObject를 생성하고 오디오 재생(bgm, efffect)을 실행하는 함수 `play`생성   
`GameManaer` :  게임실행에 필요한 함수 생성 및 호출 GameData 호출 및 저장, 오브젝트 스폰, 디스폰,   
게임 일시정지, 재생   
`PoolManager` : 풀링매니저   
`UIManager` : UI관련 팝업실행, 종료, 켐퍼스 sortingOder 설정, 특정 팝업프리펩 경로 호출   
<hr/>

### 팝업 호출용 UI_Base
`UI_Base`는 상속받는 클래스에 오브젝트(`BindObject`), 이미지(`BindImage`), 텍스트(`BindText`), 버튼(`BindButton`)함수 바인딩한다. Get `BindEvent`호출로 클릭이벤트 작성

`Bind`함수는 `Enum`을 통해 GameObject.name == Enum.GetNames(type) 오브젝트 찾고 `_objects` 저장
``` cs
protected Dictionary<Type, UnityEngine.Object[]> _objects = new Dictionary<Type, Object[]>();
```
`Get` : `_objects`으로 해당 오브젝트 리턴