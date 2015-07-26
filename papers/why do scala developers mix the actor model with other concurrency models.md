<div id="table-of-contents">
<h2>Table of Contents</h2>
<div id="text-table-of-contents">
<ul>
<li><a href="#sec-1">1. why do scala developers mix the Actor model with other concurrency models?</a>
<ul>
<li><a href="#sec-1-1">1.1. ECOOP 2013, 24 citation</a></li>
<li><a href="#sec-1-2">1.2. Abstract</a>
<ul>
<li><a href="#sec-1-2-1">1.2.1. disadvantages</a></li>
<li><a href="#sec-1-2-2">1.2.2. motivation</a></li>
<li><a href="#sec-1-2-3">1.2.3. conclusion/contribution</a></li>
</ul>
</li>
<li><a href="#sec-1-3">1.3. Introduction</a>
<ul>
<li><a href="#sec-1-3-1">1.3.1. Actor's main advantage</a></li>
<li><a href="#sec-1-3-2">1.3.2. Motivation</a></li>
<li><a href="#sec-1-3-3">1.3.3. Three Questions:</a></li>
<li><a href="#sec-1-3-4">1.3.4. Methodology</a></li>
<li><a href="#sec-1-3-5">1.3.5. Contributions</a></li>
</ul>
</li>
<li><a href="#sec-1-4">1.4. section 4: Results</a>
<ul>
<li><a href="#sec-1-4-1">1.4.1. RQ1: How Often Do Scala Programmers Mix Actors with other Kinds of Concurrent Entities?</a></li>
<li><a href="#sec-1-4-2">1.4.2. RQ2: How Many of the Programs are Distributed over the Network, and Does Distribution Influence the Way Programmers Mix Concurrency Models?</a></li>
<li><a href="#sec-1-4-3">1.4.3. RQ3: How Often Do the Actors in the Programs Use Communication Mechanisms other Than Asynchronous Messaging?</a></li>
</ul>
</li>
<li><a href="#sec-1-5">1.5. Section 5: The Reasons for Mixing Concurrency Models</a>
<ul>
<li><a href="#sec-1-5-1">1.5.1. Actor library inadequacies</a></li>
<li><a href="#sec-1-5-2">1.5.2. Actor model inadequacies</a></li>
<li><a href="#sec-1-5-3">1.5.3. Inadequate developer experience</a></li>
</ul>
</li>
<li><a href="#sec-1-6">1.6. Section 6: Implications and Discussion</a>
<ul>
<li><a href="#sec-1-6-1">1.6.1. Implications for Researchers</a></li>
<li><a href="#sec-1-6-2">1.6.2. Implications for Library Developers:</a></li>
</ul>
</li>
<li><a href="#sec-1-7">1.7. Section 8: Related Work</a>
<ul>
<li><a href="#sec-1-7-1">1.7.1. Another line of work integrates the actor model with task parallelism. Haller et al. augment the Scala actor library with join patterns. PAM adds parallel execution of messages inside of actors to achieve better performance. JCoBox combines actors and futures to implement parallel execution of tasks and synchronous messaging. Immam et al. propose a unified parallel programming model for Scala and Java that integrates the actor model with the divide-and-conquer task parallel model.</a></li>
<li><a href="#sec-1-7-2">1.7.2. These works use small benchmarks to show that implementing certain protocols with their proposed model is easier and can provide better performance than the pure actor model.</a></li>
<li><a href="#sec-1-7-3">1.7.3. However, none of these works conducts any study on real-world programs to show the weaknesses of the actor libraries or the actor model. Our study complements these works by supplying the empirical evidence for these weaknesses.</a></li>
</ul>
</li>
<li><a href="#sec-1-8">1.8. Section 9: Future Work:</a>
<ul>
<li><a href="#sec-1-8-1">1.8.1. A direction for future work is to correlate the phenomenon of mixing concurrency models with bug rates and types.</a></li>
<li><a href="#sec-1-8-2">1.8.2. A related question is whether mixing occurs across different layers of abstraction. For example, mixing may occur only on the lower, more concrete layers of the program while actors prevail on the higher, more abstract layers.</a></li>
<li><a href="#sec-1-8-3">1.8.3. Finally, it would be interesting to see how different actor libraries for the same language, for example Scala, affect the design decisions of programmers.</a></li>
</ul>
</li>
</ul>
</li>
</ul>
</div>
</div>


\## ECOOP 2013, 24 citation<a id="sec-1-1" name="sec-1-1"></a>

\## Abstract<a id="sec-1-2" name="sec-1-2"></a>

\### disadvantages<a id="sec-1-2-1" name="sec-1-2-1"></a>

1.  break the actor abstraction: This increases the chance of creating deadlocks and data races—two mistakes that are hard to make with actors.

2.  Furthermore, it prevents the use of many advanced testing, modeling, and verification tools for actors, as these require pure actor programs.

\### motivation<a id="sec-1-2-2" name="sec-1-2-2"></a>

1.  This study is the first to point out the phenomenon of mixing concurrency models by Scala developers and to systematically identify the factors leading to it. We studied 15 large, mature, and actively maintained actor programs written in Scala and found that 80% of them mix the actor model with another concurrency model.

2.  Consequently, a large part of real-world actor programs does not use actors to their fullest advantage.

\### conclusion/contribution<a id="sec-1-2-3" name="sec-1-2-3"></a>

1.  Inspection of the programs and discussion with the developers reveal two reasons for mixing that can be influenced by researchers and library-builders: weaknesses in the actor library implementations, and shortcomings of the actor model itself.

\## Introduction<a id="sec-1-3" name="sec-1-3"></a>

\### Actor's main advantage<a id="sec-1-3-1" name="sec-1-3-1"></a>

1.  The model’s restriction of communication to asynchronous message-passing simplifie sreasoning about concurrency, guarantees scalability, allows distributing the program over the network, and enables efficient tools for testing [17,32], modeling and verifying actor programs.

\### Motivation<a id="sec-1-3-2" name="sec-1-3-2"></a>

1.  This raised the question why programmers gave up the advantages of actors and mixed them with threads. Was it a temporary measure, as the programmers converted thread-based parallelism to actors? Does this indicate problems with the actor model, with the implementation of the actor libraries for Scala, or in the education of Scala programmers?

\### Three Questions:<a id="sec-1-3-3" name="sec-1-3-3"></a>

1.  RQ1. How often do Scala programmers mix actors with other kinds of concurrent entities? This question obviously goes far beyond Scala, but we decided to look first at Scala before looking at other languages

2.  RQ2. How many of the programs are distributed over the network, and does distribution influence the way programmers mix concurrency models? Our motivation for this question is that the actor model can be used to exploit multiple local processors, as well as to distribute the program over the network. Hence, one reason for mixing concurrency models could be that some models are better for particular kinds of programming than others.

3.  RQ3. How often do the actors in the programs use communication mechanisms other than asynchronous messaging? Communication through asynchronous messaging reduces the possibility of deadlock and data races, which are common problems in the shared-memory model. However, in Scala, actors can also communicate via other mechanisms such as shared locks.

\### Methodology<a id="sec-1-3-4" name="sec-1-3-4"></a>

1.  This paper describes how we selected programs to study

2.  the way we measured them, the resulting measurements (Section 4), and the conclusions we drew.

3.  We also contacted the developers, and they provided many insights into the meaning of our observations

4.  Our findings (Section 6) reveal that the reasons for mixing the actor model with other concurrency models are mostly due to weaknesses in the implementations of the libraries. However, they also show weaknesses in the actor model itself, as well as in the experience of developers.

\### Contributions<a id="sec-1-3-5" name="sec-1-3-5"></a>

1.  1. It is the first to point out the phenomenon of Scala developers mixing theactor model with other concurrency models.

2.  2. It gives statistics about mixing actors with other kinds of concurrent entities in real-world Scala programs.

3.  3. It gives recommendations for researchers and actor-library designers.

\## section 4: Results<a id="sec-1-4" name="sec-1-4"></a>

\### RQ1: How Often Do Scala Programmers Mix Actors with other Kinds of Concurrent Entities?<a id="sec-1-4-1" name="sec-1-4-1"></a>

1.  The results in Table 2 show that 13 of the 16 programs (81%) mix concurrent entities and 12 of the 15 programs (80%) mix Actor with Runnable or Future.

2.  It is therefore not surprising to find that 8 out of 15 programs (53%) that use actors also use futures.

3.  In Table 2, 10 out of 15 programs (66%) use both Actor and Runnable.

\### RQ2: How Many of the Programs are Distributed over the Network, and Does Distribution Influence the Way Programmers Mix Concurrency Models?<a id="sec-1-4-2" name="sec-1-4-2"></a>

1.  Only 3 out of 16 programs use actors for remote deployment

2.  7 out of the 16 programs are distributed

3.  This implies that developers tend to use other ways than remote actors for implementing distributed computations.

\### RQ3: How Often Do the Actors in the Programs Use Communication Mechanisms other Than Asynchronous Messaging?<a id="sec-1-4-3" name="sec-1-4-3"></a>

1.  (1) Non-blocking operations like sending asynchronous messages (sm); resolving a future (rf); and signaling a synchronization construct (ss), for example counting down a latch or releasing a lock.

2.  (2) Blocking operations like waiting to receive a message from a channel (wm); waiting for a future to be resolved (wf); and waiting for a synchronization construct to be signaled (ws), for example waiting on a latch.

3.  (3) Other operations that do not fit in either of the above categories, for example communication via external resources like files or shared objects that are not synchronization constructs.

4.  in at least 9 out of 15 programs (60%), actors use communication mechanisms other than asynchronous messaging

\## Section 5: The Reasons for Mixing Concurrency Models<a id="sec-1-5" name="sec-1-5"></a>

\### Actor library inadequacies<a id="sec-1-5-1" name="sec-1-5-1"></a>

1.  Efficient I/O

2.  Spark: Spark is a distributed computation framework that needs to exchange large blocks of data over the network. Because the developers are unsure about the actor library’s performance regarding large data transfer, they spawn dedicated threads for handling this task.

3.  “[&#x2026;] in ParallelShuffleFetcher, we are receiving large blocks of datafrom multiple machines. Most actor libraries don’t deal well with thatthey are optimized for transferring small messages (up to a few hundred bytes) [&#x2026;], and they might have a small number of IO threads that block when you’re sending something bigger. In this case, instead of worryingabout whether the actor library will handle the transfer well [&#x2026;] and whether it will affect other messages being sent by other actors, we chose to explicitly spawn threads. I’d love an actor library that also handleslarge IOs, or exposes asynchronous IO primitives, but I haven’t foundone.”

4.  Low-End Systems.

5.  Managing and Debugging Many Blocking Operations

6.  Customized Actors.

\### Actor model inadequacies<a id="sec-1-5-2" name="sec-1-5-2"></a>

1.  The example shows that implementing some coordination protocols in the actor model can be more complex than using a shared-memory model. The developers may need to add extra variables and implement more complex logic to handle the asynchrony in the actor model that is not present in the sharedmemory model. Specifically, for developers who are new to the actor model, understanding and managing coordination in an asynchronous and no-shared state model might be harder than in the shared-memory model.

2.  To address this problem, prior work has extended the Scala actor library with coordination patterns used in parallel programming, for example joins and divide-and-conquer tasks . More advanced coordination mechanisms for actor systems have also been proposed [4,31,9,27]. However,to the best of our knowledge, none has been integrated with a widely used actor library.

\### Inadequate developer experience<a id="sec-1-5-3" name="sec-1-5-3"></a>

\## Section 6: Implications and Discussion<a id="sec-1-6" name="sec-1-6"></a>

\### Implications for Researchers<a id="sec-1-6-1" name="sec-1-6-1"></a>

1.  Each model has its strengths, and developers tend to use the model that best fits the problem.

2.  However, the current implementations of actors in the Scala standard library and Akka force developers to use models other than actors to meet the application requirements.

3.  Specifically, mixtures of Actor and Future are common, as they help implementing coordination between the purely asynchronous actors.

4.  On the other hand, the results show that in three cases, mixing actors with threads is unnecessary.

5.  The actor model itself also puts a burden on developers. The property of no shared state and asynchronous communication can make implementing coordination protocols harder than using established constructs like locks.

\### Implications for Library Developers:<a id="sec-1-6-2" name="sec-1-6-2"></a>

1.  First, the API can provide commonly required features like modules for efficiently handling or customizing I/O.

2.  Second, it can prevent developers from misusing the library constructs and violating best practices. For example, if messages were restricted to immutabletypes, actors could not easily share objects by exchanging references through messages. While libraries cannot completely prevent shared state in actors, such a limitation would push developers towards using a proper design.

\## Section 8: Related Work<a id="sec-1-7" name="sec-1-7"></a>

\### Another line of work integrates the actor model with task parallelism. Haller et al. augment the Scala actor library with join patterns. PAM adds parallel execution of messages inside of actors to achieve better performance. JCoBox combines actors and futures to implement parallel execution of tasks and synchronous messaging. Immam et al. propose a unified parallel programming model for Scala and Java that integrates the actor model with the divide-and-conquer task parallel model.<a id="sec-1-7-1" name="sec-1-7-1"></a>

\### These works use small benchmarks to show that implementing certain protocols with their proposed model is easier and can provide better performance than the pure actor model.<a id="sec-1-7-2" name="sec-1-7-2"></a>

\### However, none of these works conducts any study on real-world programs to show the weaknesses of the actor libraries or the actor model. Our study complements these works by supplying the empirical evidence for these weaknesses.<a id="sec-1-7-3" name="sec-1-7-3"></a>

\## Section 9: Future Work:<a id="sec-1-8" name="sec-1-8"></a>

\### A direction for future work is to correlate the phenomenon of mixing concurrency models with bug rates and types.<a id="sec-1-8-1" name="sec-1-8-1"></a>

\### A related question is whether mixing occurs across different layers of abstraction. For example, mixing may occur only on the lower, more concrete layers of the program while actors prevail on the higher, more abstract layers.<a id="sec-1-8-2" name="sec-1-8-2"></a>

\### Finally, it would be interesting to see how different actor libraries for the same language, for example Scala, affect the design decisions of programmers.<a id="sec-1-8-3" name="sec-1-8-3"></a>

<div id="footnotes">
<h2 class="footnotes">Footnotes: </h2>
<div id="text-footnotes">

<div class="footdef"><sup><a id="fn.1" name="fn.1" class="footnum" href="#fnr.1">1</a></sup> <p>DEFINITION NOT FOUND.</p></div>

<div class="footdef"><sup><a id="fn.2" name="fn.2" class="footnum" href="#fnr.2">2</a></sup> <p>DEFINITION NOT FOUND.</p></div>

<div class="footdef"><sup><a id="fn.3" name="fn.3" class="footnum" href="#fnr.3">3</a></sup> <p>DEFINITION NOT FOUND.</p></div>

<div class="footdef"><sup><a id="fn.4" name="fn.4" class="footnum" href="#fnr.4">4</a></sup> <p>DEFINITION NOT FOUND.</p></div>

<div class="footdef"><sup><a id="fn.5" name="fn.5" class="footnum" href="#fnr.5">5</a></sup> <p>DEFINITION NOT FOUND.</p></div>

<div class="footdef"><sup><a id="fn.6" name="fn.6" class="footnum" href="#fnr.6">6</a></sup> <p>DEFINITION NOT FOUND.</p></div>

</div>
</div>
