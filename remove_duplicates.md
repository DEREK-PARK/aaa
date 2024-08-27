 **중복된 요소를 제거하는 문제**를 다뤄보겠습니다. 이 문제는 시간 복잡도를 개선하는 데 있어 유용하며, 정렬이 필요 없는 문제입니다.

### **문제 설명**
주어진 배열에서 중복된 요소를 제거하고, 중복이 없는 요소들만 포함된 새로운 배열을 반환하는 문제입니다. 

### **1. 개선 전: 중복 제거 (O(N^2))**

기본적인 방법은 중복된 요소가 있는지 배열을 반복적으로 확인하는 것입니다. 이 방법은 시간 복잡도가 \(O(N^2)\)로 비효율적입니다.

#### **중복 제거 (O(N^2)) 코드 예제**

```cpp
#include <iostream>

using namespace std;

int removeDuplicates(int arr[], int size) {
    int newSize = size;
    for (int i = 0; i < newSize; ++i) {
        for (int j = i + 1; j < newSize; ++j) {
            if (arr[i] == arr[j]) {
                // Shift elements to the left
                for (int k = j; k < newSize - 1; ++k) {
                    arr[k] = arr[k + 1];
                }
                --newSize;
                --j; // Check the new element at position j
            }
        }
    }
    return newSize;
}

void printArray(int arr[], int size) {
    for (int i = 0; i < size; ++i) {
        cout << arr[i] << " ";
    }
    cout << endl;
}

int main() {
    int arr[] = {1, 2, 2, 3, 4, 4, 5};
    int size = sizeof(arr) / sizeof(arr[0]);
    int newSize = removeDuplicates(arr, size);

    cout << "Array after removing duplicates: ";
    printArray(arr, newSize);

    return 0;
}
```

### **2. 개선 후: 중복 제거 (O(N))**

해시 집합을 사용하여 중복을 제거할 수 있습니다. 해시 집합은 요소의 존재 여부를 O(1) 시간 복잡도로 확인할 수 있어 중복 제거를 효율적으로 수행할 수 있습니다.

#### **중복 제거 (O(N)) 코드 예제**

C++98에서는 `std::set`을 사용할 수 있습니다. `std::set`은 자동으로 중복을 제거해줍니다.

```cpp
#include <iostream>
#include <set>

using namespace std;

int removeDuplicates(int arr[], int size) {
    set<int> uniqueElements;
    
    for (int i = 0; i < size; ++i) {
        uniqueElements.insert(arr[i]);
    }

    int index = 0;
    for (set<int>::iterator it = uniqueElements.begin(); it != uniqueElements.end(); ++it) {
        arr[index++] = *it;
    }

    return uniqueElements.size();
}

void printArray(int arr[], int size) {
    for (int i = 0; i < size; ++i) {
        cout << arr[i] << " ";
    }
    cout << endl;
}

int main() {
    int arr[] = {1, 2, 2, 3, 4, 4, 5};
    int size = sizeof(arr) / sizeof(arr[0]);
    int newSize = removeDuplicates(arr, size);

    cout << "Array after removing duplicates: ";
    printArray(arr, newSize);

    return 0;
}
```

### **설명**

#### **중복 제거 (O(N^2))**:
- **작동 원리**: 배열의 각 요소를 반복적으로 비교하여 중복된 요소를 찾고 제거합니다. 중복된 요소를 발견하면 배열을 왼쪽으로 이동시켜 크기를 줄입니다.
- **문제점**: 배열의 각 요소를 다른 모든 요소와 비교하므로 시간 복잡도가 \(O(N^2)\)입니다. 배열 크기가 클수록 성능이 저하됩니다.

#### **중복 제거 (O(N))**:
- **작동 원리**: `std::set`을 사용하여 배열의 각 요소를 집합에 삽입합니다. 집합은 자동으로 중복을 제거해주며, 삽입 및 검색 연산이 평균적으로 O(1) 시간 복잡도를 가집니다.
- **장점**: 시간 복잡도가 \(O(N)\)으로, 중복 제거가 훨씬 빠릅니다. 배열을 처리할 때 해시 집합을 사용하여 중복된 값을 효율적으로 제거할 수 있습니다.

### **주요 포인트**

- **해시 집합 사용**: 해시 집합을 사용하면 중복된 값을 쉽게 제거할 수 있으며, 시간 복잡도가 줄어듭니다.
- **기본 배열 방법의 비효율성**: 기본적인 중복 제거 방법은 시간 복잡도가 높아 비효율적입니다.

이 방법은 정렬이 필요하지 않고, 데이터를 처리하는 데 있어 성능을 크게 개선할 수 있는 좋은 예제입니다. 해시 집합을 사용하여 중복 제거를 더 효율적으로 수행할 수 있습니다.
