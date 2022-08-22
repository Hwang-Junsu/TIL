# 1. 연결 리스트(Linked List)란 ?

연결리스트는 모든 요소(노드)가 다음 요소에 연결된 자료구조이다. 자료가 연결되어 있기 때문에 새로운 자료를 앞쪽에 추가/삭제할 때 굉장히 유용하게 사용할 수 있다.
하지만, 특정한 자료를 불러올 때는 무조건 순회하며 찾아가는 과정이 필요하기 때문에 특정한 노드를 찾기 까다롭다는 단점이 있다.

# 1-1. 연결리스트의 Big-O(시간 복잡도)
|function|Big-O|
|------|---|
|Insertion|O(1)|
|Deletion|O(1)|
|Search|O(n)|

삽입이나 삭제를 한다면, 요소의 기존 연결을 끊은 다음 추가하거나 삽입할 위치의 자료를 연결하면 되기에 시간복잡도가 O(1)   
탐색시에는 head부터 순차적으로 자료를 찾아야 하기 때문에 시간복잡도가 O(n)


# 2. 구현
연결리스트 노드에는 데이터를 저장할 value 프로퍼티, 다음 노드의 위치를 알려주는 next 프로퍼티가 있다.
```javascript

// node 구현
function Node(element) {    
  this.element = element;   
  this.next = null;
}

// Linked List 구현
function LinkedList() {    
  this.head = new Node("head");    
  this.find = find;    
  this.append = append;    
  this.insert = insert;    
  this.remove = remove;    
  this.toString = toString;    
  this.findPrevious = findPrevious;
}

//노드 찾기
function find(item) {    
  var currNode = this.head;    
  while(currNode.element != item) {        
    currNode = currNode.next;    
  }    
  return currNode;

// 이전 노드 찾기
function findPrevious(item) {   
  var currNode = this.head;   
  while(currNode.next != null && currNode.next.element != item) {        
    currNode = currNode.next;    
  }    
  return currNode;
}

// 노드 추가
function append(newElement) {    
  var newNode = new Node(newElement); //새로운 노드 생성    
  var current = this.head; // 시작 노드    
  while(current.next != null) { // 맨 끝 노드 찾기
    current = current.next;    
  }    
  current.next = newNode;
} 
// 노드 중간 삽입
function insert(newElement, item) {    
  var newNode = new Node(newElement); //새로운 노드 생성
  var current = this.find(item); // 삽입할 위치의 노드 찾기
  newNode.next = current.next; // 찾은 노드가 가리키는 노드를 새로은 노드가 가리키기 
  current.next = newNode; // 찾은 노드는 이제부터 새로운 노드를 가리키도록 하기
  } 
  
// 노드 삭제
function remove(item) {    
  var preNode = this.findPrevious(item); // 삭제할 노드를 가리키는 노드 찾기  
  preNode.next = preNode.next.next; // 삭제할 노드 다음 노드를 가리키도록 하기
} 

// 연결 리스트의 요소들을 출력
function toString() {   
  var str = '[ ';   
  var currNode = this.head;    
  while(currNode.next != null){   
    str += currNode.next.element+' '; 
    currNode = currNode.next;    
  }  
  return str+']';
}

```
