# VQA-on-CLEVR-dataset


VISUAL QUESTION ANSWERING


INTRODUCTION
The dataset provided is a modification of the CLEVR dataset. It consists of a collection of synthesized images and a set of questions associated with each image. Your task is to predict the answers to these questions. It has about 15000 images and 135000 questions and answers for training. Most images have about 10 questions associated with them, however, some images don’t have any questions associated with them.The images contain simple 3D objects with each object having one of the 96 property profiles obtained by picking one choice each from the following four types:
Shape: Sphere, Cube, Cylinder
Size: Large, Small
Material: (Matte) Rubber, (Shiny) Metal
Color: Gray, Cyan, Blue, Purple, Brown… (8 colors)

The questions test the understanding regarding the various type of relationships between these objects. The relationships include the understanding of the position relative to the other objects i.e which of two objects lies to the left/right of the other or which of the two objects lies in front of/behind the other. 
For addressing the task at hand,we have trained the dataset on three different models and chosen the model with the best relative accuracy score. Model architectures used are:
1.  CNN-LSTM model
2.  Skip connection CNN – LSTM model
3.  CNN –LSTM model with Stacked Attention


CNN –LSTM Model
Pretrained 50-d GloVe embeddings have been used for the embedding layer of LSTM
CNN head outputs 16 feature maps of size 8x8
The question vector and flatten image vector are concatenated and fed into a series of dense layers


Skip connection CNN – LSTM Model
The model architecture has been partly inspired by skip connections used in the architecture of YOLO v2.
Skip architecture skips some layer in the neural network and feeds the output of one layer as the input to the next layer as well as some other layer (instead of only the next layer ).
The model adds skip connections to the CNN head of the vanilla CNN – LSTM Model.
The information that we had in the primary layers can be fed explicitly to the later layers using the skip architecture.

      		 	Source :  https://arxiv.org/pdf/1603.04992.pdf




CNN –LSTM Model with Stacked Attention
This model is a Keras implementation of the model proposed in the paper : 
Stacked Attention Networks for Image Question Answering.
Link to the paper :
https://www.cvfoundation.org/openaccess/content_cvpr_2016/papers/Yang_Stacked_Attention_Networks_CVPR_2016_paper.pdf
As in the paper,we have used 2 attention layers to capture region-wise relations between the objects in the image and objects referred to in the question.


To find the optimum parameters We tried to implement the Grid Search on the various the various hyper-parameters like number of dense units ,epochs,learning rate,etc . however later we came to know that one can’t apply gridsearch on multi-input models like the ones being used to solve the given problem statement. Thus various parameters like epochs,learning rate were manually tested by running various models and analysing the results. It was found that the optimizer Adadelta() at the default parameters preformed the best among the various other parameters like Adam, SGD , etc.  


