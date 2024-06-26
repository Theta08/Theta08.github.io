---
# layout : single
title: "ClickerGame 포트폴리오4"

# author_profile: true
categories:
  - ClickerGame
toc: true
toc_sticky: true
# sidebar:
#     nav: "sidebar-category"
---
### 플레이화면
<hr/>

<img src="/assets/images/playPopup.png" width="40%" height="40%" title="playPopup" alt="playPopup"/> <br/>

바인딩을 위해 enum Texts{...}, Buttons{...} 설정 및 바인딩 (오브젝트 이름과 같게해야함)   
``` cs
    enum Texts
    {
        NameText,
        Timer,
        Money,
        MoneyDrawText
    }
    enum Buttons
    {
        GameDraw,
    }
    enum AbilityItems
    {
        UI_AbilityItem_MaxHp,
        UI_AbilityItem_Attack, 
        UI_AbilityItem_Def,
    }

    public override bool Init()
    {
      
      BindText(typeof(Texts));
      BindButton(typeof(Buttons));
      Bind<UI_AbilityItem>(typeof(AbilityItems));

      ...
    }
```
게임 시작시 코르틴을 사용하여 시간을 `SaveData`에 저장한다. 몬스터가 죽으면 돈도 `SaveData`에 저장을 한다. 실시간으로 보이게 하기 위해 `update`문에다가 텍스트를 수정하게 함
```cs
    public void Update()
    {
        if (!Managers.Game.IsLive)
            return;
        
        float remainTime = Managers.Game.SaveData.PlayTime += Time.deltaTime;
        
        GetText((int)Texts.Money).text = Managers.Game.SaveData.Money.ToString("D");
        GetText((int)Texts.Timer).text = Managers.Game.GetPlayerTimer(remainTime);
    }
```
### 능력강화
1. 클릭한 스탯타입을 `UI_AbilityItem.cs`에 변수(`_statType`)로 준다. 
2. 변수에따라 해당 능력치를 `GameData`에서 `NextUpgradeInt`실행 시켜 변경한다. 
3. 플레이어 스탯에 변경된 GameData를 저장 후 초기화 시킨다.
4. 클릭한 스탯 UI만 변경내용을 업데이트 하기위해 초기화 시킨다.

```cs 

    // UI_AbilityItem.cs
    void OnUpgradeButton()
    {
        if (Managers.Game.SaveData.Money < _pay)
        {
            Debug.Log($"돈 {_pay - Managers.Game.SaveData.Money} 부족합니다.");
            return;
        }
        
        Managers.Sound.Play(Define.Sound.Effect, "Sound_Select");
    
        Managers.Game.SaveData.Money -= _pay;
        Managers.Game.SaveData.NextUpgrade(_statType);
        // 플레이어 초기화 
        Managers.Game.RefreshPlayerData();

        // 해당 초기화
        RefreshUI();
    }
    // GamaeData.cs
    public int NextUpgradeInt(Define.StatType statType)
    {
        int result = 0;
        switch (statType)
        {
            case Define.StatType.MaxHp:
                result = _maxHp + (MaxHpUpgrade.count + 1) * MaxHpUpgrade.rank;
                break;
            case Define.StatType.Attack:
                result = _attack + (AttackUpgrade.count + 1) * AttackUpgrade.rank;
                break;
            case Define.StatType.Def:
                result = _def + (DefUpgrade.count + 1) * DefUpgrade.rank;
                break;
        }
        return result;
    }

    //PlayerStat.cs
    public override void GetPlayerStat(GameData gameData)
    {
        // 세이브데이터X 경우
        if (gameData.Attack == 0 || gameData.Reset)
        {
            gameData.MaxHp = MaxHp;
            gameData.Hp = Hp;
            gameData.Attack = Attack;
            gameData.Def = Def;
            gameData.Money = 0;
            gameData.PlayTime = 0;
            
            Upgrade upgrade = new Upgrade{ count = 1, rank = 1 };

            gameData.AttackUpgrade = upgrade;
            gameData.DefUpgrade = upgrade;
            gameData.MaxHpUpgrade = upgrade;
        }
        else
        {
            MaxHp = gameData.MaxHp;
            Hp = gameData.Hp;
            Attack = gameData.Attack;
            Def = gameData.Def;
        
            Name = gameData.Name;
            Money = gameData.Money;
            PlayTime = gameData.PlayTime;

            AttackUpgrade = gameData.AttackUpgrade;
            DefUpgrade = gameData.DefUpgrade;;
            MaxHpUpgrade = gameData.MaxHpUpgrade;;
        }

        Managers.Game.SaveGame();
    }
```
### 뽑기
<hr/>

`UI_DrawPopup`프리펩을 호출한다. 스탯(MaxHp, Attack, Def)과 rank(1~3)을 랜덤으로 돌린다.
rank : rank에 따라 색깔을 변경한다.   

<img src="/assets/images/drawPopup.png" width="40%" height="40%" title="drawPopup" alt="drawPopup"/> <br/>
<!-- 소스코드 붙이기 -->