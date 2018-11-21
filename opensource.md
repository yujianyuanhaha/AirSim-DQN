# [AirSimDroneSimulator](https://github.com/AirSimDroneSimulator/AirSim)
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
4. __`captureimages.py`__ of __Object_Detection/Faster_R-CNN__
    1. `RPCError: rpclib: client error C0002: Function 'getHomeGeoPoint' was called with an invalid number of arguments. Expected: 0, got: 1`


# [Obstacle Avoidance using DDQN](https://github.com/npd15393/Obstacle-Avoidance-using-DDQN)


	


1. __`dqn_tr1.py`__
    1. `moveToPosition()` -> `moveToPositionAsync()`
    2. `goHome()` -> `goHomeAsync()`
    3. PASS!
    4. warining
        ``` bash
        WARNING:root:getVelocity API is deprecated. For ground-truth please use simGetGroundTruthKinematics() API.
        Please see https://github.com/Microsoft/AirSim/blob/master/docs/upgrade_apis.md for more info.
        WARNING:root:getPosition API is deprecated. For ground-truth please use simGetGroundTruthKinematics() API.
        Please see https://github.com/Microsoft/AirSim/blob/master/docs/upgrade_apis.md for more info.
        ```
    5. obstacle setup(TODO)

2. __`NewTestDDQN.py`__ -> `TypeError: 'module' object is not callable`
    1. [concated instead of merge](https://stackoverflow.com/questions/51075666/how-to-implement-merge-from-keras-layers) -> `ValueError: Output tensors to a Model must be the output of a Keras `Layer` (thus holding past layer metadata). Found: <keras.layers.merge.Concatenate object at 0x7f6f37298860>`

3. __`ddqn_example.py`__ -> `TypeError: 'module' object is not callable`