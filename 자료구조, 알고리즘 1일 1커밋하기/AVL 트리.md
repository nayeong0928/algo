# AVL 트리

트리 내의 어떤 노드도 좌서브 트리와 우서브 트리의 높이 차가 1보다 크지 않은 상태로 유지되는 이진 검색 트리

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
