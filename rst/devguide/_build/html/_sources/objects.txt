=======
Objects
=======

Objects are the basic storage entities in Cloud Files. They represent
the files and their optional metadata that you upload to the system.
When you upload objects to Cloud Files, the data is stored as-is
(without compression or encryption) and consists of a location
(container), the object's name, and any metadata that you assign,
consisting of key/value pairs. For example, you can choose to store a
backup of your digital photos and organize them into albums. In this
case, each object could be tagged with metadata such as
``Album : Caribbean Cruise`` or ``Album : Aspen Ski Trip``.

The only restriction on object names is that they must be less than 1024
bytes in length after URL-encoding. For example, an object name of
``C++final(v2).txt`` would be URL-encoded as
``C%2B%2Bfinal%28v2%29.txt`` and therefore is 24 bytes in length rather
than the expected 16.

Cloud Files limits the size of a single uploaded object. By default this
limit is 5 GB. However, the download size of a single object is
virtually unlimited with the use of segmentation. Segments of the larger
object are uploaded and a special manifest file is created that, when
downloaded, sends all the segments concatenated as a single object.
Segmentation also offers much greater upload speed with the possibility
of parallel uploads of the segments.

For metadata, do not exceed 90 individual key/value pairs for any one
object and do not exceed 4 KB (4096 bytes) for the total byte length of
all key/value pairs.

