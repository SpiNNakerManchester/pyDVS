## A Cython-based Dynamic Vision Sensor (DVS) emulator. It can be used within a Python environment as demonstrated in the various test files.


A DVS is a camera-like sensor which emits per-pixel asynchronous Address-Event Representation (AER) packets. These are originated due to an intensity level change has reached a certain threshold. 

This project emulates this behaviour using commodity hardware, that is a regular PC and camera. Modifications to the default behaviour where added, mainly: encoding of values using time, local inhibition and dynamic thresholds.

This is a fork of the original [pyDVS](https://github.com/chanokin/pyDVS) by Garibaldi Pineda-Garcia  
This version has been ported to Python 3 and checked with the virtual cam on MacOS Sierra.
The imports code has also been cleaned up.

Requirements:
- Cython
- Numpy
- OpenCV (with Python bindings)

Before using, compile the Cython modules by running
    
`python setup.py build_ext --inplace`  
  
in the folder where pyDVS is installed.

Files:
- `pydvs/`:
  - `generate_spikes.pyx`  - Cython backend library. Contains functions to generate spikes from a video feed.
  - `external_dvs_emulator_device*.py` - sPyNNaker class wrapper, it's compatible with OpenCV VideoCapture devices and VirtualCam.
  - `virtual_cam.py` - A camera emulator that feeds on images located in the users computer. It keeps images moving based on eye movements (e.g. micro saccades and saccades); there's a very simple attention model for the saccade mode. 

- `spynnaker_test.py` - Demonstration script for sPyNNaker compatible frontend.
- `stand_alone*.py` - Demonstration scripts for the Cython backend, they come in single- and multi-threaded versions.
- `virtual_cam_test.py` - Demonstration script for the VirtualCam class, it requires images in a directory ("./mnist" by default)
