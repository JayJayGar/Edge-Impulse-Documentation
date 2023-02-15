# Edge-Impulse-Documentation
## Creating and Setting up Project
I started by creating an account and creating a project. I set up the dashboard, and in my project info I set the labeling method to bounding boxes and the target device the board I was using.

![image](https://user-images.githubusercontent.com/90651596/215884961-55ca2732-633d-4e6e-a1bf-bd210321fcfd.png)
## Downloading and Uploading the Data Set
I began by downloading a public dataset from [Kaggle](https://www.kaggle.com), one that detects and creates bounding boxes around cars. The data was created by taking a video and splicing the video up into many images; with a `.csv` file denoting where the bounding boxes were in the training set. I originally tried to upload the file as is, but found that for creating bounding boxes with images, on Edge Impulse only a `.json` file could be used.

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
Next we head over to the Object detection tab on the left. Starting at the top, we need to make sure the target processor is set, for me it is going to be the 'Renesas RZ/V2L (with DRP-AI accelerator)'. First you are going to want to select a model, as the other settings depend on what you choose. I am going to be using `Renesas / YOLOv5 for Renesas DRP-AI`, and I am setting the training cycles to 8, as that is as many the time alloted allowed for using this model. You should choose as many training cycles are you can; and set the learning rate to 0.001% and the Validation set size to 20% for best results.Click the `Start Training` button and wait for the model to be completed.


![image](https://user-images.githubusercontent.com/90651596/216424091-963d07e8-2093-4e39-a363-64768e6f8cc9.png)


## Model Testing
To test your model, you are going to want to go to the `Model Testing` tab on the left, and hit classify all. If you get an error stating that there is an undefined toString like I did, go back to the image tab and re-generate the features.

![image](https://user-images.githubusercontent.com/90651596/218908824-cd998a70-d501-4896-a6ff-fd4ca15f4444.png)


## Exporting of Model
### Deployment
There are a couple more tabs left, but I am going to be skipping to the deployment tab. All you have to do here is select your preferred method for exporting, mine being through the board I am using "Linux (RZ/V2L)." Once you select the type of export, the only next step on the browser is to click the `Build` button.

![image](https://user-images.githubusercontent.com/90651596/216429576-7f64143c-8c08-48ef-9041-b53700e13fdb.png)
