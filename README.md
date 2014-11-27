###KidKinect
>Realtime interaction with physics simulations in a child's play-space
________________________

####TODO:
- [] verify Kinect using Silhouette example
- [] Install SimpleOpenNI on chaote laptop
- [] refactor all three code examples (and figure out how they work)
- [] update and experiment


_________________________

####DEBUG:
- [Vertices of Chanin are too close](http://forum.processing.org/two/discussion/3705/vertices-of-chain-shape-are-too-close-together-help/p1)



_________________________

####Features:
- silouette as polygon
- polygon silouette defines flow field mask
- polygon silouette edges detection
- real-time interaction with 2D geometry 

####Future Features:
- replace background with video feed
	- place the incoming image at the beginning of draw instead of background()
- replace the silouette with video feed:
	- use masking
	- use GL Graphics library, GLSL shaders to maintain good framerate
	- see example:
		- GLGraphics > Textures > Dynamic Mask

___________________________


Dependencies:  
=============  
- Processing 2.0b3 or 1.5.1 (examples tested & working with both)  
- SimpleOpenNI: A simple OpenNI wrapper for processing  
- v3ga blob detection library  
- Toxiclibs 020 (examples tested & working with 021 as well)  
- PBox2D: A simple JBox2D wrapper library  


________________________



EXAMPLES
=========
1. Kinect_Silhouette
	- verify the Kinect installation
	- create a silhouette from user depth image

2. Kinect_Flow (libs: SimpleOpenNI, v3ga)
	- turn a silhouette into a polygon
	- From Ammon Owed notes in the Kinect Physics Tutorial:  
>This second example takes things a little further. To turn a colored silhouette into a polygon, we need to first find it’s outer contour points and second find the correct order in which they form a polygon. To find the contour points of shapes, we can use blob detection. I’ve looked at several blob detection libraries and found v3ga to work quite well. First, it’s fast, which is important because you want things to run in real-time. Second, it returns an array of ordered points. While not polygon-worthy yet, it’s an important step towards a correctly formed polygon. I’ve compressed all the relevant code into the createPolygon() method of the PolygonBlob class. I’ve found the code to work quite well in turning a blob into points into a correct polygon. But of course, there may be room for improvement. Note that both the second and third example have been written for one person in front of a Kinect, but quick tests show that the code holds up reasonably well (although not perfect) for multiple persons.  
> There are many things you could do (besides 2d physics, we’ll get to that in a minute) once you have turned yourself into a quality polygon. I added a few experiments of mine at the end of the video. Some of the things you see there are triangulating the shape, voronoi-ifying the screen and using myself as a mask between two full HD videos (the originals can be found on my vimeo account). These preliminary experiments are just the tiny tip of the iceberg. There are so many things you could do. Which makes it all the more important that you think about what you want to create and which visual style you are after. In this code example the polygon shape is used to control the boundaries of a noise-based flow of particles. The code is simplified as much as possible and fully commented, so feel free to run and read the code to see what it does exactly. You will need the main sketch and the two classes.  

3. Kinect_Physics (libs: SimpleOpenNI, v3ga, Toxiclibs, PBox2D)
	- Realtime interaction with onscreen geometry  
	- What this code does in words: 
		- create a silhouette from a person, 
		- turn this silhouette into points, 
		- turn these points into a polygon, 
		- turn this polygon into a deflective shape in the box2d physics world.
	- From Ammon Owed notes in the Kinect Physics Tutorial:   
>All right, now for the pièce de résistance of this tutorial. Realtime interaction with onscreen geometry. To do this we will be using Daniel Shiffman’s PBox2D library, which is a Processing wrapper library for the Jbox2D library, which is a port of the C++ Box2D library. Gotta love open source! ;-) This code example builds on the work done in the previous example. The createPolygon() method is nearly identical. The PolygonBlob class is now extending Toxiclibs’ Polygon2D class. The main difference is that code has been added to create and destroy box2d bodies (which will allow 2D physics).  
>What this code does in words: create a silhouette from a person, turn this silhouette into points, turn these points into a polygon, turn this polygon into a deflective shape in the box2d physics world. Because all the other geometry is transferred into the same physics world, interaction between person and onscreen geometry becomes possible. Of course there are some challenges, in addition to the mentioned steps. For example, while the original virtual geometry is pretty solid, the person’s contours are ever changing, especially when the person is moving around a lot. This will result in errors in the collision detection (aka geometry will end up inside a person). That is also one of the reasons to use Toxiclibs, because it has methods that help us check if a point is inside a polygon and if so, to find the closest point on the outer contours and move the geometry to that point. It’s a bit of a quick workaround, but it works quite well. When moving slowly or not at all, this workaround isn’t used anyway, since the regular collision detection will be effective under those conditions. However if a person is moving around quickly and you don’t want geometry inside the person nor delete it, then this shortcut is useful. Although at times it may cause some non-physically correct overlapping of shapes near the contours. All in all, you can see in the video that using this combination of techniques allows you to interact with the falling shapes on your screen. Again, to run the code you will need the main sketch and the two classes.





__________________________

Sources:
=========
- [Kinect Physics Tutorials for Processing](http://www.creativeapplications.net/processing/kinect-physics-tutorial-for-processing/) - by Ammon Owed
- [SimpleOpenNI](https://code.google.com/p/simple-openni/wiki/Installation) - OpenNI library for Processing
- [Geometry, Textures & Shaders with Processing - Tutorial](http://www.creativeapplications.net/processing/geometry-textures-shaders-processing-tutorial/)
- [Code Updates for SimpleOpenNI-1.96 Kinect 2](http://forum.processing.org/two/discussion/2625/can-kinect-physics-code-examples/p1)
- [SimpleOpenNI Changes](http://forum.processing.org/two/discussion/1481/changes-to-the-latest-version-of-simple-openni/p1)
