<h1>Transfer-Learning-in-Keras</h1>
Transfer learning is a machine learning method where a model developed for a task is reused as the starting point for a model on a second task.It help us to get better accuracy with limited resource ,time and data. Here we will build three models-
<ol>
  <li><h3>MODEL 1:</h3>
<pre>
1. Use <a href='https://www.tensorflow.org/api_docs/python/tf/keras/applications/VGG16'>VGG-16</a> pretrained network without Fully Connected layers and initilize all the weights with Imagenet trained weights. 
2. After VGG-16 network without FC layers, add a new Conv block ( 1 Conv layer and 1 Maxpooling ), 2 FC layers and a Output layer to classify 16 classes.
3. Final architecture will be <b>INPUT --> VGG-16 without Top layers(FC) --> Conv Layer --> Maxpool Layer --> 2 FC layers --> Output Layer</b>
4. Train only new Conv block, FC layers, Output layer. Don't train the VGG-16 network. 

</pre>
   <li><h3>MODEL 2</h3></li>
  <pre>
1. Use <a href='https://www.tensorflow.org/api_docs/python/tf/keras/applications/VGG16' >VGG-16</a> pretrained network without Fully Connected layers and initilize all the weights with Imagenet trained weights.
2. After VGG-16 network without FC layers, don't use FC layers, use Conv layers only as Fully Connected layer. Any FC layer can be converted to a CONV layer. This conversion will reduce the number of trainable parameters in FC layers. For example, an FC layer with K=4096 that is looking at some input volume of size 7×7×512 can be equivalently expressed as a CONV layer with F=7,P=0,S=1,K=4096. In other words, we are setting the filter size to be exactly the size of the input volume, and hence the output will simply be 1×1×4096 since only a single depth column “fits” across the input volume, giving identical result as the initial FC layer.
3. Final architecture will be <b>INPUT --> VGG-16 without Top layers(FC) --> 2 Conv Layers identical to FC --> Output Layer</b>
4. Train only last 2 Conv layers identical to FC layers, 1 output layer. Don't train the VGG-16 network. 
</pre>
   <li><h3>MODEL 3</h3></li>
   
   
   <pre>
1. Use same network as Model-2 '<b>INPUT --> VGG-16 without Top layers(FC) --> 2 Conv Layers identical to FC --> Output Layer</b>' and train only last 6 layers of VGG-16 network, 2 Conv layers identical to FC layers, 1 Output layer.
</pre>
</ol>

<h2>DATA</h2>
<pre>
1. Download all the data in this folder <a href='https://drive.google.com/open?id=1Z4TyI7FcFVEx8qdl4jO9qxvxaqLSqoEu'>Data</a>.
It contains two file both images and labels. The label file list the images and their categories in the following format:
<b>path/to/the/image.tif,category</b> where the categories are numbered 0 to 15, in the following order:
   <b>0 letter
   1 form
   2 email
   3 handwritten
   4 advertisement
   5 scientific report
   6 scientific publication
   7 specification
   8 file folder
   9 news article
   10 budget
   11 invoice
   12 presentation
   13 questionnaire
   14 resume
   15 memo</b>
    
