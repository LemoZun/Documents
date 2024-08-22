# 연결리스트

## 순차리스트 사용의 단점

리스트는 배열 기반이기 때문에 연속적으로 저장되어야하는 특징을 가지고있다. <br> 중간에 데이터를 추가해야 하는 Insert 나 삭제하는 Remove인 경우 데이터의 추가적인 이동이 필요하다.
연결리스트는 이러한 상황에 유용 할 수 있다.

## 연결리스트란

- 데이터를 포함하는 노드들을 연결식으로 만든 자료구조
-  데이터와 다른 데이터 지점의 참조 변수를 가진 노드를 기본 단위로 사용한다.
-  데이터를 노드를 통해 연결식으로 구성해서 데이터의 `추가와 삭제가 용이`하다.
-  노드가 메모리에 연속적으로 배치되지 않고 `연결 구조`로 다른데이터의 위치를 확인한다.

## 연결리스트의 특징
- 데이터를 연속적으로 배치하는 배열과 다르게 연결식으로 구성된다.
- 데이터의 추가/삭제 과정에서 다른 데이터의 위치와 무관하게 진행된다.
- 연속적인 데이터 배치가 아니기 때문에 `탐색 과정`에서 인덱스 사용이 불가능하며, `처음부터 탐색`해야 한다.


        <연결 리스트의 시간 복잡도>

         접근    탐색    삽입    삭제
         O(n)    O(n)    O(1)    O(1)

## 연결리스트의 구현

연결리스트는 노드를 기본 단위로 연결식으로 구현된다. <br>
노드간의 연결구조에 따라 단방향, 양방향, 환형 으로 구분됨.
           
           
          
           1. 단방향 연결리스트
           노드가 다음 노드를 참조
           ┌────┬─┐  ┌────┬─┐  ┌────┬─┐  ┌────┬─┐
           │Data│───→│Data│───→│Data│───→│Data│ │
           └────┴─┘  └────┴─┘  └────┴─┘  └────┴─┘
          
           2. 양방향 연결리스트
           노드가 이전/다음 노드를 참조
           ┌─┬────┬─┐  ┌─┬────┬─┐  ┌─┬────┬─┐  ┌─┬────┬─┐
           │ │Data│←────→│Data│←────→│Data│←────→│Data│ │
           └─┴────┴─┘  └─┴────┴─┘  └─┴────┴─┘  └─┴────┴─┘
          
           3. 환형 연결리스트
           노드가 이전/다음 노드를 참조하며, 시작 노드와 마지막 노드를 참조
            ┌──────────────────────────────────────────┐
           ┌│┬────┬─┐  ┌─┬────┬─┐  ┌─┬────┬─┐  ┌─┬────┬│┐
           │↓│Data│←────→│Data│←────→│Data│←────→│Data│↓│
           └─┴────┴─┘  └─┴────┴─┘  └─┴────┴─┘  └─┴────┴─┘


           <연결리스트 삽입>
           새로 추가하는 노드가 이전/이후 노드를 참조한 뒤
           이전/이후 노드가 새로 추가하는 노드를 참조함
           
                    ┌─┬───┬─┐                      ┌─┬───┬─┐                      ┌─┬───┬─┐ 
                    │ │ C │ │                    ┌───│ C │───┐                  ┌───│ C │───┐
                    └─┴───┴─┘          =>        ↓ └─┴───┴─┘ ↓        =>        ↓ └─┴───┴─┘ ↓
           ┌─┬───┬─┐         ┌─┬───┬─┐    ┌─┬───┬─┐         ┌─┬───┬─┐    ┌─┬───┬─┐ ↑     ↑ ┌─┬───┬─┐
           │ │ A │←───────────→│ B │ │    │ │ A │←───────────→│ B │ │    │ │ A │───┘     └───│ B │ │
           └─┴───┴─┘         └─┴───┴─┘    └─┴───┴─┘         └─┴───┴─┘    └─┴───┴─┘         └─┴───┴─┘


           <연결리스트 삭제>
           삭제하는 노드의 이전 노드가 이후 노드를 참조한 뒤
           삭제하는 노드의 이후 노드가 이전 노드를 참조함
           
                    ┌─┬───┬─┐                      ┌─┬───┬─┐                      ┌─┬───┬─┐
                  ┌──→│ C │←──┐                    │ │ C │←──┐                    │ │ C │ │
                  │ └─┴───┴─┘ │        =>          └─┴───┴─┘ │        =>          └─┴───┴─┘
           ┌─┬───┬│┐         ┌│┬───┬─┐    ┌─┬───┬─┐         ┌│┬───┬─┐    ┌─┬───┬─┐         ┌─┬───┬─┐
           │ │ A │↓│         │↓│ B │ │    │ │ A │──────────→│↓│ B │ │    │ │ A │←───────────→│ B │ │
           └─┴───┴─┘         └─┴───┴─┘    └─┴───┴─┘         └─┴───┴─┘    └─┴───┴─┘         └─┴───┴─┘




## 연결리스트의 사용

```C#
using System.Collections.Generic;
static void Main(string[] args)
 {
     LinkedList<int> linkedList = new LinkedList<int>();

     LinkedListNode<int> node1 = linkedList.AddFirst(1); //첫자리에 삽입
     LinkedListNode<int> node2 = linkedList.AddFirst(2);
     LinkedListNode<int> node3 = linkedList.AddLast(3); // 맨 끝에 삽입
     LinkedListNode<int> node4 = linkedList.AddLast(4);

     //인덱스가 없어 노드를 기준으로
     //node2     node1       node3       node4
     //(2)  <->   (1)   <->  (3)    <->   (4)

     //특정 노드를 기준으로 삽입
     LinkedListNode<int> node5 = linkedList.AddBefore(node1, 5);
     LinkedListNode<int> node6 = linkedList.AddAfter(node1, 6);
     //node2      node5       node1       node6       node3       node4
     //(2)   <->   (5)   <->   (1)   <->   (6)   <->   (3)   <->   (4)

     //삭제
     // linkedList.RemoveAt(2); 인덱스가 없기 때문에 RemoveAt은 없다

     linkedList.Remove(3); //O(n) 탐색 후 지우기
     linkedList.Remove(node6); // O(n) 노드 지우기
     //node2      node5       node1        node4
     //(2)   <->   (5)   <->   (1)   <->    (4)

     linkedList.RemoveFirst(); // O(1)
     linkedList.RemoveLast(); // O(1)
     //   node5       node1       
     //    (5)   <->   (1)     

     // 접근 
     LinkedListNode<int> firstNode = linkedList.First; // O(1)
     LinkedListNode<int> lastNode = linkedList.Last;   // O(1)
     LinkedListNode<int> prevNode = node1.Previous;   //  O(1)   노드를 기준으로 접근 가능
     LinkedListNode<int> nextNode = node1.Next;       // O(1)

     // 탐색
     LinkedListNode<int> findNode = linkedList.Find(1); // O(n) 

    //반복
    foreach(int element in linkedList)
    {
        Console.WriteLine(element);
    }   
 }
```


 

