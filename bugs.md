1. anaconda-navigator & spyder launch fail
* former `ImportError: cannot import name 'QKeySequence'`
* later `ImportError: libicui18n.so.56: cannot open shared object file: No such file or directory`
2. `~/temp/AirSim/3D_path_finding/DQN/main.py` fail
``` bash
Using Theano backend.
2018-11-09 21:37:30.253517: I tensorflow/core/platform/cpu_feature_guard.cc:140] Your CPU supports instructions that this TensorFlow binary was not compiled to use: AVX2 FMA
Traceback (most recent call last):
  File "main.py", line 32, in <module>
    test_model = keras.models.load_model("finalb.h5")
  File "/home/jet/anaconda3/lib/python3.5/site-packages/keras/models.py", line 233, in load_model
    with h5py.File(filepath, mode='r') as f:
  File "/home/jet/anaconda3/lib/python3.5/site-packages/h5py/_hl/files.py", line 312, in __init__
    fid = make_fid(name, mode, userblock_size, fapl, swmr=swmr)
  File "/home/jet/anaconda3/lib/python3.5/site-packages/h5py/_hl/files.py", line 142, in make_fid
    fid = h5f.open(name, flags, fapl=fapl)
  File "h5py/_objects.pyx", line 54, in h5py._objects.with_phil.wrapper
  File "h5py/_objects.pyx", line 55, in h5py._objects.with_phil.wrapper
  File "h5py/h5f.pyx", line 78, in h5py.h5f.open
OSError: Unable to open file (unable to open file: name = 'finalb.h5', errno = 2, error message = 'No such file or directory', flags = 0, o_flags = 0)
```