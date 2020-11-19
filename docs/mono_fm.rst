.. OFDM_Receiver documentation master file, created by
   sphinx-quickstart on Sat Mar 23 13:02:50 2019.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Project: FM Demodulator
=========================

1) Introduction
---------------
In this project we will build an FM Demodulator and implement it on the Pynq Board.

2) Project Goal
---------------

In this project, you will use your knowledge from previous projects to implement a FM Demodulator in programmable logic. The project is divided into two parts. In the first part, you develop different functions for a FM Demodulator using HLS. A FM Demodulator consists of a linear filter, downsampler and a discriminator.The second part is to integrate the Demodulator onto the Pynq Board using "RTL2832" USB tuners to get our RF input samples. You should be able to listen to local FM radio channels using your MonoFM implementation in programmable logic. For more detail about the mono FM implementation have a look at it's source code `here <https://github.com/mwickert/scikit-dsp-comm/blob/master/sk_dsp_comm/rtlsdr_helper.py>`_.

3) Materials
------------

`Download <https://bitbucket.org/akhodamoradiUCSD/237c_draft/downloads/fm.zip>`_.

This contains a python notebook which explains the working of a Mono FM Demodulator.

For this project the following will not be provided:

* ~.cpp - The place where you write synthesizable code
* ~.h - header file with various definitions that may be useful for developing the code 
* ~test.cpp - testbench

You will have to build the entire project from scratch

4) Design Instructions
----------------------
The FM Demodulator has 3 main parts: downsampler, linear filter and discriminator.

**downsampler**
##########
This part consists of a straight forward downsampler. We have to downsample by a factor of N, that is keep every Nth sample. The implementation of downsampler can be found `here <https://github.com/mwickert/scikit-dsp-comm/blob/master/sk_dsp_comm/sigsys.py#L2673>`_.

**linear filter**
################
Build a linear filter whose function is implemented as a direct II transposed structure.

This means that the filter implements:
   a[0]*y[n] = b[0]*x[n] + b[1]*x[n-1] + ... + b[M]*x[n-M] - a[1]*y[n-1] - ... - a[N]*y[n-N]
   
 More information about the linear filter implementation can be found `here <https://github.com/scipy/scipy/blob/v1.5.4/scipy/signal/signaltools.py#L1719-L1909>`_.

**discriminator**
################



**Optimization Guidelines**

* You must always use a clock period of 10 ns.

* The output of the various architectures that you generate must match the golden output. We have broken down the project into subcomponents to allow you to develop and test them individually. You would be wise to do it in such a manner.


5) PYNQ Demo
------------

`How to set up WBFM in GNU Radio <https://bitbucket.org/akhodamoradiUCSD/237c_data_files/downloads/WESProject5_student.zip>`_.

This project is different from your previous projects in the sense that it works in real time. Effect of latency and throughput of your implementation can be observed by listening to your audio output. You are highly encouraged to modify the code to achieve a better performance and observe the throughput by changing the way you transmit data between PS and PL. Make use of the "RTL 2832" USB tuner in-order to receive the input RF Samples.


6) Submission Procedure
-----------------------

You need to demonstrate your functional hardware implementation FM Demodulator in the class. We will post schedule of each team’s demonstration later on piazza.

You must also submit your code (and only your code, not other files, not HLS project files). Your code should have everything in it so that we can synthesize it directly. This means that you should use pragmas in your code, and not use the GUI to insert optimization directives. We must be able to only import your source file and directly synthesize it. If you change test benches to answer questions, please submit them as well. You can assume that we have correctly set up the design environment. 

You must follow the file structure below. We use automated scripts to pull your data, so **DOUBLE CHECK** your file/folder names to make sure it corresponds to the instructions.

Your repo must contain a folder named "wbfm_receiver" at the top-level. This folder must be organized as follows (similar to previous projects):

**Contents:**

* **Report.pdf**

* Folder **fm-demodulator**

  - Source code (*.cpp, *.h, *.tcl only) and reports (.rpt and .xml).
  
* Folder **Demo**

  - .bit and .hwh files
  - FM.ipynb host file

**Report:** For this project, you must submit a report the throughput with 1 page for each function from section 4. You may add figures, diagrams, tables, or charts to describe your architectures with a short paragraph explaining them. No questions; no answers. Just explain your design. We will check if (1) your final FM Demodulation functions are functionally correct (they pass their test benches). The report will help us to understand your design. You also can use this report to explain your work for bonus part (check the grading section).

7) Grading Rubric
-----------------

**30 points:** Functionally correct design. You will get full credit if we are able to build your blocks without any effort. All four functions must pass their test benches. You need to report your throughput for each function in your report.

**60 points:** Pynq Demo. You will get full credit for clear audio output.

**10 points:** Report.

**Bonus:** You are free to explore and improve the existing project as you wish. The amount of extra credit will depend upon the work. Contact the professor and TAs beforehand if you wish to know how many additional points that a project enhancement will provide. Some examples of improvement are:

