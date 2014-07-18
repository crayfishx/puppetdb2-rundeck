## puppetdb_rundeck module

This module sets up puppetdb-rundeck to run under passenger and expose all host data in PuppetDB, incuding fact, to rundeck.


## Class puppetdb_rundeck

### Options

* `with_sinatra` : Manage sinatra gem (default true)
* `approot` : Application root
* `servername` : Apache server name
* `port` : Port (default 8888)
* `puppetdb_port` : PuppetDB port (default 8080)
* `puppetdb_host` : PuppetDB host (default localhost)
* `owner` : Ownership of app files (apache user)
* `group` : Group of app files (apache group)



## puppetdb-rundeck
Based on the project https://github.com/martin2110/puppetdb-rundeck, modified to expose facts and add documentation.

Enhanced to expose facter data and use the new PuppetDB2 API https://github.com/sirloper/puppetdb2-rundeck


sinatra app that glues puppetdb and rundeck together. 

set host_uri and port in the script

## Installation

    class { 'puppetdb_rundeck': }


## Usage
Within your rundeck project configuration, add a Resource Model Source of type "URL Source", pointing at the machine that this web application is running on, port 8888 (or whatever you've configured it to use per the Apache configuration)

Example:
URL Field: http://localhost:8888

Timeout: 90

Cache Results: Not checked

Any Jobs created under this Project should now have access to all nodes known by PuppetDB.

###Filtering
This plugin exposes both classes and facts of all nodes known by PuppetDB to Rundeck.  See the Rundeck documents on how to filter.  Puppet facts are exposed as Rundeck "Attributes", so to filter by all RedHat-derived machines, you could enter "osfamily: RedHat" into the filter field and it will show only nodes that PuppetDB knows to have that fact with that value.

All known facts exposed to Rundeck can be viewed by looking at the "nodes" tab and expanding any of the nodes listed below.  They are listed in the format of "Fact (attribute): Value".  Note that this list can be quite long depending on your environment.  This DOES include custom facts.



