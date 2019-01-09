# The Complete Javascript Course

## AJAX and APIS 

**What are AJAX and APIS ?**

  #### AJAX
   - Stands for Asynchronous Javascript and XML 
   - Allows us to communicate with Asynchronous Servers
   
   
  #### API
   - Stands for Application Programming Interface
   - On a very high level is basically a piece of software that can be use by another piece of software in order to allow applications to talk with each others.
   - An API is not a Server itself but a part of the Server, an application which receives a requests and sends back responses. 
   - There are 2 types of API's that you can use in Javascript: 
   
          1. Your own API, for data coming from your own server
          2. 3-rd Party API's: 
                - Google Maps
                - Embedded Youtube Videos
                - Weather Data
                - Movies Data
                - Send email or SMS


![Ajax](https://raw.githubusercontent.com/CoursesNotes/The-Complete-Javascript-Course/master/images/Ajax.png)




## USEFUL Commands 

##### 1. CONSOLE commands: 
    -  ls - shows the files contained in a Folder
    - mkdir 'folder Name' - to create a new Folder
    - rm - r - Delete a file(rm) or a folder and its containg files(rm -r)
    - clear - to clear the terminal console
    - mv - to move a file into another Folder
    - touch 'file name' - creates a new file
    - npm init - creates a package.json file( contains information about the Project for npm )
    - npm install webpack --save-dev - in order to install packages ( what --save-dev means is that it will save webpack as a development dependency of our Project). When used without -dev that package it will be saved as a dependency and not as a development dependency.
    - npm install - will install all the development dependency and non dependency as specified in your package.json file;
    - npm uninstall packageName --save - command used to uninstall a package;
   
   
#### 2. Create a basic Webpack Configuration: 

**What is Webpack?**
  - Most commonly used Asset Bundler which bundles not only javascript files but also all kind of assets like Images, Javascript, CSS;
  
  - Also webpack support 0 configuration file where you don't even need to write a configuration file. If you wanna do that all you need is to have one source folder in the root and then in there one index.js file; Webpack will created a distribution folder and put the bundled file in there. This option is just for really small Apps, for more complex Apps it is recommended to write your own Configuration;
  
  -  Also in Webpack we have production and development MODE property. 
     1. Development mode - simply build our bundle without minifying our code, in order to be as fast as possible but not compressed; 
     2. Production mode - enables all kind of optimization liek minification and tree shaking in order to reduce the bundle final size.
  
  -  To write your own webpack configuration file just go in your main src folder and add a file called webpack.config.js, which is just a regular js file in which your write your code for config: 
    
```javascript
    //write the Object in which you specify your settings, configurations: 
    // you need to export this Obj from this file via using node js syntax
    // Now to create this configuration we need to know that in webpack there are 4 core concepts: 
    //  - Entry Point
    //  - Output
    //  - Loaders 
    //  - Plugins

    const path = require('path'); //Includes a build in module 

    module.exports  = {
      // 1. Entry Property
      //Starting with the entry point all we need to do is to specify the Entry Property in this Object.
      // The Entry point is where the Webpack will start the Bundling, 
      //  so basically this is the file where it will start looking for all 
      //       the dependencies which it should then bundle together.
      //    Also here we can specify one or more entry files:
    entry: './src/js/index.js',

      // 2. Output Property
      // Tells webpack exactly where to save our bundle file. 
      // Basically in here we pass an object, in which we put a path and filename properties 
      //            which takes as values the path to the folder and file name.
      output: {
       // The Path needs to be an absolute Path
       // In order to have access to that Absolute Path, we need to use a build 
       //          in node package, the one included at line 63.
       // Now we call the method included in the path as default build, which is called resolve() 
       //  resolve() build in method, gives us access to __dirname variable
       //           - which stands for the current absolute path;
       //  so we use path.resolve(__dirname) to join the current 
       //            absolute path with the one that we want our bundle to be in: 
        path: path.resolve(__dirname, 'dist/js'),

        //standard name for webpack output
        filename: 'bundle.js'
      },

      mode: 'development'

    }; 


```

  





















