# AVL 트리

트리 내의 어떤 노드도 좌서브 트리와 우서브 트리의 높이 차가 1보다 크지 않은 상태로 유지되는 이진 검색 트리

## 테스트 (진행중)

1. 공부하는 책(쉽게 배우는 자료구조 with 자바)에는 AVL 트리를 좌회전/우회전 할 때 노드의 높이값을 전부 갱신하지 않고 둔 상태로, 노드를 삭제할 때 높이값 오류를 잡는다고 나와있다. 삭제를 하지 않는 이상 트리의 높이에 오류가 있다는 게 신경쓰여서 좌회전할 때 이동된 노드들의 높이를 방문, 높이값을 조정하는 버전으로 만들어보고 싶었다.
2. balance 과정에서는 tNode의 부모가 tNode를 가리키고 있다는 것은 고려하지 않는 것 같아서 좌회전 할 때 tNode의 item, left, right만 RChild의 값으로 바꿔주고, t가 이동하는 노드는 RChild 객체를 재활용하는 식으로 작성했다.
3. 정상적으로 들어갔는지는 깊이 우선 탐색으로 트리를 조회해보는 방식으로 프린트해볼 것이다.

```java

    private AVLNode leftRotate(AVLNode tNode) {

        Comparable tItem = tNode.item;
        AVLNode tLeft = tNode.left;
        AVLNode RChild = tNode.right;
        AVLNode RLChild = RChild.left;

        tNode.item = RChild.item;
        tNode.right = RChild.right;
        tNode.left = RChild;
        RChild.item = tItem;
        RChild.left = tLeft;
        RChild.right = RLChild;

        return tNode;
    }

    private void setHeight(AVLNode node, int height) {

        node.height = height;

        if (node.left == NIL && node.right == NIL) {
            return;
        }

        if (node.left != NIL) {
            setHeight(node.left, height + 1);
        }
        if (node.right != NIL) {
            setHeight(node.right, height + 1);
        }

    }

```
