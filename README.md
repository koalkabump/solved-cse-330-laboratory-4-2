Download Link: https://assignmentchef.com/product/solved-cse-330-laboratory-4-2
<br>
<strong style="font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen-Sans, Ubuntu, Cantarell, 'Helvetica Neue', sans-serif;">Exercise 1: </strong><span style="font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen-Sans, Ubuntu, Cantarell, 'Helvetica Neue', sans-serif;">Generate a file List.h that contains all code necessary to define the ADT Linked List as discussed in the lecture. The code that needs to be entered is listed at the end of this document. </span><strong style="font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen-Sans, Ubuntu, Cantarell, 'Helvetica Neue', sans-serif;"> </strong>




<strong>Exercise 2: </strong>Test the basics of your implementation in List.h in a file ListMain.cpp which carries out the generic task of (1) filling a linked list with a series of integers values (between 10-25, you may use random number generation), and (2) prints out all values stored in the list (you may want to define a function print_list(…) for this purpose).




<strong>Exercise 3:</strong> Provided you have completed Exercise 2, enhance your class List{…} in List.h with additional member functions:




<ul>

 <li><strong>A List function find(T x)</strong> which will search for value x in the linked list; when the value is found, the function is to return the iterator to this value; when the value is not contained in the list, the function is to return the end() iterator.</li>

</ul>




<ul>

 <li><strong>A List function selforg_find(T x)</strong> which will attempt to find value x; if x is found, this values is moved from its current position in the linked list to the very front of the list (…. The idea is that value x may a popular value that is sought frequently; when it is located in the front of the list, it can be found more cheaply/with fewer comparisons.)</li>

</ul>




Test your new functions by extending the int main() from Exercise 1 in a suitable manner.




<strong>Exercise 4:</strong> Implement a <strong>List function circulate(iterator start, int k) </strong>which begins with a list iterator set to start and then moves the iterator k steps in forwards direction. The function will return the iterator as it appears at the end of k movements of the iterator.




Test your new functions by extending the int main() from Exercise 1 in a suitable manner.




<strong>For Lab Credit: </strong>(1) Sign your name of the <strong><u>signup sheet</u></strong>. (2) <strong><u>Submit via portal</u></strong> your best effort for this lab. The portal remains open for the lab day + 2 days. W -&gt; Fri @ 1159pm, M-&gt;Wed @ 11:59pm.




<strong>*** List.h Code starts here *** </strong>




// based of code by Weiss, DSAAC


#ifndef LIST_H

#define LIST_H




#include &lt;algorithm&gt; <strong>using</strong> <strong>namespace</strong> std<strong>;</strong> template <strong>&lt;</strong>typename T<strong>&gt;</strong> class List <strong>{</strong>   private<strong>:</strong>

// The basic doubly linked list node.

// Nested inside of List, can be public

// because the Node is itself private     struct Node     <strong>{</strong>

T  data<strong>;</strong>

Node   <strong>*</strong>prev<strong>;</strong>

Node   <strong>*</strong>next<strong>;</strong>




Node<strong>(</strong> const T <strong>&amp;</strong> d <strong>=</strong> T<strong>{</strong> <strong>},</strong> Node <strong>*</strong> p <strong>=</strong> <strong>nullptr</strong><strong>,</strong> Node <strong>*</strong> n <strong>=</strong> <strong>nullptr</strong> <strong>)</strong>

<strong>:</strong> data<strong>{</strong> d <strong>},</strong> prev<strong>{</strong> p <strong>},</strong> next<strong>{</strong> n <strong>}</strong> <strong>{</strong> <strong>}</strong>




Node<strong>(</strong> T <strong>&amp;&amp;</strong> d<strong>,</strong> Node <strong>*</strong> p <strong>=</strong> <strong>nullptr</strong><strong>,</strong> Node <strong>*</strong> n <strong>=</strong> <strong>nullptr</strong> <strong>)</strong>

<strong>:</strong> data<strong>{</strong> std<strong>::</strong>move<strong>(</strong> d <strong>)</strong> <strong>},</strong> prev<strong>{</strong> p <strong>},</strong> next<strong>{</strong> n <strong>}</strong> <strong>{</strong> <strong>}</strong>

<strong>};</strong>

public<strong>:</strong>     class const_iterator

<strong>{</strong>       public<strong>:</strong>




// Public constructor for const_iterator.         const_iterator<strong>(</strong> <strong>)</strong> <strong>:</strong> current<strong>{</strong> <strong>nullptr</strong> <strong>}</strong>

<strong>{</strong> <strong>}</strong>




// Return the T stored at the current position.

// For const_iterator, this is an accessor with a

// const reference return type.         const T <strong>&amp;</strong> <strong>operator</strong><strong>*</strong> <strong>(</strong> <strong>)</strong> const

<strong>{</strong> <strong>return</strong> retrieve<strong>(</strong> <strong>);</strong> <strong>}</strong>

const_iterator <strong>&amp;</strong> <strong>operator</strong><strong>++</strong> <strong>(</strong> <strong>)</strong>

<strong>{</strong>

current <strong>=</strong> current<strong>-&gt;</strong>next<strong>;</strong>             <strong>return</strong> <strong>*</strong><strong>this</strong><strong>;</strong>

<strong>}</strong>




const_iterator <strong>operator</strong><strong>++</strong> <strong>(</strong> int <strong>)</strong>

<strong>{</strong>             const_iterator old <strong>=</strong> <strong>*</strong><strong>this</strong><strong>;</strong>

<strong>++(</strong> <strong>*</strong><strong>this</strong> <strong>);</strong>             <strong>return</strong> old<strong>;</strong>

<strong>}</strong>

const_iterator <strong>&amp;</strong> <strong>operator</strong><strong>—</strong> <strong>(</strong> <strong>)</strong>

<strong>{</strong>

current <strong>=</strong> current<strong>-&gt;</strong>prev<strong>;</strong>             <strong>return</strong> <strong>*</strong><strong>this</strong><strong>;</strong>

<strong>}</strong>




const_iterator <strong>operator</strong><strong>—</strong> <strong>(</strong> int <strong>)</strong>

<strong>{</strong>

const_iterator old <strong>=</strong> <strong>*</strong><strong>this</strong><strong>;</strong>

<strong>–(</strong> <strong>*</strong><strong>this</strong> <strong>);</strong>             <strong>return</strong> old<strong>;</strong>

<strong>}</strong>




bool <strong>operator</strong><strong>==</strong> <strong>(</strong> const const_iterator <strong>&amp;</strong> rhs <strong>)</strong> const

<strong>{</strong> <strong>return</strong> current <strong>==</strong> rhs<strong>.</strong>current<strong>;</strong> <strong>}</strong>




bool <strong>operator</strong><strong>!=</strong> <strong>(</strong> const const_iterator <strong>&amp;</strong> rhs <strong>)</strong> const           <strong>{</strong> <strong>return</strong> <strong>!(</strong> <strong>*</strong><strong>this</strong> <strong>==</strong> rhs <strong>);</strong> <strong>}</strong>

protected<strong>:</strong>         Node <strong>*</strong>current<strong>;</strong>




// Protected helper in const_iterator that returns the T

// stored at the current position. Can be called by all

// three versions of operator* without any type conversions.

T <strong>&amp;</strong> retrieve<strong>(</strong> <strong>)</strong> const

<strong>{</strong> <strong>return</strong> current<strong>-&gt;</strong>data<strong>;</strong> <strong>}</strong>




// Protected constructor for const_iterator.

// Expects a pointer that represents the current position.         const_iterator<strong>(</strong> Node <strong>*</strong>p <strong>)</strong> <strong>:</strong>  current<strong>{</strong> p <strong>}</strong>

<strong>{</strong> <strong>}</strong>




friend class List<strong>&lt;</strong>T<strong>&gt;;</strong>

<strong>}</strong>




class iterator <strong>:</strong> public const_iterator

<strong>{</strong>       public<strong>:</strong>




// Public constructor for iterator.

// Calls the base-class constructor.

// Must be provided because the private constructor         // is written; otherwise zero-parameter constructor

// would be disabled.         iterator<strong>(</strong> <strong>)</strong>

<strong>{</strong> <strong>}</strong>




T <strong>&amp;</strong> <strong>operator</strong><strong>*</strong> <strong>(</strong> <strong>)</strong>

<strong>{</strong> <strong>return</strong> const_iterator<strong>::</strong>retrieve<strong>(</strong> <strong>);</strong> <strong>}</strong>




// Return the T stored at the current position.

// For iterator, there is an accessor with a

// const reference return type and a mutator with

// a reference return type. The accessor is shown first.

const T <strong>&amp;</strong> <strong>operator</strong><strong>*</strong> <strong>(</strong> <strong>)</strong> const

<strong>{</strong> <strong>return</strong> const_iterator<strong>::</strong><strong>operator</strong><strong>*(</strong> <strong>);</strong> <strong>}</strong>

iterator <strong>&amp;</strong> <strong>operator</strong><strong>++</strong> <strong>(</strong> <strong>)</strong>

<strong>{</strong>

<strong>this</strong><strong>-&gt;</strong>current <strong>=</strong> <strong>this</strong><strong>-&gt;</strong>current<strong>-&gt;</strong>next<strong>;</strong>             <strong>return</strong> <strong>*</strong><strong>this</strong><strong>;</strong>

<strong>}</strong>




iterator <strong>operator</strong><strong>++</strong> <strong>(</strong> int <strong>)</strong>

<strong>{</strong>             iterator old <strong>=</strong> <strong>*</strong><strong>this</strong><strong>;</strong>             <strong>++(</strong> <strong>*</strong><strong>this</strong> <strong>);</strong>             <strong>return</strong> old<strong>;</strong>

<strong>}</strong>

iterator <strong>&amp;</strong> <strong>operator</strong><strong>—</strong> <strong>(</strong> <strong>)</strong>

<strong>{</strong>

<strong>this</strong><strong>-&gt;</strong>current <strong>=</strong> <strong>this</strong><strong>-&gt;</strong>current<strong>-&gt;</strong>prev<strong>;</strong>             <strong>return</strong> <strong>*</strong><strong>this</strong><strong>;</strong>

<strong>}</strong>




iterator <strong>operator</strong><strong>—</strong> <strong>(</strong> int <strong>)</strong>

<strong>{</strong>             iterator old <strong>=</strong> <strong>*</strong><strong>this</strong><strong>;</strong>             <strong>–(</strong> <strong>*</strong><strong>this</strong> <strong>);</strong>             <strong>return</strong> old<strong>;</strong>

<strong>}</strong>                 protected<strong>:</strong>

// Protected constructor for iterator.

// Expects the current position.         iterator<strong>(</strong> Node <strong>*</strong>p <strong>)</strong> <strong>:</strong> const_iterator<strong>{</strong> p <strong>}</strong>

<strong>{</strong> <strong>}</strong>




friend class List<strong>&lt;</strong>T<strong>&gt;;</strong>

<strong>}</strong>

public<strong>:</strong>     List<strong>(</strong> <strong>)</strong>

<strong>{</strong> init<strong>(</strong> <strong>);</strong> <strong>}</strong>




<strong>~</strong>List<strong>(</strong> <strong>)</strong>     <strong>{</strong>         clear<strong>(</strong> <strong>);</strong>         <strong>delete</strong> head<strong>;</strong>         <strong>delete</strong> tail<strong>;</strong>

<strong>}</strong>




List<strong>(</strong> const List <strong>&amp;</strong> rhs <strong>)</strong>

<strong>{</strong>         init<strong>(</strong> <strong>);</strong>         <strong>for</strong><strong>(</strong> auto <strong>&amp;</strong> x <strong>:</strong> rhs <strong>)</strong>             push_back<strong>(</strong> x <strong>);</strong>

<strong>}</strong>




List <strong>&amp;</strong> <strong>operator</strong><strong>=</strong> <strong>(</strong> const List <strong>&amp;</strong> rhs <strong>)</strong>

<strong>{</strong>

List copy <strong>=</strong> rhs<strong>;</strong>         std<strong>::</strong>swap<strong>(</strong> <strong>*</strong><strong>this</strong><strong>,</strong> copy <strong>);</strong>         <strong>return</strong> <strong>*</strong><strong>this</strong><strong>;</strong>

<strong>}</strong>







List<strong>(</strong> List <strong>&amp;&amp;</strong> rhs <strong>)</strong>

<strong>:</strong> theSize<strong>{</strong> rhs<strong>.</strong>theSize <strong>},</strong> head<strong>{</strong> rhs<strong>.</strong>head <strong>},</strong> tail<strong>{</strong> rhs<strong>.</strong>tail <strong>}</strong>     <strong>{</strong>

rhs<strong>.</strong>theSize <strong>=</strong> 0<strong>;</strong>         rhs<strong>.</strong>head <strong>=</strong> <strong>nullptr</strong><strong>;</strong>         rhs<strong>.</strong>tail <strong>=</strong> <strong>nullptr</strong><strong>;</strong>

<strong>}</strong>




List <strong>&amp;</strong> <strong>operator</strong><strong>=</strong> <strong>(</strong> List <strong>&amp;&amp;</strong> rhs <strong>)</strong>

<strong>{</strong>

std<strong>::</strong>swap<strong>(</strong> theSize<strong>,</strong> rhs<strong>.</strong>theSize <strong>);</strong>         std<strong>::</strong>swap<strong>(</strong> head<strong>,</strong> rhs<strong>.</strong>head <strong>);</strong>         std<strong>::</strong>swap<strong>(</strong> tail<strong>,</strong> rhs<strong>.</strong>tail <strong>);</strong>

<strong>return</strong> <strong>*</strong><strong>this</strong><strong>;</strong>

<strong>}</strong>




// Return iterator representing beginning of list.

// Mutator version is first, then accessor version.

iterator begin<strong>(</strong> <strong>)</strong>

<strong>{</strong> <strong>return</strong> iterator<strong>(</strong> head<strong>-&gt;</strong>next <strong>);</strong> <strong>}</strong>




const_iterator begin<strong>(</strong> <strong>)</strong> const

<strong>{</strong> <strong>return</strong> const_iterator<strong>(</strong> head<strong>-&gt;</strong>next <strong>);</strong> <strong>}</strong>




// Return iterator representing endmarker of list.

// Mutator version is first, then accessor version.

iterator end<strong>(</strong> <strong>)</strong>

<strong>{</strong> <strong>return</strong> iterator<strong>(</strong> tail <strong>);</strong> <strong>}</strong>




const_iterator end<strong>(</strong> <strong>)</strong> const       <strong>{</strong> <strong>return</strong> const_iterator<strong>(</strong> tail <strong>);</strong> <strong>}</strong>




// Return number of elements currently in the list.     int size<strong>(</strong> <strong>)</strong> const       <strong>{</strong> <strong>return</strong> theSize<strong>;</strong> <strong>}</strong>




// Return true if the list is empty, false otherwise.     bool empty<strong>(</strong> <strong>)</strong> const       <strong>{</strong> <strong>return</strong> size<strong>(</strong> <strong>)</strong> <strong>==</strong> 0<strong>;</strong> <strong>}</strong>




void clear<strong>(</strong> <strong>)</strong>

<strong>{</strong>

<strong>while</strong><strong>(</strong> <strong>!</strong>empty<strong>(</strong> <strong>)</strong> <strong>)</strong>             pop_front<strong>(</strong> <strong>);</strong>

<strong>}</strong>




// front, back, push_front, push_back, pop_front, and pop_back

// are the basic double-ended queue operations.

T <strong>&amp;</strong> front<strong>(</strong> <strong>)</strong>

<strong>{</strong> <strong>return</strong> <strong>*</strong>begin<strong>(</strong> <strong>);</strong> <strong>}</strong>




const T <strong>&amp;</strong> front<strong>(</strong> <strong>)</strong> const       <strong>{</strong> <strong>return</strong> <strong>*</strong>begin<strong>(</strong> <strong>);</strong> <strong>}</strong>




T <strong>&amp;</strong> back<strong>(</strong> <strong>)</strong>

<strong>{</strong> <strong>return</strong> <strong>*–</strong>end<strong>(</strong> <strong>);</strong> <strong>}</strong>




const T <strong>&amp;</strong> back<strong>(</strong> <strong>)</strong> const

<strong>{</strong> <strong>return</strong> <strong>*–</strong>end<strong>(</strong> <strong>);</strong> <strong>}</strong>




void push_front<strong>(</strong> const T <strong>&amp;</strong> x <strong>)</strong>

<strong>{</strong> insert<strong>(</strong> begin<strong>(</strong> <strong>),</strong> x <strong>);</strong> <strong>}</strong>




void push_back<strong>(</strong> const T <strong>&amp;</strong> x <strong>)</strong>

<strong>{</strong> insert<strong>(</strong> end<strong>(</strong> <strong>),</strong> x <strong>);</strong> <strong>}</strong>




void push_front<strong>(</strong> T <strong>&amp;&amp;</strong> x <strong>)</strong>

<strong>{</strong> insert<strong>(</strong> begin<strong>(</strong> <strong>),</strong> std<strong>::</strong>move<strong>(</strong> x <strong>)</strong> <strong>);</strong> <strong>}</strong>




void push_back<strong>(</strong> T <strong>&amp;&amp;</strong> x <strong>)</strong>

<strong>{</strong> insert<strong>(</strong> end<strong>(</strong> <strong>),</strong> std<strong>::</strong>move<strong>(</strong> x <strong>)</strong> <strong>);</strong> <strong>}</strong>




void pop_front<strong>(</strong> <strong>)</strong>       <strong>{</strong> erase<strong>(</strong> begin<strong>(</strong> <strong>)</strong> <strong>);</strong> <strong>}</strong>




void pop_back<strong>(</strong> <strong>)</strong>       <strong>{</strong> erase<strong>(</strong> <strong>—</strong>end<strong>(</strong> <strong>)</strong> <strong>);</strong> <strong>}</strong>




// Insert x before itr.     iterator insert<strong>(</strong> iterator itr<strong>,</strong> const T <strong>&amp;</strong> x <strong>)</strong>

<strong>{</strong>

Node <strong>*</strong>p <strong>=</strong> itr<strong>.</strong>current<strong>;</strong>

<strong>++</strong>theSize<strong>;</strong>

<strong>return</strong> iterator<strong>(</strong> p<strong>-&gt;</strong>prev <strong>=</strong> p<strong>-&gt;</strong>prev<strong>-&gt;</strong>next <strong>=</strong> <strong>new</strong> Node<strong>{</strong> x<strong>,</strong> p<strong>-&gt;</strong>prev<strong>,</strong> p <strong>}</strong>

<strong>);</strong>

<strong>}</strong>




// Insert x before itr.     iterator insert<strong>(</strong> iterator itr<strong>,</strong> T <strong>&amp;&amp;</strong> x <strong>)</strong>

<strong>{</strong>

Node <strong>*</strong>p <strong>=</strong> itr<strong>.</strong>current<strong>;</strong>

<strong>++</strong>theSize<strong>;</strong>

<strong>return</strong> iterator<strong>(</strong> p<strong>-&gt;</strong>prev <strong>=</strong> p<strong>-&gt;</strong>prev<strong>-&gt;</strong>next <strong>=</strong> <strong>new</strong> Node<strong>{</strong> std<strong>::</strong>move<strong>(</strong> x <strong>),</strong> p<strong>-&gt;</strong>prev<strong>,</strong> p <strong>}</strong> <strong>);</strong>

<strong>}</strong>




// Erase item at itr.

iterator erase<strong>(</strong> iterator itr <strong>)</strong>

<strong>{</strong>

Node <strong>*</strong>p <strong>=</strong> itr<strong>.</strong>current<strong>;</strong>         iterator retVal<strong>(</strong> p<strong>-&gt;</strong>next <strong>);</strong>         p<strong>-&gt;</strong>prev<strong>-&gt;</strong>next <strong>=</strong> p<strong>-&gt;</strong>next<strong>;</strong>         p<strong>-&gt;</strong>next<strong>-&gt;</strong>prev <strong>=</strong> p<strong>-&gt;</strong>prev<strong>;</strong>         <strong>delete</strong> p<strong>;</strong>         <strong>—</strong>theSize<strong>;</strong>




<strong>return</strong> retVal<strong>;</strong>

<strong>}</strong>




iterator erase<strong>(</strong> iterator from<strong>,</strong> iterator to <strong>)</strong>

<strong>{</strong>

<strong>for</strong><strong>(</strong> iterator itr <strong>=</strong> from<strong>;</strong> itr <strong>!=</strong> to<strong>;</strong> <strong>)</strong>             itr <strong>=</strong> erase<strong>(</strong> itr <strong>);</strong>         <strong>return</strong> to<strong>;</strong>

<strong>}</strong>




// Add for CSE 330 here …

private<strong>:</strong>     int   theSize<strong>;</strong>     Node <strong>*</strong>head<strong>;</strong>

Node <strong>*</strong>tail<strong>;</strong>

void init<strong>(</strong> <strong>)</strong>     <strong>{</strong>         theSize <strong>=</strong> 0<strong>;</strong>         head <strong>=</strong> <strong>new</strong> Node<strong>;</strong>         tail <strong>=</strong> <strong>new</strong> Node<strong>;</strong>         head<strong>-&gt;</strong>next <strong>=</strong> tail<strong>;</strong>         tail<strong>-&gt;</strong>prev <strong>=</strong> head<strong>;</strong>

<strong>}</strong> <strong>};</strong>

#endif


