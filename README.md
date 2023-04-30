Download Link: https://assignmentchef.com/product/solved-from-language-to-logic-cs221
<br>
In this assignment, you will get some hands-on experience with logic. You’ll see how logic can be used to represent the meaning of natural language sentences, and how it can be used to solve puzzles and prove theorems. Most of this assignment will be translating English into logical formulas, but in Problem 4, we will delve into the mechanics of logical inference.

To get started, launch a Python shell and try typing the following commands to add logical expressions into the knowledge base.

<pre>from logic import *Rain = Atom('Rain')           # ShortcutWet = Atom('Wet')             # Shortcutkb = createResolutionKB()     # Create the knowledge basekb.ask(Wet)                   # Prints "I don't know."kb.ask(Not(Wet))              # Prints "I don't know."kb.tell(Implies(Rain, Wet))   # Prints "I learned something."kb.ask(Wet)                   # Prints "I don't know."kb.tell(Rain)                 # Prints "I learned something."kb.tell(Wet)                  # Prints "I already knew that."kb.ask(Wet)                   # Prints "Yes."kb.ask(Not(Wet))              # Prints "No."kb.tell(Not(Wet))             # Prints "I don't buy that."</pre>

To print out the contents of the knowledge base, you can call <code>kb.dump()</code>. For the example above, you get:

<pre>==== Knowledge base [3 derivations] ===* Or(Not(Rain),Wet)* Rain- Wet</pre>

In the output, ‘*’ means the fact was explicitly added by the user, and ‘-‘ means that it was inferred. Here is a table that describes how logical formulas are represented in code. Use it as a reference guide:

<table>

 <tbody>

  <tr>

   <td><b>Name</b></td>

   <td><b>Mathematical notation</b></td>

   <td><b>Code</b></td>

  </tr>

  <tr>

   <td>Constant symbol</td>

   <td><span id="MathJax-Element-1-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-1" class="math"><span id="MathJax-Span-2" class="mrow"><span id="MathJax-Span-3" class="mtext">stanford</span></span></span></span></td>

   <td><code>Constant('stanford')</code> (must be lowercase)</td>

  </tr>

  <tr>

   <td>Variable symbol</td>

   <td><span id="MathJax-Element-2-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-4" class="math"><span id="MathJax-Span-5" class="mrow"><span id="MathJax-Span-6" class="mi">x</span></span></span></span></td>

   <td><code>Variable('$x')</code> (must be lowercase)</td>

  </tr>

  <tr>

   <td>Atomic formula (atom)</td>

   <td><span id="MathJax-Element-3-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-7" class="math"><span id="MathJax-Span-8" class="mrow"><span id="MathJax-Span-9" class="mtext">Rain</span></span></span></span><span id="MathJax-Element-4-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-10" class="math"><span id="MathJax-Span-11" class="mrow"><span id="MathJax-Span-12" class="mtext">LocatedIn</span><span id="MathJax-Span-13" class="mo">(</span><span id="MathJax-Span-14" class="mtext">stanford</span><span id="MathJax-Span-15" class="mo">,</span><span id="MathJax-Span-16" class="mi">x</span><span id="MathJax-Span-17" class="mo">)</span></span></span></span></td>

   <td><code>Atom('Rain')</code> (predicate must be uppercase)<code>Atom('LocatedIn', 'stanford', '$x')</code> (arguments are symbols)</td>

  </tr>

  <tr>

   <td>Negation</td>

   <td><span id="MathJax-Element-5-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-18" class="math"><span id="MathJax-Span-19" class="mrow"><span id="MathJax-Span-20" class="mi">¬</span><span id="MathJax-Span-21" class="mtext">Rain</span></span></span></span></td>

   <td><code>Not(Atom('Rain'))</code></td>

  </tr>

  <tr>

   <td>Conjunction</td>

   <td><span id="MathJax-Element-6-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-22" class="math"><span id="MathJax-Span-23" class="mrow"><span id="MathJax-Span-24" class="mtext">Rain</span><span id="MathJax-Span-25" class="mo">∧</span><span id="MathJax-Span-26" class="mtext">Snow</span></span></span></span></td>

   <td><code>And(Atom('Rain'), Atom('Snow'))</code></td>

  </tr>

  <tr>

   <td>Disjunction</td>

   <td><span id="MathJax-Element-7-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-27" class="math"><span id="MathJax-Span-28" class="mrow"><span id="MathJax-Span-29" class="mtext">Rain</span><span id="MathJax-Span-30" class="mo">∨</span><span id="MathJax-Span-31" class="mtext">Snow</span></span></span></span></td>

   <td><code>Or(Atom('Rain'), Atom('Snow'))</code></td>

  </tr>

  <tr>

   <td>Implication</td>

   <td><span id="MathJax-Element-8-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-32" class="math"><span id="MathJax-Span-33" class="mrow"><span id="MathJax-Span-34" class="mtext">Rain</span><span id="MathJax-Span-35" class="mo">→</span><span id="MathJax-Span-36" class="mtext">Wet</span></span></span></span></td>

   <td><code>Implies(Atom('Rain'), Atom('Wet'))</code></td>

  </tr>

  <tr>

   <td>Equivalence</td>

   <td><span id="MathJax-Element-9-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-37" class="math"><span id="MathJax-Span-38" class="mrow"><span id="MathJax-Span-39" class="mtext">Rain</span><span id="MathJax-Span-40" class="mo">&#x2194;</span><span id="MathJax-Span-41" class="mtext">Wet</span></span></span></span> (syntactic sugar for <span id="MathJax-Element-10-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-42" class="math"><span id="MathJax-Span-43" class="mrow"><span id="MathJax-Span-44" class="mtext">Rain</span><span id="MathJax-Span-45" class="mo">→</span><span id="MathJax-Span-46" class="mtext">Wet</span><span id="MathJax-Span-47" class="mo">∧</span><span id="MathJax-Span-48" class="mtext">Wet</span><span id="MathJax-Span-49" class="mo">→</span><span id="MathJax-Span-50" class="mtext">Rain</span></span></span></span>)</td>

   <td><code>Equiv(Atom('Rain'), Atom('Wet'))</code></td>

  </tr>

  <tr>

   <td>Existential quantification</td>

   <td><span id="MathJax-Element-11-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-51" class="math"><span id="MathJax-Span-52" class="mrow"><span id="MathJax-Span-53" class="mi">∃</span><span id="MathJax-Span-54" class="mi">x</span><span id="MathJax-Span-55" class="mo">.</span><span id="MathJax-Span-56" class="mtext">LocatedIn</span><span id="MathJax-Span-57" class="mo">(</span><span id="MathJax-Span-58" class="mtext">stanford</span><span id="MathJax-Span-59" class="mo">,</span><span id="MathJax-Span-60" class="mi">x</span><span id="MathJax-Span-61" class="mo">)</span></span></span></span></td>

   <td><code>Exists('$x', Atom('LocatedIn', 'stanford', '$x'))</code></td>

  </tr>

  <tr>

   <td>Universal quantification</td>

   <td><span id="MathJax-Element-12-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-62" class="math"><span id="MathJax-Span-63" class="mrow"><span id="MathJax-Span-64" class="mi">∀</span><span id="MathJax-Span-65" class="mi">x</span><span id="MathJax-Span-66" class="mo">.</span><span id="MathJax-Span-67" class="mtext">MadeOfAtoms</span><span id="MathJax-Span-68" class="mo">(</span><span id="MathJax-Span-69" class="mi">x</span><span id="MathJax-Span-70" class="mo">)</span></span></span></span></td>

   <td><code>Forall('$x', Atom('MadeOfAtoms', '$x'))</code></td>

  </tr>

 </tbody>

</table>

The operations <code>And</code> and <code>Or</code> only take two arguments. If we want to take a conjunction or disjunction of more than two, use <code>AndList</code> and <code>OrList</code>. For example: <code>AndList([Atom('A'), Atom('B'), Atom('C')])</code> is equivalent to <code>And(And(Atom('A'), Atom('B')), Atom('C'))</code>.

Write a propositional logic formula for each of the following English sentences in the given function in <code><a href="submission.py">submission.py</a></code>. For example, if the sentence is <i>“If it is raining, it is wet,”</i> then you would write <code>Implies(Atom('Rain'), Atom('Wet'))</code>, which would be <span id="MathJax-Element-13-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-71" class="math"><span id="MathJax-Span-72" class="mrow"><span id="MathJax-Span-73" class="mtext">Rain</span><span id="MathJax-Span-74" class="mo">→</span><span id="MathJax-Span-75" class="mtext">Wet</span></span></span></span> in symbols (see <code><a href="examples.py">examples.py</a></code>). Note: Don’t forget to return the constructed formula!

<ol class="problem">

 <li id="1a" class="code">[2 points] <i>“If it’s summer and we’re in California, then it doesn’t rain.”</i></li>

 <li id="1b" class="code">[2 points] <i>“It’s wet if and only if it is raining or the sprinklers are on.”</i></li>

 <li id="1c" class="code">[2 points] <i>“Either it’s day or night (but not both).”</i></li>

</ol>

You can run the following command to test each formula:

<pre>python grader.py 1a</pre>

If your formula is wrong, then the grader will provide a counterexample, which is a model that your formula and the correct formula don’t agree on. For example, if you accidentally wrote <code>And(Atom('Rain'), Atom('Wet'))</code> for <i>“If it is raining, it is wet,”</i>, then the grader would output the following:

<pre>Your formula (And(Rain,Wet)) says the following model is FALSE, but it should be TRUE:* Rain = False* Wet = True* (other atoms if any) = False</pre>

In this model, it’s not raining and it is wet, which satisfies the correct formula <span id="MathJax-Element-14-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-76" class="math"><span id="MathJax-Span-77" class="mrow"><span id="MathJax-Span-78" class="mtext">Rain</span><span id="MathJax-Span-79" class="mo">→</span><span id="MathJax-Span-80" class="mtext">Wet</span></span></span></span> (TRUE), but does not satisfy the incorrect formula <span id="MathJax-Element-15-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-81" class="math"><span id="MathJax-Span-82" class="mrow"><span id="MathJax-Span-83" class="mtext">Rain</span><span id="MathJax-Span-84" class="mo">∧</span><span id="MathJax-Span-85" class="mtext">Wet</span></span></span></span> (FALSE). Use these counterexamples to guide you in the rest of the assignment.

Write a first-order logic formula for each of the following English sentences in the given function in <code><a href="submission.py">submission.py</a></code>. For example, if the sentence is <i>“There is a light that shines,”</i> then you would write <code>Exists('$x', And(Atom('Light', '$x'), Atom('Shines', '$x')))</code>, which would be <span id="MathJax-Element-16-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-86" class="math"><span id="MathJax-Span-87" class="mrow"><span id="MathJax-Span-88" class="mi">∃</span><span id="MathJax-Span-89" class="mi">x</span><span id="MathJax-Span-90" class="mo">.</span><span id="MathJax-Span-91" class="mtext">Light</span><span id="MathJax-Span-92" class="mo">(</span><span id="MathJax-Span-93" class="mi">x</span><span id="MathJax-Span-94" class="mo">)</span><span id="MathJax-Span-95" class="mo">∧</span><span id="MathJax-Span-96" class="mtext">Shines</span><span id="MathJax-Span-97" class="mo">(</span><span id="MathJax-Span-98" class="mi">x</span><span id="MathJax-Span-99" class="mo">)</span></span></span></span> in symbols (see <code><a href="examples.py">examples.py</a></code>).

<i>Tip</i>: Python tuples can span multiple lines, which help with readability when you are writing logic expressions (some of them in this homework can get quite large)

<ol class="problem">

 <li id="2a" class="code">[2 points] <i>“Every person has a mother.”</i></li>

 <li id="2b" class="code">[2 points] <i>“At least one person has no children.”</i></li>

 <li id="2c" class="code">[2 points] Create a formula which defines <code>Daughter(x,y)</code> in terms of <code>Female(x)</code> and <code>Child(x,y)</code>.</li>

 <li id="2d" class="code">[2 points] Create a formula which defines <code>Grandmother(x,y)</code> in terms of <code>Female(x)</code> and <code>Parent(x,y)</code>.</li>

</ol>

Someone crashed the server, and accusations are flying. For this problem, we will encode the evidence in first-order logic formulas to find out who crashed the server. You’ve narrowed it down to four suspects: John, Susan, Mark, and Nicole. You have the following information:

<ul>

 <li>John says: “It wasn’t me!”</li>

 <li>Susan says: “It was Nicole!”</li>

 <li>Mark says: “No, it was Susan!”</li>

 <li>Nicole says: “Susan’s a liar.”</li>

 <li>You know that exactly one person is telling the truth.</li>

 <li>You also know exactly one person crashed the server.</li>

</ul>

<ol class="problem">

 <li id="3a" class="code">[8 points] Fill out <code>liar()</code> to return a list of 6 formulas, one for each of the above facts. Be sure your formulas are exactly in the order specified.</li>

</ol>

You can test your code using the following commands:

<pre>python grader.py 3a-0python grader.py 3a-1python grader.py 3a-2python grader.py 3a-3python grader.py 3a-4python grader.py 3a-5python grader.py 3a-all  # Tests the conjunction of all the formulas</pre>

To solve the puzzle and find the answer, <code>tell</code> the formulas to the knowledge base and <code>ask</code> the query <code>CrashedServer('$x')</code>, by running:

<pre>python grader.py 3a-run</pre>

Having obtained some intuition on how to construct formulas, we will now perform logical inference to derive new formulas from old ones. Recall that:

<ul>

 <li>Modus ponens asserts that if we have two formulas, <span id="MathJax-Element-17-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-100" class="math"><span id="MathJax-Span-101" class="mrow"><span id="MathJax-Span-102" class="mi">A</span><span id="MathJax-Span-103" class="mo">→</span><span id="MathJax-Span-104" class="mi">B</span></span></span></span> and <span id="MathJax-Element-18-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-105" class="math"><span id="MathJax-Span-106" class="mrow"><span id="MathJax-Span-107" class="mi">A</span></span></span></span> in our knowledge base, then we can derive <span id="MathJax-Element-19-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-108" class="math"><span id="MathJax-Span-109" class="mrow"><span id="MathJax-Span-110" class="mi">B</span></span></span></span>.</li>

 <li>Resolution asserts that if we have two formulas, <span id="MathJax-Element-20-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-111" class="math"><span id="MathJax-Span-112" class="mrow"><span id="MathJax-Span-113" class="mi">A</span><span id="MathJax-Span-114" class="mo">∨</span><span id="MathJax-Span-115" class="mi">B</span></span></span></span> and <span id="MathJax-Element-21-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-116" class="math"><span id="MathJax-Span-117" class="mrow"><span id="MathJax-Span-118" class="mi">¬</span><span id="MathJax-Span-119" class="mi">B</span><span id="MathJax-Span-120" class="mo">∨</span><span id="MathJax-Span-121" class="mi">C</span></span></span></span> in our knowledge base, then we can derive <span id="MathJax-Element-22-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-122" class="math"><span id="MathJax-Span-123" class="mrow"><span id="MathJax-Span-124" class="mi">A</span><span id="MathJax-Span-125" class="mo">∨</span><span id="MathJax-Span-126" class="mi">C</span></span></span></span>.</li>

 <li>If <span id="MathJax-Element-23-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-127" class="math"><span id="MathJax-Span-128" class="mrow"><span id="MathJax-Span-129" class="mi">A</span><span id="MathJax-Span-130" class="mo">∧</span><span id="MathJax-Span-131" class="mi">B</span></span></span></span> is in the knowledge base, then we can derive both <span id="MathJax-Element-24-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-132" class="math"><span id="MathJax-Span-133" class="mrow"><span id="MathJax-Span-134" class="mi">A</span></span></span></span> and <span id="MathJax-Element-25-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-135" class="math"><span id="MathJax-Span-136" class="mrow"><span id="MathJax-Span-137" class="mi">B</span></span></span></span>.</li>

</ul>

<ol class="problem">

 <li id="4a" class="writeup">[5 points] Some inferences that might look like they’re outside the scope of Modus ponens are actually within reach. Suppose the knowledge base contains the following two formulas:<b>Your task: </b>First, convert the knowledge base into conjunctive normal form (CNF). Then apply Modus ponens to derive C. Please show how your knowledge base changes as you apply derivation rules.<i>Hint:</i> You may use the fact that <span id="MathJax-Element-27-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-154" class="math"><span id="MathJax-Span-155" class="mrow"><span id="MathJax-Span-156" class="mi">P</span><span id="MathJax-Span-157" class="mo">→</span><span id="MathJax-Span-158" class="mi">Q</span></span></span></span> is equivalent <span id="MathJax-Element-28-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-159" class="math"><span id="MathJax-Span-160" class="mrow"><span id="MathJax-Span-161" class="mi">¬</span><span id="MathJax-Span-162" class="mi">P</span><span id="MathJax-Span-163" class="mo">∨</span><span id="MathJax-Span-164" class="mi">Q</span></span></span></span>.Remember, this isn’t about you as a human being able to arrive at the conclusion, but rather about the rote application of a small set of transformations (which a computer could execute).</li>

 <li id="4b" class="writeup">[5 points] Recall that Modus ponens is not complete, meaning that we can’t use it to derive everything that’s true. Suppose the knowledge base contains the following formulas:In this example, Modus ponens cannot be used to derive <span id="MathJax-Element-30-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-187" class="math"><span id="MathJax-Span-188" class="mrow"><span id="MathJax-Span-189" class="mi">D</span></span></span></span>, even though <span id="MathJax-Element-31-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-190" class="math"><span id="MathJax-Span-191" class="mrow"><span id="MathJax-Span-192" class="mi">D</span></span></span></span> is entailed by the knowledge base. However, recall that the resolution rule is complete.<b>Your task: </b>Convert the knowledge base into CNF and apply the resolution rule repeatedly to derive <span id="MathJax-Element-32-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-193" class="math"><span id="MathJax-Span-194" class="mrow"><span id="MathJax-Span-195" class="mi">D</span></span></span></span>.</li>

</ol>

In this problem, we will see how to use logic to automatically prove mathematical theorems. We will focus on encoding the theorem and leave the proving part to the logical inference algorithm. Here is the theorem:

If the following constraints hold:

<ul>

 <li>Each number <span id="MathJax-Element-33-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-196" class="math"><span id="MathJax-Span-197" class="mrow"><span id="MathJax-Span-198" class="mi">x</span></span></span></span> has exactly one successor, which is not equal to <span id="MathJax-Element-34-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-199" class="math"><span id="MathJax-Span-200" class="mrow"><span id="MathJax-Span-201" class="mi">x</span></span></span></span>.</li>

 <li>Each number is either odd or even, but not both.</li>

 <li>The successor of an even number is odd.</li>

 <li>The successor of an odd number is even.</li>

 <li>For every number <span id="MathJax-Element-35-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-202" class="math"><span id="MathJax-Span-203" class="mrow"><span id="MathJax-Span-204" class="mi">x</span></span></span></span>, the successor of <span id="MathJax-Element-36-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-205" class="math"><span id="MathJax-Span-206" class="mrow"><span id="MathJax-Span-207" class="mi">x</span></span></span></span> is larger than <span id="MathJax-Element-37-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-208" class="math"><span id="MathJax-Span-209" class="mrow"><span id="MathJax-Span-210" class="mi">x</span></span></span></span>.</li>

 <li>Larger is a transitive property: if <span id="MathJax-Element-38-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-211" class="math"><span id="MathJax-Span-212" class="mrow"><span id="MathJax-Span-213" class="mi">x</span></span></span></span> is larger than <span id="MathJax-Element-39-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-214" class="math"><span id="MathJax-Span-215" class="mrow"><span id="MathJax-Span-216" class="mi">y</span></span></span></span> and <span id="MathJax-Element-40-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-217" class="math"><span id="MathJax-Span-218" class="mrow"><span id="MathJax-Span-219" class="mi">y</span></span></span></span> is larger than <span id="MathJax-Element-41-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-220" class="math"><span id="MathJax-Span-221" class="mrow"><span id="MathJax-Span-222" class="mi">z</span></span></span></span>, then <span id="MathJax-Element-42-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-223" class="math"><span id="MathJax-Span-224" class="mrow"><span id="MathJax-Span-225" class="mi">x</span></span></span></span> is larger than <span id="MathJax-Element-43-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-226" class="math"><span id="MathJax-Span-227" class="mrow"><span id="MathJax-Span-228" class="mi">z</span></span></span></span>.</li>

</ul>

Then we have the following consequence:

<ul>

 <li>For each number, there is an even number larger than it.</li>

</ul>

Note: in this problem, “larger than” is just an arbitrary relation, and you should not assume it has any prior meaning. In other words, don’t assume things like “a number can’t be larger than itself” unless explicitly stated.

<ol class="problem">

 <li id="5a" class="code">[8 points] Fill out <code>ints()</code> to construct 6 formulas for each of the constraints. The consequence has been filled out for you (<code>query</code> in the code). You can test your code using the following commands:<pre>python grader.py 5a-0python grader.py 5a-1python grader.py 5a-2python grader.py 5a-3python grader.py 5a-4python grader.py 5a-5python grader.py 5a-all  # Tests the conjunction of all the formulas</pre>To finally prove the theorem, <code>tell</code> the formulas to the knowledge base and <code>ask</code> the query by running model checking (on a finite model):<pre>python grader.py 5a-run</pre></li>

 <li id="5b" class="writeup">[10 points] Suppose we added another constraint:

  <ul>

   <li>A number is not larger than itself.</li>

  </ul>Prove that there is no finite, non-empty model for which the resulting set of 7 constraints is consistent. This means that if we try to prove this theorem by model checking only finite models, we will find that it is false, when in fact the theorem is true for a countably infinite model (where the objects in the model are the numbers).</li>

</ol>

Semantic parsing is the task of converting natural lanugage utterances into first-order logic formulas. We have created a small set of grammar rules in the code for you in <code>createBaseEnglishGrammar()</code>. In this problem, you will add additional grammar rules to handle a wider variety of sentences. Specifically, create a <code>GrammarRule</code> for each of the following sentence structures.

<ol class="problem">

 <li id="6a" class="code">[5 points] Example: <i>Every person likes some cat.</i> General template:<pre>$Clause ← every $Noun $Verb some $Noun</pre></li>

 <li id="6b" class="code">[3 points] Example: <i>There is some cat that every person likes.</i> General template:<pre>$Clause ← there is some $Noun that every $Noun $Verb</pre></li>

 <li id="6c" class="code">[4 points] Example: <i>If a person likes a cat then the former feeds the latter.</i> General template:<pre>$Clause ← if a $Noun $Verb a $Noun then the former $Verb the latter</pre></li>

</ol>

After implementing these functions, you should be able to try some simple queries using <code><a href="nli.py">nli.py</a></code>! For example:

<pre>$ python nli.py&gt; Every person likes some cat.&gt;&gt;&gt;&gt;&gt; I learned something.------------------------------&gt; Every cat is a mammal.&gt;&gt;&gt;&gt;&gt; I learned something.------------------------------&gt; Every person likes some mammal?&gt;&gt;&gt;&gt;&gt; Yes.</pre>

5/5 - (1 vote)

This (and every) assignment has a written part and a programming part.

The full assignment with our supporting code and scripts can be downloaded as <a href="../logic.zip">logic.zip</a>.

<ol class="problem">

 <li class="writeup template">This icon means a written answer is expected in <code>logic.pdf</code>.</li>

 <li class="code template">This icon means you should write code in <code><a href="submission.py">submission.py</a></code>.</li>

</ol>

You should modify the code in <code><a href="submission.py">submission.py</a></code> between

<pre># BEGIN_YOUR_CODE</pre>

and

<pre># END_YOUR_CODE</pre>

but you can add other helper functions outside this block if you want. Do not make changes to files other than <code><a href="submission.py">submission.py</a></code>.Your code will be evaluated on two types of test cases, <b>basic</b> and <b>hidden</b>, which you can see in <code><a href="grader.py">grader.py</a></code>. Basic tests, which are fully provided to you, do not stress your code with large inputs or tricky corner cases. Hidden tests are more complex and do stress your code. The inputs of hidden tests are provided in <code><a href="grader.py">grader.py</a></code>, but the correct outputs are not. To run the tests, you will need to have <code><a href="graderUtil.py">graderUtil.py</a></code> in the same directory as your code and <code><a href="grader.py">grader.py</a></code>. Then, you can run all the tests by typing

<pre>python grader.py</pre>

This will tell you only whether you passed the basic tests. On the hidden tests, the script will alert you if your code takes too long or crashes, but does not say whether you got the correct output. You can also run a single test (e.g., <code>3a-0-basic</code>) by typing

<pre>python grader.py 3a-0-basic</pre>

We strongly encourage you to read and understand the test cases, create your own test cases, and not just blindly run <code><a href="grader.py">grader.py</a></code>.

<hr>

<b></b>General Instructions

Problem 1: Propositional logic

Problem 2: First-order logic

Problem 3: Liar puzzle

Problem 4: Logical Inference

<span id="MathJax-Element-26-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-138" class="math"><span id="MathJax-Span-139" class="mrow"><span id="MathJax-Span-140" class="mtext">KB</span><span id="MathJax-Span-141" class="mo">=</span><span id="MathJax-Span-142" class="mo">{</span><span id="MathJax-Span-143" class="mo">(</span><span id="MathJax-Span-144" class="mi">A</span><span id="MathJax-Span-145" class="mo">∨</span><span id="MathJax-Span-146" class="mi">B</span><span id="MathJax-Span-147" class="mo">)</span><span id="MathJax-Span-148" class="mo">→</span><span id="MathJax-Span-149" class="mi">C</span><span id="MathJax-Span-150" class="mo">,</span><span id="MathJax-Span-151" class="mi">A</span><span id="MathJax-Span-152" class="mo">}</span><span id="MathJax-Span-153" class="mo">.</span></span></span></span>

<span id="MathJax-Element-29-Frame" class="MathJax" tabindex="0"><span id="MathJax-Span-165" class="math"><span id="MathJax-Span-166" class="mrow"><span id="MathJax-Span-167" class="mtext">KB</span><span id="MathJax-Span-168" class="mo">=</span><span id="MathJax-Span-169" class="mo">{</span><span id="MathJax-Span-170" class="mi">A</span><span id="MathJax-Span-171" class="mo">∨</span><span id="MathJax-Span-172" class="mi">B</span><span id="MathJax-Span-173" class="mo">,</span><span id="MathJax-Span-174" class="mi">B</span><span id="MathJax-Span-175" class="mo">→</span><span id="MathJax-Span-176" class="mi">C</span><span id="MathJax-Span-177" class="mo">,</span><span id="MathJax-Span-178" class="mo">(</span><span id="MathJax-Span-179" class="mi">A</span><span id="MathJax-Span-180" class="mo">∨</span><span id="MathJax-Span-181" class="mi">C</span><span id="MathJax-Span-182" class="mo">)</span><span id="MathJax-Span-183" class="mo">→</span><span id="MathJax-Span-184" class="mi">D</span><span id="MathJax-Span-185" class="mo">}</span><span id="MathJax-Span-186" class="mo">.</span></span></span></span>

Problem 5: Odd and even integers