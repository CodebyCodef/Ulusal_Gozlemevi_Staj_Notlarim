# 🧩 Python `typing` Kütüphanesi --- Detaylı Rehber

Python dinamik tipli bir dil olsa da, büyük projelerde **tip güvenliği
(type safety)** sağlamak oldukça önemlidir.\
`typing` kütüphanesi, koduna **tip ipuçları (type hints)** eklemeni
sağlar.

------------------------------------------------------------------------

## 🧠 Typing Nedir?

`typing`, değişkenlerin ve fonksiyonların hangi tür veri ile çalıştığını
belirtmeni sağlar.

``` python
def topla(a: int, b: int) -> int:
    return a + b
```

Bu örnekte: - `a` ve `b` → `int` - dönüş değeri → `int`

------------------------------------------------------------------------

## 🎯 Neden Kullanılır?

-   Kod okunabilirliğini artırır
-   Hataları erken yakalamanı sağlar
-   IDE desteğini güçlendirir (autocomplete vs.)
-   Büyük projelerde sürdürülebilirlik sağlar

------------------------------------------------------------------------

## ⚙️ Temel Tipler

``` python
x: int = 10
y: float = 3.14
name: str = "Efe"
is_active: bool = True
```

------------------------------------------------------------------------

## 📦 Koleksiyon Tipleri

### List

``` python
from typing import List

numbers: List[int] = [1, 2, 3]
```

------------------------------------------------------------------------

### Dict

``` python
from typing import Dict

user: Dict[str, int] = {"age": 20}
```

------------------------------------------------------------------------

### Tuple

``` python
from typing import Tuple

point: Tuple[int, int] = (10, 20)
```

------------------------------------------------------------------------

### Set

``` python
from typing import Set

ids: Set[int] = {1, 2, 3}
```

------------------------------------------------------------------------

## 🔄 Union (Birden Fazla Tip)

``` python
from typing import Union

def process(value: Union[int, str]):
    print(value)
```

------------------------------------------------------------------------

## ❓ Optional

``` python
from typing import Optional

def find_user(id: int) -> Optional[str]:
    return None
```

`Optional[str]` = `str | None`

------------------------------------------------------------------------

## 🧪 Any (Her Şey)

``` python
from typing import Any

data: Any = "her şey olabilir"
```

Dikkat: Fazla kullanmak typing'in amacını bozar.

------------------------------------------------------------------------

## 🧱 Callable (Fonksiyon Tipi)

``` python
from typing import Callable

def execute(func: Callable[[int, int], int]):
    return func(2, 3)
```

------------------------------------------------------------------------

## 🧬 Generics (Genel Tipler)

``` python
from typing import TypeVar, List

T = TypeVar('T')

def first_item(items: List[T]) -> T:
    return items[0]
```

------------------------------------------------------------------------

## 🧩 TypedDict

``` python
from typing import TypedDict

class User(TypedDict):
    name: str
    age: int

user: User = {"name": "Ali", "age": 25}
```

------------------------------------------------------------------------

## 🧪 Literal

``` python
from typing import Literal

def set_mode(mode: Literal["auto", "manual"]):
    pass
```

------------------------------------------------------------------------

## 🧭 Protocol (Duck Typing Güçlendirme)

``` python
from typing import Protocol

class Flyable(Protocol):
    def fly(self) -> None:
        ...
```

------------------------------------------------------------------------

## ⚠️ Dikkat Edilmesi Gerekenler

-   Runtime'da zorunlu değildir (Python çalışmaya devam eder)
-   Ama `mypy` gibi araçlarla kontrol edilir
-   Aşırı kullanmak kodu karmaşıklaştırabilir

------------------------------------------------------------------------

## 🛠️ Typing Kontrol Araçları

-   mypy
-   pyright
-   IDE (VSCode, PyCharm)

------------------------------------------------------------------------
