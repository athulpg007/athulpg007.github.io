---
layout : default
title : Deploying Jupyter Notebooks on AWS EC2
---


# Deploying Jupyter Notebooks on AWS EC2

<center><img src="/software/aws/logo.png" alt="AWS home page" width="600"/></center> Attribution: Creative Commons, Amazon Web Sevices

Jupyter Notebooks are very popular in the scientific programming community due to their ability to integrate code, equations, visualizations, and narrative text all into one interactive document. When running a Jupyter Notebook on a local machine, we are limited by the memory and computing power available on the laptop or desktop computer.  Amazon Web Services (AWS) Elastic Compute Cloud (EC2) provides on-demand, reliable, scalable, and inexpensive cloud computing services. This step-by-step tutorial will guide you to deploy Jupyter notebooks on an EC2 instance, providing you with the ability to combine the interactive functionality of Jupyter notebooks with the easily scalable computing capabilities offered by EC2. This is especially useful for high-perfomance computing and deep learning problems which can leverage parallel processing and GPU computing architectures provided by EC2 to run these codes much faster than on your local machine, while still being able to interactively change your code and visualize the results using Jupyter notebooks.


This tutorial will help you learn how to set up an AWS EC2 instance and run Jupyter notebooks on the cloud. You will need an AWS account, and a Linux/MacOS computer with root priveleges. This process is somewhat involved, and [AWS Sagemaker](https://aws.amazon.com/sagemaker/) offers a quick way of setting up a Jupyter Notebook on AWS if you do not want to get into the details. However, setting up the EC2 server and Jupyter notebook yourself will provide you much more control and flexibility over the whole process. 

1. Go to [aws.amazon.com](https://aws.amazon.com) and sign up for an account if you do not already have one.

	<center><img src="/software/aws/aws-01.png" alt="AWS home page" width="1200"/></center> 
	<br/>
2. Launch an EC2 instance. This can be done from the Products tab. Click on the "Get Started with Amazon EC2".  
	
	<center><img src="/software/aws/aws-02.png" alt="Launch an EC2 instance" width="1200"/></center>
	<br/>

3. Sign into your AWS account.

	<center><img src="/software/aws/aws-03.png" alt="Sign in to your account" width="1200"/></center>
	<br/>

4. Click on launch instance to get stated with the EC2 instance wizard.

	<center><img src="/software/aws/aws-04.png" alt="Launch EC2" width="1200"/></center>
	<br/>

5. Choose an Amazon Machine Image (AMI). Select the Ubuntu 20.04/18.04 AMI for this tutorial.

	<center><img src="/software/aws/aws-05.png" alt="Select Ubuntu 20.04/18.04" width="1200"/></center>
	<br/>

6. Choose an instance type. For this tutorial select the t2.micro which is free-tier eligible up to 750 hours, which is plenty enough for learning purposes. Just make sure to stop the instance when we are done with the tutorial to avoid exceeding the free-tier limit. Next, click on Configure Instance Details.

	<center><img src="/software/aws/aws-06.png" alt="Select instance type" width="1200"/></center>
	<br/>

7. Configure instance details. You can leave everything as in the default settings. Make sure the Auto Assign Public IP field is set to "Use subnet setting (Enable)". Next, add storage.

	<center><img src="/software/aws/aws-07.png" alt="Configure instance details" width="1200"/></center>
	<br/>

8. Add storage. You can add up to 30 GB of storage under free-tier. For this tutorial, we will choose 16 GB which will be more than enough. Next, click Add Tags.

	<center><img src="/software/aws/aws-08.png" alt="Configure instance details" width="1200"/></center>
	<br/>

9. No action is needed on this page. Proceed to configure the security group.
	<center><img src="/software/aws/aws-09.png" alt="Add tags" width="1200"/></center>
	<br/>

10. You will see an existing rule allowing SSH connections. Edit the source field to allow connections from anywhere. Also, add a custom TCP rule with port range 8888-8900 and source from anywhere. As the warning says, this is not a very secure way of doing things so make sure not to leave sensitive data on your notebook. But this will work for learning purposes. Proceed to Review and Launch.

	<center><img src="/software/aws/aws-10.png" alt="Configure security group" width="1200"/></center>
	<br/>

11. Review the instance setup and click Launch.

	<center><img src="/software/aws/aws-11.png" alt="Review and Launch" width="1200"/></center>
	<br/>

12. You will now be asked to select an existing key pair or create a new key pair. Select "Create a new pair" and provide a name for the key pair (eg:aws-ec2-key-01). Download the key pair and store it an accessible location. You will not be able to get the file again. Proceed to Launch Instances.

	<center><img src="/software/aws/aws-12.png" alt="Download key pair" width="1200"/></center>
	<br/>

13. Click on view instances.

	<center><img src="/software/aws/aws-13.png" alt="View instances" width="1200"/></center>
	<br/>

14. You may have to wait for a few minutes for the instance to get up and running. Once it is done, you will see the instance state as "Running" and selecting the instance will display its details below. Make sure you have a public IPv4 DNS as shown below.

	<center><img src="/software/aws/aws-14.png" alt="Instance Details" width="1200"/></center>
	<br/>

15. Now we will SSH into the remote computer. Open a terminal, go to the location where the key pair. In my case, the file is located in the Downloads folder. So I will open a terminal and cd into that folder. You will need to first change permissions on the key file to avoid accidental overwriting. Make sure to replace "aws-ec2-key-01.pem" with your key pair name. Make sure the key pair is actually present in the terminal location. We will then ssh into the remote computer. Make sure to change the key pair name and the public IPv4 DNS with your own.

	```
	cd Downloads
	chmod 400 aws-ec2-key-01.pem
	ssh -i aws-ec2-key-01.pem ubuntu@ec2-54-172-185-5.compute-1.amazonaws.com 
	```

	If everything worked, you will be logged into the EC2 instance successfully.

	<center><img src="/software/aws/aws-15.png" alt="SSH into instance" width="1200"/></center>
	<br/>

16. We have finished setting up the EC2 instance and are now able to access it via SSH. We will noe proceed to set up Jupyter Notebooks on this instance. First we will download and install Ananconda. You may want to replace the Anaconda repository link with a more updated version from the [Anaconda archive](https://repo.anaconda.com/archive/).

	```
	wget https://repo.anaconda.com/archive/Anaconda3-5.3.1-Linux-x86_64.sh 
	```

	<center><img src="/software/aws/aws-16.png" alt="Download Anaconda" width="1200"/></center>
	<br/>

17. Install Anaconda. Review and accept the license terms and choose the default install location. It will take a few minutes to install the packages.

	```
	bash Anaconda3-5.3.1-Linux-x86_64.sh
	```
	<center><img src="/software/aws/aws-17.png" alt="Download Anaconda" width="1200"/></center>
	<br/>

18. When asked if you want the installer to initialize Anaconda3 in your `/home/ubuntu/.bashrc`, select `Yes`. You can skip the installation of Microsoft Visual Studio.

	<center><img src="/software/aws/aws-18.png" alt="Initialize in .bashrc" width="1200"/></center>
	<br/>

19. Anaconda is now installed on your EC2 instance.

	<center><img src="/software/aws/aws-19.png" alt="Installation complete." width="1200"/></center>
	<br/>

20. Use the PATH variable to allow conda commands to be called from anywhere on the remote computer.

	```
	export PATH=~/anaconda3/bin:$PATH
	```
	<center><img src="/software/aws/aws-20.png" alt="Set PATH." width="1200"/></center>
	<br/>

21. As a general development rule, it is good practice to create a new conda environemnt so that you get a sandboxed environment which is isolated from your system-wide python installation. Create a new python3 conda environment called `env1`. 

	```
	conda create -n env1 python=3
	```
	<center><img src="/software/aws/aws-21.png" alt="Create env." width="1200"/></center>
	<br/>

22. Activate the new environment you just created.


	```
	source activate env1
	```
	<center><img src="/software/aws/aws-22.png" alt="Activate env." width="1200"/></center>
	<br/>

23. Install some packages, ipython and jupyterlab into env1 using conda.

	```
	conda install numpy pandas jupyterlab scipy matplotlib ipython
	```
	<center><img src="/software/aws/aws-23.png" alt="Install packages" width="1200"/></center>
	<br/>

24. Type ipython to bring up the interactive IPython shell. We will use the passd utility to create a password for our Jupyter Notebooks. Enter the password you would like to use. The IPython prompt will output an SHA key which you will need to copy and paste elsewhere where you can access it later.
	
	```
	ipython
	from IPython.lib import passwd
	passwd()
	```

	<center><img src="/software/aws/aws-24.png" alt="Set password" width="1200"/></center>
	<br/>

25. Exit IPython and generate a config file for the Jupyter Notebook.

	```
	exit
	jupyter notebook --generate-config
	```

	<center><img src="/software/aws/aws-25.png" alt="Generate config file" width="1200"/></center>
	<br/>

26. Create a directory to store the certificate and cd into it.

	```
	mkdir certs
	cd certs
	```

	<center><img src="/software/aws/aws-26.png" alt="Make certs dir" width="1200"/></center>
	<br/>

27. Create a self-signed certificate using the following command. Answer the prompted questions, you can leave most fields empty or provide your information if you wish. This will generate a certificate for us.

	```
	sudo openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem
	```

	<center><img src="/software/aws/aws-27.png" alt="Create certificate" width="1200"/></center>
	<br>

28. We will now need to edit the jupyter config file.

	
	```
	cd ~/.jupyter
	nano jupyter_notebook_config.py
	```

	<center><img src="/software/aws/aws-28.png" alt="Edit the jupyter config file" width="1200"/></center>
	<br>

29. Add the following text to the top of the config file.

	```
	c = get_config()
	c.IPKernelApp.pylab = 'inline' 
	c.NotebookApp.certfile = u'/home/ubuntu/certs/mycert.pem' 
	c.NotebookApp.ip = '*' 
	c.NotebookApp.open_browser = False 
	c.NotebookApp.password = u'sha1:5592963916a0:425ca0f9f2a610f96cd8532e4f1cc5df3f202e14' 
	c.NotebookApp.port = 8889
	```

	Make sure to change the SHA key with your key, and choose a port number in the range 8888-8900. For this tutorial, we will use 8889. Save the config file (`Ctrl+S`) and exit the editor (`Ctrl+X`)

	<center><img src="/software/aws/aws-29.png" alt="Edit the jupyter config file" width="1200"/></center>
	<br>

30. Change directory back to home and create a directory where you want to run Jupyter notebooks from.

	```
	cd ..
	mkdir notebook-dir
	cd notebook-dir
	```

	<center><img src="/software/aws/aws-30.png" alt="Create a directory for notebooks" width="1200"/></center>
	<br>

31. Change ownership of these items. If you skip or miss this step, you might get a "Permission Denied" error message when you try to lauch your Jupyter notebook.
	
	```
	sudo chown -R $USER /home/
	sudo chown -R $USER ~/.local/share/jupyter/
	cd ..
	```

	<center><img src="/software/aws/aws-31.png" alt="Change ownership" width="1200"/></center>
	<br>

	Note: I actually got an error for the second line, but some people needed that line to get it working. So I suggest you try it.

32. We are now ready to launch our Jupyter notebook. Make sure to change the IPv4 address to that of your instance.
	```
	jupyter notebook --ip=ec2-54-172-185-5.compute-1.amazonaws.com
	```
	<center><img src="/software/aws/aws-31b.png" alt="Launch notebook" width="1200"/></center>
	<br>

	The terminal will print out the location of the Jupyter notebook. In my case, the notebook is running at `https://ec2-54-172-185-5.compute-1.amazonaws.com:8889/`. Copy this (your web address) and paste into your browser.

33. If everything worked correctly, you will get a warning that the connection is not secure. Since you know you have set it up, it is safe to proceed. Click Advanced, and Accept the Risk and Continue to proceed.

	<center><img src="/software/aws/aws-33.png" alt="Security Warning" width="1200"/></center>
	<br>

34. Enter the password you chose earlier for your Jupyter Notebook.
	<center><img src="/software/aws/aws-34.png" alt="Security Warning" width="1200"/></center>
	<br>

35. Finally, we have arrived at our Jupyter notebook on the cloud.
	<center><img src="/software/aws/aws-35.png" alt="Jupyter Notebook on the cloud" width="1200"/></center>
	<br>

36. To demonstrate the flexibility offered by having an SSH connection and a Jupyter notebook on the cloud, we will run a deep learning example problem using Keras. Close the notebook browser window and use `Ctrl+C` twice in the terminal to shutdown the notebook server. Install keras on the remote computer and restart the notebook server. Open the address as in step 32 to open the Jupyter Notebook.
	```
	conda install keras
	jupyter notebook --ip=ec2-54-172-185-5.compute-1.amazonaws.com
	```
	<center><img src="/software/aws/aws-36.png" alt="Jupyter Notebook on the cloud" width="1200"/></center>
	<br>

37. Create a new Python 3 notebook in the notebook-dir folder called keras-demo. This demo will use convolutional neural networks to classify MNIST digits and the code can be accessed on [GitHub](https://github.com/fchollet/deep-learning-with-python-notebooks/blob/master/5.1-introduction-to-convnets.ipynb). Alternatively, you can download the .ipynb notebook file [here](/software/aws/keras-demo.ipynb) and upload it to your Jupyter Notebook in the browser.

	<center><img src="/software/aws/aws-37.png" alt="keras-demo-1" width="1200"/></center>
	<br> 
	<center><img src="/software/aws/aws-38.png" alt="keras-demo-2" width="1200"/></center>
	<br> 
	<center><img src="/software/aws/aws-39.png" alt="keras-demo-1" width="1200"/></center>
	<br> 
	<center><img src="/software/aws/aws-40.png" alt="keras-demo-2" width="1200"/></center>
	<br>   
	<center><img src="/software/aws/aws-41.png" alt="keras-demo-1" width="1200"/></center>
	<br> 

38. There you go! You have succesfully deployed a Jupyter notebook on the AWS EC2. **Before you forget, make sure to close the notebook window, shut down the notebook server (`Ctrl+C`) and stop the EC2 instance before leaving.  If you leave the instance running and it exceeds the 750 hour free-tier, you will incur charges.** To stop the instance, go to the EC2 dashboard, select the instance and Instance State -> Stop instance.  

	<center><img src="/software/aws/aws-42.png" alt="keras-demo-1" width="1200"/></center>
	<br> 

	Obviously, you might be thinking I could have probably run this problem faster on my laptop than on t2.micro instance. That is true. But remenber we used the t2.micro because it was free and the demo problem is not a demanding one. For problems which require much more computing power, you can simply select a more powerful instance type possibly with GPU support (such as the p2.xlarge) which will allow you to run your codes much faster than any local workstation. Of course, the more capable the instance the more expensive it becomes; but I assume someone will be willing to pay for it if they need to use such large computing resources. 

	In any case, the EC2 charges are a fraction of what it would cost you to buy a brand new high performance CPU + GPU, and for most purposes AWS EC2 offers a very competitive price. 

	

	If you have made it this far, please take a moment to celebrate your achievement with some inspirational music.

	[![Music](http://img.youtube.com/vi/zSgiXGELjbc/0.jpg)](https://www.youtube.com/watch?v=zSgiXGELjbc "Carl Sagan - 'A Glorious Dawn' ft Stephen Hawking")

# Credits

Obviously I did not figure all this out by myself! Here are some links which have been very helpful in putting this together. Some of them had issues getting everything to work correctly, hopefully this tutorial will not have those issues. If you found this article helpful, or if you faced any issues or have a better way of doing this, please connect with me on [LinkedIN](https://www.linkedin.com/in/athulpg007/) and let me know.

1. [Michael Galarnyk's YouTube playlist](https://www.youtube.com/playlist?list=PLtQQKsdL7EPxZO_z7enI4tH1IJSYCER46) and [GitHub](https://github.com/mGalarnyk/Installations_Mac_Ubuntu_Windows/tree/master/AWS).

2. [Code & Learn's YouTube video](https://www.youtube.com/watch?v=vfjbECWi7F0)]

3. [StackOverFlow](https://stackoverflow.com/questions/53097180/permissionerror-errno-13-permission-denied-when-accessing-to-aws-ec2)

4. [François Chollet's GitHub](https://github.com/fchollet/deep-learning-with-python-notebooks) and Deep Learning [Textbook](https://www.manning.com/books/deep-learning-with-python?a_aid=keras&a_bid=76564dff).
























































