# Face-Recognition

Project on Face Recognition using OpenCV

We will implement a classical face recognition system using OpenCV library. The process will be carried out in two phases.

  - **Face Detection**
  - **Face Recognition**
  
Before we get started, you need to install some libraries. 

1. First of all you will need **Python 3.5** or more in your computer. You can easily check if it is installed by typing "python" in your terminal/command prompt. If not, [install python](https://www.python.org/downloads/) .

2. Now you need **OpenCV**. For this, you can run the command ***pip install opencv-python*** and ***pip install opencv-contrib-python***. Here is a detailed information of how you can [install OpenCV](https://pypi.org/project/opencv-python/).

3. The last library that you need is Pillow. It is used to access the images path and load them into our program. To install it, run ***pip install Pillow*** this command on your terminal.

That's it! You can now start writing your own programs and access OpenCV's power to do various Computer Vision projects. So let's get started with face detection.

## Face detection 

*Don't feel like reading the information below and want to directly get started with the implemenation??? Run the commands in italics and get started*

> *python face_detection.py*

Face detection is used nowadays in many kinds of applications like smartphone cameras, human computer interaction, social media and surveillance. It can be done using various pre-trained models which can do the heavy lifting for us to detect faces. OpenCV has various cascade classifiers which can detect faces with their different aspects like eye, nose and lips location. They are saved in a  XML file which we can access easily. There are line features, edge features and rectangle features in these models.

A Haar Cascade is basically a classifier which is used to detect particular objects from the source. The haarcascade_frontalface_default.xml is a haar cascade designed by OpenCV to detect the frontal face. A Haar Cascade works by training the cascade on thousands of negative images with the positive image superimposed on it. The haar cascade is capable of detecting features from the source. You can [explore more](
https://docs.opencv.org/3.4.3/d7/d8b/tutorial_py_face_detection.html) about Haar Cascade for face detection.

The program *face_detection.py* is able to locate the face in the given image using the same Cascade Classifier. Just make sure to specify the path where the haarcascade_frontalface_default.xml file is stored. I have uploaded the xml file in the repo. **It is recommended that you store this haarcascade_frontalface_default.xml file in the same folder where the face_detection.py is present.** You can [download](https://github.com/opencv/opencv/tree/master/data/haarcascades) various xml files and try diffrent things other than only face detection.

## Create Dataset

> *python create_dataset.py*

This script is used to store the facial images in the database which will be used to train the recognizer. Storing whole image will make it difficult to recognize the faces. Hence we will crop only the face from the captured image and store it to the folder. The rectangle that we drew over the face in the face_detection.py script, same concept will be applied to store the facial image. We have the co-ordinates of the rectangle which we can use to crop the image from the video. The script will create a folder named dataset where it will store all the images. If the folder is not present, it will do that for you!
One thing to notice is that we store the images in grayscale format. This is because the algorithm we use needs black and white images. It will further be explained when we talk about LBPH recognizer.

## Train the Recognizer

> *python train_recognizer.py*

Once we have saved faces to the dataset, its time to train a recognizer to recognize faces that are similar to the images in datset. In this script, we access the dataset folder and provide each image to the recognizer for analysis. We will be using ***LBPHFaceRecognizer*** for recognition of the face. Each image's label(id) will be extracted by spliting the path of image and the recogniser will output the label of the new image that will be provided to it for recognition. 

Make sure that you have created a folder named "trainer" on the same location. The trained recogniser will sotred in this folder for further use i.e to recognise new images. 

Lets see how the LBPH algorithm works.

**Local Binary Pattern Histograms (LBPH)**

 LBPH is one of the methods which is preferred nowadays for facial recognition applications. It is used in computer vision, image processing, and pattern recognition. As it describes the texture and structure of the image it is used for feature extraction. LBPH can be applied to represent a face image and reduce the face dimensions.
The original LBP operator works on the 8- neighbors of a pixel. The image is divided into small regions called cells. Each pixel in the cell is compared with each of its eight neighbors. The center pixel value will be used as the threshold value . The eight-neighbors-pixel will be set to one if its value is equal to or greater than the center pixel; otherwise, the value is set to zero. Accordingly, the LBP code for the center pixel is generated by concatenating the eight neighbor pixel values (ones or zeroes) into a binary code, which is converted to a 256-dimensional decimal for convenience as a texture descriptor of the center pixel.

For more detailed explaination of this algorithm, you can go [here.](https://towardsdatascience.com/face-recognition-how-lbph-works-90ec258c3d6b)

## Recognize faces

> *python video_recognition.py*

We are all set now. Till now we did all the work required for recognizing your face like creating a dataset and training a model. Now its time to actually see how the program recognises the face. But for that, you need get your hands dirty on the code written in the video_recognition.py script. On the line number **18**, there is a list named as **names**. It has the names which needs to be shown while the script recognises the face. You need to edit that list and fill in the names you wish. Remember that saved some images using create_dataset.py script? Just recall the user id you entered before the images were actually captured. The is corresponds to the index of the name that is present in the list. For example, if Omkar saved his images using user id = 1, then the list should be updated by the name "Omkar" at the index 1, where at present it is written as "User 1". Just fill in the proper name in this list corresponding to the user id in the dataset folder. If you have saved n users images while executing create_dataset.py script, you must have n+1 entries in the **names** list present in video_recognition.py script. The 0th index in kept "None" as we don't have any entry for user id=0.
Once you execute this script, the video frame will pop up and the known faces(trained images) will get recognized. On line number 54 of the video_recognition.py script, you will find a condition which compares the confidence with an arbitary number.This acts as a thresold value which specifies what is the minimum confidence required to predict the id of the face in the video. You can play around with this threshold to get accurate results.

**Yeaahhh!** You have used the powers of OpenCV and Python for facial recognition. This can be further used for many applications where facial recognition can be implemented to build some interesting projects. This was the simplest algorithm that we can use for face recognition. There are many more advanced algorithms you can explore if this domain excites you. That's all I'hv got to share in this repo. Thanks for exploring the code and hope you enjoyed it!

**Happy Coding**

## Credits and References

1 [OpenCV Documentation Page](https://docs.opencv.org/2.4/modules/contrib/doc/facerec/facerec_tutorial.html#local-binary-patterns-histograms)

2 [Face Detection Documentation](https://opencv-python-tutroals.readthedocs.io/en/latest/py_tutorials/py_objdetect/py_face_detection/py_face_detection.html)

3 [Towards Data Science : Understanding LBPH Algorithm](https://towardsdatascience.com/face-recognition-how-lbph-works-90ec258c3d6b)

