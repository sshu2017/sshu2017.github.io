Title: TensorFlow on Windows 10 Using Docker Installation Method
Date: 2016-05-17 23:31
Author: shushi2000
Category: Machine Learning
Slug: tensorflow-on-windows-10-using-docker-installation-method
Status: published

I am taking an online course of Deep Learning now and it requires me to use TensorFlow. I spent a lot of time searching around, testing different things, and finally managed to run TensorFlow on my windows 10 laptop. So I think maybe I should write a post to remind myself, just in case I need to do it again in the future. And I hope this post can save someone else's time too.

The overview section of [Download and Setup page](https://www.tensorflow.org/versions/r0.8/get_started/os_setup.html) says there are four different ways to install TensorFlow:

1.  Pip install
2.  Virtualenv install
3.  Anaconda install
4.  Docker install

Since I have heard about docker for a while but never get a chance to use it, I think it is a great opportunity for me to learn how to use docker. So I chose the Docker install method here. It looks pretty simple, only three steps.

[![steps](http://shishu.info/wp-content/uploads/2016/05/Capture15.jpg){.aligncenter .wp-image-139 .size-full width="802" height="194"}](http://shishu.info/wp-content/uploads/2016/05/Capture15.jpg)

However, these three steps took me a whole morning...

First, I went to the [Install Docker for Windows](https://docs.docker.com/windows/step_one/) page and followed the instructions. I have no idea about whether the virtualization is enabled or not on my laptop, and my Task Manager looks different with the image shown on the instruction page.

[![Task Manager](http://shishu.info/wp-content/uploads/2016/05/Capture1-1.jpg){.aligncenter .wp-image-151 .size-full width="1058" height="632"}](http://shishu.info/wp-content/uploads/2016/05/Capture1-1.jpg)

I struggled with this and the BIOS for a while and found out that the virtualization IS enabled from the System Information (by runing msinfo32 command).

[![msinfo32](http://shishu.info/wp-content/uploads/2016/05/system-info.jpg){.aligncenter .wp-image-152 .size-full width="1252" height="631"}](http://shishu.info/wp-content/uploads/2016/05/system-info.jpg)

Next, I installed the Docker Toolbox since I am pretty sure I am use a 64-bit Windows. This process is very easy and straightforward. After installing Docker Toolbox, three more icons showed up on my desktop.

[![short cuts](http://shishu.info/wp-content/uploads/2016/05/Capture14.jpg){.aligncenter .wp-image-153 .size-full width="451" height="195"}](http://shishu.info/wp-content/uploads/2016/05/Capture14.jpg)

I launched the Docker Toolbox terminal by double-clicking the Quickstart Terminal icon and made my very first docker command: "**docker run hello-world**". So far so good.

[![terminal](http://shishu.info/wp-content/uploads/2016/05/Capture5.jpg){.aligncenter .wp-image-144 .size-full width="659" height="484"}](http://shishu.info/wp-content/uploads/2016/05/Capture5.jpg)

 

So now I have finished the first step: "**Install Docker on your machine**". But I had no idea how to do the second step: "**Create a Docker group to allow launching containers without sudo**".  And the big lesson I learned here is that, **this second step is NOT necessary**, at least in my case. I skipped this step and went ahead to the third step: "**Launch a Docker container with the TensorFlow image**".

I first tried "**\$ docker run it gcr.io/tensorflow/tensorflow**" and everything looked good from the terminal, which said "**The Jupyter Notebook is running at http://\[all ip addresses on your system\]:8888/**". Wait, what are "all ip addresses"? I typed in "localhost:8888" in my Chrome browser address bar but the Jupyter Notebook did not load...

[![localhost not working](http://shishu.info/wp-content/uploads/2016/05/localhost-not-working.jpg){.aligncenter .wp-image-154 .size-full width="734" height="478"}](http://shishu.info/wp-content/uploads/2016/05/localhost-not-working.jpg)

Once again, [a post on stackoverflow](http://stackoverflow.com/questions/35582875/unable-to-start-tensorflow-within-docker-on-windows) is my life-saver. I followed the answer and everything worked out. First I ran the command "**\$ docker-machine ip default**" and figured out the ip address should be 192.168.99.100. Then I started the TensorFlow docker container again by using command "**\$ docker run -it -p 8888:8888 gcr.io/tensorflow/tensorflow**". Now the Jupyter Notebook is working at 192.168.99.100:8888.

[![Capture10](http://shishu.info/wp-content/uploads/2016/05/Capture10-1.jpg){.aligncenter .wp-image-147 .size-full width="960" height="473"}](http://shishu.info/wp-content/uploads/2016/05/Capture10-1.jpg)

I opened the first notebook and made a test run on the first cell. It worked!

This is how I installed TensorFlow on my laptop via Docker. I hope it is useful to you. Feel free to leave your comments or questions below!

 
