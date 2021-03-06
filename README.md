# README for package: Well-Building-Project-Images2Movies

## Author details: 
Name: Sam Huguet  
E-mail: samhuguet1@gmail.com  
Date created: 11<sup>th</sup> August 2021

## Description: 
- This code has been deisgned to consider several directories full of images, then 'stitch' those images together to create a video. 
- This code was written for Dr. Shakti Lamba, to help process image data captured as part of the [well building project](http://shaktilamba.com/research-2/well-building-project/).
- At this time of writing, Dr. Lamba is a researcher at The University of Exeter, Penryn campus. Her interest lies in "how people cooperate to solve public goods dilemmas", and in how this cooperation has evolved. 
- I have included ```.ipynb``` and ```.py``` file, so that JupyterLab can be easily used alongside other IDEs. 

## Package architecture: 
* Images2Movies: 
  * This is where the main code is stored. 
  * There are module files (these contain the individual functions) and RUNME files (these actually call (use) the functions). 
  * There are ```.py``` files for general purpose IDEs, and ```.ipynb``` files for JupyterLab.
* img:
  * This is where images are stored. These images are used to illustrate this README document. 
  * There is also a power point file in case you want to a diagram similar to Fig. 1.
* .gitignore: 
  * I use software called 'Git Bash' to sync my local files with those within this GitHub repositry. The .gitignore file contains a list of directories (e.g. text files with project notes), and prevents Git Bash from uplodaing them; I don't want to clutter up this repo!
* LICENCE.txt:
  * The licence explaining how this code can be used. 
* README.md:
  * The file which creates the README for this code. 
* environment.yml:
  * A file to allow you to re-create this code's environment in conda. 
* requirements.txt:
  * A file to allow you to re-create this code's environment using pip. 

## Software requirements to run the code: 
- You can run this code on your own computer for free, providing you download and install the following software:  
(1) Anaconda: This is an immensely useful platform from which you can download the correct version of many languages with their respective packages. Anaconda also allows you to create specific environments for specific projects. You can manage packages and environments outside of Anaconda should you wish.  
(2) Python 3.7. This can be installed through Anaconda.  
(3) An IDE (Integrated development environment). This is the software which allows you to easily interact with the code. I would recommend JupyterLab, for which I have included many ```.ipynb``` files. JupyterLab can be installed through Anaconda.   
(4) The packages required to create the correct environment. The package list will be stored [here - see environment.yml, package-list.txt and requirements.txt](https://github.com/SamHSoftware/Well-Building-Project-Images2Movies).   

## The code expects your data to be organised in the following way: 
- This code expects there to be a single 'parent' folder (a.k.a. directories), which contains all the folders for individual villages. In my case, the parent directory was the (D:) drive, representing the hard-drive I was using.  
- Within this parent directory, there needs to be a specific hierarchy of folders.   
- This image gives a visual explanation of how to organise the data:

<figure>
    <img src="https://github.com/SamHSoftware/Well-Building-Project-Images2Movies/blob/main/img/file_structure.png?raw=true" alt="The heirarchy of folders needed for the code to work" width="700"/>  
    <figcaption>Fig.1 - The heirarchy of folders needed for the code to work.</figcaption>
</figure>  
  
- It does not matter what the parent directory, village folder, well folders or EK folders are called, *providing* that they order correctly when you observe the folders when sorting by name. E.g. If you're making a video for Well_X, then you'd want the folder ```100EK``` to come before folder ```101EK``` when sorting by name in windows explorer. 
- The Imagefolders must have a 8 digit date within their name, organised as DDMMYYYY. Do not seperate the parts of this date with any characters, including spaces and underscores.
- The DCIM folders *must* be named 'DCIM'. 
- Your images can be ```.jpg``` or ```.png```. You will simply need to chnage a input arg in the code (explained below). This input arg will be case sensitive! 

## If you want, you can test that the code works before using it:
It is often common practice to test that functions are working as exected. This is because software changes over time, and commands which might have done one thing, might be edited and to do another several years later. Thus, I have included additional 'test' code which checks that the primary functions are working as ecpected. Here's how to use the 'test' code:  

(1) Within the ```tests``` folder, open ```test_Images2Movies_module.ipynb```. You can use the ```.py``` file instead if you'd like to.

(2) Run ```test_Images2Movies_module.ipynb```. A popup dialog box will appear (see example below), with which you should select the following folder: ```\Well-Building-Project-Images2Movies\tests\test_parent_dir\Well_1```. The script will consider each of the primary functions, and will check that they output the expected values. If assertion errors are raised, then you will need to debug the code, and may contact me for help. 

<figure>
    <img src="https://github.com/SamHSoftware/Well-Building-Project-Images2Movies/blob/main/img/folder_selection.PNG?raw=true" alt="A folder selection dialog box" width="500"/>
    <figcaption>Fig.2 - A folder selection dialog box.</figcaption>
</figure>  

## How to use the code: 

(1) Open the ```RUNME.ipynb``` script. By highlighting individual functions, you will be able to run the code sequentially. This is what we're going to do now. 

(2) First, select and run the following code: 
```
# Import the necessary packages.
from Images2Movies_module import *
```

This line imports the functions I wrote for this application. You can think of it as loading up the scientific protocols for an experiment. 

(3) Modify the following input arg: ```create_all_videos```. When ```create_all_videos = 1```, the code will ask you to select the parent directory, and will adjust to create videos from every single well directory. When ```create_all_videos = 0```, the code will ask you to select an individual well directory, and for which it will make an individual video.  

(4) Select and run the following code (you do not need to change any of the input args): 
```
# A function to allow the user to select the folder contianing the subfolders of images.
# Function input arg 1: create_all_videos [bool] --> When 0, asks for the Well diirectory. When 1, asks for the parent directory (contains the village folder).
# Function input arg 2: test [bool] --> When 1, will change the gui title to that of the test gui.
# Function output 1: The path of the folder selected by the user. 
folder_selection_dialog(create_all_videos = 0,
                        test = 0)
```

A popup dialog box will appear (see Fig.2). With this, you need to select the relevant folder (either the parent directory, or a well directory). The ```well_folders``` can be seen in Fig.1 as ```Well_1``` and ```Well_n```. 

(5) Finally, select and run the final function:
```
# A function to organise the creation of movies. 
# Function input arg 1: selected_directory [string] --> The well or village directory, as previously selected. 
# Function input arg 2: create_all_videos [bool] --> When 0, creates individual videos from the well directory. When 1, considers every well directory and makes videos for all of them.
# Function input arg 3: file_type [string] --> The image file type which is searched for to create the movies.
# Function input arg 4: frame_rate [int] --> Desired frame rate. !!!SET TO 0 IF YOU USE movie_time or subsampling_rate!!!
# Function input arg 5: movie_time [int] --> Desired movie length (min). !!!SET TO 0 IF YOU USE frame_rate or subsampling_rate!!!
# Function input arg 6: movie_extension [string] --> Your desired movie file extension. Tested for .avi and .mp4. 
# Function input arg 7: video_width [int] --> The desired video width (the height will be altered proportionally. 
# Function input arg 8: subsampling_rate [float] --> A variable to be used when you want the biggest movie to be of a particular length, and all other videos to be subsampled proportionally. !!!SET TO 0 WHEN USING frame_rate or movie_time!!!. Wen set to above 0, ensure frame_rate=0 and movie_time=0. Calculated with: (50 * desired time for biggest movie in seconds) / number of images in biggest movie.
# Function output 1: The movie will be saved to 'selected_directory'. 
create_movie(selected_directory,
             create_all_videos = create_all_videos,
             file_type = '.JPG',
             frame_rate = 0,
             movie_time = 5,
             movie_extension = '.mp4',
             video_width = 1920,
             subsampling_rate = 0)
```

You will notice that there are several input args. You don't need to change the first two. However, you might need to change all the others.  

There are three types of video that you can make:  
* A ```frame_rate``` video:
  * These videos have a constant frame rate. Thus, the movies will be of varying durations.
  * No images are ommitted from these videos.
  * When specifying ```frame_rate```, ensure ```movie_time``` and ```subsampling_rate``` are set to 0.  
  * Provide an integer value for the frame rate you desire. 
  * Please do not specify a ```frame_rate``` above 50, as your monitor may not be able to handle it. 
  * The video(s) will be saved to your well folder(s) with the following format: {villageName}\_{wellName}\_fps{frame_rate}\_w{video_width}{movie_extension}.
* A ```movie_time``` video: 
  * These videos have a constant duration. To achieve this, other video properties must vary. If the image sequence is short, and needs to be shown slowly, a low frame rate between 1 and 50 will be automatically selected, and no images are ommitted. If the image sequence is large, and needs to be shown quickly to view it over the required duration, then it's entirely possible that a frame rate of 50 will be insufficient to 'compress' the images into the required time. Thus, above this threshold (which is calculated automatically in the code) the code chooses a frame rate of 50, but also skips (omits) images to speed up the video. When only certain images are shown, it is referred to as subsampling. Image sequences of different sizes will have different subsampling rates.
  * When specifying ```movie_time```, ensure ```frame_rate``` and ```subsampling_rate``` are set to 0. 
  * Provide a value in minutes to control how long your video will be. 
  * The video(s) will be saved to your well folder(s) with the following format: {villageName}\_{wellName}\_fixedLength_w{video_width}{movie_extension}.
* A ```subsampling_rate``` video: 
  * These videos are created using a single fixed rate of subsampling (so that that all they look like they're the same speed) and have fixed frame rates of 50 fps. However, the videos will have varying durations due to the different number of images which need to go into making individual videos. For instance, if we subsample 10% of images from 100 and 1000 images, we'll end up with videos containing 10 and 100 frames. Both will have been subsampled at the same rate, but the longer image sequence will still make a longer video. To be clear, images are omitted using this technique. 
  * Why would you choose this? Let's say you have a specific image sequence (SIS) which works well as a 5 minute video. Let's say that this SIS too long to make into a short video using a frame rate between 1 and 50. Thus, this SIS would be subsampled at a specific rate, one calculated by the code.   
  * Perhaps you want all your other videos to be subsampled at the same frequency, so that all your videos appear to have the same speed. This is where you should use the ```subsampling_rate``` arg. 
  * When specifying ```subsampling_rate```, ensure ```frame_rate``` and ```movie_time``` are set to 0. 
  * You will need to calculate ```subsampling_rate```. To calculate ```subsampling_rate```, use: (50 * desired duration for SIS in seconds) / number of images in SIS. 
  * The video(s) will be saved to your well folder(s) with the following format: {villageName}\_{wellName}\_PSR_w{video_width}{movie_extension}, where PSR stands for Proportional Sampling Rate.
