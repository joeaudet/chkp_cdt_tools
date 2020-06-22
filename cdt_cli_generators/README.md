# ckhp_cdt_tools
This tool is designed to make using the [Check Point Central Deployment Tool (CDT)](https://supportcenter.checkpoint.com/supportcenter/portal?eventSubmit_doGoviewsolutiondetails=&solutionid=sk111158) CLI version easier by generating properly formatted CLI syntax for candidate list generation, and execution of the same deployment plan. Basic knowledge of CDT is necessary to get the most use of this tool.

<a href="http://www.pinktech.pro/cdt_tool_demo/cdt_cli_generator_mdm.html" target="_blank">Demo Site</a>

### Tool overview
MDM based environments may employ multiple 'Multi Domain Management (MDM)' servers. This tool supports a single MDM server, or multiple.

The CDT CLI tool needs to be run from the MDM server where the domain is ACTIVE.
Some environments may have ACTIVE domains on different MDM servers. The tool is design to link those together to make sure the CLI output is correct.

mdmservername <-> activemdmserver | These values need to be the same so that when you select the MDM server where the domain is active, it will only show you those domains.

Commands to make the folders using the default values, run from expert mode on the MDM server:
```
mkdir /opt/CPcdt/candidate_lists
mkdir /opt/CPcdt/deployment_plans
mkdir /opt/CPcdt/filter_lists
```

### Download & Usage
1. This file can be operated locally on a workstation or hosted off a server. Only HTML, javascript, and jQuery 2.2 minified are used within the file. No local system access is needed.
1. Download the HTML file <a href="https://raw.githubusercontent.com/joeaudet/chkp_cdt_tools/master/cdt_cli_generators/cdt_cli_generator_mdm.html" target="_blank">cdt_cli_generator_mdm.html</a> from a command prompt to workstation or server:
	```
	curl -O https://raw.githubusercontent.com/joeaudet/chkp_cdt_tools/master/cdt_cli_generators/cdt_cli_generator_mdm.html
	```
1. Open the HTML file in a browser, select an MDM server, a domain, a deployment plan, enter a activity name (used in output file usage), then click the button to Create Commands

### Tool customization
- Edit the HTML file in an editor to change the data objects for use in your environment (these are comma separated):
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
			{ desc: "R80.30 No JHF Upgrade - Copy and Import Package", filename: "r8030_import_only_dp" },
			{ desc: "R80.30 No JHF Upgrade - Install", filename: "r8030_install_dp"},
			{ desc: "R80.30 JHF T155 - Copy and Import Package", filename: "r8030_t155_only_import_only_dp"},
			{ desc: "R80.30 JHF T155 - Install", filename: "r8030_t155_only_install_dp"}
		];
		```
- Default File locations used within the tool:
	- /opt/CPcdt/ - CDT main path
	- /opt/CPcdt/candidate_lists/ - Candidate List CSV Files
	- /opt/CPcdt/deployment_plans/ - Deployment Plan XML Files
	- /opt/CPcdt/filter_lists/ - Filter Files