=============
iOS streaming
=============

The Cloud Files CDN allows you to stream video to iOS devices without
needing to convert your video. After you CDN-enable your container, you
have the tools necessary for streaming media to multiple devices. To
leverage this ability, you must check the client's user agent with
JavaScript. An example of the user agent check and how to use it
follows.

#. CDN-enable your container. Two streaming URIs are
   created: the container's streaming URI (``X-Cdn-Streaming-Uri``) and
   its iOS streaming URI (``X-Cdn-Ios-Uri``).

#. Perform a **HEAD** request against the CDN-enabled container to view
   these URIs.

#. Link to your content in a HTML page by using a ``<video>`` element.

#. Set the SRC attribute of the ``<video>`` element to the full
   streaming URI for your container plus the name of your content. In
   the following example, the streaming video is MobyDick.mp4.

   **Example: HTML 5 video element**

   .. code::

       <video width=”640” height=”480” id="videotag">
         <source src=”http://084cc2790632ccee0a12-346eb45fd42c58ca13011d659bfc1ac1.
         r49.stream.cf0.rackcdn.com/MobyDick.mp4” />
       </video>

#. Add JavaScript to the ``<head>`` element of your HTML page to check
   if the user agent is an iOS device. If it is, the JavaScript should
   use the container's iOS streaming URI (``X-Cdn-Ios-Uri``) instead of
   the regular streaming URI. The Cloud Files CDN delivers the properly
   formatted content for iOS devices only when the iOS streaming URI is
   used. In the following example, the JavaScript sets the ``<src>``
   attribute of the ``<video>`` element ``videotag`` to the iOS
   Streaming URI. Remember to add your content's name to the end of the
   iOS streaming URI.

   **Example: JavaScript for user agent check**

   .. code::

       <script type=”text/javascript”>

           function isIOS(){
               return ((navigator.userAgent.match(/iPhone/i)) ||(navigator.userAgent.match(/iPod/i)) || (navigator.userAgent.match(/iPad/
       i))) != null;
           }

           function init(){
               if (isIOS()){
                  document.getElementById(“videotag”).src = “http://084cc2790632ccee0a12-346eb45fd42c58ca13011d659bfc1ac1.
                  iosr.cf0.rackcdn.com/MobyDick.mp4”;
               }
           }

       </script>

#. Add ``init()`` to the ``<body>`` element of your HTML page to call
   the user agent check when the page loads, as shown in the following
   example.

   **Example: Load JavaScript in HTML page**

   .. code::

       <body onload=”init()”>

With these pieces of code in place, the proper content streams are set
for iOS devices.

