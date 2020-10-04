# Face-recognition-with-python

Project description
Face Recognition
Recognize and manipulate faces from Python or from the command line with
the world’s simplest face recognition library.
Built using dlib’s state-of-the-art face recognition
built with deep learning. The model has an accuracy of 99.38% on the
Labeled Faces in the Wild benchmark.
This also provides a simple face_recognition command line tool that lets
you do face recognition on a folder of images from the command line!
PyPI
Build Status
Documentation Status
Features
Find faces in pictures
Find all the faces that appear in a picture:

image3

import face_recognition
image = face_recognition.load_image_file("your_file.jpg")
face_locations = face_recognition.face_locations(image)
Find and manipulate facial features in pictures
Get the locations and outlines of each person’s eyes, nose, mouth and chin.

image4

import face_recognition
image = face_recognition.load_image_file("your_file.jpg")
face_landmarks_list = face_recognition.face_landmarks(image)
Finding facial features is super useful for lots of important stuff. But you can also use for really stupid stuff
like applying digital make-up (think ‘Meitu’):
image5

Identify faces in pictures
Recognize who appears in each photo.

image6

import face_recognition
known_image = face_recognition.load_image_file("biden.jpg")
unknown_image = face_recognition.load_image_file("unknown.jpg")

biden_encoding = face_recognition.face_encodings(known_image)[0]
unknown_encoding = face_recognition.face_encodings(unknown_image)[0]

results = face_recognition.compare_faces([biden_encoding], unknown_encoding)
You can even use this library with other Python libraries to do real-time face recognition:

image7

See this example for the code.

Installation
Requirements
Python 3.3+ or Python 2.7
macOS or Linux (Windows not officially supported, but might work)
Installing on Mac or Linux
First, make sure you have dlib already installed with Python bindings:

How to install dlib from source on macOS or Ubuntu
Then, install this module from pypi using pip3 (or pip2 for Python 2):

pip3 install face_recognition
If you are having trouble with installation, you can also try out a
pre-configured VM.
Installing on Raspberry Pi 2+
Raspberry Pi 2+ installation instructions
Installing on Windows
While Windows isn’t officially supported, helpful users have posted instructions on how to install this library:

@masoudr’s Windows 10 installation guide (dlib + face_recognition)
Installing a pre-configured Virtual Machine image
Download the pre-configured VM image (for VMware Player or VirtualBox).
Usage
Command-Line Interface
When you install face_recognition, you get a simple command-line program
called face_recognition that you can use to recognize faces in a
photograph or folder full for photographs.
First, you need to provide a folder with one picture of each person you
already know. There should be one image file for each person with the
files named according to who is in the picture:
known

Next, you need a second folder with the files you want to identify:

unknown

Then in you simply run the command face_recognition, passing in
the folder of known people and the folder (or single image) with unknown
people and it tells you who is in each image:
$ face_recognition ./pictures_of_people_i_know/ ./unknown_pictures/

/unknown_pictures/unknown.jpg,Barack Obama
/face_recognition_test/unknown_pictures/unknown.jpg,unknown_person
There’s one line in the output for each face. The data is comma-separated
with the filename and the name of the person found.
An unknown_person is a face in the image that didn’t match anyone in
your folder of known people.
ADJUSTING TOLERANCE / SENSITIVITY
If you are getting multiple matches for the same person, it might be that
the people in your photos look very similar and a lower tolerance value
is needed to make face comparisons more strict.
You can do that with the --tolerance parameter. The default tolerance
value is 0.6 and lower numbers make face comparisons more strict:
$ face_recognition --tolerance 0.54 ./pictures_of_people_i_know/ ./unknown_pictures/

/unknown_pictures/unknown.jpg,Barack Obama
/face_recognition_test/unknown_pictures/unknown.jpg,unknown_person
If you want to see the face distance calculated for each match in order
to adjust the tolerance setting, you can use --show-distance true:
$ face_recognition --show-distance true ./pictures_of_people_i_know/ ./unknown_pictures/

/unknown_pictures/unknown.jpg,Barack Obama,0.378542298956785
/face_recognition_test/unknown_pictures/unknown.jpg,unknown_person,None
