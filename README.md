# Udacity-Self-driving-car-simulator-pytorch-code

Training and testing self-driving car in udacity self-driving-car simulator:

**On Windows:**

https://github.com/pgebert/autonomous_car_simulation code respository is great for training and testing models on Windows machine with or without GPU. I recommend using pgebert's code if you want to do all the process in windows machine. Small models will still have reasonable training time if GPU is not present. BUT if model size increases, training time sharply increases. So if you do not have GPU in windows machine and model is large, training will take too long.

*But if you have access to a linux machine with GPU, and want to train model on it, follow this below procedure:*

**The pgebert's code has bias term in it, but we can train the model successfully without having any bias. I have removed the bias and trained it successfully!. Check dataloader.py to see the changes**

**On Linux:**

Udacity simulator did not run in linux (at least I could not make it work even after trying lot of online available solutions). The simulator window pops up and closes immediately when we try to open the simulator in linux.

So how do we do training and testing in linux?
There are few changes that needs to be done to the above (pgebert's) code and few procedures required to be followed to make this work!

* Training data generation: Done using windows machine
* Training model: Done using Linux Machine with GPU
* Testing: Done on windows machine 

Summary of steps:

**Training data generation:**

* Step 1: Windows: Generate training data from simulator by using 'TRAINING MODE'
* Step 2: Linux: Move data to linux machine
* Step 3: Linux: Edit the driving_log.csv file. First three columns have paths to images, change them to match with path where the 'IMG' folder is stored in linux machine.
* Step 4: Linux: Place the driving_log.csv in parent folder of the code where model.py is kept. 'IMG' folder can be kept in any folder as long as the path is provided in driving_log.csv file

**Training model:**

* Step 5: Linux: Set **cfg.cuda=True** in the model.py file. This is done to use GPU
* Step 6: Linux: RUN model.py to train the network on GPU. Trained model will be saved in .pth file extenstion.

**Testing:**

* Step 7: Windows: You can make a duplicate repository of code used on linux machine in Windows.
* Step 8: Windows:  In model.py file, add **map_location='cpu'** to torch.load(). Example: self.net.load_state_dict(torch.load('model_ST_Cuda.pth',map_location='cpu')) . A CUDA error will be raised if this is not done in the model.py file.
* Step 9: Windows:  In model.py file, set **cfg.cuda=False**.
* Step 10: Windows: Open Udacity simulator and choose 'AUTONOMOUS MODE'. Select the same track which was used to generate the training data.
* Step 11: Windows: Run drive.py file. Make sure trained model name matches with the model name which loadModel() function loads.
* Step 12: Be amazed that it works!


The data generated from the simulator has ONE folder and ONE csv file, 1. 'IMG' Folder containing  training Images and 2. 'driving_log.csv' file containing steering angle, throttle values, brake values and speed for each frame/image captured.

**If you are having problems with setting up conda environment for this code using .yml provided here. I recommend installing packages one by one manually in a new environment [There are not a lot of packages to install]. This will definitely help in setting up environment!**



