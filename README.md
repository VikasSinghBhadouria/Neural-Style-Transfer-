# Neural-Style-Transfer-
A deep learning based model to use two images (One for content , one for style ) and 
generate a third image  with content of first and style of second .

What does Style Transfer mean?

During the past few years we’ve seen a slew of apps like prisma and other similar apps popping up which style your photos 
in a way wherein they look like paintings. Offering you a variety of beautiful styles some of which are paintings by famous
artists like Starry Night by Van Gogh. Trying to explain this concept just with words might be difficult.

https://cdn-images-1.medium.com/max/1600/0*F3xvwBKFhaQ3Mh_k

there are two input images namely content image and style image that are used to a generate a new image called stylized image. 
A few things to notice about this image is that it has the same content as the content image and has a style similar to that 
of the style image. It looks good and we are pretty sure it’s not achieved by overlapping these two images .
so how do we get here what is the math behind this idea?
We use VGG19, as suggested in the paper. In addition, since VGG19 is a relatively simple model 
(compared with ResNet, Inception, etc) the feature maps actually work better for style transfer.

In order to access the intermediate layers corresponding to our style and content feature maps,
we get the corresponding outputs by using the Keras Functional API to define our model with the desired output activations.

we’ll load our pretrained image classification network. Then we grab the layers of interest as we defined earlier. 
Then we define a Model by setting the model’s inputs to an image and the outputs to the outputs of the style and content layers. In other words, we created a model that will take an input image and output the content and style intermediate layers!

Define and create our loss functions (content and style distances)

Content Loss:
Our content loss definition is actually quite simple. We’ll pass the network both the desired content image and our base input
image. This will return the intermediate layer outputs (from the layers defined above) from our model. Then we simply take the
euclidean distance between the two intermediate representations of those images.

Style Loss:
Computing style loss is a bit more involved, but follows the same principle, this time feeding our network the base input image
and the style image. However, instead of comparing the raw intermediate outputs of the base input image and the style image, 
we instead compare the Gram matrices of the two outputs.


To generate a style for our base input image, we perform gradient descent from the content image to transform it into an image
that matches the style representation of the original image. We do so by minimizing the mean squared distance between the feature
correlation map of the style image and the input image. 

Run Gradient Descent

In this case, we use the Adam optimizer in order to minimize our loss. We iteratively update our output image such that it 
minimizes our loss: we don’t update the weights associated with our network, but instead we train our input image to minimize
loss. In order to do this, we must know how we calculate our loss and gradients. Note that the L-BFGS optimizer,
which if you are familiar with this algorithm is recommended, but isn’t used in this tutorial because a primary motivation 
behind this tutorial was to illustrate best practices with eager execution. By using Adam, we can demonstrate the 
autograd/gradient tape functionality with custom training loops.

Compute the loss and gradients
We’ll define a little helper function that will load our content and style image, feed them forward through our network, which will then output the content and style feature representations from our model.



Apply and run the style transfer process
And to actually perform the style transfer:


And that’s it!

Refer : https://medium.com/artists-and-machine-intelligence/neural-artistic-style-transfer-a-comprehensive-look-f54d8649c199
