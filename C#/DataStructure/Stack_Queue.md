# 스택 & 큐

## 스택
후입선출(LIFO) 방식의 자료구조로, 가장 최신 입력된 순서대로 처리해야 하는 상황에 사용한다

## 스택의 구현

리스트의 사용법만 다르게 해서 구현이 가능하다.

           - 삽입 -
                   top                      top
                    ↓                        ↓
           ┌─┬─┬─┬─┬─┬─┬─┬─┐      ┌─┬─┬─┬─┬─┬─┬─┬─┐
           │1│2│3│4│5│ │ │ │  =>  │1│2│3│4│5│6│ │ │
           └─┴─┴─┴─┴─┴─┴─┴─┘      └─┴─┴─┴─┴─┴─┴─┴─┘
          
           - 삭제 -
                     top                  top
                      ↓                    ↓
           ┌─┬─┬─┬─┬─┬─┬─┬─┐      ┌─┬─┬─┬─┬─┬─┬─┬─┐
           │1│2│3│4│5│6│ │ │  =>  │1│2│3│4│5│ │ │ │
           └─┴─┴─┴─┴─┴─┴─┴─┘      └─┴─┴─┴─┴─┴─┴─┴─┘

## 스택의 사용
```C#
using System.Collections.Generic;
static void Main()
{
    Stack<int> stack = new Stack<int>();

    for (int i = 0; i < 5; i++)
    {
        stack.Push(i);  //  O(1) 집어넣기
    }

    Console.WriteLine(stack.Peek());   // O(1) 다음으로 나올 

    while (stack.Count > 0)
    {
        Console.WriteLine(stack.Pop());   // O(1) 꺼내기
    }
}

```
### 사용처
- 이전의 작업을 취소해서 그 직전 작업으로 돌아가기 위한 상황 
- 후입선출이 요구되는 상황에서 다양하게 활용 가능

## 큐

선입선출(FIFO) 방식의 자료구조로, 입력된 순서대로 처리해야 하는 상황에 사용한다.

## 큐의 구현

           <큐 구현>
           1. 배열 사용
           선입선출(FIFO), 후입후출(LILO) 을 구현하기 위해 배열을 생성하고 순차적으로 데이터를 배치
               ┌─┬─┬─┬─┬─┬─┬─┬─┐
            앞 │1│2│3│4│5│ │ │ │  뒤
               └─┴─┴─┴─┴─┴─┴─┴─┘
          
           - 삽입 -
           비어있는 가장 뒷쪽에 데이터를 배치
            ┌─┬─┬─┬─┬─┬─┬─┬─┐        ┌─┬─┬─┬─┬─┬─┬─┬─┐
            │1│2│3│4│5│ │ │ │   =>   │1│2│3│4│5│6│ │ │
            └─┴─┴─┴─┴─┴─┴─┴─┘        └─┴─┴─┴─┴─┴─┴─┴─┘
          
           - 삭제 -
           가장 앞쪽 데이터를 출력하고 빈자리를 채우기 위해 나머지 데이터를 앞당기기 진행
            ┌─┬─┬─┬─┬─┬─┬─┬─┐        ┌─┬─┬─┬─┬─┬─┬─┬─┐
            │1│2│3│4│5│6│ │ │   =>   │2│3│4│5│6│ │ │ │
            └─┴─┴─┴─┴─┴─┴─┴─┘        └─┴─┴─┴─┴─┴─┴─┴─┘
          
           - 문제발생 -
           큐의 삭제 과정시 나머지 데이터를 앞당겨야하는 N번의 작업 발생
            ┌─┬─┬─┬─┬─┬─┬─┬─┐        ┌─┬─┬─┬─┬─┬─┬─┬─┐        ┌─┬─┬─┬─┬─┬─┬─┬─┐
            │1│2│3│4│5│6│ │ │   =>   │ │2│3│4│5│6│ │ │   =>   │2│3│4│5│6│ │ │ │
            └─┴─┴─┴─┴─┴─┴─┴─┘        └─┴─┴─┴─┴─┴─┴─┴─┘        └─┴─┴─┴─┴─┴─┴─┴─┘

           2. 전단 & 후단
           삽입 & 삭제 시 데이터를 앞당기지 않고 head와 tail을 표시하여 삽입할 위치와 삭제할 위치를 지정
          
           - 삽입 -
           tail 위치에 데이터를 추가하고 tail을 한칸 뒤로 이동
               h       t                h         t
               ↓       ↓                ↓         ↓      
            ┌─┬─┬─┬─┬─┬─┬─┬─┐        ┌─┬─┬─┬─┬─┬─┬─┬─┐
            │ │2│3│4│5│ │ │ │   =>   │ │2│3│4│5│6│ │ │
            └─┴─┴─┴─┴─┴─┴─┴─┘        └─┴─┴─┴─┴─┴─┴─┴─┘
          
           - 삭제 -
           head 위치에 데이터를 추가하고 head을 한칸 뒤로 이동
               h         t                h       t
               ↓         ↓                ↓       ↓
            ┌─┬─┬─┬─┬─┬─┬─┬─┐        ┌─┬─┬─┬─┬─┬─┬─┬─┐
            │ │2│3│4│5│6│ │ │   =>   │ │ │3│4│5│6│ │ │
            └─┴─┴─┴─┴─┴─┴─┴─┘        └─┴─┴─┴─┴─┴─┴─┴─┘
          
           - 문제발생 -
           큐의 배열 마지막 위치까지 사용하는 경우 빈자리가 없어 저장 불가한 상황 발생
                 h         t              h           t
                 ↓         ↓              ↓           ↓
            ┌─┬─┬─┬─┬─┬─┬─┬─┐        ┌─┬─┬─┬─┬─┬─┬─┬─┐
            │ │ │3│4│5│6│7│ │   =>   │ │ │3│4│5│6│7│8│
            └─┴─┴─┴─┴─┴─┴─┴─┘        └─┴─┴─┴─┴─┴─┴─┴─┘

           3. 순환배열
           배열의 끝까지 도달하여 빈자리가 없을 경우 처음으로 돌아가서 빈공간을 활용
          
           - 마지막위치 도달시 -
           다시 가장 앞 위치를 사용하여 빈공간을 재활용
                    h     t          t       h           
                    ↓     ↓          ↓       ↓           
           ┌─┬─┬─┬─┬─┬─┬─┬─┐        ┌─┬─┬─┬─┬─┬─┬─┬─┐
           │ │ │ │ │5│6│7│ │   =>   │ │ │ │ │5│6│7│8│
           └─┴─┴─┴─┴─┴─┴─┴─┘        └─┴─┴─┴─┴─┴─┴─┴─┘
          
           - 문제발생 -
           tail이 head을 침범하는 경우 모든 공간이 비어있는 상황과 가득차 있는 상황을 구분할 수 없음
           
                   th                       th       
                   ↓↓                       ↓↓       
           ┌─┬─┬─┬─┬─┬─┬─┬─┐        ┌─┬─┬─┬─┬─┬─┬─┬─┐
           │ │ │ │ │ │ │ │ │        │5│6│7│8│1│2│3│4│
           └─┴─┴─┴─┴─┴─┴─┴─┘        └─┴─┴─┴─┴─┴─┴─┴─┘
             비어있는 경우             가득찬 경우

           4. 포화상태확인
           head와 tail이 일치하는 경우를 비어있는 경우로 판정
           tail이 head 전위치에 있는 경우를 실제로는 한자리가 비어있지만 가득찬 경우로 판정
                   th                      t h       
                   ↓↓                      ↓ ↓       
           ┌─┬─┬─┬─┬─┬─┬─┬─┐        ┌─┬─┬─┬─┬─┬─┬─┬─┐
           │ │ │ │ │ │ │ │ │        │5│6│7│ │1│2│3│4│
           └─┴─┴─┴─┴─┴─┴─┴─┘        └─┴─┴─┴─┴─┴─┴─┴─┘
             비어있는 경우         가득찬 경우(로 판정)


## 큐의 구현

```C#
using System.Collections.Generic;
static void Main()
{
    Queue<int> queue = new Queue<int>();

    for (int i = 0; i < 5; i++)
    {
        queue.Enqueue(i); // O(1) 데이터 넣기
    }

    Console.WriteLine(queue.Peek()); // O(1) 다음으로 나올 데이터 확인

    while (queue.Count > 0)
    {
        Console.WriteLine(queue.Dequeue()); //O(1) 데이터 꺼내기
    }
}
```

