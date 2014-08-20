ClassVis
========

ClassVis is a utility to generate diagrams of relationships between InterSystems Caché Classes. 

ClassVis uses the open source Graphviz tool to render the diagrams. See http://www.graphviz.org/

Installation
------------

1) Install Graphviz (http://www.graphviz.org/)

2) Load and compile the ClassVis.xml file in Caché:

	do $system.OBJ.Load("ClassVis.xml","c")

3) Ensure that the Graphviz 'dot' command is on the System Path OR call SetPath^ClassVis(path), and pass the path to the Graphviz bin directory.

	do SetPath^ClassVis("/usr/local/graphviz/bin/")

Note that the trailing slash is required.

Usage
-----

ClassVis has two modes: one for showing compile dependencies, and one for showing relationships between the classes. They are both called the same way:

do CompileDeps^ClassVis(clslist,flags,outfile,imgtype,keepfiles)

do Schema^ClassVis(clslist,flags,outfile,imgtype,keepfiles)

the parameters are:

	clslist - The list of starting classes. Related classes will be included based on the flags. This can use the * wildcard (e.g., Sample.*), or be a regular expression contained in '/' characters (e.g., '/Sample\..*/'.).

	flags - Controls the output. Values are:

		Common: 
			a - include Persistent classes (default: true)
			s - include Serial classes (default: false)
			r - include Registered classes (default: false)
			d - include DataType and Stream classes (default: false)
		
			p - include %-classes (default: false)
			e - include Ensemble System classes (default: false)
			h - include HealthShare System classes (default: false)
		
		CompileDeps:
			v - include reverse dependencies (default: false)

		Schema:
			i - include Super Class (default: false)
			c - include CompileAfter/DependsOn (default: false)
	
	outfile - the path and name of the file to contain the image.
	
	imgtype -  the type of image. The default is 'svg'. Valid values are any of the supported formats for GraphViz. See here for the complete list: http://www.graphviz.org/content/output-formats

	keepfiles - This parameter is for debugging only. If 1, do not delete intermediate files. The defualt is 0.

