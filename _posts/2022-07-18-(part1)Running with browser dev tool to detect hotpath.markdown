This blog contains 2 parts.
In Part1(here), I will show you the essential tech in the dev tool and even more general test methods.


What I thought first thing is that same as another profiler (like [Perf](https://perf.wiki.kernel.org/index.php/Main_Page), [gnu gprof](https://man7.org/linux/man-pages/man1/gprof.1.html), [gperftools](https://github.com/gperftools/gperftools)).

BUT, after diving into I found it more EXTENSIBLE and simple.

----
### the major different

the above profiler will call low-level unit&&registers to touch the key components changes  (eg: most cache/branch miss position/function)

yet, the browser will record the high level  (eg: frame ratio, network, memory usage, and TIME cost)


### the usage
I am running with chrome, but I think another browser same as this.

Remember that we will focus on the performance(or time) first:


Back to gr-web, try the deployed page:[here](https://marcnewlin.github.io/gnuradio-web/)

0. same as grc, we need to draw our graph first

1. enter `F12` on your keyboard and select tab `performance`

2. And then click Record![](https://wd.imgix.net/image/admin/Re0KNyMRmkswFBpNYVW3.png?auto=format).

3. After that, click `generate` and `execute`

4. Finally after the result shows, we click Record![](https://wd.imgix.net/image/admin/Re0KNyMRmkswFBpNYVW3.png?auto=format) again.

> you even can try to record the page loading file if you have interest


**Important: do not exit early or takes a long time to record**

(browser cannot get whole data to use to analyze if exit early and

if takes a long time to record the browser will cost more time to analyze since you get more data)


### the analysis
Hope you have finished the above steps, and I will produce a simple graph that also captures valuable data.

The moment: after click `generate` and `exectute` will be highlight(yellow?)
Ok, the `generate` only take a bit time, but also call wasm function:
![Screenshot from 2022-07-18 11-02-23](https://user-images.githubusercontent.com/98031688/179439729-970ae872-e8ca-487b-a062-ea94c56b2932.png)
the `exec` dominate the major time:
![Screenshot from 2022-07-18 11-09-44](https://user-images.githubusercontent.com/98031688/179439889-fe900ec1-a79c-4b75-8f71-31d9ed4b109e.png)




### what is in part2
Hey, we need to port the `volk` kernel to simd, the current is using the generic CPP code translated to python.

So, there could be different implements(you see, the origin CPP->python code, simd-wasm porting code, grc export python code)

It will be posted soon(I promise if there everything is well)

