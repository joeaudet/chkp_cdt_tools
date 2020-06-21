# ckhp_cdt_tools
Tools to help with using Check Point CLI CDT based tools MDM environment

Environments may employ multiple 'Multi Domain Management (MDM)' servers, and this tool supports a single server, or many.

The CDT CLI tool needs to be run from the MDM server where the domain is ACTIVE.
Some environments may have ACTIVE domains on different MDM servers. The tool is design to link those together to make sure the CLI output is correct.

mdmservername <-> activemdmserver | These values need to be the same so that when you select the MDM server where the domain is active, it will only show you those domains.

### Download & Use (Tested in Chrome and Firefox)
1. This file can be operated locally on a workstation or hosted off a server. Only HTML, javascript, and jQuery 2.2 minified are used within the file. No local system access is needed.
1. Download the HTML file [cdt_cli_generator_mdm.html](https://raw.githubusercontent.com/joeaudet/chkp_cdt_tools/master/cdt_cli_generators/cdt_cli_generator_mdm.html) from a command prompt to workstation or server:
	```
	curl -O https://raw.githubusercontent.com/joeaudet/chkp_cdt_tools/master/cdt_cli_generators/cdt_cli_generator_mdm.html
	```
1. Edit the HTML file in an editor to change the data objects for use in your environment (these are comma separated):
	- mdmServerObj (this is an object where you define your MDM servers)
		- desc: What you want to see displayed in the dropdown menu
		- mdmservername: Suggest making this the actual MDM servername. Will need to match the domains 'activemdmserver' value as appropriate
		- ipaddress: IP address of the MDM server (NOT the domain servers)
		- Example object:
		```
		var mdmServerObj = [
			{ desc: "MDM1", mdmservername: "mdm1", ipaddress: "1.1.1.1" },
			{ desc: "MDM2", mdmservername: "mdm2", ipaddress: "2.2.2.2" }
		];
		```
	- domainsObj
		- desc: What you want to see displayed in the dropdown menu
		- activemdmserver: This needs to be an exact case sensitive match to what you specified in the MdmServerObj:mdmservername value
		- ipaddress: IP address of the active domain server (NOT the MDM servers)
		- Example object:
		```
		var domainsObj = [
			{ desc: "Domain1", activemdmserver: "mdm1", ipaddress: "1.1.1.50"},
			{ desc: "Domain2", activemdmserver: "mdm2", ipaddress: "2.2.2.50"}
		];
		```
	- deploymentPlansObj
		- desc: What you want to see displayed in the dropdown menu
		- filename: The name of the deployment plan file name (do not include .xml - the tool will append it)
		```
		var deploymentPlansObj = [
			{ desc: "Create Gateway Snapshot", filename: "create_gateway_snapshot_dp" },
			{ desc: "R80.30 No JHF Upgrade - Copy and Import Package", filename: "r8030_import_only_dp" },
			{ desc: "R80.30 No JHF Upgrade - Install", filename: "r8030_install_dp"},
			{ desc: "R80.30 JHF T155 - Copy and Import Package", filename: "r8030_t155_only_import_only_dp"},
			{ desc: "R80.30 JHF T155 - Install", filename: "r8030_t155_only_install_dp"}
		];
		```
1. Open the HTML file in a browser, select an MDM server, then a domain, then a deployment plan, enter a change request ID, click the button to Create Commands
