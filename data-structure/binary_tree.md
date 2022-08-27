# 1. Binary_tree?
이진트리는 컴퓨터 응용에서 가장 많이 활용되는 아주 중요한 트리구조이다. 노드의 유한 집합으로서 공백이거나 루트와
두 개의 분리된 이진트리인 경우 왼쪽 서브트리와 오른쪽 서브트리로 구성된다.   
![tree](https://t1.daumcdn.net/cfile/tistory/99E6B23E5B339DBB33)

# 2. 이진트리의 연결 표현
```javascript
function TreeNode(val, left, right) {
     this.val = (val===undefined ? 0 : val)
     this.left = (left===undefined ? null : left)
     this.right = (right===undefined ? null : right)
 }
```
다음과 같이 왼쪽노드와 오른쪽노드, 현재노드를 나타내는 left, right, val을 포함하는 구조로 되어 있다.   
만약 서브트리가 공백이라면 해당 노드는 null이 된다.

# 3. 트리의 순회
- 전위순회(preorder traverse) : 뿌리(root)를 먼저 방문
- 중위순회(inorder traverse) : 왼쪽 하위 트리를 방문 후 뿌리(root)를 방문
- 후위순회(postorder traverse) : 하위 트리를 모두 방문 후 뿌리(root)를 방문

![traverse](https://mblogthumb-phinf.pstatic.net/20120331_173/rlakk11_1333202999001hceVs_JPEG/4.jpg?type=w2)   
위와 같은 트리가 있다고 한다면 각각 순회 방법은 아래와 같다.   
 
- 전위 순회 : 0->1->3->7->8->4->9->10->2->5->11->6
- 중위 순회 : 7->3->8->1->9->4->10->0->11->5->2->6
- 후위 순회 : 7->8->3->9->10->4->1->11->5->6->2->0
