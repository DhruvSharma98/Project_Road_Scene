## fau box links
input_video.mp4
https://faubox.rrze.uni-erlangen.de/getlink/fi4SkMw7qgsHNDEmYtSQR5/input_video.mp4

model.onnx
https://faubox.rrze.uni-erlangen.de/getlink/fiQHYEVH7FSYSk9pfskf8o/model.onnx

trained on cityscapes model checkpoint
https://faubox.rrze.uni-erlangen.de/getlink/fiQxx8EmbRenukfSUVyJpY/trained_on_cityscapes.ckpt

fine-tuned on mapillary model checkpoint
https://faubox.rrze.uni-erlangen.de/getlink/fiVwCRYbMxHR2ZnoxcNnXb/fine_tuned_mapillary.ckpt


## Sample environment creation (Windows)

conda create -n myenv python=3.9

pip install torch==2.1.2 torchvision==0.16.2 torchaudio==2.1.2 --index-url https://download.pytorch.org/whl/cu121

pip install -r requirements.txt


## Running scripts

------to run rsu_vi.py------
1. input video and GPS file should be in "input" folder
2. model.onnx should be in "model_weights" folder

then run terminal command
**for video input**
```bash
python rsu_vi.py "input/input_video.mp4" "segmentation_output.avi" "model_weights/model.onnx" "input/new.gpx" --headless
```

**for image folder input**
```bash
python rsu_vi.py "images" "segmentation_output" "model_weights/model.onnx" "input/new.gpx"
```

**for camera input**
```bash
python python rsu_vi.py 0 "cam_output.avi" "model_weights/model.onnx" "input/new.gpx"
```

------to run onnx_export.py------
run terminal command
```bash
python onnx_export.py --pytorch="fine_tuned_mapillary.ckpt"
```


------to train cityscapes model (city_training.py)------
1. set the dataset_path in city_config.py
2. run city_training.py script

dataset_path - path to the directory where leftImg8bit and gtFine folders of cityscapes dataset are present



------to convert mapillary masks to grayscale (convert_masks_to_grayscale.py)------
1. set the json_path, masks_path, op_path in map_config.py
2. convert_masks_to_grayscale.py script

json_path - path to config.json file in mapillary dataset
masks_path - directory of rgb masks to convert to grayscale
op_path - directory where converted grayscale masks will be saved



------to fine-tune on mapillary dataset (training_pipeline.py)------
1. set the mapillary_train_path, mapillary_val_path, mapillary_test_path, city_ckpt_path in map_config.py
2. run training_pipeline.py script

mapillary_train_path - directory where mapillary training images and labels folder are present
mapillary_val_path - directory where mapillary validation images and labels folder are present
mapillary_test_path - directory where mapillary testing images and labels folder are present
city_ckpt_path - checkpoint path of the model trained on cityscapes dataset



------to perform inference on an image (inference.py)------
1. set the map_ckp_path, img_dir, op_dir in map_config.py
2. run inference.py script

map_ckp_path - path of model fine_tuned on mapillary dataset
img_dir - directory of images to segment
op_dir - output directory where segmented images are saved


* the following warning can be ignored
[W NNPACK.cpp:64] Could not initialize NNPACK! Reason: Unsupported hardware.

