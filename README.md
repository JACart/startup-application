# startup-application
# Project Description
A Java GUI that was built to support the startup process of the JMU Autonomous Vehicle. The
user will launch the program and a GUI will appear. The user can then select the features they
want to enable on the cart. Some features include small map, full map, online mode, and
research mode. If the user decides not to pick any features, the default features the cart will
run with are small map, offline, and non-research mode. Once the cart is running the uer has
the option to click the &quot;Kill Terminal Processes&quot;. This will automatically stop the cart and
terminate all processes associated with the cart (ROS, ZED, local server, etc.).

# How to run the program
1. Open a terminal
2. $cd catkin_ws/src/startup-application
3. java GUI

# Compiling program (if changes are made)
If changes are made to the Java script it must be recompiled before it is ran.
1. Open a terminal
2. $cd catkin_ws/src/startup-application
3. javac GUI -&gt; compiles
4. java GUI -&gt; runs

*After you have tested and confirmed that the changes you made to the Java script work, you
must also update the JACart git startup-application repository.

# Adding new properties to runArgs
To add new properties to the launch script (current properties consist of fullmap, research
mode, and pos tracking), create a component for checking whether user would like such
property (ie checkbox or selection) and add to chain of conditions which add to the runArgs
string. This will be passed as arguments to run.sh

# Adding processes
1. Add new systems startup in the run.sh script, all process startup through this script. If a new
system is added, implement it into the kill sequence. Follow the following to add to the process
kill system:
String[] kill&lt;SYSTEM&gt;Cmd = new String[] {&quot;gnome-terminal&quot;, &quot;--tab&quot;, &quot;-e&quot;, &quot;sh -c \&quot;ps axf | grep
&lt;SYSTEM-NAME&gt; | grep -v grep | awk &#39;{print \\\&quot;kill -15 \\\&quot; $1}&#39; | sh\&quot;&quot;};

a) Change &lt;SYSTEM&gt; in the variable name to something relative (does not have to be specific
to actual system name).

b) Change &lt;SYSTEM-NAME&gt; in the grep script to the name of the process running. This must be
specific to the process and should only flag the process wanting to kill as the script will
terminate any PIDs connecting to such name.
c) Add kill&lt;SYSTEM&gt;Cmd to the try-catch: proc = new ProcessBuilder(kill&lt;SYSTEM&gt;Cmd).start();
2. To check if the name selected for &lt;SYSTEM-NAME&gt; you may search using &quot;ps axf | grep
&lt;SYSTEM-NAME&gt;&quot; and view results.
# Collaborators
Amber Oliver and Alejandro Muniz-Samalot
