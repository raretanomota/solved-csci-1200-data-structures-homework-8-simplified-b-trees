Download Link: https://assignmentchef.com/product/solved-csci-1200-data-structures-homework-8-simplified-b-trees
<br>
In this assignment we will be implementing a partial and <strong>modified </strong>version of <em>B</em><sup>+ </sup>trees. As a result, online resources may not use the same terminology or may describe implementation details that are not relevant to our HW8 implementation. You should read the entire assignment before beginning your work. You should also make sure you understand the basic concepts discussed at the end of Lecture 19. It is highly recommended that before you begin coding, you practice constructing a couple of trees (using <em>b </em>= 3<em>,b </em>= 4) by hand and then checking your work with this online visualization tool: <a href="https://www.cs.usfca.edu/~galles/visualization/BPlusTree.html">https://www.cs.usfca.edu/</a><a href="https://www.cs.usfca.edu/~galles/visualization/BPlusTree.html">~</a><a href="https://www.cs.usfca.edu/~galles/visualization/BPlusTree.html">galles/visualization/BPlusTree.html</a>

The bulk of the assignment will focus on proper insertion in a <em>B</em><sup>+ </sup>tree, which is described on the <strong>next page</strong>. <strong>Implementation Details</strong>

In this assignment we will assume that the keys we insert are unique, i.e. for a particular <em>B</em><sup>+ </sup>tree, we will never call insert(3); insert(3);. You will find it beneficial to borrow code from our partial implementation of the <em>ds </em><em>set </em>class. We will not implement iterators, so find() should instead return a pointer to a <em>BPlusTreeNode</em>. The print functions only need to work with types/classes that already work with operator&lt;&lt;. You must implement all of the functions required to make <em>hw8 test.cpp </em>compile and run correctly.
<h1>Hints</h1>
Unless the tree is empty, find() will always return a pointer to a node in the tree. You do not need to store NULL pointers. In the middle of an insertion, it is okay to let your nodes hold too many keys or children as long as you fix it before the insertion and splits are finished. Since this is a tree, some things will be more “natural” to do with recursion.
<h1>Submission</h1>
While you are encouraged to write your own test functions, we will not be looking at them. You only need to submit a <em>README.txt </em>and <em>BPlusTree.h </em>file. Dr. Memory will be used on this assignment and you will be penalized for leaks and memory errors in your solution. The points and test cases required for submitting on Friday without being charged a late day will be posted at the top of the Submitty HW8 submission page. <strong>Extra Credit</strong>

With the way <em>print BFS() </em>is currently expected to output, it is not possible to tell which nodes are children of a particular node. Assuming that each key is short (i.e. no more than 2 characters wide), implement a function, <em>print BFS </em><em>pretty() </em>that still uses a BFS ordering and a vertical layout like <em>print BFS()</em>, but that has appropriate spacing so the structure of the tree is apparent. There are several possible ways to handle this, so you may choose whatever design you think is reasonable. Make sure to leave a note in your <em>README </em>if you implement the extra credit.
<h1>Insertion</h1>
Starting from an empty tree, with <em>b </em>= 3 in this example we do the following:
<ol>
 	<li>This example starts with one possible tree with <em>b </em>= 3 and the keys “a”-“f”.</li>
 	<li>insert(ant) causes a leaf to become too full.</li>
 	<li>The leaf containing “a”, “ant”, “b” is split into two nodes, but this makes the parent too full.</li>
 	<li>The parent is also split, creating a grandparent to the leaf that caused the split. Note that since this was a</li>
</ol>
split of an internal node, the key inherited by the new parent is not duplicated in the right-hand split node (“c” is not in either of the new root’s children). A split at a leaf always has the potential to cause more splits all the way up to the splitting the root.
<ol>
 	<li>insert(b); creates a root node with “b” in it.</li>
 	<li>insert(a); adds “a” to the root node</li>
 	<li>insert(c); adds “c” to the root node, which makes it too full.</li>
 	<li>The root node splits into two nodes, one with “a” and one with “b”, and “c”. A new parent is created, with the first value from the new right-hand node (“b”) placed in it. A node split should create two new nodes and put half of the orginal node’s keys into each of the new nodes. Whenever there are an odd number of keys in a node that needs to be split, the “extra” key will go to the right-hand node.</li>
</ol>