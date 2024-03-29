비선형 자료 구조란 일렬로 나열하지 않고 자료 순서나 관계가 복잡한 구조를 말한다.
일반적으로 트리나 그래프를 말한다.

## 그래프
그래프는 정점과 간선으로 이루어진 자료 구조를 말한다.

### 정점과 간선
어떠한 곳에서 어떠한 곳으로 무언가를 통해 간다고 했을 때 '어떠한 곳'은 정점(vertex)이 되고 '무언가'는 간선(edge)이 된다.

만약 자신의 위치에서 하나의 목적지로 간다고 했을 때, 가는 길이 간선이고 자신의 위치와 목적지가 정점이된다.

정점에서 정점 사이의 간선이 하나의 방향만 있다면 그것은 '단방향 간선이'고, 양방향이라면 '양방향 간선'이 된다.

정점으로 나가는 간선을 해당 점점의 outdegree라고 하며, 들어오는 간선을 해당 점점의 indegree라고 한다.

정점과 간선으로 이루어진 집합을 '그래프(graph)'라고 한다.

#### 가중치
가중치는 간선과 정점 사이에 드는 비용을 뜻한다. 1번 노드와 2번 노드까지 가는 비용이 한 칸이라면 1번 노드에서 2번 노드까지의 가중치는 한 칸이다.

## 트리
트리는 그래프 중 하나로 그래프의 특징처럼 정점과 간선으로 이루어져 있고, 트리 구조로 배열된 일종의 계층적 데이터의 집합이다. 루트 노드, 내부 노드, 리프 노드 등으로 구성된다. 참고로 트리로 이루어진 집합을 숲이라고 한다.

### 트리의 특징
1. 부모, 자식 계층 구조를 가진다. 같은 경로상에서 어떤 노드보다 위에 있으면 부모, 아래에 있으면 자식 노드가 된다.
2. V - 1 = E라는 특징이 있다. 간선 수는 노드 수 - 1이다.
3. 임의의 두 노드 사이의 경로는 '유일무이'하게 '존재'한다. 즉, 트리 내의 어떤 노드와 어떤 노드까지의 경로는 반드시 있다.

### 트리의 구성
트리는 루트 노드, 내부 노드, 리프 노드로 이루어져 있다.

### 루트 노드
가장 위에 있는 노드를 뜻한다. 보통 트리 문제가 나오고 트리를 탐색할 때 루트 노드를 중심으로 탐색하면 문제가 쉽게 풀리는 경우가 많다.

### 내부 노드
루트 노드와 내부 노드 사이에 있는 노드를 뜻한다.

### 리프 노드
자식 노드가 없는 노드를 뜻한다.


#### 트리의 높이와 레벨
![](https://velog.velcdn.com/images/cnj9912/post/38f13b05-4751-47c6-9834-e1d39842f433/image.png)

- 깊이 : 트리에서의 깊이는 각 노드마다 다르며, 루트 노드부터 특정 노드까지 최단 거리로 갔을 대의 거리를 말한다. 예를 들어 노드 E의 깊이는 2이다.
- 높이 : 트리의 높이는 루트 노드부터 리프 노드까지 거리 중 가장 긴 거리를 의미하며, 앞 그림의 트리 높이는 3이다.
- 레벨 : 트리의 레벨은 주어지는 문제마다 조금씩 다르지만 보통 깊이와 같은 의미를 지닌다. 노드 A를 0레벨이라고 하고 B, C, D 노드까지의 레벨을 1레벨이라고 할 수도 있고, 노드 A를 레벨 1이라고 한다면 노드 B, C, D는 2레벨이 된다.
- 서브트리 : 트리 내의 하위 집합을 서브트리라고 한다. 트리 내에 있는 부분집합이라고도 보면 된다. 지금 보면 노드 F, J, K가 이 트리의 하위 집합으로 "저 노드들은 서브트리이다."라고 한다.

### 이진 트리
이진 트리는 자식의 노드 수가 두 개 이하인 트리를 의미하며, 이를 다음과 같이 분류한다.
![](https://velog.velcdn.com/images/cnj9912/post/24882539-52cb-4219-b452-88ad63038503/image.png)

- 정이진 트리(full binary tree) : 자식 노드가 0 또는 두 개인 이진 트리를 의미한다.
- 완전 이진 트리(complete binary tree) : 왼쪽에서부터 채워져 있는 이진 트리를 의미한다. 마지막 레벨을 제외하고는 모든 레벨이 완전히 채워져 있으며, 마지막 레벨의 경우 왼쪽부터 채워져 있다.
- 변질 이진 트리(degenerate binary tree) : 자식 노드가 하나밖에 없는 이진 트리를 의미한다.
- 포화 이진 트리(perfect binary tree) : 모든 노드가 꽉 차 있는 이진 트리를 의미한다.
- 균형 이진 트리(balanced binary tree) : 왼쪽과 오른쪽 노드의 높이 차이가 1 이하인 이진 트리를 의미한다. map, set을 구성하는 레드 블랙 트리는 균형 이진 트리중 하나이다.

### 이진 탐색 트리
이진 탐색 트리(BST)는 노드의 오른쪽 하위 트리에는 '노드 값보다 큰 값'이 있는 노드만 포함되고, 왼쪽 하위 트리에는 '노드 값보다 작은 값'이 들어 있는 트리를 말한다.

이때 왼쪽 및 오른쪽 하위 트리도 해당 특성을 가진다. 이렇게 두면 '검색'을 하기에 용이하다. 왼쪽에는 작은 값, 오른쪽에는 큰 값이 이미 정해여 있기 때문에 10을 찾으려고 한다면 25의 왼쪽 노드들만 찾으면 된다는 것은 자명하다. 보통 요소를 찾을 때 이진 탐색 트리의 경우 O(logn)이 걸린다. 하지만 최악의 경우 O(n)이 걸린다. 그 이유는 이진 탐색 트리는 삽입 순서에 따라 선형적일 수 있기 때문이다.

### AVL 트리
AVL 트리(Adelson-Velsky and Landis tree)는 앞서 설명한 최악의 경우 선형적인 트리가 되는 것을 방지하고 스스로 균형을 잡는 이진 탐색 트리이다. 두 자식 서브트리의 높이는 항상 최대 1만틈 차이 난다는 특징이 있다.

### 레드 블랙 트리
레드 블랙 트리는 균형 이진 탐색 트리로 탐색, 삽입, 삭제 모두 시간 복잡도가 O(logn)이다. 각 노드는 빨간색 또는 검은색의 색상을 나타내는 추가 비트를 저장하며, 삽입 삭제 중에 트리가 균형을 유지하도록 하는 데 사용된다.
참고로 "모든 리프 노드와 루트 노드는 블랙이고 어떤 노드가 레드이면 그 노드의 자식은 반드시 블랙이다." 등의 규칙을 기반으로 균형을 잡는 트리이다.

## 힙
힙은 완전 이진 트리 기반의 자료 구조이며, 최소힙과 최대힙 두 가지가 있고 해당 힙에 따라 특정한 특징을 지킨 트리를 말한다.
- 최대힙 : 루트 노드에 있는 키는 모든 자식에 있는 키 중에서 가장 커야 한다. 또한 각, 노드의 자식 노드와의 관계도 이와 같은 특징이 재귀적으로 이루어져야 한다.
- 최소힙 : 최소힙에서 루트 노드에 있는 키는 모든 자식에 있는 키 중에서 최솟값이어야 한다. 또한, 각 노드의 자식 노드와의 관계도 이와 같은 특징이 재귀적으로 이루어져야 한다.

### 최대힙의 삽입
힙에 새로운 요소가 들어오면, 일단 새로운 노드를 힙의 마지막 노드에 이어서 삽입한다. 이 새로운 노드를 부모 노드들과의 크기를 비교하며 교환해서 힙의 성질을 만족시킨다.

### 최대힙의 삭제
최대힙에서 최댓값은 루트 노드이므로 루트 노드가 삭제되고, 그 이후 마지막 노드와 루트 노드를 스왑하여 또다시 스왑등의 과정을 거쳐 재구성된다.

## 우선순위 큐
우선순위 큐는 수선순위 대기열이라고도 하며, 대기열에서 우선순위가 높은 요소가 우선 순위가 낮은 요소보다 먼저 제공되는 자료 구조이다. 우선순위 큐는 힙을 기반으로 구현된다.

