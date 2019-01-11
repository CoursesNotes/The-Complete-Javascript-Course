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
    - npm install webpack --save-dev - in order to install packages ( what --save-dev means is that it 
         will save webpack as a development dependency of our Project). When used without -dev that package
         it will be saved as a dependency and not as a development dependency.
    - npm install - will install all the development dependency and 
                    non dependency as specified in your package.json file;
    - npm uninstall packageName --save - command used to uninstall a package;
    - npm run SCRIIPT-NAME - command used to run an npm script
   
##### 2. VC(Visual Code) EMMET Commands: 
    -  ! + tab - Write exclamation point + hit the tab, writes a pre-formatted HTML skeleton. 
 
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

-  In order to test out our webpack file config, we need to create a new Javascript file, create a test.js file and export( use the official ES6 **export default** syntax) a piece of code and then go ahead in your javascript entry file and import the newly created module, see example below: 

```javascript
    //creating a new js file - test.js and adding some code
    console.log(`This file is being imported!`)
    
    //using the ES6 syntax for exporting:
    export default 22; 


    // going back in my entry point file - index.js, I am importing the newly created module: 
    // Attention:  When we import from a module we don't even need to specify the file extension.
    //             What is exported from the module is stored in the variable number
    import number from './test'; 
    
    //Keep in mind that this code it won't even work in the browser if we didn't use webpack(or any other bundler), 
    //        since the webpack does the bundling and joining files job;
    console.log( ` I imported ${number} from another module`); 
    
    //
```
 -  Install webpack command line interface usinng the command line: **npm install webpack-cli**
 -  Next step is to go to package.json and add an npm script, i called it npm to call the webpack and run the newly created npm script(npm run dev), like in the example below: 
 
  ```javascript
        {
          "name": "forkify",
          "version": "1.0.0",
          "description": "Forkify Project",
          "main": "index.js",
          "scripts": {
            //npm script calls the webpack
            //as soon as we start the npm script called dev it will then open up the webpack,
            //  look up at our file confing and then do the work that we specified there.
            // It will read our entry file, do it's work ahd output it in bundle.js as we specified in the config.
            // Why do we have to use an npm script for this? - Well because this the the best way
            //      to lunch our locally installed dev dependency. 
            //We can also set the Webpack mode here -  this one is for development 
            "dev": "webpack --mode development",
            
            // npm script which runs webpack with the mode setted to production
            "build": "webpack --mode production"
          },
          "author": "Cosmina Palade",
          "license": "ISC",
          "devDependencies": {
            //here we only have webpack but we also need webpack command line interface
            "webpack": "^4.28.3",
            "webpack-cli": "^4.28.3"
          }
        }

    Command Line: npm run dev 
  ```

For optimization we can use webpack dev server to our setup in ordert to automatically reload the page when we save our code. So besides all the amazing functionalities included in webpack it also provides us with a development server, which automatically bundles all our javascript files and then reloads the App in the Browser. Since is an npm package we have to install it via the following command line: **npm install webpack-dev-server --save-dev** as shown below: 

```javascript
      {
        "name": "forkify",
        "version": "1.0.0",
        "description": "Forkify Project",
        "main": "index.js",
        "scripts": {
          "dev": "webpack --mode development",
          "build": "webpack --mode production"
        },
        "author": "Cosmina Palade",
        "license": "ISC",
        "devDependencies": {
          "webpack": "^4.28.3",
          "webpack-dev-server": "^3.1.14"
        },
        "dependencies": {
          "webpack-cli": "^3.2.1"
        }
      }


```

 Now we have to Configure our dev server and for this we have to go back to webpack.config.js file and add another property named "devServer" in which we pass an Obj literal with a set of properties to spcify the configuration as shown in the example below:
 
 ```javascript
 
      const path = require('path');

      module.exports = {
          entry: './src/js/index.js',
          output: {
              path: path.resolve(__dirname, 'dist/js'),
              filename: 'bundle.js'
          },
          devServer: {
              //here we specify the folder from which webpack should serve the files:
              contentBase: './dist'
          }

      }
 
 
 ```

 - Next step is to create a npm script usually called start - which will always be a script which keeps running in the background and updates the browser as soon as we change our code. 
  
```javascript
    {
      "name": "forkify",
      "version": "1.0.0",
      "description": "Forkify Project",
      "main": "index.js",
      "scripts": {
        "dev": "webpack --mode development",
        "build": "webpack --mode production",
        // by specifying open what it actually does it opens the page in the Browser
        "start": "webpack-dev-server --mode development --open"
      },
      "author": "Cosmina Palade",
      "license": "ISC",
      "devDependencies": {
        "webpack": "^4.28.3",
        "webpack-dev-server": "^3.1.14"
      },
      "dependencies": {
        "webpack-cli": "^3.2.1"
      }
    }

```
 - Next step is to optimise our configurations even better byu adding Plugins, because rememeber in Webpack we have 4 major configurations which we can set - Entry Points, Outputs and Plugins. 
 
 **What are Plugins?**  -  Allow us to do complex processing of our input files, in this case index.html, for this we have to use a plug-in called HTML Webpack Plugin and in order to use it you need to install it. The Command line for it is: 

>  npm install html-webpack-plugin --save-dev

Just like before we have to require this package and save it in a variable: 

```javascript
    {
      "name": "forkify",
      "version": "1.0.0",
      "description": "Forkify Project",
      "main": "index.js",
      "scripts": {
        "dev": "webpack --mode development",
        "build": "webpack --mode production",
        "start": "webpack-dev-server --mode development --open"
      },
      "author": "Cosmina Palade",
      "license": "ISC",
      "devDependencies": {
        "html-webpack-plugin": "^3.2.0",
        "webpack": "^4.28.3",
        "webpack-dev-server": "^3.1.14"
      },
      "dependencies": {
        "webpack-cli": "^3.2.1"
      }
    }

```

 - FINAL STEP - is to Integrate Babel into our workflow, to complete the setup. 
 
**What is BABEL?** - Babel is a Javascript Compiler making possible the use of next generation Javascript. 

Setting Up Babel: 
  In order to make Babel work you need to: 
> (1) Dowload Babel packages; 
> (2) Add the settings for Babel in webpack.confi file;
> (3) Create a Babel config file.

> STEP **(1) Dowload Babel packages**: 
   > _npm install babel-core_ - which contains the core functionalities of the compiler; 
   > _npm install babel-preset-env_ - Babel preset which takes care that all the modern JavaScript features are converted back to ES5;
   > _npm install babel-loader_ - Needed for Webpack to actually load Babel files; 
 
 
 > NOTE:
 > _You can install many packages in the same command_
 
 ```javascript
    
    //installing multiple packages with the same commanand line:
    npm install babel-core babel-preset-env babel-loader --save-dev

```
> STEP **(2) Add the settings for Babel in webpack.confi file**: 

**What does the Loaders in Webpack do?** 
   - Allows us to import or load all kind of different files and more importantly to process them(like converting SASS to CSS Code or convert ES6 to ES5 Javascript);

**What do we have to write in the webpack.config file in order to enable the Babel compiler?** 
   - We enable it by using the module.exports module property and asign it an Object in which we pass the property rules. The rules property receives and array with all the loaders that we want to use - see example below: 
      
 ```javascript
 
  //in webpack.config.js add the following properties:
  
 module.exports = {
    entry: './src/js/index.js',
    output: {
        path: path.resolve(__dirname, 'dist'),
        filename: 'js/bundle.js'
    },
    devServer: {
        //here we specify the folder from which webpack should serve the files:
        contentBase: './dist'
    },
    module: {
        rules: [
            {
                //Regular expression testing for all the Javascript files
                //  The test is looking for all the files and check if they end in js
                test: /\.js$/,
                //excludes anything that is a node modules folder
                // if wqe wouldn't do that, than Babel would apply to all of the thousands Javascript files inside node
                exclude: /node_modules/,
                use: {
                    loader: 'babel-loader'
                }
            }
        ]
    }

```
 
 > STEP **(3) Create a Babel config file**: 
 
Just create a new file with the name **.babelrc** which will be automatically recognized by the IDE as babel 6 file. 
In here all we pass is just an Object. The **.babelrc** file is just a dot file and not a javascript file. 
Here is the full setup:
 
 
```javascript
    {
        // preset is a collection of code transform plug-ins,
        // they are piece of code which apply transformation to our code
        "preset": [
            //stands for environment which is the Browser
            // corresponds to babel-preset-env
            "env", {
                "target": {
                    "browsers": [
                        //Babel automatically figures out which ES6 features
                        // needs to convert in order to work on 
                        // the last five verions of all the browsers 
                        "last 5 versions",
                        "ie >= 8"
                    ]
                }
            }
        ]
    }


```
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 <!-- 


```javascript

```

-->

 
 













