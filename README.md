Download Link: https://assignmentchef.com/product/solved-hcp-project-2
<br>



Parallel Programming using OpenMP




This project will introduce you to parallel programming using OpenMP.

<h1>1.      Parallel reduction operations using OpenMP [10 points]</h1>

The file <em>dotProduct/dotProduct.cpp </em>contains a serial version of a C++ code that computes the dot product <em>α </em>= <em>a<sup>T </sup></em>· <em>b </em>of two vectors <em>a </em>∈ R<em><sup>N </sup></em>and <em>b </em>∈ R<em><sup>N</sup></em>. Below is a code snippet:

<table width="675">

 <tbody>

  <tr>

   <td width="675"><em>// serial execution</em><em>// Note that we do extra iterations to reduce relative timing overhead </em>time_start = wall_time(); <strong>for</strong>( <strong>int </strong>iterations=0; iterations&lt;NUM_ITERATIONS; iterations++) { alpha=0.0;<strong>for</strong>( <strong>int </strong>i=0; i&lt;N; i ++) { alpha += a[i] * b[i];}}</td>

  </tr>

 </tbody>

</table>

Solve the following tasks:

<ol>

 <li>Implement a parallel version of the dot product (i) using the OpenMP <em>reduction </em>clause, and (ii) using the OpenMP <em>parallel </em>and <em>critical </em></li>

 <li>Run the serial and both parallel versions on the ICS cluster and measure their execution times. Make a performance scaling chart for the serial version and both parallel versions using various number of threads from <em>p </em>= 1<em>,….,</em>24 for various vector lengths of <em>N </em>= 100<em>,</em>000, <em>N </em>= 1<em>,</em>000<em>,</em>000, <em>N </em>= 10<em>,</em>000<em>,</em>000, <em>N </em>= 100<em>,</em>000<em>,</em>000, and <em>N </em>= 1<em>,</em>000<em>,</em>000<em>,</em>000. In addition to the performance scaling, plot the parallel efficiency for all these dot product benchmarks.</li>

 <li>Please summarize your observations at what size of <em>N </em>it would be beneficial to use a multi-threaded version of a dot product on one compute node of ICS cluster .</li>

</ol>

Hint: Next let’s build the code. You have to load the gcc module.

[<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="681d1b0d1a2804070f0106">[email protected]</a>]$ module load gcc

[<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="2356504651634f4c444a4d">[email protected]</a>]$ make

Execute the code using 1 thread:

[<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="b0c5c3d5c2f0dcdfd7d9de">[email protected]</a>]$ salloc –exclusive

[<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="f88d8b9d8ab8919b8b96979c9da0a0">[email protected]</a>]$ export OMP_NUM_THREADS=1

[<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="c9bcbaacbb89a0aabaa7a6adac9191">[email protected]</a>]$ ./dotProduct

or <em>t </em>threads:

[<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="0e7b7d6b7c4e6261696760">[email protected]</a>]$ salloc –exclusive [<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="7e0b0d1b0c3e171d0d10111a1b2626">[email protected]</a>]$ export OMP_NUM_THREADS=t

[<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="5623253324163f3525383932330e0e">[email protected]</a>]$ ./dotProduct

1

<h1>2.      The Mandelbrot set using OpenMP [30 points]</h1>

Write a sequential code in C to visualize the Mandelbrot set. The set bears the name of the “Father of the Fractal Geometry,” Benoˆıt Mandelbrot. The Mandelbrot set is the set of complex numbers <em>c </em>for which the sequence (<em>z,z</em><sup>2 </sup>+ <em>c,</em>(<em>z</em><sup>2 </sup>+ <em>c</em>)<sup>2 </sup>+ <em>c,</em>((<em>z</em><sup>2 </sup>+ <em>c</em>)<sup>2 </sup>+ <em>c</em>)<sup>2 </sup>+ <em>c,</em>(((<em>z</em><sup>2 </sup>+ <em>c</em>)<sup>2 </sup>+ <em>c</em>)<sup>2 </sup>+ <em>c</em>)<sup>2 </sup>+ <em>c,…</em>) does not approach infinity. Mandelbrot set images are made by sampling complex numbers and determining for each whether the result tends towards infinity when a particular mathematical operation is iterated on it. Treating the real and imaginary parts of each number as image coordinates, pixels are colored according to how rapidly the sequence diverges, if at all. More precisely, the Mandelbrot set is the set of values of <em>c </em>in the complex plane for which the orbit of 0 under iteration of the complex quadratic polynomial <em>z<sub>n</sub></em><sub>+1 </sub>= <em><sup>z</sup></em><em><sub>n</sub></em><sup>2 </sup>+ <em>c </em>remains bounded. That is, a complex number <em>c </em>is part of the Mandelbrot set if, when starting with <em>z</em><sub>0 </sub>= 0 and applying the iteration repeatedly, the absolute value of <em>z<sub>n </sub></em>remains bounded however large <em>n </em>gets. For example, letting <em>c </em>= 1 gives the sequence 0<em>,</em>1<em>,</em>2<em>,</em>5<em>,</em>26<em>,… </em>which tends to infinity. As this sequence is unbounded, 1 is not an element of the Mandelbrot set. On the other hand, <em>c </em>= −1 gives the sequence 0<em>,</em>−1<em>,</em>0<em>,</em>−1<em>,</em>0<em>,… </em>which is bounded, and so −1 belongs to the Mandelbrot set.

The set is defined as follows:

M := {<em>c </em>∈ C : the orbit stays bounded}

where <em>f<sub>c </sub></em>is a complex function, usually <em>f<sub>c</sub></em>(<em>z</em>) = <em>z</em><sup>2 </sup>+ <em>c </em>with <em>z,c </em>∈ C. One can prove that if for a <em>c </em>once a point of the series <em>z,f<sub>c</sub></em>(<em>z</em>)<em>,f<sub>c</sub></em><sup>2</sup>(<em>z</em>)<em>,… </em>gets farther away from the origin than a distance of 2, the orbit will be unbounded, hence <em>c </em>does not belong to M. Plotting the points whose orbits remain within the disk of radius 2 after MAXITERS iterations gives an approximation of the Mandelbrot set. Usually a color image is obtained by interpreting the number of iterations until the orbit “escapes” as a color value. This is done in the following pseudo code:

<table width="675">

 <tbody>

  <tr>

   <td width="675"><strong>for </strong>all c in a certain range <strong>do</strong>z = 0 n = 0<strong>while </strong>|c| &lt; 2 and n &lt; MAX_ITERS <strong>do </strong>z = zˆ2 + c n = n + 1 end <strong>while </strong>plot n at position c end <strong>for</strong></td>

  </tr>

 </tbody>

</table>

The entire Mandelbrot set in Figure 1 is contained in the rectangle −2<em>.</em>1 ≤ &lt;(<em>c</em>) ≤ 0<em>.</em>7, −1<em>.</em>4 ≤ =(<em>c</em>) ≤ 1<em>.</em>4. To create an image file, use the routines from <em>mandel/pngwriter.c </em>found in the git repository like so:

<table width="675">

 <tbody>

  <tr>

   <td width="675"><strong>#include </strong>“pngwriter.h” png_data* pPng = png_create (width, height); <em>// create the graphic</em><em>// plot a point at (x, y) in the color (r, g, b) (0 &lt;= r, g, b &lt; 256) </em>png_plot (pPng, x, y, r, g, b); png_write (pPng, filename); <em>// write to file</em></td>

  </tr>

 </tbody>

</table>

You need to link with -lpng. You can set the RBG color to white (<em>r,g,b</em>) = (255<em>,</em>255<em>,</em>255) if the point at (<em>x,y</em>) belongs to the Mandelbrot set, otherwise it can be (<em>r,g,b</em>) = (0<em>,</em>0<em>,</em>0)

<em>// plot the number of iterations at point (i, j) </em><strong>int </strong>c = ((<strong>long</strong>) n <sub>*</sub> 255) / MAX_ITERS; png_plot (pPng, i, j, c, c, c);

Record the time used to compute the Mandelbrot set. How many iterations could you perform per second? What is the performance in MFlop/s (assume that 1 iteration requires 8 floating point operations)? Try different image sizes. Please use the following C code fragment to report these statistics.

printf (“Total time: %g millisconds
”, (nTimeEnd-nTimeStart)/1000.0);

printf (“Image size: %ld x %ld = %ld Pixels
”, IM_WIDTH, IM_HEIGHT, (IM_WIDTH*IM_HEIGHT)); printf (“Total number of iterations: %ld
”, nTotalIterationsCount);

Figure 1: The Mandelbrot set

printf (“Avg. time per pixel: %g microseconds
”, (nTimeEnd – nTimeStart)/((IM_WIDTH * IM_HEIGHT)); printf (“Avg. time per iteration: %g microseconds
”,(nTimeEnd-nTimeStart)/nTotalIterationsCount); printf (“Iterations/second: %g
”, nTotalIterationsCount/(nTimeEnd-nTimeStart)*1e6); printf (“MFlop/s: %g
”, nTotalIterationsCount * 8.0 / (nTimeEnd-nTimeStart));

Solve the following problems:

<ol>

 <li>Implement the computation kernel of the Mandelbrot set in <em>mandel/mandel seq.c</em>:</li>

</ol>

<table width="639">

 <tbody>

  <tr>

   <td width="639"><strong>for </strong>(j = 0; j &lt; IMAGE_HEIGHT; j++){ cx = MIN_X;<strong>for </strong>(i = 0; i &lt; IMAGE_WIDTH; i++){x = cx; y = cy; x2 = x * x; y2 = y * y;<em>// compute the orbit z, f(z), fˆ2(z), fˆ3(z), …</em><em>// count the iterations until the orbit leaves the circle |z|=2.</em><em>// stop if the number of iterations exceeds the bound MAX_ITERS.</em><em>// &gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt; CODE IS MISSING</em><em>// &lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt; CODE IS NISSING</em><em>// n indicates if the point belongs to the mandelbrot set // plot the number of iterations at point (i, j) </em><strong>int </strong>c = ((<strong>long</strong>) n * 255) / MAX_ITERS; png_plot (pPng, i, j, c, c, c); cx += fDeltaX;} cy += fDeltaY;} <strong>unsigned long </strong>nTimeEnd = get_time ();</td>

  </tr>

 </tbody>

</table>

<ol start="2">

 <li>Count the total number of iterations in order to correctly compute the benchmark statistics. Use the variable nTotalIterationsCount.</li>

 <li>Parallelize the Mandelbrot code that you have written using OpenMP. Compile the program using the GNU C compiler (gcc) with the option -fopenmp. Compare the timings of the parallelized program to those of the sequential program using a meaningful graphical representation.</li>

</ol>

Hint: Next let’s build and execute the code with <em>t </em>threads. You have to load the gcc module.

[<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="cbbeb8aeb98ba7a4aca2a5">[email protected]</a>]$ module load gcc

[<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="3144425443715d5e56585f">[email protected]</a>]$ make

[<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="3045435542705c5f57595e">[email protected]</a>]$ salloc –exclusive

[<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="0a7f796f784a63697964656e6f5252">[email protected]</a>]$ export OMP_NUM_THREADS=t

[<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="3540465047755c56465b5a51506d6d">[email protected]</a>]$ ./mandel_omp

<h1>3.      Bug hunt [20 points]</h1>

You can find in the code directory for this project a number of short OpenMP programs (<em>bugs/omp bug1 1-5.c</em>), which all contain compile-time or run-time bugs. Identify the bugs, explain what is the problem and suggest how to fix it (there is no need to submit the correct modified code).

Hints:

<ol>

 <li><em>c: </em>check tid</li>

 <li><em>c: </em>check shared vs. private</li>

 <li><em>c: </em>check barrier</li>

 <li><em>c: </em>stacksize! <a href="https://stackoverflow.com/questions/13264274/why-segmentation-fault-is-happening-in-this-openmp-code">http://stackoverflow.com/questions/13264274</a></li>

 <li><em>c: </em>locking order?</li>

</ol>

<h1>4.      Parallel histogram calculation using OpenMP [20 points]</h1>

The following code fragment calculates a histogram with 16 bins from a random sequence with a normal distribution stored in an array vec:

<table width="675">

 <tbody>

  <tr>

   <td width="675">time_start = wall_time(); <em>// Compute histogram</em><strong>for</strong>(<strong>long </strong>i = 0; i &lt; VEC_SIZE; ++i) {dist[vec[i]]++;} time_end = wall_time();</td>

  </tr>

 </tbody>

</table>

Parallelize the histogram computations using OpenMP. You can find the serial C example code in <em>hist/hist seq.c</em>. Report runtimes for the original (serial) code, the 1-thread and the N-thread parallel versions. Does your solution scale? If it does not, make it scale! (It really should!)

Hint: Next let’s build and execute the code with <em>t </em>threads. You have to load the gcc module.

[<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="780d0b1d0a3814171f1116">[email protected]</a>]$ module load gcc

[<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="7306001601331f1c141a1d">[email protected]</a>]$ make

[<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="5227213720123e3d353b3c">[email protected]</a>]$ salloc –exclusive

[<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="3540465047755c56465b5a51506d6d">[email protected]</a>]$ export OMP_NUM_THREADS=t

[<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="aedbddcbdceec7cdddc0c1cacbf6f6">[email protected]</a>]$ ./hist_omp

<h1>5.      Parallel loop dependencies with OpenMP [20 points]</h1>

Parallelize the loop in the following piece of code <em>recursion/recur seq.c </em>in the repository using OpenMP:

<table width="675">

 <tbody>

  <tr>

   <td width="675"><strong>double </strong>up = 1.00001; <strong>double </strong>Sn = 1.0; <strong>double </strong>opt[N+1]; <strong>int </strong>n; <strong>for </strong>(n=0; n&lt;=N; ++n) { opt[n] = Sn;Sn *= up;}</td>

  </tr>

 </tbody>

</table>

The parallelized code should work independently of the OpenMP schedule pragma that you will use. Please also try to avoid – as far as possible – expensive operations that might harm serial performance. To solve this problem you might want to use the firstprivate and lastprivate OpenMP clauses. The former acts like private with the important difference that the value of the global variable is copied to the privatized instances. The latter has the effect that the listed variables values are copied from the lexically last loop iteration to the global variable when the parallel loop exits. Please report the scaling of your solution.

Next let’s build and execute the code. You have to load the gcc module.

[<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="542127312614383b333d3a">[email protected]</a>]$ module load gcc

[<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="5e2b2d3b2c1e3231393730">[email protected]</a>]$ make

[<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="d1a4a2b4a391bdbeb6b8bf">[email protected]</a>]$ salloc –exclusive

[<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="3c494f594e7c555f4f525358596464">[email protected]</a>]$ ./recur_seq

<ul>

 <li></li>

</ul>