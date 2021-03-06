# deeplearning-encode

This POC is trying to use deep learning based method to detect interested object in video stream, then use the detection rectangle as ROI region and feed into encode application for ROI based encoding, with which the region of interested object will be allocated more bits in encoding, therefore better visual quality.

## Implementation #1: MSDK encode with detector class (standalone)

**Note1**: When link OpenCV library into MSDK app, it seems we cannot use OpenCV dynamic library (DLL) because MSDK app will run into a failure in OpenCV NN module. There is no such issue if use OpenCV static library (LIB). 

**Note2**: When link OpenCV static library into MSDK, for debug build, there are some LINK errors in building app (suspect MSDK sample app compiling config issue?), so have to use release build to workaround it.


## Implementation #2: OpenCV Python + MSDK Encode (two steps)

### Step1: Object detection

- **framework**: OpenCV + Caffe
- **Network**: MobileNet SSD (Single Shot MultiBox Detection)

![result1](https://github.com/mintaka33/deeplearning-encode/blob/master/result/p1.png?raw=true)

### Step2: ROI based Encoding

- **framework**: MSDK simple encode
- **encode config**: CQP(qp=40) + DeltaQP(delta_qp = -20)
- **platform**: Intel KBL Gen9 GPU

![result2](https://github.com/mintaka33/deeplearning-encode/blob/master/result/p2.png?raw=true)

![result3](https://github.com/mintaka33/deeplearning-encode/blob/master/result/p3.png?raw=true)
