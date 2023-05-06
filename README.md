Download Link: https://assignmentchef.com/product/solved-ece_cs5510-homework-3
<br>
<h2>1.1            Java memory model</h2>

Consider the class shown in listing 1. According to what you have been told about the Java memory model, will the <em>reader </em>method ever divide by zero?

<ul>

 <li><strong>class </strong>VolatileExample {</li>

 <li><strong>int </strong>x = 0;</li>

 <li><strong>volatile boolean </strong>v = <strong>false</strong>;</li>

 <li><strong>public void </strong>writer() {</li>

 <li>x = 42;</li>

 <li>v = <strong>true</strong>;</li>

 <li>}</li>

 <li><strong>public void </strong>reader() {</li>

 <li><strong>if </strong>(v == <strong>true</strong>) {</li>

 <li><strong>int </strong>y = 100/x;</li>

 <li>}</li>

 <li>}</li>

 <li>}</li>

</ul>

Listing 1: Volatile field example from section 1.1

<h2>1.2            Sequential Consistency (1)</h2>

For the following executions, please indicate if they are sequentially consistent. All variables are intially set to 0.

<ol>

 <li>P1: W(x,1);</li>

</ol>

P2: R(x,0); R(x,1);

<ol start="2">

 <li>P1: W(x,1); P2: R(x,1); R(x,0);</li>

 <li>P1: W(x,1); P2: W(x,2);</li>

</ol>

P3: R(x,1); R(x,2);

<ol start="4">

 <li>P1: W(x,1); P2: W(x,2);</li>

</ol>

P3: R(x,2); R(x,1);

<ol start="5">

 <li>P1: W(x,1); P2: W(x,2);</li>

</ol>

P3: R(x,2); R(x,1);

P4: R(x,1); R(x,2);

<ol start="6">

 <li>P1: W(x,1); R(x,1); R(y,0); P2: W(y,1); R(y,1); R(x,1);</li>

</ol>

P3: R(x,1); R(y,0);

P4: R(y,0); R(x,0);

<ol start="7">

 <li>P1: W(x,1); R(x,1); R(y,0); P2: W(y,1); R(y,1); R(x,1);</li>

</ol>

P3: R(y,1); R(x,0);

<h2>1.3            Sequential Consistency</h2>

<strong>P1                 P2                 P3</strong>

x = 1;            y = 1;             z = 1;

print(y,z);      print(x,z);      print(x,y);

All variables are stored in a memory system which offers sequential consistency. All operations, even the print statements, are atomic<a href="#_ftn1" name="_ftnref1"><sup>[1]</sup></a>. Are the following sequences legal outputs?

<ol>

 <li>001011</li>

 <li>001111</li>

 <li>001110</li>

</ol>

Explain your answer by showing one possible interleaving of the instructions that might lead to the legal output. In case of an illegal output, explain why no possible interleaving exists.

<h2>1.4            Consistency (1</h2>

Consider a <em>memory object </em>that encompasses two register components. We know that if both registers are quiescently consistent, then so is the memory object. Does the converse hold? If the memory object is quiescently consistent, are the individual registers quiescently consistent? Outline a proof or give a counterexample.

<h2>1.5            Consistency (2)</h2>

Give an example of an execution that is quiescently consistent but not sequentially consistent, and another that is sequentially consistent but not quiescently consistent.

<h2>1.6            Linearizability (1)</h2>

For the following history of a shared register with the operations write(x)/void and read()/x, answer the questions below.

B: r.write(1) A: r.read()

C: r.write(2)

A: r:1

B: r:void

C: r:void

B: r.read() B: r:1

A: q.write(3) C: r.read() A: q:void

<ol>

 <li>What is <em>H|B</em>?</li>

 <li>What is <em>H|r</em>?</li>

 <li>Turn <em>H </em>into a complete subhistory <em>H<sup>0</sup></em>.</li>

 <li>Is <em>H<sup>0 </sup></em>sequential?</li>

 <li>Is <em>H<sup>0 </sup></em>well-formed?</li>

 <li>Is <em>H<sup>0 </sup></em>linearizable? If yes, prove it!</li>

 <li>If the first two events are swapped, is the resulting history equivalent to <em>H</em>?</li>

</ol>

<h2>1.7            Linearizability (2) [7 points]</h2>

Is the following history of a FIFO queue with the operations enq(x)/void deq()/x linearizable? If yes, prove it! Is it sequentially consistent?

A: r.enq(x) A: r:void

B: r.enq(y)

A: r.deq() B: r:void

A: r:y

<h2>1.8            Linearizability (3)</h2>

Is the following history of a fo queue with the operations enq(x)/void deq()/x linearizable? If yes, prove it!

A: q.enq(x)

B: q.enq(y)

A: q:void B: q:void

A: q.deq()

C: q.deq()

A: q:y C: q:y

<h2>1.9            Compositional Linearizability [7 points]</h2>

Proove the “only if” part of Theorem 3.6.1, reprinted below.

<em>H </em>is linearizable if, and only if, for each object <em>x</em>, <em>H|x </em>is linearizable.

<h2>1.10             More Histories (1) [7 points]</h2>

Is this a linearizable execution?

<table width="400">

 <tbody>

  <tr>

   <td width="59">Time</td>

   <td width="172">Task <em>A</em></td>

   <td width="169">Task <em>B</em></td>

  </tr>

  <tr>

   <td width="59">0</td>

   <td width="172">Invoke q.enq(x)</td>

   <td width="169"> </td>

  </tr>

  <tr>

   <td width="59">1</td>

   <td width="172">Work on q.enq(x)</td>

   <td width="169"> </td>

  </tr>

  <tr>

   <td width="59">2</td>

   <td width="172">Work on q.enq(x)</td>

   <td width="169"> </td>

  </tr>

  <tr>

   <td width="59">3</td>

   <td width="172">Return from q.enq(x)</td>

   <td width="169"> </td>

  </tr>

  <tr>

   <td width="59">4</td>

   <td width="172"> </td>

   <td width="169">Invoke q.enq(y)</td>

  </tr>

  <tr>

   <td width="59">5</td>

   <td width="172"> </td>

   <td width="169">Work on q.enq(y)</td>

  </tr>

  <tr>

   <td width="59">6</td>

   <td width="172"> </td>

   <td width="169">Work on q.enq(y)</td>

  </tr>

  <tr>

   <td width="59">7</td>

   <td width="172"> </td>

   <td width="169">Return from q.enq(y)</td>

  </tr>

  <tr>

   <td width="59">8</td>

   <td width="172"> </td>

   <td width="169">Invoke q.deq()</td>

  </tr>

  <tr>

   <td width="59">9</td>

   <td width="172"> </td>

   <td width="169">Return x from q.deq()</td>

  </tr>

 </tbody>

</table>

<h2>1.11             More Histories (2) [7 points]</h2>

Is this a linearizable execution?

<table width="400">

 <tbody>

  <tr>

   <td width="59">Time</td>

   <td width="172">Task <em>A</em></td>

   <td width="169">Task <em>B</em></td>

  </tr>

  <tr>

   <td width="59">0</td>

   <td width="172">Invoke q.enq(x)</td>

   <td width="169"> </td>

  </tr>

  <tr>

   <td width="59">1</td>

   <td width="172">Work on q.enq(x)</td>

   <td width="169">Invoke q.enq(y)</td>

  </tr>

  <tr>

   <td width="59">2</td>

   <td width="172">Work on q.enq(x)</td>

   <td width="169">Return from q.enq(y)</td>

  </tr>

  <tr>

   <td width="59">3</td>

   <td width="172">Return from q.enq(x)</td>

   <td width="169"> </td>

  </tr>

  <tr>

   <td width="59">4</td>

   <td width="172"> </td>

   <td width="169">Invoke q.deq()</td>

  </tr>

  <tr>

   <td width="59">5</td>

   <td width="172"> </td>

   <td width="169">Return x from q.deq()</td>

  </tr>

 </tbody>

</table>

<h2>1.12             More Histories (3) [7 points]</h2>

Is this a linearizable execution?

<table width="400">

 <tbody>

  <tr>

   <td width="59">Time</td>

   <td width="177">Task <em>A</em></td>

   <td width="164">Task <em>B</em></td>

  </tr>

  <tr>

   <td width="59">0</td>

   <td width="177">Invoke q.enq(x)</td>

   <td width="164"> </td>

  </tr>

  <tr>

   <td width="59">1</td>

   <td width="177">Return from q.enq(x)</td>

   <td width="164"> </td>

  </tr>

  <tr>

   <td width="59">2</td>

   <td width="177"> </td>

   <td width="164">Invoke q.enq(y)</td>

  </tr>

  <tr>

   <td width="59">3</td>

   <td width="177">Invoke q.deq()</td>

   <td width="164">Work on q.enq(y)</td>

  </tr>

  <tr>

   <td width="59">4</td>

   <td width="177">Work on q.deq()</td>

   <td width="164">Return from q.enq(y)</td>

  </tr>

  <tr>

   <td width="59">5</td>

   <td width="177">Return y from q.deq()</td>

   <td width="164"> </td>

  </tr>

 </tbody>

</table>

<h2>1.13             AtomicInteger [7 points]</h2>

The AtomicInteger class (in the java.util.concurrent.atomic package) is a container for an integer value. One of its methods is <strong>boolean </strong>compareAndSet

(<strong>int </strong>expect, <strong>int </strong>update).

This method compares the object’s current value to expect. If the values are equal, then it atomically replaces the object’s value with update and returns <strong>true</strong>. Otherwise, it leaves the object’s value unchanged and returns <strong>false</strong>. This class also provides <strong>int </strong>get(), which returns the object’s actual value.

Consider the FIFO queue implementation shown in listing 2. It stores its items in an array items, which, for simplicity, we will assume has unbounded size. It has two AtomicInteger fields: head is the index of the next slot from which to remove an item, and tail is the index of the next slot in which to place an item. Give an example showing that this implementation is not linearizable.

<h2>1.14             Herlihy/Wing queue [9 points]</h2>

This exercise examines a queue implementation (listing 3) whose enq() method does not have a linearization point.

The queue stores its items in an items array, which for simplicity we will assume never hits CAPACITY. The tail field is an AtomicInteger, initially zero. The enq() method reserves a slot by incrementing tail and then storing the item at that location. Note that these two steps are not atomic: there is an interval after tail has been incremented but before the item has been stored in the array.

The deq() method reads the value of tail, then traverses the array in ascending order from slot zero to the tail. For each slot, it swaps <strong>null </strong>with the current contents, returning the first non-<strong>null </strong>item it finds. If all slots are <strong>null</strong>, the procedure is restarted.

Give an example execution showing that the linearization point for enq() cannot occur at line 14<a href="#_ftn2" name="_ftnref2"><sup>[2]</sup></a>. Give another example execution showing that the linearization point for enq() cannot occur at line 15. Since these are the only two memory accesses in enq(), we must conclude that enq() has no single linearization point. Does this mean enq() is not linearizable?

<ul>

 <li><strong>class </strong>IQueue&lt;T&gt; {</li>

 <li>AtomicInteger head = <strong>new </strong>AtomicInteger(0);</li>

 <li>AtomicInteger tail = <strong>new </strong>AtomicInteger(0);</li>

 <li>T[] items = (T[]) <strong>new </strong>Object[Integer.MAX_VALUE];</li>

 <li><strong>public void </strong>enq(T x) {</li>

 <li><strong>int </strong>slot;</li>

 <li><strong>do </strong>{</li>

 <li>slot = tail.get();</li>

 <li>} <strong>while </strong>(!tail.compareAndSet(slot, slot+1));</li>

 <li>items[slot] = x;</li>

 <li>}</li>

 <li><strong>public </strong>T deq() <strong>throws </strong>EmptyException {</li>

 <li>T value;</li>

 <li><strong>int </strong>slot;</li>

 <li><strong>do </strong>{</li>

 <li>slot = head.get();</li>

 <li>value = items[slot];</li>

 <li><strong>if </strong>(value == <strong>null</strong>)</li>

 <li><strong>throw new </strong>EmptyException();</li>

 <li>} <strong>while </strong>(!head.compareAndSet(slot, slot+1));</li>

 <li><strong>return </strong>value;</li>

 <li>}</li>

 <li>}</li>

</ul>

Listing 2: IQueue implementation

<ul>

 <li><strong>public class </strong>HWQueue&lt;T&gt; {</li>

 <li>AtomicReference&lt;T&gt;[] items;</li>

 <li>AtomicInteger tail;</li>

 <li><strong>static final int </strong>CAPACITY = 1024;</li>

</ul>

5

<ul>

 <li><strong>public </strong>HWQueue() {</li>

 <li>items = (AtomicReference&lt;T&gt;[])Array.</li>

</ul>

newInstance(AtomicReference.<strong>class</strong>, CAPACITY);

<ul>

 <li><strong>for </strong>(<strong>int </strong>i = 0; i &lt; items.length; i++) {</li>

 <li>items[i] = <strong>new </strong>AtomicReference&lt;T&gt;(<strong>null</strong>);</li>

 <li>}</li>

 <li>tail = <strong>new </strong>AtomicInteger(0);</li>

 <li>}</li>

 <li><strong>public void </strong>enq(T x) {</li>

 <li><strong>int </strong>i = tail.getAndIncrement();</li>

 <li>items[i].set(x);</li>

 <li>}</li>

 <li><strong>public </strong>T deq() {</li>

 <li><strong>while </strong>(<strong>true</strong>) {</li>

 <li><strong>int </strong>range = tail.get();</li>

 <li><strong>for </strong>(<strong>int </strong>i = 0; i &lt; range; i++) {</li>

 <li>T value = items[i].getAndSet(<strong>null</strong>);</li>

 <li><strong>if </strong>(value != <strong>null</strong>) {</li>

 <li><strong>return </strong>value;</li>

 <li>}</li>

 <li>}</li>

 <li>}</li>

 <li>}</li>

 <li>}</li>

</ul>

Listing 3: Herlihy/Wing queue

<h1>2              Practice [Extra Credit 15 points]</h1>

<h2>Using a Linearizability Checker</h2>

A linearizability checker, as described by <a href="https://github.com/jepsen-io/knossos">Jepsen Knossos</a><a href="https://github.com/jepsen-io/knossos">,</a> works as follows: Given a history of operations by a set of clients and some single-threaded model, attempts to show whether the history is linearizable with respect to that model.

Use the Knossos linearizability checker to evaluate the histories provided in Problems 1.6–1.8 above. To receive full-credit, you should run the checker as described in <a href="https://github.com/jepsen-io/knossos#as-a-library">Knossos#as-a-library</a><a href="https://github.com/jepsen-io/knossos#as-a-library">,</a> and provide screenshots showing your inputs and the output of the tool. A README file has been attached to the assignment page that describes how to setup the library. Compare your answers to problems 1.6–1.8 and the checker’s output; is the outcome of the checker correct? Remember, the author of the checker doesn’t claim the checker to be correct and thus, you must verify the outcome by hand (which you should have already done in the Theory section).

Don’t submit any code as part of this assignment. Include only screenshots in your submission PDF document.

<a href="#_ftnref1" name="_ftn1">[1]</a> no operation can overlap with other operations

<a href="#_ftnref2" name="_ftn2">[2]</a> Hint: give an execution where two enq() calls are not linearized in the order they execute line 14.