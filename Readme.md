### :book: History

---

> 2/13 : 2/14과목평가 대비 개념 정리



<br/>



### 2월 14일 과목평가 준비

공부해야할 내용

> Array, String 
>
> Stack, Queue
>
> Linkedlist
>
> Tree



<br/>

### 

### 완전 검색(Exhaustive Search)

---





### :zap:**순열(Permutaion)**

> 일반적으로 서로다른 N개의 원소 중에서 R개를 뽑아 **한줄로 나열**하는 방법, 알고리즘 분석 기법 중 완전탐색 부분에 해당한다. 서로다른 N명의 후보 중에서 R명을 뽑아 한줄로 줄을 세우는데 뽑힌 사람이 누구인지도 중요하지만 순열에서 가장 중요하게 생각해야하는 부분은 뽑힌 사람들이 **어느 위치에 배치**시키느냐이다. 뽑힌 R명의 사람을 줄을 세울 때 서있는 위치가 바뀌는 경우를 모두 다른 경우로 카운팅 해야한다. 
>
> **반복문**을 사용해서 코드를 작성할 수도 있지만, 뽑아야하는 사람 수에 따라서 반복문이 여러번 겹쳐야 하기 때문에 **고정적이지 않은 변수**에 대해서 처리하기 어려운 부분이 생긴다. 따라서 **재귀**적으로 줄을 세우기 위해 뽑힌 사람의 수를 체크해가며 가능한 모든 방법을 탐색해야한다.

<br/>

**순열 구현**

```java
// 1. 반복문으로 순열 구현 
{1,2,3}을 포함하는 모든 순열 생성;
for(int i=1; i<=3; i++){
    if(int j=1; i-j<=3; j++){
        if(i!=j){
            for(int k=1; k<=3; k++){
                if(k!=i && k!=j){
                    System.out.println(i,j,k);
                }
            }
        }
    }
}
// 2. 재귀로 순열 구현
numbers[] :순열 저장 배열
isSelected[] : 인덱스에 해당하는 숫자가 사용중인지 저장하는 배열
void perm(cnt){
    if(cnt == 3)
        순열 생성 완료;
   	else{
        for(int i=1; i<=3; i++)
            if (isSeleced[i] == true)
                continue;
        	number[cnt] = i;
        	isSelected[i] = true;
        	perm(cnt+1);
        	iseSelected[i] = false;
    }
}

```



<br/><br/>

### :zap:**조합(Combination)**

> 일반적으로 서로다른 N개의 원소 중에서 R개를 **순서없이** 뽑는 가지수를 의미하고, 알고리즘 분석 기법 중 완전탐색 부분에 해당한다. 
>
> 서로 다른 n개의 원소를 가지는 어떤 집합에서 **순서에 상관없이** r개의 원소를 선택하는 것이며, 이는 n개의 원소로 이루어진 집합에서 r개의 원소로 이루어진 부분집합을 만드는 것 혹은 찾는 것과 같다.
>
> 선택의 순서와 상관없이 같은 원소들이 선택되었다면 같은 조합이며 다른 원소들이 선택되었다면 다른 조합이다.

<br/>**조합 구현**

```java
static int N, R;
static int[] input; // 전체 input
static int[] numbers; // 선택된 조합 배열

// 일반적인 조합 nCr
public static void combination1(int cnt, int start) {
    // combination1(0,0);
    if(cnt == R) {
        System.out.println(Arrays.toString(numbers));
        return;
    }
    for(int i=start; i<N; i++) {
        numbers[cnt] = input[i];
        combination(cnt+1, i+1); // 자기 다음 카운트로 재귀
    }
}

// 중복조합 nHr
public static void combination2(int cnt, int start) {
    // combination2(0,0);
    if(cnt == R) {
        System.out.println(Arrays.toString(numbers));
        return;
    }
    for(int i=start; i<N; i++) {
        numbers[cnt] = input[i];
        combination(cnt+1, i); // 자기 자신을 포함해서 재귀
    }
}
```





<br/><br/>

### :zap:**부분집합(Subset)**

> 집합에 포함된 원소들을 선택하는 것이다. 다수의 중요 알고리즘들이 원소들의 그룹에서 최적의 부분 집합을 찾는 것이다.
>
> 부분집합의 수를 계산할 때 원소의 개수가 N개인 집합에서 만들 수 있는 부분집합의 개수는 **2^N개** 이다. 이는 각 원소를 부분집합에 **포합시키거나** **포합시키지 않는** 2가지 경우를 모든원소에 적용한 경우의 수로 아무 원소도 선택되지 않는 부분집합부터 시작하여 모든 원소가 포함되어있는 부분집합을 포함한다.
>
> ex) N개의 원소 중 가방에 몇가지 원소를 가방에 집어넣을 때 가방에 들어갈 수 있는 종류의 집합

<br/>

**부분집합 구현**

```java
static int N;
static boolean[] isSelected; // 부분집합에 포함 여부를 저장한 배열
static int[] input; // 숫자 배열

public static void generateSubset(int cnt) { 
    // 부분집합에 고려해야하는 원소, 직전까지 고려한 원소수
    if(cnt == N) { // 부분집합 완성 시 작동
        for(int i=0; i<N; i++) {
            System.out.print((isSelected[i]?input[i]:"X")+" ");
        }
        System.out.println();
        return;
    }
    isSelected[cnt] = true;
    generateSubset(cnt+1);  // 해당 원소가 포함된 경우
    isSelected[cnt] = false; 
    generateSubset(cnt+1); // 해당 원소가 포함되지 않은 경우
}

	/** i:단계, sumT : 맛의 현재 단계까지의 합, sumK : 칼로리의 현재 단계까지의 합
	  현재까지 계산한 결과를 매번 가지고 다니자 * */
public static void dfs(int i, int sumT, int sumK ) {
    // basis part 선택한 재료들의 맛의 총합, 칼로리의 총합을 구해서,
    //칼로리 제한범위 이내에서 최대 맛을 찾기
    if(i == N) {	
        if(sumK <= L && maxT < sumT) { 
            maxT = sumT;
        }
        return;
    } else if(sumK <= L) { //--1--
        return;
    }
    // 선택함
    dfs(i+1, sumT+v[i][0], sumK+v[i][1]);
    // 선택안함
    dfs(i+1, sumT, sumK);
}
```

<br/>

<br/>



### :zap:stack

---

<br/>**stack의 특성**

>물건을 쌓아 올리듯 자료를 쌓아올린 형태의 자료구조 
>
>스택에 저장된 자료는 **선형 구조**
>
>선형구조 : 자료 간의 관계가 **1대 1**의 관계
>
>비선형 구조 : 자료 간의 관계가 **1대 N**의 관계
>
>후입선출구조(**LIFO**, Last in first out) => 나중에 들어간 원소가 먼저 나온다.

<br/>

**주요연산**

>push
>
>pop
>
>peek



<br/>

**주요 메서드**

```java
Stack<String> stack = new linkedList<String>();
stack.push();
stack.pop();
stack.peek();
stack.isEmpty();
```

<br/>

 **대표적인 문제**

- 괄호 검사, Function Call, 계산기(중위표기식 => 후위표기식으로 변환)

<br/>

<br/>





### :zap:Queue

---



**<br/>Queue의 특성**

>스택과 마찬가지로 삽입과 삭제의 위치가 제한적인 자료구조
>
>큐의 **뒤에서는 삽입만** 하고, 큐의 **앞에서는 삭제**만 이루어진다.
>
>선입 선출 구조(**FIFO**, First in First out) : 가장 먼저 삽입된 원소가 가장 먼저 삭제된다.

<br/>

**Queue의 기본연산**

>enQueue : 삽입
>
>deQueue : 삭제



<br/>

**주요 메서드**

```java
Queue<String> queue = new Linkedlist<String>();
queue.offer();
queue.poll();
queue.add();
queue.remove();
queue.isEmpty();
queue.size();
```



<br/><br/>





### :zap:List

---



<br/>**List의 특성**

> **순서를 가진 데이터**의 집합을 가리키는 추상 자료형(Abstract Data type)
>
> 동일한 데이터를 가지고 있어도 상관없다.
>
> 구현 방법에 따라서 크게 2가지
>
> - **순차 리스트**(ArrayList) : **배열을 기반**으로 구현된 리스트
> - **연결 리스트**(LinkedList) : 메모리의 **동적할당을 기반**으로 구현된 리스트

<br/>

**ArrayList의 특징**

> 1차원 바열에 항목들을 **순서대로 저장**
>
> 데이터의 종류에 따라 구조화된 자료구조 사용 가능
>
> 배열의 **인덱스**를 이용해 원하는 위치의 데이터 접근

<br/> 

**ArrayList의 문제점**

> 1. 단순 배열을 이용해 순차리스트를 구현하는 경우, 자료의 삽입/삭제 연산 과정에서 연속적인 메모리 배열을 위해 **원소들을 이동시키는 작업이 필요**
> 2. 원소의 개수가 많고, **삽입/삭제 연산이 빈번**하게 일어날수록 **작업에  소요되는 시간이 증가**
> 3. 배열의 크기가 정해져 있는 경우, 실제로 사용될 메모리보다 크게 할당하여 **메모리의 낭비를 초래**할 수 있고, 반대로 할당된 메모리보다 많은 자료를 사용하여 새롭게 배열을 만들어 작업을 해야 하는 경우가 발생

<br/>



**LinkedList의 특징**

> 자료의 **논리적인 순서**와 메모리 상의 물리적인 순서가 **일치하지 않다**.
>
> 개별적으로 위치하고 있는 원소를 연결하여 하나의 전체적인 자료구조 형성
>
> **링크**를 통해 원소를 접근, 물리적인 순서를 맞추기 위한 작업이 필요하지 않다.
>
> 자료구조의 크기를 동적으로 조절 가능, 메모리의 효율적인 사용이 가능하다.



  <br/>

**주요 메서드**

```java
		List<String> list = new LinkedList<String>();
		list.add(string);
		list.contains(object);
		list.get(index);
		list.remove(index);
		list.remove(object);
		list.toArray();
		list.isEmpty();
```

<br/>

**대표적인 문제**

> Single Linked List
>
> Double Linked List
>
> Circular Linked List

<br/><br/>





### :zap:Tree

---

**<br/>Tree의 특징**

> **비선형 구조**
>
> 원소들 간에 **1:N 관계**를 가지는 자료구조
>
> 원소들 간에 **계층 관계**를 가지는 계층형 자료구조
>
> 상위 원소에서 하위 원소로 내려가면서 확장되는 트리 모양의 구조

<br/>



**용어 정리**

> 노드(node) : 트리의 원소
>
> 간선(edge) : 노드와 노드를 연결하는 선으로 부모 노드와 자식 노드를 연결
>
> 루트 노드(root Node) : 트리의 시작노드인 최상위 노드
>
> 형제 노드(sibling Node) - 같은 부모 노드의 자식 노드들
>
> 조상 노드 - 간선을 따라 루트 노드까지 이르는 경로에 있는 모든 노드들
>
> 서브 트리(subtree) - 부모 노드와 연결된 간선을 끊었을 때 생성되는 트리
>
> 자손 노드 - 서브 트리에 있는 하위 레벨의 노드들
>
> **차수(degree)**
>
> - 노드의 차수 : 노드에 연결된 **자식 노드의 수**
> - 트리의 차수 : 트리에 있는 **노드의 차수 중에서 가장 큰 값**
> - 단말노드(leaf Node) : **차수가 0인 노드**, 즉 자식 노드가 없는 노드
>
> **높이**
>
> - 노드의 높이 : **루트에서** 노드에 이르는 **간선의 수**, 노드의 레벨
> - 트리의 높이 : 트리에 있는 **노드의 높이 중에서 가장 큰 값**, 최대 레벨



<br/>

<br/>**이진 트리**

> **차수가 2인 트리**
>
> 각 노드가 자식 노드를 최대한 2개 까지만 가질 수 있는 트리
>
> 모든 노드들이 최대 2개의 서브트리를 갖는 특별한 형태의 트리
>
> 높이 h에서 노드의 최대 개수 : 2^h 개
>
> 높이가 h인 이진트리가 가질 수 있는 노드의 최소 개수 : h+1 개
>
> 높이가 h인 이진트리가 가질 수 있는 노드의 최대 개수 : 2^(h+1) - 1 개



<br/>

**이진트리의 종류**

> **완전 이진트리(Complete Binary Tree)**
>
> > 포화 이진트리의 노드 번호 1번부터 n번까지 빈자리가 없는 이진 트리
>
> **편향 이진트리(Skewed BInary Tree)**
>
> > 높이 h에 대한 최소 개수의 노드를 가지면서 한쪽 방향의 자식 노드만을 가진 이진트리
> >
> > 왼쪽 편향 이진트리, 오른쪽 편향 이진트리

<br/>

**이진트리의 표현**

> 노드번호가 i 기준, root node번호 1
>
> 부모노드 번호 : i / 2
>
> 왼쪽 자식노드 번호 : 2 * i
>
> 오른쪽 자식노드 번호 : 2 * i + 1
>
> 레벨 n의 노드 번호 시작 번호 : 2^n



<br/><br/>

### :zap:**비선형 자료구조 완전탐색**

> 비선형 구조인 트리, 그래프의 각 노드를 **중복되지 않게** 전부 방문(visit)하는 것
>
> 비선형구조는 선형 구조에서와 같이 **선후 연결 관계를 알 수 없다.**
>
> 2가지 방법
>
> > **깊이 우선 탐색 (BFS, Breadth First Search)**
> >
> > **너비 우선 탐색(DFS, Depth First Search)**

<br/>

**BFS ( Breadth First Search)**

> 루트 노드의 자식 노드들을 먼저 모두 차례로 방문 후에, 방문했던 자식 노드들을 기준으로 하여 다시 해당 노드의 자식 노드들을 차례로 방문하는 방식
>
> 인접한 노드들에 대해 탐색한 후, 다시 너비우선탐색을 진행 => **Queue 활용**

**DFS( Depth First Search )**

> 루트 노드에서 출발하여, 한 방향으로 갈 수 있는 경로가 있는 곳까지 깊이 탐색해 가다가 더 이상 갈 곳이 없게 되면, 가장 마지막에 만났던 갈림길 간선이 있는 노드로 되돌아와서 다른 방향의 노드로 탐색을 계속 반복하여 결국 모든 노드를 방문하는 순회 방법
>
> 가장 마지막에 만났던 갈림길의 노드로 되돌아가서 다시 깊이 우선 탐색을 반복해야 하므로 **재귀적으로 구현**하거나 후입선출 구조의 **스택 사용**해서 구현

<br>

<br/>**이진트리의 3가지 순회방법**

> **Preorder Traversal (전위 순회)**
>
> ​	VLR 순서 
>
> ​	부모노드 방문 후, 자식노드를 좌, 우 순서로 방문
>
> 
>
> **Inorder Traversal (중위 순회)** 
>
> ​	LVR 순서
>
> ​	왼쪽 자식노드, 부모노드, 오른쪽 자식노드 순으로 방문
>
> 
>
> **PostOrder Traversal (후위 순회)**
>
> ​	LRV 순서
>
> ​	자식노드를 좌우 순서로 방문한 후, 부모노드로 방문



### <br/><br/>

### :zap:Heap

---

**<br/>Heap 자료구조의 특징**

> **완전 이진 트리**에 있는 노드 중에서 키 값이 가장 큰 노드나 키 값이 가장 작은 노드를 찾기 위해 만든 자료구조
>
> 최대 힙(max Heap) : 키 값이 가장 큰 노드를 찾기 위한 **완전 이진 트리**
>
> 최소 힙(min Heap) : 키 값이 가장 작은 노드를 찾기 위한 **완전 이진 트리**
>
> 힙에서는 루트 노드의 원소만을 삭제 가능
>
> 루트 노드의 원소를 삭제하여 반환



<br/>

**힙의 활용 - Priority Queue**

> 우선순위 큐를 구현하는 가장 효율적인 방법이 힙을 사용
>
> 노드 하나의 추가/삭제의 시간 복잡도  : O(log N)
>
> 최대값/최소값 : O(1) 

<br/><br/>

