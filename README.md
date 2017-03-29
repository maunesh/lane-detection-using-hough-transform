# lane-detection-using-hough-transform
Lane Detection Project, using Hough Transform

<img src="laneLines_thirdPass.jpg" width="480" alt="Combined Image" />

# Finding Lane Lines on the Road 

When we drive, we use our eyes to decide where to go.  The lines on the road that show us where the lanes are act as our constant reference for where to steer the vehicle.  Naturally, one of the first things we would like to do in developing a self-driving car is to automatically detect lane lines using an algorithm.

In this project we will detect lane lines in images using Python and OpenCV.  

## To Run
**Step 1:** Install Python 3

To run this project, you will need Python 3 along with the numpy, matplotlib, and OpenCV libraries, as well as Jupyter Notebook installed. 

I recommend downloading and installing the Anaconda Python 3 distribution from Continuum Analytics because it comes prepackaged with many of the Python dependencies you will need for this and future projects, makes it easy to install OpenCV, and includes Jupyter Notebook.  Beyond that, it is one of the most common Python distributions used in data analytics and machine learning, so a great choice if you're getting started in the field.

Choose the appropriate Python 3 Anaconda install package for your operating system <A HREF="https://www.continuum.io/downloads" target="_blank">here</A>.   Download and install the package.

If you already have Anaconda for Python 2 installed, you can create a separate environment for Python 3 and all the appropriate dependencies with the following command:

`>  conda create --name=yourNewEnvironment python=3 anaconda`

`>  source activate yourNewEnvironment`

**Step 2:** Installing OpenCV

Once you have Anaconda installed, first double check you are in your Python 3 environment:

`>python`    
`Python 3.5.2 |Anaconda 4.1.1 (x86_64)| (default, Jul  2 2016, 17:52:12)`  
`[GCC 4.2.1 Compatible Apple LLVM 4.2 (clang-425.0.28)] on darwin`  
`Type "help", "copyright", "credits" or "license" for more information.`  
`>>>`   
(Ctrl-d to exit Python)

run the following commands at the terminal prompt to get OpenCV:

`> pip install pillow`  
`> conda install -c https://conda.anaconda.org/menpo opencv3`

then to test if OpenCV is installed correctly:

`> python`  
`>>> import cv2`  
`>>>`  (i.e. did not get an ImportError)

(Ctrl-d to exit Python)

**Step 3:** Installing moviepy  

I recommend the "moviepy" package for processing video in this project (though you're welcome to use other packages if you prefer).  

To install moviepy run:

`>pip install moviepy`  

and check that the install worked:

`>python`  
`>>>import moviepy`  
`>>>`  (i.e. did not get an ImportError)

(Ctrl-d to exit Python)

**Step 4:** Opening the code in a Jupyter Notebook

You will complete this project in a Jupyter notebook.  If you are unfamiliar with Jupyter Notebooks, check out <A HREF="https://www.packtpub.com/books/content/basics-jupyter-notebook-and-python" target="_blank">Cyrille Rossant's Basics of Jupyter Notebook and Python</A> to get started.

Jupyter is an ipython notebook where you can run blocks of code and see results interactively.  All the code for this project is contained in a Jupyter notebook. To start Jupyter in your browser, run the following command at the terminal prompt (be sure you're in your Python 3 environment!):

`> jupyter notebook`

A browser window will appear showing the contents of the current directory.  Click on the file called "P1.ipynb".  Another browser window will appear displaying the notebook.  Follow the instructions in the notebook to complete the project.  


## Pipeline

* I am first converting the color image (or a frame from a video) to a grayscale image. This enables us to work on a single channel of the image, instead of working on all 3 channels (BGR). So this is computationally less intensive
* Then I am applying Gaussian Blur to the image. I also tried Bilateral Filtering, since this filtering preserves edges better, compared to Gaussian Filter. However, I did not see a big advantage in this project, so I kept the Gaussian Filtering in my code to be consistent with given specifications.
* Then I applied Canny Edge detection on this smoothed image.
* To make this process more efficent, I used a small GUI tool. 
  Here's the demo of the tool: 
          https://youtu.be/xdiekchp-Uc
* On this Edge image, I filtered region of interest by applying a mask. Since we are primarily interested in edges in the region where we expect our road to be, I removed the edges in other areas of the image.
* Then I applied Hough Lines algorithm on this masked edge image. This gives us line segments where we have edges near the lane lines. 
* Once I get the lane line segments, I extrapolated the left lane line and right lane line, based on the angle.
* Since we are using Polar coordinates in Hough Transform, our left line will have negative slope and the right line will have positive slope. Based on this, I classify each line segment to be either a left line segment or a right line segment. Then I take average of all left line segments and draw an extrapolated left line. I apply same method for extrapolating the right line segment as well. To make the extrapolated lines more stable and less wobbly, I applied weighted sum of previous slope and current slope of each line. This allows smooth transitioning of the slope, so the outcome looks more stable.


## Video Output

#### Project Video:
Detecting White Lane Lines:  https://youtu.be/VXccUjr322A
<br />
Detecting Yellow Lane Lines:  https://youtu.be/t38wJ3V3Mi8
<br />
Challenge Video:  https://youtu.be/6eJAxwa-qDY
<br />


## Blog Post
https://medium.com/@maunesh/finding-the-right-parameters-for-your-computer-vision-algorithm-d55643b6f954


