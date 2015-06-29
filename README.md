# rosinstall

This repo is holding the `.rosinstall` file used with OSL team repositories. The `rosinstall` system is used to automatically download and synchronize a bunch of remote repos with ROS software using a simple facility called `rosws` (for more info please see below). 

Before starting please be sure to use the right `.rosinstall` file according to your current ROS version. If a new version is released please create a new `<ros_version_name>.rosinstall` file by copying and updating the last working one.

## Usage

Please make sure to start from a ROS clean environment if this is your first experience with this tool. To get your local environment up-to-date with the development code you need to follow some steps. Assuming you are working with ROS Indigo just type:
	
	cd src
	git clone git@github.com:oceansystemslab/rosinstall.git
	cd rosinstall
	cp indigo.rosinstall ../.rosinstall
	cd ..
	rosws update

This will parse the chosen `<version>.rosinstall` file and it will download all the required code from the remote repositories. 

### Rosbuild Workspaces

If then code you are downloading is for a `rosbuild` workspace to be used in a overlay mode (the default option during transition period) now you need to recreate the startup scripts:

	cd src
	rosws regenerate
	source setup.bash

This will activate the `rosbuild` workspace you just downloaded.

### Catkin Workspaces

If then code you are downloading is for a `catkin` workspace now you can go to the top-level folder and start the make procedure:

	cd ..
	catkin_make

## Customization

By OSL convention any `.rosinstall` is composed of three main sections, the `setup`, the `main` and the `local`. The first two are required while the latter is used to customize your installation with your local packages before they have been released.

Here is an example of a `.rosinstall` file (a plain YAML file):

	# indigo.rosinstall
	- setup-file: {local-name: /opt/ros/jade/setup.sh}

	# main repos
	- git: {local-name: rosinstall, uri: 'git@github.com:oceansystemslab/rosinstall.git', version: master}
	# ...

	# local pacakges can be added here using the keywork 'other'
	# 	- other: {local-name: <package_dir>}

The `setup` is telling the `rosinstall` system which ROS workspace to overlay on. Think the overlay system as a russian matryoshka doll where the new workspace will wrap an existing one. In the default case the ROS standard workspace is used. In the case you want to customize the use of these `.rosinstall` file, for instance if you have multiple workspaces, you can edit (but not push back to the repo) your local `.rosinstall` file, changing the `setup` section by pointing at a different existing workspace.

## Activation

In order to work with the downloaded code, after following the steps above one of the build systems, make sure to source from your local `~/.bashrc` the `setup.bash` file of your new workspace.

For instance if working with `rosbuild` just add to your `~/.bashrc`:
	
	source ~/src/setup.bash

## References

Please be sure to give a quick read about the use of `rosws` tool and the `rosinstall` framework:
  - http://wiki.ros.org/rosws
  - http://docs.ros.org/independent/api/rosinstall/html/rosws_tutorial.html
  - http://docs.ros.org/independent/api/rosinstall/html/rosinstall_file_format.html
