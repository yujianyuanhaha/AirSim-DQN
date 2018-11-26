# ~~Wolverine~~
__Deep Reinforcement Learning for UAV__   
Semester Project for EE5894 Robot Motion Planning, Fall2018, Virginia Tech      
Team Members:​​ ~~Chadha, Abhimanyu, Ragothaman, Shalini and~~ Jianyuan (Jet) Yu      
Contact: ~~Abhimanyu(abhimanyu16@vt.edu),  Shalini(rshalini@vt.edu)~~, Jet(jianyuan@vt.edu)  
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


## Reference
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
2. install __Airsim__, [official guide](https://github.com/Microsoft/AirSim/blob/master/docs/build_linux.md), Ubuntu start from 1.2.0.
    ``` bash
        git clone https://github.com/Microsoft/AirSim.git
        cd AirSim
        ./setup.sh
        ./build.sh
    ```
3. install __CNTK__
    PyPI does NOT support Ubuntu18.04, and wheel (.whl) files way does not support python 3.7.0 so far, if no version fit your computer, try _make conda virtual environment_. e.g. I make a python2.7 environment to go on.
    1. fix `libmpi_cxx.so.1` errror  -> follow [refer](https://tweaks-tips.blogspot.com/2017/12/microsoft-cntk-libmpi-importerror.html), `sudo ln -s /usr/lib/x86_64-linux-gnu/libmpi_cxx.so.20 /usr/lib/x86_64-linux-gnu/libmpi_cxx.so.1` and `sudo ln -s /usr/lib/x86_64-linux-gnu/libmpi.so.20.10.1 /usr/lib/x86_64-linux-gnu/libmpi.so.12`  and update the path as `export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/lib/x86_64-linux-gnu`.
    2. fix `libmklml.so`. -> install by `conda install -c anaconda mklml` and update path by `export LD_LIBRARY_PATH=/home/jet/anaconda3/envs/py2/lib:$LD_LIBRARY_PATH`. 

Currently pass import cntk with warning
``` bash
/home/jet/anaconda3/envs/py2/lib/python2.7/site-packages/cntk/cntk_py_init.py:47: UserWarning: Unsupported Linux distribution (ubuntu-18.04). CNTK supports Ubuntu 16.04 and above, only.
  warnings.warn('Unsupported Linux distribution (%s-%s). CNTK supports Ubuntu 16.04 and above, only.' % (__my_distro__, __my_distro_ver__))
```
However, new problem is `DQNcar.py` cannot run through, with bugs __MemoryError__ as 
```
/home/jet/anaconda3/envs/py2/lib/python2.7/site-packages/cntk/cntk_py_init.py:47: UserWarning: Unsupported Linux distribution (ubuntu-18.04). CNTK supports Ubuntu 16.04 and above, only.
  warnings.warn('Unsupported Linux distribution (%s-%s). CNTK supports Ubuntu 16.04 and above, only.' % (__my_distro__, __my_distro_ver__))
Connected!
Client Ver:1 (Min Req: 1), Server Ver:1 (Min Req: 1)

Traceback (most recent call last):
  File "DQNcar.py", line 505, in <module>
    agent = DeepQAgent((NumBufferFrames, SizeRows, SizeCols), NumActions, monitor=True)
  File "DQNcar.py", line 270, in __init__
    self._memory = ReplayMemory(memory_size, input_shape[1:], 4)
  File "DQNcar.py", line 35, in __init__
    self._states = np.zeros((size,) + sample_shape, dtype=np.float32)
MemoryError
```


3. test
4. test `DQN_car.py`

Notice:
1. when test `hello_car.py`, make sure you open the UE4Editor and click the PLAY button.






# install CNTK
cntk current does not support ubuntu 18.04
1. downgrade python to 3.5.0
2. install `numpy`, `msgpack-rpc-python`
3. install related `.whl`, e.g. python3.5.0+cntk2.5.0 with (https://cntk.ai/PythonWheel/CPU-Only/cntk-2.5-cp35-cp35m-linux_x86_64.whl)
4. `conda install -c anaconda mklml`
5. update path `export LD_LIBRARY_PATH=/home/jet/anaconda3/lib:$LD_LIBRARY_PATH`, cd to related path to check lib like `libmklml.so` exisit.
6. type `python`, type `import cntk` to test.
Output would be like
``` bash
/home/jet/anaconda3/lib/python3.5/site-packages/cntk/cntk_py_init.py:47: UserWarning: Unsupported Linux distribution (ubuntu-18.04). CNTK supports Ubuntu 16.04 and above, only.
  warnings.warn('Unsupported Linux distribution (%s-%s). CNTK supports Ubuntu 16.04 and above, only.' % (__my_distro__, __my_distro_ver__))

```

# Reference Projects
* [Autonomous Driving using End-to-End Deep Learning: an AirSim tutorial](https://github.com/Microsoft/AutonomousDrivingCookbook/tree/master/AirSimE2EDeepLearning) - official
* [Object Tracing with UAV in AirSim Environment](https://github.com/AirSimDroneSimulator) - implement DQN with tensorflow/keras rather than CNTK. 
* [Obstacle-Avoidance-using-DDQN](https://github.com/npd15393/Obstacle-Avoidance-using-DDQN) - CNTK