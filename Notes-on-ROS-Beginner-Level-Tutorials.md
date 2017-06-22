---
title: Notes on ROS Beginner Level Tutorials
date: 2016-05-13 09:59:51
tags: ROS
categories: ROS
---
# Beginner Level ROS Tutorials (1): Catkin Work Spaces and Packages
I am learning ROS recently. The materials include:
  
* [ROS wiki Tutorials](http://wiki.ros.org/ROS/Tutorials)
* [A Gentle Introduction to ROS](https://cse.sc.edu/~jokane/agitr/) by Jason M. O'Kane. Free ebook in English and Chinese are provided on the author's website.
* Programming Robots with ROS. This book is more detailed and thorough, and the examples are all written in Python.  
* And a [ROS Cheatsheet](https://github.com/ros/cheatsheet/releases/tag/0.0.1)
## 1. Preliminary
### Workspaces  

Before we start writing any ROS code, we need to set up a workspace for this code to live in. A workspace is simply a set of directories in which a related set of ROS code lives.  

First we have to maker sure we have **added the system-wide ROS setup script to
our .bashrc file** with the following command:  
`user@hostname$ echo "source /opt/ros/indigo/setup.bash" >> ~/.bashrc`  
`user@hostname$ source ~/.bashrc`  

Or we can **source the file by hand**:  
`user@hostname$ source /opt/ros/indigo/setup.bash`  

Then **make a catkin workspace**:  
`user@hostname$ mkdir -p ~/catkin_ws/src`  
This creates a workspace directory called catkin\_ws (although you can call it anything you like), with a src directory inside it for your code.   

Then **initialize it**:  
`user@hostname$ cd ~/catkin_ws/src`  
`user@hostname$ catkin_init_workspace`  
This creates a CMakeLists.txt file for you in the src directory.  

Then we have to **build the workspace** by `catkin_make`, which will build any packages located in ~/catkin_ws/src:  
`user@hostname$ cd ~/catkin_ws`  
`user@hostname$ catkin_make`  
This will generate two new directories: **build** and **devel**. **build** is where catkin is going to store the results of some of its work, like libraries and executable programs if you use C++. We’ll largely ignore build since we don’t need it much when using Python. **devel** contains a number of files and directories, the most interesting of which are the **setup files**. 
 
Running these configures your system to use this workspace, and the code that’s (going to be) contained inside it. Assuming you’re using the default commandline shell (bash) and are still in the top-level directory of your workspace, you can do this with:  
`user@hostname$ source devel/setup.bash`  
**This is what we have to do every time we open a new window**    

---  

### Packages  
ROS software is organized into packages, each of which contains some combination
of code, data, and documentation. Packages sit inside workspaces, in the src directory. Each package directory must include a CMakeLists.txt file and a package.xml file that describes the contents of the package and how catkin should interact with it.  

**Creating a new package** is easy:  
`user@hostname$ cd ~/catkin_ws/src`  
`user@hostname$ catkin_create_pkg my_awesome_code rospy`  
This changes the directory to src (where packages live) and invokes **catkin\_create\_pkg** to make the new package called my\_awesome\_code, which depends on the (already existing) rospy package. If your new package depends on other existing packages, you can also list them on the command line.  
The catkin\_create\_pkg command makes a directory with the same name as the new
package (my\_awesome\_code) with a **CMakeLists.txt** file, a **package.xml** file, and a src directory in it.  

Once you have a created package, you can put your Python nodes in the **src directory**. Other files go in directories under the package directory, too. For instance, launch files, which we’ll talk about soon, conventionally go in a directory called launch.  

Then to **build the new package**:  
`user@hostname$ cd ~/catkin_ws`  
`user@hostname$ catkin_make`  
The above commands will build any catkin projects found in the src folder. This command will generate two new folders under the **my\_awesome\_code directory**. The **build folder** is the default location of the build space and is where cmake and make are called to configure and build your packages. The **devel folder** is the default location of the devel space, which is where your executables and libraries go before you install your packages. 

