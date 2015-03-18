# rosinstall
The .rosinstall file for OSL team repositories. 
Please make sure to use the right .rosinstall file according to your current ROS version.

If a new version is released please make sure to create a new `<ros_version_name>.rosinstall` file.

## Usage

To get your local environment up-to-date with the development code use:

	cd src
	git clone git@github.com:oceansystemslab/rosinstall.git
	cd rosinstall
	cp indigo.rosinstall ../.rosinstall
	cd ..
	rosws update -j4

This will parse the chosen `<version>.rosinstall` file and it will download all
the required code from the remote repositories. Please make sure to start from a
clean environment if this is your first experience with this tool.

## References

Please be sure to give a quick read about the use of `rosws` tool and the `rosinstall` framework:
  - http://wiki.ros.org/rosws
  - http://docs.ros.org/independent/api/rosinstall/html/rosws_tutorial.html
  - http://docs.ros.org/independent/api/rosinstall/html/rosinstall_file_format.html
