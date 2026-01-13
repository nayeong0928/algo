# AVL 트리

- 트리 내의 어떤 노드도 좌서브 트리와 우서브 트리의 높이 차가 1보다 크지 않은 상태로 유지되는 이진 검색 트리
- 균형이 깨지면 가장 낮은 서브트리부터 수선

## 높이 조정

높이 조정이 필요할 때는
1. 원소 삽입: 새로운 원소 삽입으로 트리 불균형
2. 원소 삭제: 원소가 삭제됨으로써 트리 불균형, 상위 루트까지 불균형해질 수 있음
따라서 삽입/삭제 시 어떤 불균형인지 타입을 확인하고 회전하는 과정이 필요

### 타입 확인
- LL트리: 중심노드의 왼자식의 좌서브트리
- LR트리: 중심노드의 왼자식의 우서브트리
- RR트리: 중심노드의 오른쪽 자식의 우서브트리
- RL트리: 중심노드의 오른쪽 자식의 좌서브트리

```java

    private int needBalance(AVLNode t) {
        int type = ILLEGAL;

        if (t.left.height + 2 <= t.right.height) {
            if (t.right.left.height <= t.right.right.height) {
                type = RR;
            } else {
                type = RL;
            }
        } else if (t.left.height + 2 > t.right.height) {
            if (t.left.left.height <= t.left.right.height) {
                type = LR;
            } else {
                type = LL;
            }
        }

        return type;
    }

```

### 타입별 해결방법

|타입|가장 깊은 트리|해결방법|
|------|---|---|
|LL타입|t.left.left|t 우회전|
|LR타입|t.left.right|t.left 좌회전 -> t 우회전|
|RR타입|t.right.right|t 좌회전|
|RL타입|t.right.left|t.right 우회전 -> t 좌회전|

```java

    private AVLNode balanceAVL(AVLNode tNode, int type) {
        AVLNode returnNode = NIL;

        switch (type) {
            case LL:
                returnNode = rightRotate(tNode);
                break;
            case LR:
                tNode.left = leftRotate(tNode.left);
                returnNode = rightRotate(tNode);
                break;
            case RR:
                returnNode = leftRotate(tNode);
                break;
            case RL:
                tNode.right = rightRotate(tNode.right);
                returnNode = leftRotate(tNode);
                break;
            default:
                System.out.println("Impossible type!!!");
                break;
        }
        return returnNode;
    }

```

### 회전

```java

    private AVLNode leftRotate(AVLNode t) {
        AVLNode RChild = t.right;

        if (RChild == NIL) {
            System.out.println(t.item + "'s RChild shouldn't be NIL!!!");
        }
        AVLNode RLChild = RChild.left;
        RChild.left = t;
        t.right = RLChild;
        t.height = 1 + Math.max(t.left.height, t.right.height);
        RChild.height = 1 + Math.max(RChild.left.height, RChild.right.height);
        return RChild;
    }

    private AVLNode rightRotate(AVLNode t) {
        AVLNode LChild = t.left;

        if (LChild == NIL) {
            System.out.println(t.item + "'s item LChild shouln't be NIL!!!");
        }
        AVLNode LRChild = LChild.right;
        LChild.right = t;
        t.left = LRChild;
        t.height = 1 + Math.max(t.left.height, t.right.height);
        LChild.height = 1 + Math.max(LChild.left.height, LChild.right.height);
        return LChild;
    }

```
