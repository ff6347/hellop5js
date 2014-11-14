P5.js client/server side workshop
=================================

__Pre:__  
Processing is great. It can create so many things, is easy to use and crossplatform. But (there is always a but if somebody starts an introduction like this) getting sketches to the web is not that easy. Using the exported applets is not a good choice because the user will get an warning that there is Java running. Using Processing.js seemed always a bit buggy. Also it does not give you the full power of Javascript.  

P5.js enters the stage. Crowd goes wild.  
P5.js is what we needed. A framework using most of the Processing syntax and all of its spirit. You can use all what Javascript has to offer you (like Processing did with Java).  

If you want to keep reading about P5.js go [over here](http://p5js.org/).  

--------------------

##prerequisites  

You will need to get and install:  

- A server (I recommend [uberspace.de](https://uberspace.de/))  
- A text editor (I recommend [Sublime Text 3](http://www.sublimetext.com/3) or [Atom](https://atom.io/))  
- node.js (go get it. From the [binary download](http://nodejs.org/) or via [homebrew Mac](http://brew.sh/) `brew install node` or [Chocolatey Win](https://chocolatey.org/) `choco install nodejs.install`)
- install [bower](http://bower.io/) with node `npm install -g bower`
- install a simple [http server](https://github.com/nodeapps/http-server) with node `npm install -g http-server`
- and maybe [Grunt](http://gruntjs.com/) also with node `npm install -g grunt-cli`  
- A Terminal (Windows CMD or Mac Terminal.app)  

You need to learn some basics of the command line interface. We will do this step by step. If you want to speed up things a bit take a look at this great online book. [cli.learncodethehardway.org](http://cli.learncodethehardway.org/book/)  

##Client Side p5.js  

Open your Terminal and move to a good place like the Desktop.  

Mac:  

    cd ~/Desktop

Win:  

    cd c:\Users\(username)\Desktop  

Make a folder.  

    mkdir hellop5js  

Now cd into it.  

    cd hellop5js  

To setup your envoirment and install p5.js run:  

    bower init

and follow the instructions. It will look something like this:
    
    ? name: hellop5js
    ? version: 0.1.0
    ? description: somehing
    ? main file: index.html
    ? what types of modules does this package expose?:
    ? keywords:
    ? authors: fabiantheblind <icke@fabianmoronzirfas.me>
    ? license: MIT
    ? homepage:
    ? set currently installed components as dependencies?: Yes
    ? add commonly ignored files to ignore list?: Yes
    ? would you like to mark this package as private which prevents it from being accidentally published to the registry?: Yes
    
    {
      name: 'hellop5js',
      version: '0.1.0',
      authors: [
        'fabiantheblind <icke@fabianmoronzirfas.me>'
      ],
      description: 'somehing',
      main: 'index.html',
      license: 'MIT',
      private: true,
      ignore: [
        '**/.*',
        'node_modules',
        'bower_components',
        'test',
        'tests'
      ]
    }
    
    ? Looks good?: Yes

Then run:  

    bower install p5js --save
    bower install jquery --save

Great. We are nearly there. Now create a file with your favorite text editor with this content.  

    <!doctype html>
    <html lang="en">
    <head>
      <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
      <title>a title</title>
      <meta name="description" content="something">
      <meta name="author" content="me">
      <link rel="stylesheet" type="text/css" href="styles.css">
      <!--[if lt IE 9]>
      <script src="http://html5shiv.googlecode.com/svn/trunk/html5.js"></script>
      <![endif]-->
    </head>
    <body>
        <div id="thesketch"></div>
        <script type="text/javascript" src="bower_components/jquery/dist/jquery.min.js"></script>
        <script type="text/javascript" src="bower_components/p5js/lib/p5.min.js"></script>
        <script type="text/javascript" src="main.js"></script>
    </body>
    </html>

Now create another file called styles.css next to it. We leave it empty for now. Just for information. This is your CSS file. You can add in things like this.  

    body{
      background-color: #90308d;
    }

The most important thing comes now. Create your first p5.js sketch.  
Create a file called main.js next to the index.html and enter the following code into it.  

    function setup(){
      var the_canvas = createCanvas(640, 360);
      the_canvas.parent('thesketch');
    }
    
    function draw(){
    // draw some simple shapes
    // hint! The order in which you draw is important
    // change x and y to move him around
    var x = width/2;
    var y = 25;
    var w = 23; // make him bigger or smaller
    var h = w; // distort by changing the h seperatly
    var bmi = 1; // body mass index
    // a line takes 4 values the starting point and the end point
    line(x - w, y + h, x +w, y+h);
    // a ellipse always takes 4 values as parameter
    ellipse(x, y, w, h);
    // a point just two
    point(x, y); // look he has a nose
    // a rectangle also takes 4 values like the ellipse
    // but draws from its upper left corner
    rect(x-bmi/2, y + h, bmi, h);
    // you can also draw free forms by using vertecies
    noFill();
    beginShape();
    vertex(x - w, y + h*3);
    vertex(x - w, y + h*2);
    vertex(x + w, y + h*2);
    vertex(x + w, y + h*3);
    endShape();
    }

Now go back to your terminal and enter

    http-server

and point your browser to this link [http://0.0.0.0:8080/](http://0.0.0.0:8080/).  
To stop the server just hit "CTRL + C".  
Awesome. You just created your first p5.js sketch with a basic setup for client side Javascript programming. If you want to make this available on the web there are several ways. I recommend these two.  

- Use github  
- Use your own uberspace.de server  


###Github:  

create a new repository on github called "hellop5js". Leave it empty. Don't create a .gitignore nor a README.md we will do this by ourselves.  
It should look something like this.  

![](images/new-repo.png)  

Copy the clone url "git@github.com:fabiantheblind/hellop5js.git" to the clipboard

go to your terminal and stop the server if it is still running.  
Now we are going to to do several things:  

- create a local git repo
- create a .gitignore
- create a README.md
- add the remote address
- move the js libraries we need to the root  
- add all out files to the version control
- create a branch for our github page  
- push to the server (master and gh-pages branch)  

Just follow these instructions step by step. (Not yet tested on windows)  
_Note: Most of the commands should work the same on windows and mac. To use git from the CMD see this [stackoverflow](http://stackoverflow.com/questions/11000869/command-line-git-on-windows) question_  

Enter into the Terminal:  

    git init  
    echo "node_modules" >> .gitignore
    echo "bower_components" >> .gitignore  
    echo "Hello p5.js" >> README.md
    git remote add origin git@github.com:fabiantheblind/hellop5js.git
    cp bower_components/jquery/dist/jquery.min.js jquery.min.js
    cp bower_components/p5js/lib/p5.min.js p5.min.js
    git add -A :/
    git commit -a -m "inital local commit"
    git branch gh-pages
    git push origin master
    git push origin gh-pages

