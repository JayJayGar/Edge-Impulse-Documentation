# Edge-Impulse-Documentation
## Creating and Setting up Project
I started by creating an account and creating a project. I set up the dashboard, and in my project info I set the labeling method to bounding boxes and the target device the board I was using.

![image](https://user-images.githubusercontent.com/90651596/215884961-55ca2732-633d-4e6e-a1bf-bd210321fcfd.png)
## Downloading and Uploading the Data Set
I began by downloading a public dataset from [Kaggle](https://www.kaggle.com), one that detects and creates bounding boxes around cars. The data was created by taking a video and splicing the video up into many images; with a `.csv` file denoting where the bounding boxes were in the training set. I originally tried to upload the file as is, but found that with creating bounding boxes with image only a `.json` file could be used

Knowing that Edge Impulse requires a `.json` file for bounding boxes, I used an online resource to parse the data into a `.json`. It created an unformatted and unusable file, so I created a [script](https://github.com/JayJayGar/.JSON-editor) to parse it using the accepted format, which can be [found here](https://docs.edgeimpulse.com/docs/edge-impulse-cli/cli-uploader#bounding-boxes). The script also renames the file into `bounding_boxes.labels` which is needed for uploading the file.

Going into the Data Aquisition tab on the left, I uploaded the training and test data. Make sure to upload the `bounding_boxes.labels` with the training set the first time, as you cannot add the boxes after the images have been uploaded. If some files fail to attach bounding boxes or the the controls still need to be labeled, you will need to manually tag them.

![image](https://user-images.githubusercontent.com/90651596/215886727-0c3d8b09-ec15-4a1d-bdb9-3e17d639f543.png)
Going into the Labeling Queue, you have a couple options of making bounding boxes. You can either `Track objects between frames`(manually) or `Classify using YOLOv5`(automatically). I chose to do them manually, as many of the ones I had left were controls.

## Impulse Design
### Create Impulse
Next we are going to want to go into the Impulse Design tab on the left. You can change the resolution of the video and images by changing the size in the `Image data` block. If you use FOMO or YOLOv5, you need to have a resolution of 160x160 and 320x320 respectively. Because I am using YOLOv5 later on, I set it to 320x320. I chose the basic `Image` processor block. As for the learning block I chose the `Object Detection (Images)` block. After adding all of the blocks, save the impulse to move on.

![image](https://user-images.githubusercontent.com/90651596/215889140-f1c2854f-7b8d-4f60-93ac-9b40d4b32d89.png)

### Image
Move on to the next option on the left, the image section under Impulse Design. At the top click the 'generate features' tab and click on the `Generate features` button. A graph will appear denoting that the features necessary for model have been created.

![image](https://user-images.githubusercontent.com/90651596/215893317-c7ee9508-1aed-4efe-aeab-c1ce691896ba.png)

### Object Detection
Next we head over to the Object detection tab on the left. Starting at the top, we need to make sure the target processor is set, for me it is going to be the 'Renesas RZ/V2L (with DRP-AI accelerator)'.



![image](https://user-images.githubusercontent.com/90651596/215895315-71c77de6-d168-44a6-a6f8-a5dff6194dca.png)



