# Animator -- MVC architecture
# Introduction
This project follows the MVC architecture to complete the transformation from flat graphics to effective animations. It draws animations based on how the descriptions from text, independent of how the descriptions are generated. <br>
The main of EasyAnimator class read the input from Terminal to the controller, and output the corresponding files and views depending on the read parameters. <br>
The format of the input command such as:<br>
 -in "name-of-animation-file" -view "type-of-view" -out "where-output-show-go" -speed "integer-ticks-per-second"


# Model

Model represents an animated model, including shapes and actions. It is able to support 2D shapes that described rectangles and ovals. The model also supports adding various kinds of animations to shapes, such as moving, changing color, and changing shape.

#### Shape Interface & AbstractShape
The Interface of abstract class shape specifies some properties, such as type, size, color. 
AbstractShape consists of type of shape, position, width, height, and color. Also includes functions to set element values by given values.

#### Rectangle & Oval
Two AbstractShape implementation classes, representing Rectangle and Oval. Both derived classes have additional properties for representing shape types.
Rectangle declares fields of width height to express its size.
Oval declares fields of two radiuses to express its size.

#### Animation
The animation class has properties of animation starting time, position, color, and shape.

#### Model Interface
The interface contains all operations that all model should support. Models is able to support adding shapes and animations. It also has some getters to get information about this model.

#### ModelImpl
This is the implementation class of the model interface, getting shape and its animation of the graphics. 
Build shape through addShape(), to add shapes and given names to List<ShapeSet> shapes. The choice includes rectangle and oval. 
Build animation though choice of action()s to List<Animation> animations. The choice includes appearDisappear, moves, color, and scale. 
Build current state by adding new shape by the previous saved shape. 
Make toString() to format text output.
All shapes and animations are stored in a list at a given time tick. 
Create AnimationBuilderImpl implements AnimationBuilder. It constructs shape and animation by input file. 

### Other Classes and Enums
ActionType
An Enum of different actions, includes Move, Color, Scale, AppearDisappear.

#### Point2D
A Class to store and implement a 2D coordinate system.

#### ShapeSet
A Class to store name of shape and shape object.

#### ShapeType
An Enum of different shapes, includes Rectangle and Oval.



# View

View will draw and play the animation inside a window, effectively reproducing the sample animations shown in the images in the model section.

#### Iview Interface
Specifies the view types, including Text view, SVG view, and Visual view.

#### SVGView
The implementation class of SVGView in the Iview interface generates the SVG style code according to the string output from Textview. It collects parameters of color, X, Y, width, height, and type reformulating it into SVG format. They will be appended with the head and tail, to generate a complete SVG file. 

#### TextView
The implementation class of TextView in the Iview interface generates text string descriptions. It contains information about shape objects that generated by model at specific time range, includes shape-type, color, X, Y, width, and height.

#### JFramePanel
JFramePanel Class, drawing panels based on list of shapes to generates visual view.

#### JFrameView
JFrame initializes the drawing panel and draws shapes in the animation generated by the model.

#### ButtonJFrameView
ButtonJFrameView adds buttons and draws data from JFrameView. It will automatically draw animation when invoke it. Different button represents different functions, includes loop, start, pause, resume, restart, increase speed, and decrease speed. 
Controller

# Controller
Controller launch methods for controlling the display of different views (visual, text, and SVG views). Complete the control connection from user click button option to the corresponding view action feedback.


# Other Tool Package
#### AnimationBuilder Interface
Animate the model and set up the model.

#### AnimationReader
AnimationReader implements the methods in the AnimationBuilder interface, uses the AnimationBuilder instance of the incoming Animation type model, builds the animation model and sets the boundaries of the model.



# EasyAnimator
This main class represents switch of animation. It creates an Application run configuration in Eclipse/IntelliJ that chooses cs5004.animator.EasyAnimator as its main class. it will read in command line, and to decide which of views been called, pass input to model and view. 

Instruction of using EasyAnimator
Using IntelliJ → Run → Edit Configuration, enter the formatting of command line as:<br>
 -in "Enter file name" -view "view type" -out "output of file path" -speed "frames per second"
 
 Example：
 -in src/main/resources/testfiles/smalldemo.txt -view svg -out src/main/resources/svgs/out.svg -speed 20 <br>
 (Take src/main/resources/testfiles/smalldemo.txt with speed 20 output SVG file. The output of file path is located in src/main/resources/svgs/out.svg)
 
 -in src/main/resources/testfiles/smalldemo.txt -view visual <br>
 Display visual view of smalldemo.txt
 
 -in src/main/resources/testfiles/smalldemo.txt -view text <br>
 Text output of smalldemo.txt
 
 -in src/main/resources/testfiles/buildings.txt -view playback <br>
 Display playback with bottons, includes loop, start, resume, restart, increase-speed, decrease-speed
