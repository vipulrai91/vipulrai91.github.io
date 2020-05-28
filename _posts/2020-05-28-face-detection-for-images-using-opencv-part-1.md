---
layout: post
cover-img: assets/img/path.jpg
tags:
  - deep learning
  - object detection
  - Tensorflow
  - Keras
comments: true
---

# This is part one of this series where we will finally build a face mask detector at the end of the series.

## For this tutorial we are going to use OpenCV and prebuilt model shipped with it.

Face Detection is subset of object detection. It is not similar to object classification.

The major difference as mentioned here at [stackoverflow.com](https://stackoverflow.com/questions/31750076/what-is-the-difference-between-object-detection-and-object-classification) answer.

**Object classification** - Given an image, classify this image to some class like Apple, bus, forest etc.<br>
**Object detection** - Given an image, find out if there exist a patch(or coordinates) where the class exists? eg - Given an image predict whether classes(like oranges, truck, lion) exist in image or not.

Since this is an object detection problem,here we need to find the co-ordinates where the face exists in the given image.

To start with head to [Github](https://github.com/vipulrai91/mask-detection/tree/master/app/face_detector/model), to download a pre trained caffe model (we would train model from scratch in future parts) and prototxt file (Clone the whole repository to get the complete code)

Make sure you run this command from home dir

```console
pip install -r requirements.txt
```

This will install all required packages into your local system.

A better practice would be to always have separate environments for different usages (Can be accomplished by using [Anaconda](https://www.anaconda.com/products/individual))

Now having the setup ready we are good to dive into the code.

Since we will be using console to run this and initialize various objects we would be ArgumentParser The code for which is below

<script src="https://gist.github.com/vipulrai91/2408462b5bb2ab234d7632879d85b59a.js">
</script>

Now, let's load the model in memory and read the images and convert it to OpenCV readable format

<script src="https://gist.github.com/vipulrai91/c68e20ffe1d55d91b0d283f1f8524f16.js">
</script>

Our initial Image looks like this.

![input image](/assets/img/face_detect/family.jpg)

Credit: Image by [1138694](https://pixabay.com/users/1138694-1138694/?utm_source=link-attribution&utm_medium=referral&utm_campaign=image&utm_content=1016311) from [Pixabay](https://pixabay.com/?utm_source=link-attribution&utm_medium=referral&utm_campaign=image&utm_content=1016311)

<script src="https://gist.github.com/vipulrai91/2afbfd6ce818a2ee001943ba39bbd14a.js">
</script>

Now we iterate over the detections to extract the confidence (how much percentage the model is confident about predictions) , filtering out weaker confidence , by default it is 0.5 (50%) but this is adjustable.

Finally the output would be the same image with faces marked in boundaries.

![output image](/assets/img/face_detect/out_face.jpg)

This was out of box implementation using pre-trained model provided by OpenCV

In the future posts we would be training model from scratch.

References :<br>
[stackoverflow.com](https://stackoverflow.com/questions/31750076/what-is-the-difference-between-object-detection-and-object-classification)<br>
[pyimagesearch.com](https://www.pyimagesearch.com)
