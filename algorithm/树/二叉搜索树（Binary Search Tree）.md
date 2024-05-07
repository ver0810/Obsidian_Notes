### 定义
一棵二叉树，根节点的左孩子的值*小于*根节点的值， 节点的右孩子的值*大于*根节点。

### 性质
- BST 的中序遍历是从小到大的顺序
- 
### 节点的插入

```cpp
void insert (BiTree* tree, int value){
    Node* node = new Node;
    node->val = value;
    node->left = nullptr;
    node->right = nullptr;
  
    if (tree -> root == NULL){
        tree -> root = node;
    }
    else{
        Node* temp = tree -> root;
        while (temp != NULL)
        {
            if (value < temp->val){
                if (temp -> left == NULL){
                    temp -> left = node;
                    return ;
                }
                else{
                    temp = temp->left;
                }
            }
            else{
                if (temp->right == NULL){
                    temp->right = node;
                    return ;
                }
                else{
                    temp = temp->right;
                }
            }
        }
    }
}
```

### 树的高度

```cpp
int get_hight(Node* node){
	if (node == NULL) return 0;
	else{
		int left_h = get_hight(node->left);
		int right_h = get_hight(node->right);
	}
	return left_h >= right_h ? left_h + 1 : right_h + 1;
}
```

### 搜索最大值
任意二叉树
```cpp
```