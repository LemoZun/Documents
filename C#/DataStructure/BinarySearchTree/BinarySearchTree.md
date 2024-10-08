# 이진 탐색 트리(Binary Search Tree)

### 목표
1. 이진탐색트리에 대하여 조사한 후 해당 개념에 대하여 서술
2. 이진탐색트리의 구현원리 구조, 삽입 & 삭제 & 탐색 과정
3. 이진탐색트리의 전위순회, 중위순회, 후위순회에 대해 조사하고 정렬이 보장되는 순회방식을 조사
4. 이진탐색트리의 불균형 문제에 대해 조사하고 이를 해결하기 위한 방법에 대해 조사

## 이진 탐색 트리의 정의
이진탐색트리는 계층적인 자료를 표현하는 트리의 한 종류로 각각의 노드가 최대 두개의 자식노드를 가지는 이진트리이다. 부모 노드를 기준으로 조건에 만족하면 왼쪽, 그렇지 않다면 오른쪽 자식으로 보낸다.

![이진탐색트리](binarySearchTree1.gif) <br>
다음은 부모 노드보다 숫자가 작다면 왼쪽으로, 그렇지 않다면 오른쪽 노드로 보내는 이진탐색트리이다.

### 이진 탐색 트리의 삽입 삭제 탐색 과정

1. **삽입** <br>
이진 탐색 트리에서의 삽입은 우선 루트 노드가 존재하는지 부터 시작한다.   
      1. 루트노드가 없다면 루트 노드를 생성하고 종료한다.   
      2. 루트노드가 있다면 노드를 순회하며 삽입할 값과 현재 노드의 값을 비교하고 삽입할 값이 현재 노드보다 작다면 왼쪽 서브트리로 이동하고, 현재노드보다 크다면 오른쪽 서브트리로 이동하는 과정을 반복한다.   
      3. 도달한 곳에 노드가 없다면 새 노드를 생성한 후 삽입할 값을 할당하고 해당 위치에 삽입한다.   <br>
   
시간복잡도의 경우 평균적인 경우 자식 노드가 최대 두개이며 자식노드로 내려갈 때마다 절반이 되므로 시간 복잡도는 O(log n) 이며 노드가 한쪽에 치우친 최악의 경우 모든 노드를 내려가며 탐색해야 하기 때문에 시간 복잡도는 O(n)이다.

2. **삭제** <br>
이진 탐색 트리의 삭제 과정은 세 경우를 고려해야 한다   
       1. 자식이 없는 노드일 경우 : 삭제할 노드를 그대로 제거한다.   
       2. 자식이 하나인 노드 : 노드를 제거하고 자식 노드를 부모 노드에 연결한다.   
       3. 자식이 두개인 노드 : 오른쪽 서브 트리의 가장 작은값 혹은 왼쪽 서브트리의 가장 큰 값으로 대체하고 해당값을 가진 노드를 삭제한다.

시간복잡도의 경우 삽입과 동일한 이유로 평균적인 경우 O(log n)이며 최악인 경우 O(n)이다. 

3. **탐색** <br>
