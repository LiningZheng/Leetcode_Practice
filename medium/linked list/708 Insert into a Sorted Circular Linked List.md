### 1 messy initial solution

```java
public ListNode insert(ListNode node, int x) {
    // write your code here

    ListNode newNode = new ListNode(x);
    if (node == null) {
        newNode.next = newNode;
        return newNode;
    }

    ListNode curs = node;

    // check the case where every node has the same val
    boolean sameVals = true;
    while (curs.next != node) {
        if (curs.val != curs.next.val) {
            sameVals = false; 
            break;
        }
        curs = curs.next;
    }
    if (sameVals) {
        insertBehind(node, newNode);
        return newNode;
    }
    
    
    while (true) {
        if (curs.val == x) {
            insertBehind(curs, newNode);
            break;
        } else if (curs.val < x) {
            while (curs.next.val < x && curs.val <= curs.next.val) {
                curs = curs.next;
            }
            insertBehind(curs, newNode);
            break;
        } else { 
            while (curs.val <= curs.next.val) {  // go to the begin (the smallest in the list)
                curs = curs.next;
            }
            if (curs.next.val > x) { // even begin > x
                insertBehind(curs, newNode);
                break;
            } else { //curs go to the begin
                curs = curs.next;
            }
        }
    }
    return newNode;
}

private void insertBehind(ListNode node, ListNode newNode) {
    newNode.next = node.next;
    node.next = newNode;
}
```
supose we are inserting 4, there are some cases:

1) 3 5 1; the normal case where there's a perfect spot between 3 and 5

2) 2 2 2 or 6 6 6; the same-value case

3) 1 2 3 or 7 8 9; where 4 is bigger or smaller than all the numbers on the list

### 2
```java
public ListNode insert(ListNode node, int x) {
    // write your code here

    ListNode newNode = new ListNode(x);
    if (node == null) {
        newNode.next = newNode;
        return newNode;
    }

    ListNode curs = node;

    while(true) {
        if (curs.val <= x && curs.next.val >= x) break;

        if (curs.val > curs.next.val) { // come to the begin
            if (curs.val <= x || curs.next.val >= x) break;
            else {
                curs = curs.next;
                continue;
            }
        }

        if (curs.next == node) break; // has returned to the begin

        curs = curs.next; 
    }

    insertBehind(curs, newNode);
    return newNode;
}

private void insertBehind(ListNode node, ListNode newNode) {
    newNode.next = node.next;
    node.next = newNode;
}
```
we view those cases in a different manner. let's define "begin" as the smallest value in the original list

a) a perfect spot. 3, 5

b) we have come to the begin of the list.
b.a) all the values are smaller or bigger than 4, corresponding to case 3) mentioned above.
b.b) otherwise. keep looking

c) we have come to the entry point where the search started, corresponding to case 2)

d) otherwise. keep searching next


