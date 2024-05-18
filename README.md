# Yolov8 and V9 TensorRT

---


# Prepare the environment

1. Install `CUDA` follow [`CUDA official website`](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#download-the-nvidia-cuda-toolkit).

   🚀 RECOMMENDED `CUDA` >= 12.2

2. Install `TensorRT` follow [`TensorRT official website`](https://developer.nvidia.com/nvidia-tensorrt-8x-download).

   🚀 RECOMMENDED `TensorRT` >= 8.6.1

3. Install [`ultralytics`](https://github.com/ultralytics/ultralytics) package for ONNX export or TensorRT API building.

   ``` shell
    pip install ultralytics==8.0.196

    from IPython import display
    display.clear_output()

    import ultralytics
    ultralytics.checks()

   ```
4. Prepare your own PyTorch weight such as `yolov8s.pt`.

***NOTICE:***

Please use the latest `CUDA` and `TensorRT`, so that you can achieve the fastest speed !

If you have to use a lower version of `CUDA` and `TensorRT`, please read the relevant issues carefully !

# Normal Usage

If you get ONNX from origin [`ultralytics`](https://github.com/ultralytics/ultralytics) repo, you should build engine by yourself.

You can only use the `Python` inference code to deserialize the engine and do inference.

5. We have created the **custom dataset ** using 'Roboflow'

6. Make directory as datasets inside the datasets folder import the roboflow api key download the dependencies packages to support.
 ``` shell  
 !mkdir /content/datasets
 %cd /content/datasets
 # Roboflow API Key to import the dataset to colab
 !pip install roboflow


 from roboflow import Roboflow
 rf = Roboflow(api_key="XXXXXXXXXXXXXXXXXXXXX")
 project = rf.workspace("deepika-xxxxxx").project("object-detection")
 version = project.version(1)
 dataset = version.download("yolov8")
 ```
Download the zip files and extract the zip files of datasets.

7. Run the epochs weights with our custom datasets. train, test and validate the finalized two sets one is best.pt and last.pt versions.
``` shell
!yolo task=detect mode=train model=yolov8s.pt imgsz=1920 data="/pathto/data.yaml" epochs=35 batch=2 name=yolov8s_custom
```
we have mentioned 35 epochs and images size 1920 to get a better mean average precision values of each epochs weight and which epochs will provide best values.



