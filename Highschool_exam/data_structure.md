# 기말고사와 함께하는 자료구조

## 트리 용어
- `정점(node)` : 하나의 점. vertex라고도 함
- `루트(root)` : 부모가 없는 노드
- `서브 트리(subtree)` : 기존 트리에서 하위의 트리 구조. 어떤 노드를 기준점으로 잡았을 때, 아래에 위치한 각각의 트리 구조를 서브트리라고 함. (트리 속의 작은 트리!)
- `간선(edge)` : 노드 간의 연결선
- `노드의 차수(degree)` : 서브 트리의 개수
- `단말 노드`, `잎 노드` (terminal/leaf) : 차수가 0인 노드
- `비단말노드(non terminal)` : 단말 노드 이외의 노드들
- `자식 노드(child node)` : 노드 X의 서브 트리의 루트들은 X의 자식
- `부모 노드(parent node)` : X는 그 자식들의 부모
- `형제 노드(sibling node)` : 부모가 같은 자식 노드들
- `조상 노드(ancestor node)` : 루트부터 노드에 이르는 경로상의 모든 노드들
- `자손 노드(descendent node)` : 서브 트리 상의 모든 노드들
- `트리의 차수(degree)` : **트리에 속한 노드의 최대 차수**
- `수준(level)` : 트리의 각 층에 매겨지는 번호. 루트의 레벨은 1이며 한 층씩 내려갈 수록 1 증가ㅓ
- `높이(height)` / `깊이(depth)` : **트리에 속한 노드의 최대 수준**
- `포리스트(forest)` : 트리들의 집합
- level n에서 가질 수 있는 최대 노드 수는 `2의 n-1제곱` (이진트리)
- 위에서 유의해야 할 것이, `자식 노드`와 `부모 노드`는 각각 한 층 아래 또는 한 층 위의 노드만 말하는 것이다. 그에 반하여 `조상 노드`와 `자손 노드`는 한 층이 아닌 위 노드 전체 혹은 아래 노드 전체를 뜻한다.

![image](https://user-images.githubusercontent.com/80818534/145148913-f15a2fc7-8fe9-4363-add8-84f045ccb4a5.png)

## DFS, BFS

- DFS : 깊이 우선 탐색 (스택)(재귀함수를 이용한 미로탐색 등에 주로 사용됨)
- BFS : 너비 우선 탐색 (큐)

![image](https://user-images.githubusercontent.com/80818534/145134548-78e4698f-34db-4622-8f5b-0b4287c80e25.png)
![image](https://user-images.githubusercontent.com/80818534/145136170-a50c74ac-772a-411a-9366-d537544b0515.png)
![image](https://user-images.githubusercontent.com/80818534/145136399-86886f56-0f78-46a6-8627-729dfa9ff6de.png)
위 사진에서 각 노드들의 위치는 다르지만 결과값은 1,2,3,4,5,6,7,8,9로 같다.

## 인접리스트, 인접행렬

- 트리 혹은 그래프를 `인접리스트(Adjacency List)`(연결리스트)로 표현해보자

![image](https://user-images.githubusercontent.com/80818534/145149846-1439f368-eae4-4187-98bf-42dc9b0ebd25.png)

- 트리 혹은 그래프를 `인접행렬(Adjacency Matrix)`로 표현해보자

![image](https://user-images.githubusercontent.com/80818534/145149882-434d6e34-8f3e-458a-ae08-55fa96dbf847.png)

## 최소 신장 트리

- `신장 트리(spanning tree)` : 그래프 내에 있는 모든 정점을 연결하고 **사이클이 없는 그래프**
- n개의 정점이 있으면 신장 트리의 간선은 `n-1`개
- `최소 신장 트리(Minimum Spanning Tree)` : 각 간선이 가지고 있는 가중치의 합이 최소가 되는 신장 트리
- 최소 신장 트리를 만들기 위해 `크루스칼(kruskal) 알고리즘`과 `프림(prim) 알고리즘`을 사용

![image](https://user-images.githubusercontent.com/80818534/145150405-b1c0c7eb-c4a3-4e08-aba3-776e00876374.png)

- `크루스칼(kruskal) 알고리즘` : 가중치가 작은 것부터 연결

![image](https://user-images.githubusercontent.com/80818534/145151225-abc4f585-171c-4a63-89fe-41afd7ac1713.png)

- `프림(prim) 알고리즘` : 시작 노드부터 정복해가며 더 작은 가중치의 간선들을 선택 (이전에 선택된 노드까지 포함하여 가중치 작은 간선 결정)

![image](https://user-images.githubusercontent.com/80818534/145151267-8b6e3426-229c-4394-be5f-519e2ab9390f.png)

## 완전 이진 트리, 포화 이진 트리

- `완전 이진 트리` : 노드가 왼쪽부터 차곡차곡 채워진 형태의 트리
- `포화 이진 트리` : 완전 꽉 차있는 트리

![image](https://user-images.githubusercontent.com/80818534/145150917-c785aeeb-be99-4977-a40a-5e331f3b6812.png)

- 완전 이진 트리, 포화 이진 트리 둘 다 `배열`로 구현 가능
- \[0\] 인덱스를 사용하지 않는 것이 편리
- 부모 노드는 `자식 노드의 인덱스 / 2`
- 자식 노드는 `부모 노드의 인덱스 * 2` 혹은 `부모 노드의 인덱스 * 2 + 1`
- ex) 5번 인덱스의 부모 노드 인덱스는 5 / 2 = 2
