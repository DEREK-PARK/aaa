C++에는 몇 가지 유사한 표준 스트림이 있습니다. 이들은 각각 다른 용도로 사용되며, 표준 입력 및 출력 처리를 위한 다양한 기능을 제공합니다.


### **1. `cout` (Standard Output Stream)**
- **용도**: 표준 출력 스트림으로, 일반적인 출력(예: 프로그램 결과, 사용자 메시지 등)을 화면에 표시할 때 사용됩니다.
- **버퍼링**: `cout`은 **버퍼링**이 되어 있어서 출력이 효율적으로 관리됩니다. 즉, 출력 데이터는 버퍼에 저장되었다가, 버퍼가 가득 차거나 프로그램이 종료되거나 `flush`가 호출되면 화면에 출력됩니다.
- **예시**:
    ```cpp
    #include <iostream>

    int main() {
        std::cout << "Hello, World!" << std::endl;
        return 0;
    }
    ```
    - 이 코드에서 `cout`은 "Hello, World!"를 화면에 출력합니다.

### **2. `cerr` (Standard Error Stream)**
- **용도**: 표준 에러 스트림으로, 오류 메시지나 중요한 경고를 출력할 때 사용됩니다. 주로 디버깅 목적으로 사용되며, `cout`과는 다르게 즉시 화면에 출력됩니다.
- **버퍼링**: `cerr`은 **버퍼링되지 않은(unbuffered)** 스트림입니다. 즉, 출력되는 데이터가 즉시 화면에 표시됩니다. 이는 오류 메시지가 가능한 한 빨리 사용자의 눈에 띄게 하기 위함입니다.
- **예시**:
    ```cpp
    #include <iostream>

    int main() {
        std::cerr << "An error occurred!" << std::endl;
        return 0;
    }
    ```
    - 이 코드에서 `cerr`은 "An error occurred!"라는 오류 메시지를 화면에 즉시 출력합니다.

### **3. `cin` (Standard Input Stream)**
- **용도**: 표준 입력 스트림으로, 사용자로부터 데이터를 입력받을 때 사용됩니다. 기본적으로 키보드 입력을 처리합니다.
- **예시**:
    ```cpp
    #include <iostream>

    int main() {
        int number;
        std::cout << "Enter a number: ";
        std::cin >> number;
        std::cout << "You entered: " << number << std::endl;
        return 0;
    }
    ```
    - 이 코드에서 `cin`은 사용자가 입력한 숫자를 받아 `number` 변수에 저장합니다.

### **4. `clog` (Standard Log Stream)**
- **용도**: 표준 로그 스트림으로, 일반적인 정보 메시지나 로그 메시지를 출력할 때 사용됩니다. `cerr`와 비슷하게 에러나 경고보다 덜 긴급한 메시지를 출력하는 데 사용됩니다.
- **버퍼링**: `clog`은 **버퍼링**됩니다. 따라서 `cout`과 같이 출력이 버퍼에 저장되었다가 일정 시점에 출력됩니다.
- **예시**:
    ```cpp
    #include <iostream>

    int main() {
        std::clog << "This is a log message." << std::endl;
        return 0;
    }
    ```
    - 이 코드에서 `clog`은 "This is a log message."라는 로그 메시지를 버퍼링 후 출력합니다.
`cout`과 `cerr`는 C++에서 콘솔에 출력을 하기 위해 사용되는 두 가지 표준 스트림입니다. 이 두 스트림의 주요 차이점은 출력되는 데이터의 용도와 처리 방식에 있습니다.

### **스트림 요약**
- **`cout`**: 일반적인 출력. 버퍼링됨. 표준 출력 스트림.
- **`cerr`**: 오류 메시지 출력. 버퍼링되지 않음. 표준 에러 스트림.
- **`cin`**: 사용자 입력을 처리. 표준 입력 스트림.
- **`clog`**: 일반적인 로그 메시지 출력. 버퍼링됨. 로그 출력용.

이 스트림들은 모두 `iostream` 헤더에 정의되어 있으며, 각각의 용도에 따라 적절히 사용됩니다. `cout`, `cerr`, `clog`은 모두 출력 스트림이지만, 그 목적과 버퍼링 처리 방식에 따라 다르게 활용됩니다. `cin`은 입력을 담당하는 스트림으로, 프로그램에서 사용자 입력을 받을 때 기본적으로 사용됩니다.
