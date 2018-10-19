# OpenCv_Image_Detection


Introduction
What is face recognition? Or what is recognition? When you look at an apple fruit, your mind immediately tells you that this is an apple fruit. This process, your mind telling you that this is an apple fruit is recognition in simple words. So what is face recognition then? I am sure you have guessed it right. When you look at your friend walking down the street or a picture of him, you recognize that he is your friend Paulo. Interestingly when you look at your friend or a picture of him you look at his face first before looking at anything else. Ever wondered why you do that? This is so that you can recognize him by looking at his face. Well, this is you doing face recognition.

But the real question is how does face recognition works? It is quite simple and intuitive. Take a real life example, when you meet someone first time in your life you don't recognize him, right? While he talks or shakes hands with you, you look at his face, eyes, nose, mouth, color and overall look. This is your mind learning or training for the face recognition of that person by gathering face data. Then he tells you that his name is Paulo. At this point your mind knows that the face data it just learned belongs to Paulo. Now your mind is trained and ready to do face recognition on Paulo's face. Next time when you will see Paulo or his face in a picture you will immediately recognize him. This is how face recognition work. The more you will meet Paulo, the more data your mind will collect about Paulo and especially his face and the better you will become at recognizing him.

Now the next question is how to code face recognition with OpenCV, after all this is the only reason why you are reading this article, right? OK then. You might say that our mind can do these things easily but to actually code them into a computer is difficult? Don't worry, it is not. Thanks to OpenCV, coding face recognition is as easier as it feels. The coding steps for face recognition are same as we discussed it in real life example above.

Training Data Gathering: Gather face data (face images in this case) of the persons you want to recognize
Training of Recognizer: Feed that face data (and respective names of each face) to the face recognizer so that it can learn.
Recognition: Feed new faces of the persons and see if the face recognizer you just trained recognizes them.
OpenCV comes equipped with built in face recognizer, all you have to do is feed it the face data. It's that simple and this how it will look once we are done coding it.

visualization

OpenCV Face Recognizers
OpenCV has three built in face recognizers and thanks to OpenCV's clean coding, you can use any of them by just changing a single line of code. Below are the names of those face recognizers and their OpenCV calls.

EigenFaces Face Recognizer Recognizer - cv2.face.createEigenFaceRecognizer()
FisherFaces Face Recognizer Recognizer - cv2.face.createFisherFaceRecognizer()
Local Binary Patterns Histograms (LBPH) Face Recognizer - cv2.face.createLBPHFaceRecognizer()
We have got three face recognizers but do you know which one to use and when? Or which one is better? I guess not. So why not go through a brief summary of each, what you say? I am assuming you said yes :) So let's dive into the theory of each.

EigenFaces Face Recognizer
This algorithm considers the fact that not all parts of a face are equally important and equally useful. When you look at some one you recognize him/her by his distinct features like eyes, nose, cheeks, forehead and how they vary with respect to each other. So you are actually focusing on the areas of maximum change (mathematically speaking, this change is variance) of the face. For example, from eyes to nose there is a significant change and same is the case from nose to mouth. When you look at multiple faces you compare them by looking at these parts of the faces because these parts are the most useful and important components of a face. Important because they catch the maximum change among faces, change the helps you differentiate one face from the other. This is exactly how EigenFaces face recognizer works.

EigenFaces face recognizer looks at all the training images of all the persons as a whole and try to extract the components which are important and useful (the components that catch the maximum variance/change) and discards the rest of the components. This way it not only extracts the important components from the training data but also saves memory by discarding the less important components. These important components it extracts are called principal components. Below is an image showing the principal components extracted from a list of faces.

Principal Components eigenfaces_opencv source

You can see that principal components actually represent faces and these faces are called eigen faces and hence the name of the algorithm.

So this is how EigenFaces face recognizer trains itself (by extracting principal components). Remember, it also keeps a record of which principal component belongs to which person. One thing to note in above image is that Eigenfaces algorithm also considers illumination as an important component.

Later during recognition, when you feed a new image to the algorithm, it repeats the same process on that image as well. It extracts the principal component from that new image and compares that component with the list of components it stored during training and finds the component with the best match and returns the person label associated with that best match component.

Easy peasy, right? Next one is easier than this one.

FisherFaces Face Recognizer
This algorithm is an improved version of EigenFaces face recognizer. Eigenfaces face recognizer looks at all the training faces of all the persons at once and finds principal components from all of them combined. By capturing principal components from all the of them combined you are not focusing on the features that discriminate one person from the other but the features that represent all the persons in the training data as a whole.

This approach has drawbacks, for example, images with sharp changes (like light changes which is not a useful feature at all) may dominate the rest of the images and you may end up with features that are from external source like light and are not useful for discrimination at all. In the end, your principal components will represent light changes and not the actual face features.

Fisherfaces algorithm, instead of extracting useful features that represent all the faces of all the persons, it extracts useful features that discriminate one person from the others. This way features of one person do not dominate over the others and you have the features that discriminate one person from the others.

Below is an image of features extracted using Fisherfaces algorithm.

Fisher Faces eigenfaces_opencv source
