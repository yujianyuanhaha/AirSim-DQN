# API lookup
* [pdf]()
* linux command


# Environment Setup
[version](https://github.com/Microsoft/AirSim/releases/tag/v1.2.0Linux) for many other environments. e.g. cities. Although many of them are for Windows, copy them to related folders.  
* remeber to backup a clean version before you start your own version.


# UE4Editor easily crashed

# PATH setup im IPython terminal of Spyder
`export LD_LIBRARY_PATH=/home/jet/anaconda3/lib:$LD_LIBRARY_PATH` work in raw terminal, while not in IPython. 
1. alter to VS Code & write `~/.bashrc` & run under base -> PASS
2. install mklml lib  -> FAIL
3. [%env foo=bar](https://ipython.readthedocs.io/en/stable/interactive/shell.html#environment-variables), follow the format like other env variables. -> FAIL
4. copy `~/anaconda3/lib/libmklml_intel.so` to the other path `~/anaconda3/lib/python3.5/site-packages/`, and `chmod` -> FAIL
5. write to `~/.bashrc` -> FAIL
6. conda base env
    1. start from (base) prompt -> FAIL
    2. in ipython `workon` -> FAIL


# update api
Both the open source use on __Airsim 1.2.0__ or earlier, refer to [update api](https://github.com/Microsoft/AirSim/blob/master/docs/upgrade_apis.md) for some substitute. Some of them still work with warinings, while some pop erors.
## getPosition( ) getVelocity( ) getCollisionInfo() 
1. `WARNING:root:getPosition API is deprecated. For ground-truth please use simGetGroundTruthKinematics() API.`
2. `WARNING:root:getVelocity API is deprecated. For ground-truth please use simGetGroundTruthKinematics() API.` 
3. `WARNING:root:getCollisionInfo API is renamed to simGetCollisionInfo. Please update your code`  


__SOLUTION__
replace any `getPosition( )` as `simGetGroundTruthKinematics().position`, and `getVelocity()` as `simGetGroundTruthKinematics().linear_velocity`. as reference from [`client.py`](https://github.com/Microsoft/AirSim/blob/master/PythonClient/airsim/client.py)  
``` python
    def getPosition(self):
        logging.warning("getPosition API is deprecated. For ground-truth please use simGetGroundTruthKinematics() API." + self.upgrade_api_help)
        return self.simGetGroundTruthKinematics().position
    def getVelocity(self):
        logging.warning("getVelocity API is deprecated. For ground-truth please use simGetGroundTruthKinematics() API." + self.upgrade_api_help)
    return self.simGetGroundTruthKinematics().linear_velocity
```
Also, `getCollisionInfo()` is renamed to `simGetCollisionInfo()`. 


# [AirSimDroneSimulator](https://github.com/AirSimDroneSimulator/AirSim)

Based on __Keras__.

1. install `theano`, `h5py`
2. run __`main.py`__ of __3D_path_finding/DQN__
    1. change path to DQN
    2. open `main.ipynb`,download `main.py`
    3. debug `#from DQN.RL_dataset import Dataset` -> 
`from RL_dataset import Dataset` of `RL_dataset.py`
    4. `Unable to open file (unable to open file: name = 'finalb.h5', errno = 2, error message = 'No such file or directory', flags = 0, o_flags = 0)` -> miss `finalb.h5` file. -> disable the read of this file -> `msgpackrpc.error.RPCError: rpclib: client error C0002: Function 'getHomeGeoPoint' was called with an invalid number of arguments. Expected: 0, got: 1`
3. run __`main.py`__ of __3D_path_finding/DDQN__
    1. `ImportError: No module named 'cv2'` -> `conda install -c conda-forge opencv`
    2. `RPCError: rpclib: client error C0002: Function 'getHomeGeoPoint' was called with an invalid number of arguments. Expected: 0, got: 1` ->
4. run __`test.py`__ of __3D_path_finding/DDQN__
5. __`captureimages.py`__ of __Object_Detection/Faster_R-CNN__
    1. `RPCError: rpclib: client error C0002: Function 'getHomeGeoPoint' was called with an invalid number of arguments. Expected: 0, got: 1` -> version issue - replace `AirSimClient` as `client`


# [Obstacle Avoidance using DDQN](https://github.com/npd15393/Obstacle-Avoidance-using-DDQN)
based on __CNTK__.

	


1. __`dqn_tr1.py`__ (starter)
    1. `moveToPosition()` -> `moveToPositionAsync()`
    2. `goHome()` -> `goHomeAsync()`
    3. ~~`NameError: name 'AirSimImageType' is not defined`~~ -> PASS
    4. ~~warining~~
        ``` bash
        WARNING:root:getVelocity API is deprecated. For ground-truth please use simGetGroundTruthKinematics() API.
        Please see https://github.com/Microsoft/AirSim/blob/master/docs/upgrade_apis.md for more info.
        WARNING:root:getPosition API is deprecated. For ground-truth please use simGetGroundTruthKinematics() API.
        Please see https://github.com/Microsoft/AirSim/blob/master/docs/upgrade_apis.md for more info.
        ```
    5. obstacle setup(TODO)
    4. not receive api call in UE4 (TODO).

2. __`NewTestDDQN.py`__ (official)
    1. ~~[concated instead of merge](https://stackoverflow.com/questions/51075666/how-to-implement-merge-from-keras-layers) -> `ValueError: Output tensors to a Model must be the output of a Keras `Layer` (thus holding past layer metadata). Found: <keras.layers.merge.Concatenate object at 0x7f6f37298860>`~~
    2. `TypeError: 'module' object is not callable` -> py3 grammer of import
    3. `ValueError: Negative dimension size caused by subtracting 8 from 4 for 'conv2d_1/convolution' (op: 'Conv2D') with input shapes: [?,4,84,84], [8,8,84,16].` OR ``
        1. tricks, debug into to see the size, `model.input_size`, `model.output_size` after each `Conv2D` and `Max2Dpooling`. Likely input is unmatched.
        2. [refer codes](https://github.com/keras-team/keras/blob/master/examples/mnist_cnn.py) `from keras import backend as K; K.image_data_format()` -> `'channels_last'` / __input_shape = (img_rows, img_cols, 1)__ PASS

3. __`ddqn_example.py`__ (sample code, nothing to do with AirSim) 
    1. `merge()`-> `TypeError: 'module' object is not callable`
        1. reinstalll tensorflow and keras
    2. `concate()` -> size unmatch
    3. can concate substitute the expired merge?


## ToDo
1. the CNN, the network match
2. print action and reward
3. file and data save


## corrupt env
Collide with Plane, Car -> set plane coord, Multirotor -> wait
1. go on fix -> set the plane coord
2. ~~copy and work on a new one~~ -> Fail
3. ~~start over comiple~~ -> Fail