C++의 스트림 클래스 (iostream)에는 다양한 조작자(manipulator)와 플래그(flags)가 있어 출력 포맷을 세밀하게 제어할 수 있습니다. 아래는 이러한 조작자와 플래그들을 최대한 많이 정리한 표입니다. 이들은 주로 iostream, iomanip 헤더에서 제공되며, 데이터의 출력 형식과 관련된 다양한 옵션을 제공합니다.

### **스트림 조작자 및 플래그**
(`using namespace std;`를 미리 선언했다 가정하고 `std::` 은 모두 생략했습니다.)

| 조작자/플래그       | 설명                                              | 예시                                                      |
|---------------------|---------------------------------------------------|-----------------------------------------------------------|
| `hex`               | 16진수 형식으로 출력                              | `cout << hex << 255;` // 0xff                            |
| `dec`               | 10진수 형식으로 출력 (기본값)                     | `cout << dec << 255;` // 255                             |
| `oct`               | 8진수 형식으로 출력                              | `cout << oct << 255;` // 377                             |
| `showbase`          | 숫자 앞에 진법을 나타내는 접두사 (0x, 0o) 출력    | `cout << showbase << hex << 255;` // 0xff                 |
| `noshowbase`        | 숫자 앞에 진법 접두사 출력 안 함 (기본값)         | `cout << noshowbase << hex << 255;` // ff                  |
| `fixed`             | 소수점 이하 자리수를 고정하여 출력                | `cout << fixed << 3.14159;` // 3.141590                  |
| `scientific`        | 과학적 표기법으로 출력                           | `cout << scientific << 3.14159;` // 3.141590e+00         |
| `setprecision`      | 소수점 이하 자리수를 지정                         | `cout << setprecision(2) << 3.14159;` // 3.14            |
| `setw`              | 출력 필드의 너비를 지정                          | `cout << setw(10) << 123;` // "        123"              |
| `setfill`           | 출력 필드의 빈 공간을 채울 문자 지정              | `cout << setfill('0') << setw(10) << 123;` // "0000000123"|
| `left`              | 출력 정렬을 왼쪽으로 맞춤                        | `cout << left << setw(10) << 123;` // "123       "        |
| `right`             | 출력 정렬을 오른쪽으로 맞춤 (기본값)               | `cout << right << setw(10) << 123;` // "       123"       |
| `internal`          | 출력 정렬을 내부로 맞춤                          | `cout << internal << setw(10) << 123;` // "       123"    |
| `showpoint`         | 소수점 이하에 0을 강제로 표시                    | `cout << showpoint << 1.0;` // 1.0                       |
| `noshowpoint`       | 소수점 이하 0을 표시하지 않음 (기본값)             | `cout << noshowpoint << 1.0;` // 1                        |
| `boolalpha`         | `bool` 값을 `true`/`false`로 출력                  | `cout << boolalpha << true;` // true                     |
| `noboolalpha`       | `bool` 값을 1/0으로 출력 (기본값)                  | `cout << noboolalpha << true;` // 1                      |
| `endl`              | 줄 바꿈 및 버퍼를 비웁니다                         | `cout << "Hello" << endl;` // "Hello\n"                  |
| `flush`             | 버퍼를 비우지만 줄 바꿈은 하지 않음               | `cout << "Hello" << flush;` // "Hello"                   |

### **사용 예시**

```cpp
#include <iostream>
#include <iomanip>

using namespace std;

int main() {
    int number = 255;
    double pi = 3.14159;

    // 16진수 형식으로 출력
    cout << "Hex: " << hex << number << endl; // 0xff

    // 8진수 형식으로 출력
    cout << "Oct: " << oct << number << endl; // 377

    // 소수점 이하 2자리로 출력
    cout << "Fixed: " << fixed << setprecision(2) << pi << endl; // 3.14

    // 과학적 표기법으로 출력
    cout << "Scientific: " << scientific << pi << endl; // 3.141590e+00

    // 출력 필드 너비와 채울 문자 설정
    cout << "Width: " << setw(10) << setfill('0') << number << endl; // 0000000255

    // 출력 정렬
    cout << "Left: " << left << setw(10) << number << "End" << endl; // 255       End
    cout << "Right: " << right << setw(10) << number << "End" << endl; //       255End

    // 불리언 값을 true/false로 출력
    cout << "Boolalpha: " << boolalpha << true << endl; // true

    return 0;
}
```

### **설명**

- **조작자(Manipulators)**: 스트림의 출력 형식을 제어합니다. 예를 들어, `hex`, `dec`, `fixed`, `scientific` 등은 숫자의 형식을 조정합니다.
- **플래그(Flags)**: 스트림의 상태나 동작 방식을 설정합니다. 예를 들어, `showbase`, `noshowbase`, `showpoint` 등은 출력에 추가적인 형식 지정을 제공합니다.
- **버퍼 조작**: `endl`, `flush`는 출력 버퍼를 관리하는 데 사용됩니다. `endl`은 줄 바꿈과 버퍼를 비우며, `flush`는 버퍼만 비우고 줄 바꿈은 하지 않습니다.

이 조작자와 플래그를 사용하면 출력 포맷을 세밀하게 조정할 수 있어, 프로그램의 출력 결과를 더욱 명확하고 원하는 형식으로 제어할 수 있습니다.
