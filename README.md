DDCLI
=====
###by Dave Dribin

an Objective-C library to help write command line  applications by simplifying parsing command line options and  eliminating much of the boiler plate code.

The getopt_long(3) function is used to parse command options, but the complexity of using this function is hidden by an Objective-C wrapper (DDGetoptLongParser). Key-Value Coding (KVC) is used to set the options on a target class. A simple example should help make this clear.

http://www.dribin.org/dave/software/ddcli/api/

###Modifications in the repo:
PPC support dropped, 64bit mode and ARC compatibility added.

*note: the project remains non-arc so it is available in 32bit and 64bit both but it has been modified to work with projects that DO use arc.*

For that I changed the `DDGetoptOption struct` to no longer include a `NSString *longOption` but a `const char *longOption` 

so From the example above one would have to modify:

	- (void) application: (DDCliApplication *) app
    willParseOptions: (DDGetoptLongParser *) optionsParser;
	{
    	DDGetoptOption optionTable[] = 
	    {
    	    // Long         Short   Argument options
        	{@"output",     'o',    DDGetoptRequiredArgument},
			{@"help",       'h',    DDGetoptNoArgument},
    	    {nil,           0,      0},
	    };
    	[optionsParser addOptionsFromTable: optionTable];
	}
	
to:

    ...
        	{"output",     'o',    DDGetoptRequiredArgument},
			{"help",       'h',    DDGetoptNoArgument},
    ...
    
no more @" but only " -> NSString to char*