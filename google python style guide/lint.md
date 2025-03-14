## 2.1 Lint
이 [pylintrc](https://google.github.io/styleguide/pylintrc)를 사용하여 코드에 `pylint` 를 실행하세요. 

### 2.1.1 정의
`pylint` 는 Python 소스 코드에서 버그와 스타일 문제를 찾아주는 도구입니다. C나 C++처럼 정적 언어에서 컴파일러가 감지하는는 문제들을 찾아냅니다. 그러나 Python은 동적 특성을 갖고 있기 때문에 일부 경고가 부정확할 수도 있으나 이런 잘못된 경고는 비교적 드물게 발생합니다. 

### 2.1.2 장점
철자 오류, 변수 할당 전에 사용 등의 쉽게 놓칠 수 있는 오류를 잡아줍니다.


### 2.1.3 단점
`pylint` 는 완벽하지 않습니다. 이를 효과적으로 활용하려면 때때로 코드 스타일을 조정하거나, 경고를 무시하거나, 직접 수정해야 할 수도 있습니다.

### 2.1.4 권장 사항
코드에 `pylint` 를 반드시 실행하세요.

부적절한 경고로 인해 다른 중요한 문제가 가려지지 않도록 하세요. 경고를 숨기려면 줄 단위 주석을 사용할 수 있습니다:

```python
def do_PUT(self):  # WSGI 이름이므로 pylint: disable=invalid-name을 사용하세요.
```

`pylint` 경고는 각각 기호 이름 (empty-docstring) 으로 식별됩니다. Google에서 정의한 경고는 `g-` 로 시작합니다.

억제하는 이유가 기호 이름만으로 명확하지 않다면 설명을 추가하세요.

이러한 방식으로 경고를 숨기면 나중에 쉽게 검색하고 다시 검토할 수 있다는 장점이 있습니다.

다음 방법으로 `pylint` 경고 목록을 확인할 수 있습니다:

```bash
pylint --list-msgs
```

특정 메시지에 대한 자세한 정보를 얻으려면 다음을 사용하세요:

```bash
pylint --help-msg=invalid-name
```

`pylint: disable-msg` 는 더이상 사용되지 않으므로 대신 `pylint: disable` 을 사용하는 것이 좋습니다.

사용되지 않는 인자에 대한 경고는 함수의 시작 부분에서 해당 변수를 삭제하여 제거할 수 있습니다. 이때 삭제하는 이유를 설명하는 주석을 반드시 포함하세요. "Unused."와 같은 간단한 설명이면 충분합니다. 예를 들어:

```python
def viking_cafe_order(spam: str, beans: str, eggs: str | None = None) -> str:
    del beans, eggs  # Unused by vikings (viking에는 사용되지 않음)
    return spam + spam + spam
```

이 경고를 억제하는 다른 일반적인 방법으로는 사용되지 않는 인자의 식별자로 `_` 를 사용하거나, 인자 이름 앞에 `unused_` 를 접두어로 붙이거나, 이를 `_`에 할당하는 방식이 있습니다. 이런 방식은 허용되지만 더 이상 권장되지 않습니다. 인자를 이름으로 전달하는 호출자와의 호환성을 깨뜨릴 수 있으며 인자가 실제로 사용되지 않는다는 것을 보장하지 않기 때문입니다.