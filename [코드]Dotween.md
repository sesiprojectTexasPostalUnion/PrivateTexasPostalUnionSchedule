# Dotween์ ๋ํด์

---

<aside>
๐ก **HEADER**

</aside>

---

# ๊ฐ์

---

์ ๋ํฐ์์ ์ ๋๋ฉ์ดํ, ์ถ์ , ์ด๋ ๋ฑ์ ์ฌ์ฉ๋๋ Dotween์ ๋ํ์ฌ ์์๋ณด๊ธฐ ํนํ ๋ฒํผ ๊ด๋ จ

<aside>
โ ๏ธ ์์ฑ์๊ธฐ 2023๋ 02์

</aside>

<aside>
โ ๏ธ unity 2021.3.1f1 ์์ ์งํ๋์์ต๋๋ค.

</aside>

---

# import

[DOTween (HOTween v2)](https://assetstore.unity.com/packages/tools/animation/dotween-hotween-v2-27676)

์ ๋งํฌ์์ ์ ๋ํฐ ํ๋ก์ ํธ์ ์ํฌํธ ์งํํด์ฃผ์ธ์

## ๋ฐ์ํ ๋ฒํผ ๋ง๋ค๊ธฐ

**๋ฒํผ์ผ๋ก ๋ง๋ค๊ณ  ์ถ์ Prefab ๋ฑ์ ์ฝ๋๋ค์ ์ํฌํธํ  ํ์๊ฐ ์์ต๋๋ค**

์์ ์ด๋ฏธ์ง)

![image.jpg1](image/dotweenbtn1.PNG)
### 1. ํ ๊ธ

---

```csharp
using UnityEngine;
using UnityEngine.UI;
using TMPro;
using DG.Tweening;

/// <summary>
/// Sample of button Asset
/// </summary>
public class ButtonController : MonoBehaviour
{
    /// <summary>
    /// Toggle Button 
    /// </summary>
    private bool Isclicked;
    void Awake()
    {
        Button button = GetComponent<Button>();
        button.onClick.AddListener(OnClick);
    }

    void OnClick()
    {
        if (Isclicked == false)
        {
            Isclicked = true;
            //ใtransform์scale์๊ฐ์1.1f๋กใ0.5์ด๊ฐใ๋ณด๊ฐ๋ฐฉ๋ฒ์OutElastic
            transform.DOScale(1.1f, 0.5f).SetEase(Ease.OutElastic);
            GetComponentInChildren<TMP_Text>().text = "Clicked!";
            
        }
        else
        {
            Isclicked = false;
            transform.DOScale(1.0f, 0.5f).SetEase(Ease.OutElastic);
            GetComponentInChildren<TMP_Text>().text = "Button";
        }
    }
}
```

ํด๋น ์ฝ๋๋ฅผ ์ผ๋ฐ์ ์ธ UI ๋ฒํผ์ ์ถ๊ฐ๋ง ํด์ฃผ๋ฉด ํด๋ฆญ ์ ํฌ๊ธฐ๊ฐ ์ปค์ก๋ค ์ค์ด๋๋ ๋ฐ์์ ํฉ๋๋ค.


### 2. ๋ฃจํ

---

```csharp
using UnityEngine;
using DG.Tweening;

public class ButtonController_2 : MonoBehaviour
{
    void Awake()
    {
        StartStrongButtonAnim();
    }

    void StartStrongButtonAnim()
    {
        transform.DOScale(0.15f, 1f)
        .SetRelative(true)
        .SetEase(Ease.OutQuart)
        .SetLoops(-1, LoopType.Restart);
    }
}
```

์ฝ๋๋ฅผ ์ผ๋ฐ์ ์ธ UI ๋ฒํผ์ ์ถ๊ฐ๋ง ํด์ฃผ๋ฉด ์ปค์ก๋ค ์์์ก๋ค ํ๋ ์ ๋๋ฉ์ด์์ ๊ธฐ๋ณธ์ ์ผ๋ก ๋ฌดํ๋ฐ๋ณตํฉ๋๋ค.



<aside>
* ์ ๋ ์ข๋ฅ์  ์ฝ๋๋ก ๊ธฐ๋ณธ์ ์ธ ๋ฐ์ํ ui๋ฅผ ๋ง๋ค ์ ์์ต๋๋ค.
</aside>



## ํ์ ๋ง๋ค๊ธฐ

**ํ์์ผ๋ก ๋์ฐ๊ณ  ์ถ์ Prefab ๋ฑ์ ์ฝ๋๋ค์ ์ํฌํธ, ๋ฒํผ์ ํ ๋นํ  ํ์๊ฐ ์์ต๋๋ค**

์์ ์ด๋ฏธ์ง)

![image.jpg1](image/dotweenbtn2.PNG)

์์ ์ด๋ฏธ์ง 2)

![image.jpg1](image/dotweenbtn3.PNG)

### 1. ์ปค์ง๋ ํํ์ ํ์

---

```csharp
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using DG.Tweening;

public class PannelController_1 : MonoBehaviour
{
    RectTransform rectTransform;
    void Awake()
    {
        transform.localScale = Vector3.zero;
    }

    public void ShowWindow()
    {
        transform.DOScale(1f, 1f).SetEase(Ease.OutBounce);
    }
}
```

ShowWindow() ๋ฅผ ํธ์ถ (๋ฒํผ ๋ฑ์ ๋ฑ๋กํด ํธ์ถ) ํ๋ฉด ์ปค์ง๋ฉด์ ๋ฑ์ฅํ๋ ํ์์ด ์์ฑ๋ฉ๋๋ค.

### 2. ๋จ์ด์ง๋ ๋๋

---

```csharp
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using DG.Tweening;

public class PannelController_2 : MonoBehaviour
{
    RectTransform rectTransform;
    void Awake()
    {
       rectTransform = GetComponent<RectTransform>();
       rectTransform.anchoredPosition = new Vector3(0, 700, 0);
    }

    public void ShowWindow()
    {
       rectTransform.DOLocalMoveY(0f, 1f).SetEase(Ease.OutBounce);
    }
}
```

ShowWindow() ๋ฅผ ํธ์ถ (๋ฒํผ ๋ฑ์ ๋ฑ๋กํด ํธ์ถ) ํ๋ฉด ๋จ์ด์ง๋ฉด์ ๋ฑ์ฅํ๋ ํ์์ด ์์ฑ๋ฉ๋๋ค.




