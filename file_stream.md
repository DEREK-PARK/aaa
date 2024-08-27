`ifstream`, `ofstream`, `fstream`은 C++에서 파일 입출력을 처리하기 위해 사용하는 세 가지 주요 스트림 클래스입니다. 이들은 각각 파일의 입력, 출력, 또는 둘 다를 처리하기 위해 사용됩니다. 각 클래스의 주요 차이점과 용도를 아래에 설명하겠습니다.

### 1. **`ifstream` (Input File Stream)**
- **용도**: 파일에서 데이터를 읽어올 때 사용합니다.
- **기본 모드**: `ios::in` (읽기 전용 모드)
- **특징**:
  - 파일을 열 때 기본적으로 파일이 존재해야 하며, 파일이 없으면 스트림이 열리지 않습니다.
  - 파일의 내용을 프로그램 내로 가져와 처리할 때 사용됩니다.

#### **`ifstream` 사용 예시**
```cpp
#include <iostream>
#include <fstream>
#include <string>

int main() {
    std::ifstream inFile("example.txt");
    if (!inFile) {
        std::cerr << "파일 열기 실패" << std::endl;
        return 1;
    }

    std::string line;
    while (std::getline(inFile, line)) {
        std::cout << line << std::endl;
    }

    inFile.close();
    return 0;
}
```

### 2. **`ofstream` (Output File Stream)**
- **용도**: 파일에 데이터를 쓸 때 사용합니다.
- **기본 모드**: `ios::out` (쓰기 전용 모드)
- **특징**:
  - 파일을 열 때, 파일이 존재하지 않으면 새 파일을 생성합니다.
  - 파일이 존재하면 기본적으로 기존 파일의 내용을 덮어씁니다(기존 내용을 유지하고 뒤에 덧붙이려면 `ios::app` 플래그를 추가).
  - 데이터를 프로그램에서 파일로 출력할 때 사용됩니다.

#### **`ofstream` 사용 예시**
```cpp
#include <iostream>
#include <fstream>
#include <string>

int main() {
    std::ofstream outFile("example.txt");
    if (!outFile) {
        std::cerr << "파일 열기 실패" << std::endl;
        return 1;
    }

    std::string text = "Hello, World!\n";
    outFile << text;

    outFile.close();
    return 0;
}
```

### 3. **`fstream` (File Stream)**
- **용도**: 파일에서 데이터를 읽고 쓸 때 모두 사용됩니다.
- **기본 모드**: `ios::in | ios::out` (읽기/쓰기 모드)
- **특징**:
  - `fstream`은 `ifstream`과 `ofstream`의 기능을 모두 포함하고 있으며, 파일을 읽고 쓰는 작업을 동시에 처리할 수 있습니다.
  - 파일이 존재하지 않으면 파일을 생성하며, 기본적으로 파일을 열 때 덮어쓰기 모드로 열립니다.
  - 파일을 읽기와 쓰기가 모두 필요한 경우에 사용됩니다.

#### **`fstream` 사용 예시**
```cpp
#include <iostream>
#include <fstream>
#include <string>

int main() {
    std::fstream file("example.txt", std::ios::in | std::ios::out | std::ios::app);
    if (!file) {
        std::cerr << "파일 열기 실패" << std::endl;
        return 1;
    }

    // 파일에 쓰기
    file << "Appending this text.\n";

    // 파일의 현재 위치를 다시 파일의 시작으로 이동
    file.seekg(0);

    // 파일 읽기
    std::string line;
    while (std::getline(file, line)) {
        std::cout << line << std::endl;
    }

    file.close();
    return 0;
}
```

### **정리**
- **`ifstream`**: 파일로부터 데이터를 **읽기** 전용으로 사용하는 스트림 클래스입니다.
- **`ofstream`**: 파일에 데이터를 **쓰기** 전용으로 사용하는 스트림 클래스입니다.
- **`fstream`**: 파일에서 **읽기**와 **쓰기**를 동시에 수행할 수 있는 스트림 클래스입니다.

이들 클래스는 각각의 용도에 맞게 사용되며, `fstream`은 두 기능이 모두 필요한 경우 적합합니다. 각 스트림 클래스는 파일의 입출력 작업을 보다 안전하고 직관적으로 처리할 수 있도록 설계되었습니다.
