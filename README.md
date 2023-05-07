Download Link: https://assignmentchef.com/product/solved-eel3135-lab-7
<br>
<strong>Implementing IIR Filters in MATLAB</strong>

We have been using the MATLAB function filter to implement FIR filters. It turns out that the same function can also be employed to implement IIR filters. Consider the general IIR filter specified by the difference equation:

<h2>L       M X         X</h2>

<em>a<sub>k</sub>y</em>[<em>n </em>− <em>l</em>] = <em>b<sub>k</sub>x</em>[<em>n </em>− <em>k</em>]<em>., </em>(1) <em>l</em>=0          <em>k</em>=0

Put the feedback coefficients <em>a</em><sub>0</sub><em>,a</em><sub>1</sub><em>,…,a<sub>L </sub></em>into the (<em>L</em>+1)-dimensional vector a and the feedforward coefficients <em>b</em><sub>0</sub><em>,b</em><sub>1</sub><em>,…,b<sub>M </sub></em>into the (<em>M </em>+1)-dimensional vector b (note that neither a nor b gives the impulse response of the IIR filter). Then

y = filter(b,a,x);

implements the IIR filter on the input signal vector x to give the output vector y, assuming the initial rest condition. For example, the simple first-order IIR filter:

<em>y</em>[<em>n</em>] = 0<em>.</em>9<em>y</em>[<em>n </em>− 1] + 2<em>x</em>[<em>n</em>] − <em>x</em>[<em>n </em>− 1]

may be implemented using the following lines of MATLAB code:

a = [1 -0.9]; b = [2 -1];

y = filter(b,a,x);

Do help filter in MATLAB to learn more about implementing IIR filters using the function filter.

<h1>Lab 7 Exercises</h1>

<ul>

 <li>Unless stated otherwise, you must submit your solutions to all the lab exercises in this section.</li>

 <li>Your laboratory solutions should be submitted on Canvas as a single PDF. The simplest way is to put your codes and answers for all the lab exercises in a single MATLAB Publisher script and use %% to separate the codes and answers for different exercises into different sections as described in the information section of Lab 1.</li>

 <li><strong>Plot all magnitude spectrums in this lab in dB scale.</strong></li>

</ul>

<strong>Exercise 7.1:</strong>

This exercise shows you how to generate the impulse response of an IIR filter using the MATLAB function filter. Recall the impulse response of any LTI system is the system’s output when the input is the unit impulse signal. Hence, given the feedback and feedforward tap vectors a and b of an IIR filter, we may simply do h = filter(b,a,impulse);

to obtain the impulse response of the IIR filter in the vector h with the input vector impulse representing the unit impulse signal. Nevertheless, one must pay attention to the fact that the filter function generates an output vector of the same length as that of the input vector. For an IIR filter, the impulse response is of infinite length. Thus, the filter function may only give a truncated version of the true impulse response of the IIR filter. Intuitively, the longer the truncation, the better is the approximation. Thus, your input vector impulse must be long enough so that filter outputs a “good” enough approximation to the impulse response of an IIR filter. I’ll leave it to you to determine how long the input vector impulse needs to be and how to generate it for each case below.

<ul>

 <li>For each of the IIR filters below, analytically determine an expression for the impulse response, find the transfer function and its ROC, and draw the pole-zero plot. Use the MATLAB function filter to generate and plot (use stem) the impulse response. Compare your plot with the expression that you obtain analytically. Try to correlate the location(s) of the pole(s) to the plot of your impulse response. In particular, correlate the pole location(s) with the speed of decay/growth in magnitude of the impulse response. Determine also whether the filter is stable or not.

  <ol>

   <li><em>y</em>[<em>n</em>] = 0<em>.</em>8<em>y</em>[<em>n </em>− 1] + <em>x</em>[<em>n</em>]</li>

   <li><em>y</em>[<em>n</em>] = −0<em>.</em>8<em>y</em>[<em>n </em>− 1] + <em>x</em>[<em>n</em>]</li>

  </ol></li>

</ul>

<ul>

 <li><em>y</em>[<em>n</em>] = −0<em>.</em>8<em>y</em>[<em>n </em>− 1] + <em>x</em>[<em>n </em>− 10] iv) <em>y</em>[<em>n</em>] = 2<em>y</em>[<em>n </em>− 1] + 2<em>x</em>[<em>n</em>]</li>

</ul>

<ul>

 <li>For each of the IIR filters below, analytically find the transfer function and its ROC, and draw the pole-zero plot. Use the MATLAB function filter to generate and plot (use stem) the impulse response. Try to correlate the location(s) of the pole(s) to the plot of your impulse response. In particular, correlate the pole location(s) with the speed of decay/growth in magnitude and any oscillatory characteristics of the impulse response. Determine also whether the filter is stable or not. If the filter is stable, determine analytically the frequency response of the filter and plot its magnitude response in MATLAB. Correlate the shape of the magnitude response with the pole location(s).

  <ol>

   <li><em>y</em>[<em>n</em>] = 1<em>.</em>0cos(0<em>.</em>2<em>π</em>)<em>y</em>[<em>n </em>− 1] − 0<em>.</em>25<em>y</em>[<em>n </em>− 2] + <em>x</em>[<em>n</em>] ii) <em>y</em>[<em>n</em>] = 1<em>.</em>8cos(0<em>.</em>2<em>π</em>)<em>y</em>[<em>n </em>− 1] − 0<em>.</em>81<em>y</em>[<em>n </em>− 2] + <em>x</em>[<em>n</em>]</li>

  </ol></li>

</ul>

iii) <em>y</em>[<em>n</em>] = 1<em>.</em>98cos(0<em>.</em>2<em>π</em>)<em>y</em>[<em>n </em>− 1] − 0<em>.</em>9801<em>y</em>[<em>n </em>− 2] + <em>x</em>[<em>n</em>]

<h2><strong>Exercise 7.2: </strong>(Notch Filter)</h2>

This exercise shows you how to use a more selective version of a nulling filter to remove a sinusoidal interfering signal that corrupts the same audio signal in Exercise 6.2. The corrupted audio signal is provided in the WAV file bad wannabe.wav. Note that the frequency of the sinusoidal interference may not be the same as that in Exercise 6.2.

<ul>

 <li>Load bad wannabe.wav into MATLAB. Repeat Exercise 6.2 by using the same nulling FIR filter prototype discussed there. In particular, save the filtered audio signal to the WAV file fired wannabe.wav. Submit this WAV file. Listen to the filtered audio, and comment on its quality.</li>

 <li>Now consider the IIR notch filter specified by the following transfer function:</li>

</ul>

(2)

where ˆ<em>ω</em><sub>0 </sub>determines the normalized radian frequency of the notch and <em>α </em>is a positive real number that determines the “sharpness” of the notch. State the range of <em>α </em>for which the IIR filter above is stable. Choose ˆ<em>ω</em><sub>0 </sub>to be the frequency of the sinusoidal interference that you determined in (a). Draw the pole-zero plot of the IIR filter for a choice of <em>α </em>that makes the filter stable and for a choice of <em>α </em>that makes the filter unstable. Select a few values of <em>α </em>that make the filter stable and plot the filter’s magnitude response for each choice of <em>α</em>. Deduce a general rule to describe the “sharpness” of the notch as a function of <em>α</em>.

<ul>

 <li>Analytically determine the difference equation for the IIR notch filter whose transfer function is given by (2). Using the difference equation, write a MATLAB function to generate the feedback vector a and feedforward vector b that allow us to implement the IIR notch filter. Your function should be in the following form:</li>

</ul>

[b a] = notch(w0, alpha);

where w0 and alpha specify the values of ˆ<em>ω</em><sub>0 </sub>and <em>α </em>in (2), respectively.

<ul>

 <li>Use your notch function to generate b and a by choosing alpha=0.99 and w0 to be the normalized radian frequency of the sinusoidal interference. Apply this IIR notch filter to remove the interference in bad wav. Save the filtered signal to the WAV file iired wannabe.wav. Submit this WAV file. Listen to this filtered audio, and comment on its quality w.r.t. that of the filtered audio using the FIR nulling filter in (a). Plot the magnitude spectrum of this filtered signal and compare it with that of the filtered signal obtained in (a). Use the differences in the magnitude spectrums to explain the different audio quality achieved by using the FIR nulling filter in (a) and the IIR notch filter here in removing the sinusoidal interference.</li>

</ul>