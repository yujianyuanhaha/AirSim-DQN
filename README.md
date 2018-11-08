# Wolverine
__Deep Reinforcement Learning for UAV__   
Semester Project for EE5894 Robot Motion Planning, Fall2018, Virginia Tech      
Team Members:​​ Chadha, Abhimanyu, Ragothaman, Shalini and Jianyuan (Jet) Yu      
Contact: Abhimanyu(abhimanyu16@vt.edu),  Shalini(rshalini@vt.edu), Jet(jianyuan@vt.edu)  
Simulator: [AirSim](https://github.com/Microsoft/AirSim)  
Open Source Library: [CNTK](https://github.com/Microsoft/CNTK)

# Install AirSim on Mac  
0. Before start
    * make sure good network connection and speed, the whole installation cost more than 20G size download.  
    * my case: 
        * Hardware - MacBook Pro (Retina, 13-inch, Early 2015); 
        * Graphics - Intel Iris Graphics 6100 1536 MB; 
        * OS - **High Sierra Version 10.13.6**; 
        * Xcode - verison 10.0    
    * install Xcode, and do lanuch to make sure it is well installed.   
1. install [Epic Games Launcher](https://www.unrealengine.com/download )  
2. launch Epic Games Launcher, in left Bar, click "Library", install the **Unreal Engine**, where I choose the newest version 4.20, the installation take around an hour for the ~20G download .  
3. after unreal engine is installed, launch it. Choose "Learn" at left Bar, select the **Landscape Mountains** scence, which is the official and most widely used one, and it cost ~2G download.   
4. When download finished, choose "Create Project" to save it.
5. Build Airsim:
    * change path to where you want to install, for my case, I choose ```~```.
    * ```
        git clone https://github.com/Microsoft/AirSim.git
        cd AirSim
        ./setup.sh
        ./build.sh
        ```  
    * the build take me around 20 min      
    
6. Run Blocks, open the ```Blocks.uproject``` under ```Unreal/Environments/Blocks/```, it may ask you to rebuild.  
7. copy the folder ```unreal/plugins``` of ```Blocks``` to ```LandscapeMountains```, in that airsim could run as a plugin in this project.
8. Launch the ```LandscapeMountains.uproject```.  


# Reference
* install AriSim on Mac in Chinese(https://blog.csdn.net/qq_26919935/article/details/80901773)  


# Install AirSim on Ubuntn 18.04
1. install __UE__
    1. signup Unreal Engine
    2. connect git account
    3. `git clone -b 4.17 https://github.com/EpicGames/UnrealEngine.git`
    4. cd UnrealEngine
    5. `/Setup.sh`
    6. `./GenerateProjectFiles.sh`
    7. `make`
    8. test lanuch by `Engine/Binaries/Linux/UE4Editor`
    The 5~7 step would eat up ~40G size of disk(while ~8G at Windows) and take ~4h time.
2. install __Airsim__
    1. todo
    2. test
3. install __CNTK__
    PyPI does NOT support Ubuntu18.04, and wheel (.whl) files way does not support python 3.7.0 so far, if no version fit your computer, try _make conda virtual environment_. e.g. I make a python2.7 environment to go on.
    1.
    2.
    3. test
    4. test `DQN_car.py`

Notice:
1. when test `hello_car.py`, make sure you open the UE4Editor and click the PLAY button.

