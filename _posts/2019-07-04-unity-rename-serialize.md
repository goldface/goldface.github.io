# 직렬화 된 필드의 이름 변경하기

## 변수 이름 변경하기
아래와 같은 클래스가 있을 경우
```CSharp
using UnityEngine;

class MyClass : MonoBehaviour
{
    [SerializeField]
    private string m_MyVariable;
}
```

`m_MyVariable`의 변수를 다른 이름 `m_AnotherVariable`으로 변경 할 경우 Prefab이나 Scene에 배치된 오브젝트들의 설정값이 변경되게 됩니다.
이를 원치 않을 경우 아래와 같은 방법으로 해결 할 수 있습니다.

```CSharp
using UnityEngine;
using UnityEngine.Serialization;

class MyClass : MonoBehaviour
{
    [FormerlySerializedAs("m_MyVariable")]
    [SerializeField]
    private string m_AnotherVariable;
}
```

`[SerializeField]`를 사용하지않은 public으로 선언된 변수를 변경할 경우
```CSharp
using UnityEngine;
using UnityEngine.Serialization;

class MyClass : MonoBehaviour
{
    [FormerlySerializedAs("myValue")]
    [SerializeField]
    private string m_Value;
    public string myValue
    {
        get { return m_Value; }
        set { m_Value = value; }
    }
}
```

변경한 변수이름을 다시 변경하는 것도 가능합니다.
```CSharp
using UnityEngine;
using UnityEngine.Serialization;

class MyClass : MonoBehaviour
{
    [FormerlySerializedAs("m_MyVariable")]
    [FormerlySerializedAs("m_ABetterName")]
    [SerializeField]
    private string m_EvenBetterName;
}
```
선언한 `Attribute`를 언제 제거 할 수 있습니까?  
이름을 변경 한 후 `Scene`과 `Asset`을 다시 저장 한 후 속성을 제거할 수 있습니다.