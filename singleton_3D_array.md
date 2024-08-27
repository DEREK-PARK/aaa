텍스트 파일에서 3차원 배열 데이터를 읽어들여 메모리에 저장하고, 프로그램 종료 시 메모리를 해제하는 방법을 보여드리겠습니다.
소멸되지 않았다면 실제제 텍스트 파일을 10번이든 100번이든 불러도 1번만 메모리가 생성됩니다.

### **수정된 코드**

#### **1. 데이터 파일 (`data.txt`)**

3차원 배열을 저장하기 위해 데이터 파일의 형식을 지정해야 합니다. 예를 들어, 각 값은 공백으로 구분됩니다. 파일 내용 예시는 다음과 같습니다:

```
5000 300 20
1 2 3 ... (총 5000*300*20개의 값)
```

#### **2. C++ 코드**

```cpp
#include <iostream>
#include <fstream>
#include <cstdlib>  // For exit()

using namespace std;

class SuperArray {
public:
    static SuperArray* getInstance(const char* filename) {
        if (!instance) {
            instance = new SuperArray(filename);
        }
        return instance;
    }

    ~SuperArray() {
        // 메모리 해제
        for (int i = 0; i < d1; ++i) {
            for (int j = 0; j < d2; ++j) {
                delete[] array[i][j];
            }
            delete[] array[i];
        }
        delete[] array;
    }

    int getValue(int i, int j, int k) const {
        if (i >= 0 && i < d1 && j >= 0 && j < d2 && k >= 0 && k < d3) {
            return array[i][j][k];
        }
        return -1;  // 범위가 벗어난 경우
    }

private:
    SuperArray(const char* filename) {
        ifstream file(filename);
        if (!file) {
            cerr << "파일을 열 수 없습니다: " << filename << endl;
            exit(1);
        }

        // 파일에서 배열의 크기 읽기
        file >> d1 >> d2 >> d3;

        // 동적 메모리 할당
        array = new int**[d1];
        for (int i = 0; i < d1; ++i) {
            array[i] = new int*[d2];
            for (int j = 0; j < d2; ++j) {
                array[i][j] = new int[d3];
            }
        }

        // 배열 값 읽기
        for (int i = 0; i < d1; ++i) {
            for (int j = 0; j < d2; ++j) {
                for (int k = 0; k < d3; ++k) {
                    file >> array[i][j][k];
                }
            }
        }
    }

    static SuperArray* instance;
    int*** array;
    int d1, d2, d3;
};

// 싱글톤 인스턴스 초기화
SuperArray* SuperArray::instance = 0;

int main() {
    // SuperArray의 인스턴스를 얻고 데이터를 사용
    SuperArray* superArray = SuperArray::getInstance("data.txt");

    // 데이터 값 출력 (예: (0, 0, 0) 위치의 값)
    cout << "Value at (0,0,0): " << superArray->getValue(0, 0, 0) << endl;

    // 프로그램이 종료되면 소멸자에 의해 메모리 해제
    return 0;
}
```

### **설명**

1. **싱글톤 패턴**:
   - `SuperArray` 클래스는 싱글톤 패턴을 사용하여 프로그램 내에서 오직 하나의 인스턴스만 생성되도록 합니다.
   - `getInstance` 메서드는 파일에서 3차원 배열 데이터를 읽어 동적 메모리에 저장합니다.

2. **파일 읽기 및 메모리 할당**:
   - `ifstream`을 사용하여 데이터 파일을 읽습니다.
   - 첫 번째 줄에서 배열의 크기 (d1, d2, d3)를 읽고, 이후에 3차원 배열의 값을 읽어 메모리에 저장합니다.

3. **메모리 해제**:
   - `~SuperArray` 소멸자에서 동적으로 할당된 메모리를 해제하여 메모리 누수를 방지합니다.

4. **데이터 접근**:
   - `getValue` 메서드를 통해 배열의 특정 위치에 있는 값을 반환합니다. 배열의 인덱스가 유효하지 않으면 `-1`을 반환합니다.

### **장점**
- **메모리 효율성**: 데이터가 실행 파일에 포함되지 않고 외부 텍스트 파일에서 동적으로 읽어 메모리에 저장됩니다.
- **유지 보수**: 데이터 파일을 수정하면 코드 변경 없이 데이터 값을 업데이트할 수 있습니다.
- **성능**: 데이터가 필요한 경우에만 메모리에 로드하여, 프로그램 실행 중 메모리 사용을 최적화합니다.

이 접근 방식을 통해 3차원 배열을 효과적으로 관리하고, 메모리 사용을 최적화할 수 있습니다.
