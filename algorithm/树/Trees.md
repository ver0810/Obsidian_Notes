A tree has a root label and a list of branches 
Each branches is a tree

```python
def tree(label, branches=[]):
	for branch in branches:
		assert is_tree(branch)
	return [label] + list(branches) #Creates a list from a sequence of branches

def label(tree):
	return tree[0]

def branches(tree):
	return tree[1:]

# How we to know it is a tree
def is_tree(tree):
	if type(tree) != list or len(tree) < 1:
		return False
	for branch in branches(tree):
		if not is_tree(tree):
			return False
	return True


```