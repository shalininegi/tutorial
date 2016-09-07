#Package Management and using grunt with Quindar Angular

First off, you should familiarize yourself with the tools we are using. You’ll find documentation on each tool with its link below:

npm (https://www.npmjs.com/)

grunt(http://gruntjs.com/)

Grunt is a code that compresses code from several files into one file, and edits the html to call that one file, saving the computer substantial processing time. This tutorial will walk through an example using quindar-angular that uses grunt to handle its third party dependencies.


##Step Involved

The purpose of this tutorial is to combine all the local file into one file as a destination.

Install all the dependencies by running the following command

```
./buildme.sh
```
This will install all the dependencies mentioned in your package.json file.

Alternatively, you can install the required dependencies by type the following

```
npm install
```

In addition to this, we also need to install grunt globally such as:

```

$ npm install grunt --save
$ npm install grunt grunt-contrib-concat -save

```

After manually adding all dependencies, your package should look will this:

```javascript

{
  "name": "tutorial8a",
  "version": "0.0.1",
  "devDependencies": {
    "async": "^2.0.1",
    "body-parser": "^1.15.2",
    "express": "^4.14.0",
    "fs": "0.0.2",
    "grunt": "^1.0.1",
    "grunt-contrib-concat": "^1.0.1",
    "http": "0.0.0",
    "nodemon": "^1.10.0",
    "path": "^0.12.7",
    "request": "^2.74.0"
  },
  "dependencies": {
    "grunt": "^1.0.1",
    "grunt-contrib-concat": "^1.0.1"
  }
}

```

###Url Concat

Grunt is especially helpful to us because of the contributed task, concat, which combines files both by request and automatically by suffix.


Place the following code into the grunt file.

```javascript

module.exports = function(grunt) {

  grunt.initConfig({
           urlconcat: {
                      all: {
                          src: [
                              'app/styles/styles.css',
                              'app/styles/colors.css',
                              'app/styles/core.css',
                              'app/styles/components.css',
                              'app/styles/angular-gridster.min.css',
                              'app/styles/gridsterDashboard.css',
                              'app/styles/quindarWidgets.css',
                              'app/styles/widgets.css',
                              'app/styles/icons/fontawesome/styles.min.css',
                              'app/styles/icons/icomoon/styles.css'
                          ],
                          dest: 'localFile/scripts/local.css'
                      }
                  }
      });

```

The initConfig does exactly what its name suggests: configures the initial grunt states. Within concat, the src section is a list of source files from which to draw code and dest section is the destination of the new concatenated code.



The best part is that we can concat every file with the same suffix with *.suffix (every css with *.css, etc.) as is demonstrated in the above code.


Now run it in terminal

```

$ grunt urlconcat

```
This command will concat all the source file from app/styles into destination file which is finally placed under localFile/scripts/local.css. So, now all your local source file is placed under localFile/scripts/local.css.


