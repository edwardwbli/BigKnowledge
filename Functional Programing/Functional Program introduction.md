
<div class="post">
		<h1 class="postTitle">
			<a id="cb_post_title_url" class="postTitle2" href="http://www.cnblogs.com/kym/archive/2011/03/07/1976519.html">函数式编程扫盲篇</a>
		</h1>
		<div class="clear"></div>
		<div class="postBody">
			<div id="cnblogs_post_body"><p><font color="#0000ff"><strong>1. 概论</strong></font></p>
<p>在过去的近十年的时间里，面向对象编程大行其道。以至于在大学的教育里，老师也只会教给我们两种编程模型，面向过程和面向对象。</p>
<p>孰不知，在面向对象产生之前，在面向对象思想产生之前，函数式编程已经有了数十年的历史。</p>
<p>那么，接下来，就让我们回顾这个古老又现代的编程模型，让我们看看究竟是什么魔力将这个概念，将这个古老的概念，在21世纪的今天再次拉入了我们的视野。</p>
<p><font color="#0000ff"><strong></strong></font></p>
<p><font color="#0000ff"><strong>2. 什么是函数式编程</strong></font></p>
<p>在<a href="http://en.wikipedia.org/wiki/Functional_programming">维基百科</a>中，已经对函数式编程有了很详细的介绍。</p>
<p>那我们就来摘取一下Wiki上对Functional Programming的定义：</p>
<blockquote>
<p>In <a href="http://en.wikipedia.org/wiki/Computer_science">computer science</a>, <strong>functional programming</strong> is a <a href="http://en.wikipedia.org/wiki/Programming_paradigm">programming paradigm</a> that treats <a href="http://en.wikipedia.org/wiki/Computation">computation</a> as the evaluation of <a href="http://en.wikipedia.org/wiki/Function_(mathematics)">mathematical functions</a> and avoids <a href="http://en.wikipedia.org/wiki/Program_state">state</a> and <a href="http://en.wikipedia.org/wiki/Immutable_object">mutable</a> data.</p></blockquote>
<p>简单地翻译一下，也就是说<font color="#ff0000"><strong>函数式编程是一种编程模型，他将计算机运算看做是数学中函数的计算，并且避免了状态以及变量的概念</strong></font>。</p>
<p>接下来，我们就来剖析下函数式编程的一些特征。</p>
<p><strong><font color="#0000ff"></font></strong></p>
<p><strong><font color="#0000ff">3. 从并发说开来</font></strong></p>
<p>说来惭愧，我第一个真正接触到函数式编程，要追溯到两年以前的《<a href="http://book.douban.com/subject/3260311/" target="_blank">Erlang程序设计</a>》，我们知道Erlang是一个支持高并发，有着强大容错性的函数式编程语言。</p>
<p>因为时间太久了，而且一直没有过真正地应用，所以对Erlang也只是停留在一些感性认识上。在我眼里，Erlang对高并发的支持体现在两方面，第一，<font color="#ff0000"><strong>Erlang对轻量级进程的支持</strong></font>（请注意此处进程并不等于操作系统的进程，而只是Erlang内部的一个单位单元），第二，<font color="#ff0000"><strong>就是变量的不变性</strong></font>。</p>
<p><strong><font color="#0000ff"></font></strong></p>
<p><strong><font color="#0000ff">4. 变量的不变性</font></strong></p>
<p>在《<a href="http://book.douban.com/subject/3260311/" target="_blank">Erlang程序设计</a>》一书中，对变量的不变性是这样说的，Erlang是目前唯一变量不变性的语言。具体的话我记不清了，我不知道是老爷子就是这么写的，还是译者的问题。我在给这本书写书评的时候吹毛求疵地说：</p>
<blockquote>
<p>我对这句话有异议，切不说曾经的Lisp，再到如今的F#都对赋值操作另眼相看，低人一等。单说如今的Java和C#，提供的final和readonly一样可以支持变量的不变性，而这个唯一未免显得有点太孤傲了些。</p></blockquote>
<p>让我们先来看两段程序，首先是我们常见的一种包含赋值的程序：</p>
<p>class Account: <br>&nbsp;&nbsp;&nbsp; def __init__(self,balance): <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; self.balance = balance <br>&nbsp;&nbsp;&nbsp; def desposit(self,amount): <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; self.balance = self.balance + amount <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; return self.balance <br>&nbsp;&nbsp;&nbsp; def despositTwice(self): <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; self.balance = self.balance * 2 <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; return self.balance</p>
<p>if __name__ == '__main__': <br>&nbsp;&nbsp;&nbsp; account = Account(100) <br>&nbsp;&nbsp;&nbsp; print(account.desposit(10)) <br>&nbsp;&nbsp;&nbsp; print(account.despositTwice())</p>
<p>&nbsp;</p>
<p>这段程序本身是没有问题的，但是我们考虑这样一种情况，现在有多个进程在同时跑这一个程序，那么程序就会被先desposit 还是先 despositTwice所影响。</p>
<p>但是如果我们采用这样的方式：</p>
<p>def makeAccount(balance): <br>&nbsp;&nbsp;&nbsp; global desposit <br>&nbsp;&nbsp;&nbsp; global despositTwice <br>&nbsp;&nbsp;&nbsp; def desposit(amount): <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; result = balance + amount <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; return result <br>&nbsp;&nbsp;&nbsp; def despositTwice(): <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; result = balance * 2 <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; return result <br>&nbsp;&nbsp;&nbsp; def dispatch(method): <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; return eval(method) <br>&nbsp;&nbsp;&nbsp; return dispatch</p>
<p>if __name__ == '__main__': <br>&nbsp;&nbsp;&nbsp; handler = makeAccount(100) <br>&nbsp;&nbsp;&nbsp; print(handler('desposit')(10)) <br>&nbsp;&nbsp;&nbsp; print(handler('despositTwice')())</p>
<p>&nbsp;</p>
<p>这时我们就会发现，无论多少个进程在跑，因为我们本身没有赋值操作，所以都不会影响到我们的最终结果。</p>
<p>但是这样也像大家看到的一样，采用这样的方式没有办法保持状态。</p>
<p>这也就是我们在之前概念中看到的无状态性。</p>
<p><font color="#0000ff"><strong></strong></font></p>
<p><font color="#0000ff"><strong>5. 再看函数式编程的崛起</strong></font></p>
<p>既然已经看完了函数式编程的基本特征，那就让我们来想想数十年后函数式编程再次崛起的幕后原因。</p>
<p>一直以来，作为函数式编程代表的Lisp，还是Haskell，更多地都是在大学中，在实验室中应用，而很少真的应用到真实的生产环境。</p>
<p>先让我们再来回顾一下伟大的摩尔定律：</p>
<blockquote>
<p>1、<a href="http://baike.baidu.com/view/1355.htm">集成电路</a>芯片上所集成的电路的数目，每隔18个月就翻一番。 </p>
<p>2、<a href="http://baike.baidu.com/view/1125.htm">微处理器</a>的性能每隔18个月提高一倍，而价格下降一半。 </p>
<p>3、用一个美元所能买到的<a href="http://baike.baidu.com/view/2358.htm">电脑</a>性能，每隔18个月翻两番。 </p></blockquote>
<p>一如摩尔的预测，整个信息产业就这样飞速地向前发展着，但是在近年，我们却可以发现摩尔定律逐渐地失效了，芯片上元件的尺寸是不可能无限地缩小的，这就意味着芯片上所能集成的电子元件的数量一定会在某个时刻达到一个极限。那么当技术达到这个极限时，我们又该如何适应日益增长的计算需求，电子元件厂商给出了答案，就是多核。</p>
<p>多<font color="#ff0000"><strong>核并行程序设计就这样被推到了前线，而命令式编程天生的缺陷却使并行编程模型变得非常复杂，无论是信号量，还是锁的概念，都使程序员不堪其重。</strong></font></p>
<p>就这样，函数式编程终于在数十年后，终于走出实验室，来到了真实的生产环境中，无论是冷门的Haskell，Erlang，还是Scala，F#，都是函数式编程成功的典型。</p>
<p><font color="#0000ff"><strong></strong></font></p>
<p><font color="#0000ff"><strong>6. 函数式编程的第一型</strong></font></p>
<p>我们知道，对象是面向对象的第一型，那么函数式编程也是一样，函数是函数式编程的第一型。</p>
<p>我们在函数式编程中努力用函数来表达所有的概念，完成所有的操作。</p>
<p>在面向对象编程中，我们把对象传来传去，那<font color="#ff0000"><strong>在函数式编程中，我们要做的是把函数传来传去，而这个，说成术语，我们把他叫做高阶函数</strong></font>。</p>
<p>那我们就来看一个高阶函数的应用，熟悉js的同学应该对下面的代码很熟悉，让哦我们来写一个在电子电路中常用的滤波器的示例代码。</p>
<p>&nbsp;</p>
<p>def Filt(arr,func): <br>&nbsp;&nbsp;&nbsp; result = [] <br>&nbsp;&nbsp;&nbsp; for item in arr: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; result.append(func(item)) <br>&nbsp;&nbsp;&nbsp; return result</p>
<p>def MyFilter(ele): <br>&nbsp;&nbsp;&nbsp; if ele &lt; 0 : <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; return 0 <br>&nbsp;&nbsp;&nbsp; return ele</p>
<p>if __name__ == '__main__': <br>&nbsp;&nbsp;&nbsp; arr = [-5,3,5,11,-45,32] <br>&nbsp;&nbsp;&nbsp; print('%s' % (Filt(arr,MyFilter)))</p>
<p>&nbsp;</p>
<p>哦，之前忘记了说，什么叫做高阶函数，我们给出定义：</p>
<blockquote>
<p>在<a href="http://zh.wikipedia.org/wiki/%E6%95%B0%E5%AD%A6">数学</a>和<a href="http://zh.wikipedia.org/wiki/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%A7%91%E5%AD%A6">计算机科学</a>中，<strong>高阶函数</strong>是至少满足下列一个条件的<a href="http://zh.wikipedia.org/wiki/%E5%87%BD%E6%95%B0">函数</a>:</p>
<ul><li>接受一个或多个函数作为输入</li><li>输出一个函数 </li></ul></blockquote>
<p><font color="#000000">那么，毫无疑问上面的滤波器，就是高阶函数的一种应用。</font></p>
<p><font color="#ff0000"><strong>在函数式编程中，函数是基本单位，是第一型，他几乎被用作一切，包括最简单的计算，甚至连变量都被计算所取代。在函数式编程中，变量只是一个名称，而不是一个存储单元，这是函数式编程与传统的命令式编程最典型的不同之处。</strong></font></p>
<p>让我们看看，变量只是一个名称，在上面的代码中，我们可以这样重写主函数：</p>
<p>if __name__ == '__main__': <br>&nbsp;&nbsp;&nbsp; arr = [-5,3,5,11,-45,32] <br>&nbsp;&nbsp;&nbsp; func = MyFilter <br>&nbsp;&nbsp;&nbsp; print('%s' % (Filt(arr,func)))</p>
<p>当然，我们还可以把程序更精简一些，利用函数式编程中的利器，map,filter和reduce :</p>
<p>if __name__ == '__main__': <br>&nbsp;&nbsp;&nbsp; arr = [-5,3,5,11,-45,32] <br>&nbsp;&nbsp;&nbsp; print('%s' % (map(lambda&nbsp;x : 0 if x&lt;0 else&nbsp;x ,arr)))</p>
<p>&nbsp;</p>
<p>这样看上去是不是更赏心悦目呢？</p>
<p>这样我们就看到了，函数是我们编程的基本单位。</p>
<p><strong><font color="#0000ff"></font></strong></p>
<p><strong><font color="#0000ff">7. 函数式编程的数学本质</font></strong></p>
<p>忘了是谁说过：一切问题，归根结底到最后都是数学问题。</p>
<p>编程从来都不是难事儿，无非是细心，加上一些函数类库的熟悉程度，加上经验的堆积，而真正困难的，是如何把一个实际问题，转换成一个数学模型。这也是为什么微软，Google之类的公司重视算法，这也是为什么数学建模大赛在大学计算机系如此被看重的原因。</p>
<p>先假设我们已经凭借我们良好的数学思维和逻辑思维建立好了数学模型，那么接下来要做的是如何把数学语言来表达成计算机能看懂的程序语言。</p>
<p>这里我们再看在第四节中，我们提到的赋值模型，同一个函数，同一个参数，却会在不同的场景下计算出不同的结果，这是在数学函数中完全不可能出现的情况，<font color="#ff0000"><strong>f(x) = y ，那么这个函数无论在什么场景下，都会得到同样的结果，这个我们称之为函数的确定性。</strong></font></p>
<p>这也是赋值模型与数学模型的不兼容之处。而<font color="#ff0000"><strong>函数式编程取消了赋值模型，则使数学模型与编程模型完美地达成了统一</strong></font>。</p>
<p><font color="#0000ff"><strong></strong></font></p>
<p><font color="#0000ff"><strong>8. 函数式编程的抽象本质</strong></font></p>
<p>相信每个程序员都对抽象这个概念不陌生。</p>
<p>在面向对象编程中，我们说，<font color="#ff0000"><strong>类是现实事物的一种抽象表示。那么抽象的最大作用在我看来就在于抽象事物的重用性</strong></font>，一个事物越具体，那么他的可重用性就越低，因此，我们再打造可重用性代码，类，类库时，其实在做的本质工作就在于提高代码的抽象性。而再往大了说开来，<font color="#ff0000"><strong>程序员做的工作，就是把一系列过程抽象开来，反映成一个通用过程</strong></font>，然后用代码表示出来。</p>
<p>在面向对象中，我们把事物抽象。而在函数式编程中，我们则是在将函数方法抽象，第六节的滤波器已经让我们知道，函数一样是可重用，可置换的抽象单位。</p>
<p>那么我们说<font color="#ff0000"><strong>函数式编程的抽象本质则是将函数也作为一个抽象单位，而反映成代码形式，则是高阶函数</strong></font>。</p>
<p>&nbsp;</p>
<p><font color="#0000ff"><strong>9.状态到底怎么办</strong></font></p>
<p>我们说了一大堆函数式编程的特点，但是我们忽略了，这些都是在理想的层面，我们回头想想第四节的变量不变性，确实，我们说，函数式编程是无状态的，可是在我们现实情况中，状态不可能一直保持不变，而状态必然需要改变，传递，那么我们在函数式编程中的则是将其保存在函数的参数中，作为函数的附属品来传递。</p>
<p>ps：在Erlang中，进程之间的交互传递变量是靠“信箱”的收发信件来实现，其实我们想一想，从本质而言，也是将变量作为一个附属品来传递么！</p>
<p>我们来看个例子，我们在这里举一个求x的n次方的例子，我们用传统的命令式编程来写一下：</p>
<p>def expr(x,n): <br>&nbsp;&nbsp;&nbsp; result = 1 <br>&nbsp;&nbsp;&nbsp; for i in range(1,n+1): <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; result = result * x <br>&nbsp;&nbsp;&nbsp; return result</p>
<p>if __name__ == '__main__': <br>&nbsp;&nbsp;&nbsp; print(expr(2,5))</p>
<p>&nbsp;</p>
<p>这里，我们一直在对result变量赋值，但是我们知道，在函数式编程中的变量是具有不变性的，那么我们为了保持result的状态，就需要将result作为函数参数来传递以保持状态：</p>
<p>def expr(num,n): <br>&nbsp;&nbsp;&nbsp; if n==0: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; return 1 <br>&nbsp;&nbsp;&nbsp; return num*expr(num,n-1)</p>
<p>if __name__ == '__main__': <br>&nbsp;&nbsp;&nbsp; print(expr(2,5))</p>
<p>呦，这不是递归么！</p>
<p>&nbsp;</p>
<p><font color="#0000ff"><strong>10. 函数式编程和递归</strong></font></p>
<p>递归是函数式编程的一个重要的概念，循环可以没有，但是递归对于函数式编程却是不可或缺的。</p>
<p>在这里，我得承认，我确实不知道我该怎么解释递归为什么对函数式编程那么重要。我能想到的只是递归充分地发挥了函数的威力，也解决了函数式编程无状态的问题。（如果大家有其他的意见，请赐教）</p>
<p>递归其实就是将大问题无限地分解，直到问题足够小。</p>
<p>而递归与循环在编程模型和思维模型上最大的区别则在于：</p>
<p><font color="#ff0000"><strong>循环是在描述我们该如何地去解决问题。</strong></font></p>
<p><font color="#ff0000"><strong>递归是在描述这个问题的定义。</strong></font></p>
<p>那么就让我们以斐波那契数列为例来看下这两种编程模型。</p>
<p>先说我们最常见的递归模型，这里，我不采用动态规划来做临时状态的缓存，只是说这种思路：</p>
<p>def Fib(a): <br>&nbsp;&nbsp;&nbsp; if a==0 or a==1: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; return 1 <br>&nbsp;&nbsp;&nbsp; else: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; return Fib(a-2)+Fib(a-1)</p>
<p>&nbsp;</p>
<p>递归是在描述什么是斐波那契数列，这个数列的定义就是一个数等于他的前两项的和，并且已知Fib(0)和Fib(1)等于1。而程序则是用计算机语言来把这个定义重新描述了一次。</p>
<p>那接下来，我们看下循环模型：</p>
<p>def Fib(n): <br>&nbsp;&nbsp;&nbsp; a=1 <br>&nbsp;&nbsp;&nbsp; b=1 <br>&nbsp;&nbsp;&nbsp; n = n - 1 <br>&nbsp;&nbsp;&nbsp; while n&gt;0: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; temp=a <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; a=a+b <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; b=temp <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; n = n-1 <br>&nbsp;&nbsp;&nbsp; return b</p>
<p>&nbsp;</p>
<p>这里则是在描述我们该如何求解斐波那契数列，应该先怎么样再怎么样。</p>
<p>而我们明显可以看到，递归相比于循环，具有着更加良好的可读性。</p>
<p>但是，我们也不能忽略，递归而产生的StackOverflow，而赋值模型呢？我们懂的，函数式编程不能赋值，那么怎么办？</p>
<p>&nbsp;</p>
<p><font color="#0000ff"><strong>11.&nbsp; 尾递归，伪递归</strong></font></p>
<p>我们之前说到了递归和循环各自的问题，那怎么来解决这个问题，函数式编程为我们抛出了答案，尾递归。</p>
<p>什么是尾递归，用最通俗的话说：<font color="#ff0000"><strong>就是在最后一部单纯地去调用递归函数</strong></font>，这里我们要注意“单纯”这个字眼。</p>
<p>那么我们说下尾递归的原理，<font color="#ff0000"><strong>其实尾递归就是不要保持当前递归函数的状态，而把需要保持的东西全部用参数给传到下一个函数里，这样就可以自动清空本次调用的栈空间。</strong></font>这样的话，占用的栈空间就是常数阶的了。</p>
<p>在看尾递归代码之前，我们还是先来明确一下递归的分类，我们将<strong><font color="#ff0000">递归分成“树形递归”和“尾递归”，什么是树形递归，就是把计算过程逐一展开，最后形成的是一棵树状的结构</font></strong>，比如之前的斐波那契数列的递归解法。</p>
<p>那么我们来看下斐波那契尾递归的写法：</p>
<p>def Fib(a,b,n): <br>&nbsp;&nbsp;&nbsp; if n==0: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; return b <br>&nbsp;&nbsp;&nbsp; else: <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; return Fib(b,a+b,n-1)</p>
<p>这里看上去有些难以理解，我们来解释一下：传入的a和b分别是前两个数，那么每次我都推进一位，那么b就变成了第一个数，而a+b就变成的第二个数。</p>
<p>这就是尾递归。其实我们想一想，这不是在描述问题，而是在寻找一种问题的解决方案，和上面的循环有什么区别呢？我们来做一个从尾递归到循环的转换把！</p>
<p>最后返回b是把，那我就先声明了，b=0</p>
<p>要传入a是把，我也声明了，a=1</p>
<p>要计算到n==0是把，还是循环while n!=0</p>
<p>每一次都要做一个那样的计算是吧，我用临时变量交换一下。temp=b ; b=a+b;a=temp。</p>
<p>那么按照这个思路一步步转换下去，是不是就是我们在上面写的那段循环代码呢？</p>
<p><font color="#ff0000"><strong>那么这个尾递归，其实本质上就是个“伪递归”，</strong></font>您说呢？</p>
<p>既然我们可以优化，对于大多数的函数式编程语言的编译器来说，他们对尾递归同样提供了优化，使尾递归可以优化成循环迭代的形式，使其不会造成堆栈溢出的情况。</p>
<p>&nbsp;</p>
<p><strong><font color="#0000ff">12. 惰性求值与并行</font></strong></p>
<p>第一次接触到惰性求值这个概念应该是在Haskell语言中，看一个最简单的惰性求值，我觉得也是最经典的例子：</p>
<p>在Haskell里，有个repeat关键字，他的作用是返回一个无限长的List，那么我们来看下：</p>
<p>take 10 (repeat 1)&nbsp;&nbsp; </p>
<p>就是这句代码，如果没有了惰性求值，我想这个进程一定会死在那里，可是结果却是很正常，返回了长度为10的List，List里的值都是1。这就是惰性求值的典型案例。</p>
<p>我们看这样一段简单的代码：</p>
<p>def getResult(): <br>&nbsp;&nbsp;&nbsp; a = getA()&nbsp;&nbsp; //Take a long time <br>&nbsp;&nbsp;&nbsp; b = getB()&nbsp;&nbsp; //Take a long time <br>&nbsp;&nbsp;&nbsp; c = a + b </p>
<p>这段代码本身很简单，在命令式程序设计中，编译器（或解释器）会做的就是逐一解释代码，按顺序求出a和b的值，然后再求出c。</p>
<p>可是我们从并行的角度考虑，求a的值是不是可以和求b的值并行呢？也就是说，直到执行到a+b的时候我们编译器才意识到a和b直到现在才需要，那么我们双核处理器就自然去发挥去最大的功效去计算了呢！</p>
<p>这才是惰性求值的最大威力。</p>
<p>当然，惰性求值有着这样的优点也必然有着缺点，我记得我看过一个例子是最经典的：</p>
<p>def Test(): <br>&nbsp;&nbsp;&nbsp; print('Please enter a number:') <br>&nbsp;&nbsp;&nbsp; a = raw_input()</p>
<p>可是这段代码如果惰性求值的话，第一句话就不见得会在第二句话之前执行了。</p>
<p>&nbsp;</p>
<p><strong><font color="#0000ff">13. 函数式编程总览</font></strong></p>
<p>我们看完了函数式编程的特点，我们想想函数式编程的应用场合。</p>
<p>1. 数学推理</p>
<p>2. 并行程序</p>
<p>那么我们总体地说，其实函数式编程最适合地还是解决局部性的数学小问题，要让函数式编程来做CRUD，来做我们传统的逻辑性很强的Web编程，就有些免为其难了。</p>
<p>就像如果要用Scala完全取代今天的Java的工作，我想恐怕效果会很糟糕。而让Scala来负责底层服务的编写，恐怕再合适不过了。</p>
<p>而在一种语言中融入多种语言范式，最典型的C#。在C# 3.0中引入Lambda表达式，在C# 4.0中引入声明式编程，我们某些人在嘲笑C#越来越臃肿的同时，却忽略了，这样的语法糖，带给我们的不仅仅是代码书写上的遍历，更重要的是编程思维的一种进步。</p>
<p>好吧，那就让我们忘记那些C#中Lambda背后的实现机制，在C#中，还是在那些更纯粹地支持函数式编程的语言中，尽情地去体验函数式编程带给我们的快乐把！</p></div><div id="MySignature"></div>
<div class="clear"></div>
<div id="blog_post_info_block">
<div id="BlogPostCategory"></div>
<div id="EntryTag"></div>
<div id="blog_post_info"><div id="green_channel">
        <a href="javascript:void(0);" id="green_channel_digg" onclick="DiggIt(1976519,cb_blogId,1);green_channel_success(this,'谢谢推荐！');">好文要顶</a>
            <a id="green_channel_follow" onclick="follow('ec43420b-63cf-dd11-9e4d-001cf0cd104b');" href="javascript:void(0);">关注我</a>
    <a id="green_channel_favorite" onclick="AddToWz(cb_entryId);return false;" href="javascript:void(0);">收藏该文</a>
    <a id="green_channel_weibo" href="javascript:void(0);" title="分享至新浪微博" onclick="ShareToTsina()"><img src="//common.cnblogs.com/images/icon_weibo_24.png" alt=""></a>
    <a id="green_channel_wechat" href="javascript:void(0);" title="分享至微信" onclick="shareOnWechat()"><img src="//common.cnblogs.com/images/wechat.png" alt=""></a>
</div>
<div id="author_profile">
    <div id="author_profile_info" class="author_profile_info">
            <a href="http://home.cnblogs.com/u/kym/" target="_blank"><img src="//pic.cnblogs.com/face/u35999.jpg" class="author_avatar" alt=""></a>
        <div id="author_profile_detail" class="author_profile_info">
            <a href="http://home.cnblogs.com/u/kym/">飞林沙</a><br>
            <a href="http://home.cnblogs.com/u/kym/followees">关注 - 22</a><br>
            <a href="http://home.cnblogs.com/u/kym/followers">粉丝 - 433</a>
        </div>
    </div>
    <div class="clear"></div>
    <div id="author_profile_honor">荣誉：<a href="http://www.cnblogs.com/expert/" target="_blank">推荐博客</a></div>
    <div id="author_profile_follow">
                <a href="javascript:void(0);" onclick="follow('ec43420b-63cf-dd11-9e4d-001cf0cd104b');return false;">+加关注</a>
    </div>
</div>
<div id="div_digg">
    <div class="diggit" onclick="votePost(1976519,'Digg')">
        <span class="diggnum" id="digg_count">56</span>
    </div>
    <div class="buryit" onclick="votePost(1976519,'Bury')">
        <span class="burynum" id="bury_count">0</span>
    </div>
    <div class="clear"></div>
    <div class="diggword" id="digg_tips">
    </div>
</div>
</div>
<div class="clear"></div>
<div id="post_next_prev"><a href="http://www.cnblogs.com/kym/archive/2011/03/05/1971604.html" class="p_n_p_prefix">« </a> 上一篇：<a href="http://www.cnblogs.com/kym/archive/2011/03/05/1971604.html" title="发布于2011-03-05 14:40">mongodb小结(转)</a><br><a href="http://www.cnblogs.com/kym/archive/2011/03/15/1984380.html" class="p_n_p_prefix">» </a> 下一篇：<a href="http://www.cnblogs.com/kym/archive/2011/03/15/1984380.html" title="发布于2011-03-15 03:47">载入Haskell的函数</a><br></div>
</div>


		</div>
		<div class="postDesc">posted @ <span id="post-date">2011-03-07 23:12</span> <a href="http://www.cnblogs.com/kym/">飞林沙</a> 阅读(<span id="post_view_count">59890</span>) 评论(<span id="post_comment_count">54</span>)  <a href="https://i.cnblogs.com/EditPosts.aspx?postid=1976519" rel="nofollow">编辑</a> <a href="#" onclick="AddToWz(1976519);return false;">收藏</a></div>
	</div>

