# bigfix_plugin_export

repo for an example bigfix server plugin service for exporting custom content

src/export_all_sites_plugin.py is an example bigfix server plugin service for exporting custom content and commit it to a git repo.

This python script can be run on the command line, or through a github action, or as a BigFix Server Plugin Service.

The only thing that really makes it a "BigFix Server Plugin Service" is that it can accept BigFix Server connection details on the command line, and in the way that is typically used for BigFix Server Plugins.

src/export_all_sites_python_windows.xml is an example config file that can be used on windows for running export_all_sites_plugin.py as a BigFix Server Plugin Service. This config file gets put in the Config folder of the Applications folder of the BigFix Server installation folder.

The key is the argments and how they are passed into it.

See the example command:

`"C:\Program Files\Python311\python.exe" "C:\Program Files (x86)\BigFix Enterprise\BES Server\Applications\export_all_sites\export_all_sites_plugin.py" -besserver %BESHTTP% -r %RESTURL% -u %MOUSERNAME% -p %MOPASSWORD% -v -d`

The plugin can also be run on a Linux BigFix root server by tweaking this command.

For example:

`/usr/bin/python3 /var/opt/BESServer/Applications/export_all_sites/export_all_sites_plugin.py -besserver %BESHTTP% -r %RESTURL% -u %MOUSERNAME% -p %MOPASSWORD% -v -d`

---

You can also just invoke it directly on the command line as well, like:

`python export_all_sites_plugin.py -besserver %BESHTTP% -r %RESTURL% -u %MOUSERNAME% -p %MOPASSWORD% -v -d`

You would need to substitute the variables in the %% for the actual values of the connection details and account you wish to use.

---

To setup as a bigfix server plugin service on the BigFix root server:

- Setup BigFix server plugin service if not done so already
- Install python or use pyinstaller to turn it into an executable.
 - If installing python, then install dependencies as well.
- Create a folder inside the Applications folder inside the BigFix Server folder
 - C:\Program Files (x86)\BigFix Enterprise\BES Server\Applications\export_all_sites
 - /var/opt/BESServer/Applications/export_all_sites
- Put python script or binary in that folder
- create a definition file in the config folder (see examples in src)
 - C:\Program Files (x86)\BigFix Enterprise\BES Server\Applications\Config
 - /var/opt/BESServer/Applications
- check MFS log in logs folder for invocations
- check export_all_sites log in the plugin folder for run logs
