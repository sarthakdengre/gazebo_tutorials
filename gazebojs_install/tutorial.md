# Overview

GazeboJs provides a scripting interface to the Gazebo simulator. Specifically, it provides a javascript client for the simulator, using NodeJs and built on Google's V8 script engine.

GazeboJs is a C++ addon to NodeJs that is loaded inside node process at runtime (using the `require` javascript function). Once loaded, it provides javascript functions that communicate with the Gazebo simultation server (the gzserver process) over the network, using the Gazebo transport library.
This is the same mechanism that the Gazebo simulation client (the gzclient process) uses to communicate with the simulation server.
The source code for this project can be found here: <https://bitbucket.org/osrf/gazebojs>

[[file:files/gazebojs_overview.png|640px]]

This page explains how to install the GazeboJs Node bindings to Gazebo.




### Ubuntu Linux

This tutorial shows how to download, install and compile Gazebojs on a computer where Gazebo and its  development libraries are installed.

#### Setup

Install the osrf repository and install the development libraries, dependending on the version of Gazeobo you are using (for example, libgazebo4-dev for Gazebo 4. see http://gazebosim.org/tutorials?tut=install). The dev Debian package contains the Gazebo header files that are necessary for the gazebojs installation. This is because the NodeJs Gazebo modules are automatically compiled on your machine when the 'npm install gazebojs' is invoked (see below).
Like Gazebo, gazebojs module uses semantic versioning, so the major version of gazebojs should be the same as the major version of Gazebo you are using. You can specify rules about the version of gazebojs you want to use in the `package.json` file (see https://www.npmjs.org/doc/files/package.json.html).

Install nodejs and npm 

    sudo apt-get install nodejs npm

You may have to install nodejs-legacy if the `node` command does not exist:

    sudo apt-get install nodejs-legacy

Install jansson (JSON library)

    sudo apt-get install libjansson-dev

Make sure that these packages can be found in your pkg-config path. You can check this by executing this command without any error:

    pkg-config --cflags gazebo jansson protobuf


#### Running

Now that everything is installed, here are the steps to test it:


Create a NodeJs project directory
 
    mkdir gz_node_inst
    cd gz_node_inst


Install Gazebojs

     npm install gazebojs

This operation should download and compile the latest gazebojs. There is a C++ compilation phase where a NodeJs module is created. There should now be a `gz_node_inst/node_modules` directory.



Test your installation:

Launch Gazebo in a separate terminal and verify that the simulation is running (Sim Time increases):

    gazebo


Use the 'node' command to invoke the NodeJs REPL console

    node

Type in the following command to load the gazeboJs module, create a simulation client and pause the running simulation

    var gazebojs = require('gazebojs')
    var sim = new gazebojs.Gazebo()
    sim.pause()

You should see the simulation stop in Gazebo.
