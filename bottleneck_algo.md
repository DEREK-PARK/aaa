"O(N^2) 알고리즘을 O(N log N)으로 개선"이라는 주제로 성능 병목을 해결하는 예제를 만들겠습니다. 예제에서는 두 가지 알고리즘을 사용하여 동일한 문제를 해결할 것입니다. 먼저, 비효율적인 O(N^2) 알고리즘을 구현하고, 그 다음에는 더 효율적인 O(N log N) 알고리즘으로 개선하겠습니다.

### **문제 정의**

주어진 배열에서 두 수의 합이 특정 값 `target`과 일치하는 두 수를 찾는 문제를 다루겠습니다. 이 문제는 다양한 방법으로 해결할 수 있습니다.

### **1. O(N^2) 알고리즘 (비효율적)**

이 알고리즘은 배열의 모든 쌍을 확인하여 합이 `target`과 일치하는지를 확인합니다.

```cpp
#include <iostream>
#include <vector>

using namespace std;

// O(N^2) 알고리즘
bool findPairWithSum(const vector<int>& arr, int target) {
    int n = arr.size();
    for (int i = 0; i < n; ++i) {
        for (int j = i + 1; j < n; ++j) {
            if (arr[i] + arr[j] == target) {
                return true;  // 쌍을 찾았음
            }
        }
    }
    return false;  // 쌍을 찾지 못함
}

int main() {
    vector<int> arr = {2, 7, 11, 15};
    int target = 9;

    if (findPairWithSum(arr, target)) {
        cout << "쌍을 찾았습니다!" << endl;
    } else {
        cout << "쌍을 찾지 못했습니다." << endl;
    }

    return 0;
}
```

### **설명**

- **시간 복잡도**: O(N^2). 이중 루프를 통해 모든 가능한 쌍을 검사합니다.
- **문제**: 배열의 크기가 커지면 성능이 급격히 나빠집니다. 예를 들어, 1000개의 요소가 있는 경우, 최대 499,500번의 비교가 필요합니다.

### **2. O(N log N) 알고리즘 (효율적)**

이 알고리즘은 배열을 정렬한 후, 두 포인터를 사용하여 효율적으로 쌍을 찾습니다.

```cpp
#include <iostream>
#include <vector>
#include <algorithm>  // sort

using namespace std;

// O(N log N) 알고리즘
bool findPairWithSum(vector<int> arr, int target) {
    sort(arr.begin(), arr.end());  // 배열을 정렬합니다

    int left = 0;
    int right = arr.size() - 1;

    while (left < right) {
        int sum = arr[left] + arr[right];
        if (sum == target) {
            return true;  // 쌍을 찾았음
        } else if (sum < target) {
            ++left;  // 합이 작으면 왼쪽 포인터를 오른쪽으로 이동
        } else {
            --right;  // 합이 크면 오른쪽 포인터를 왼쪽으로 이동
        }
    }
    return false;  // 쌍을 찾지 못함
}

int main() {
    vector<int> arr = {2, 7, 11, 15};
    int target = 9;

    if (findPairWithSum(arr, target)) {
        cout << "쌍을 찾았습니다!" << endl;
    } else {
        cout << "쌍을 찾지 못했습니다." << endl;
    }

    return 0;
}
```

### **설명**

- **시간 복잡도**: O(N log N). 정렬에 O(N log N) 시간이 소요되며, 이후 두 포인터를 사용하여 O(N) 시간에 해결합니다.
- **장점**: 배열을 정렬한 후 두 포인터를 사용하여 쌍을 효율적으로 찾을 수 있습니다. 이는 O(N^2) 알고리즘에 비해 훨씬 더 빠릅니다.

### **비교**

1. **비효율적 알고리즘 (O(N^2))**:
   - **장점**: 구현이 간단합니다.
   - **단점**: 배열이 클 경우 성능이 급격히 저하됩니다.

2. **효율적 알고리즘 (O(N log N))**:
   - **장점**: 정렬과 두 포인터 접근 방식을 사용하여 성능이 훨씬 개선됩니다.
   - **단점**: 정렬에 시간이 필요하며, 정렬된 배열을 다시 사용할 수 없습니다.

이 두 알고리즘을 비교함으로써 성능 병목 문제를 해결할 수 있는 다양한 접근 방식을 이해할 수 있으며, 효율적인 알고리즘이 어떻게 문제 해결 속도를 개선하는지 확인할 수 있습니다.
