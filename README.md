## NGINX Info

Version `0.0.1 alpha`

Helping NGINX users migrate from NGINX OSS to Plus.

We want to make it easier for customers using NGINX open source to upgrade safely and easily to NGINX Plus.

## Build / Installation

The tool does not require any 3rd-party software or modules. The shell-script generated by the `build.py` script can be directly copied and executed on the target server.

To build the shell script clone the repository and create a virtual-environment
`python3 -m venv nginxinfo` and activate `source nginxinfo/bin/activate`. Install the dependencies for the build script.

`python3 -m pip install -r requirements.txt`.

Make the python build.py script executable.
`chmod +x ./build.py` 

#### Build the shell script
` ./build.py > nginxinfo.sh && chmod +x nginxinfo.sh`

The generated shell script can be copied to the server and executed.

## Run
Currently we support 3 runtime modes.
- quite (`-q`) will print nothing but return an exit-code
- normal (default) will print only important information for the upgrade.
- debug / verbose (`-v`). Will print the parsing output as well as all information printed in the normal mode.

#### Example output
```shell

(nginxinfo)$ ./nginxinfo.sh

  NGINX Info Report
  =================
  - Version: `nginxinfo v0.1 alpha`
  - Source: https://github.com/tippexs/ngxinfo
  - Build date: 2021-10-5


  NGINX Version
  -------------

  - NGINX version: nginx-1.21.3
  - OpenSSL version: OpenSSL 1.0.2k-fips  26 Jan 2017
  - Proveance: CentOS Linux

  Configuration
  -------------

  NGINX is installed but not up and running. No network information available.
  - Found unsupoported directives:
    - header_filter_by_lua_file (x1)
    - header_filter_by_lua_block (x1)

  Security
  --------

   ** Nothing found **

  Summary
  -------
  Do not upgrade to NGINX Plus without first discussing this project with your F5/NGINX representative
```

## ToDos

- More NGINX Version Information (source branch, release date)
- Calculate an Upgrade-Score based on different information(Operating system, unknown directives and / or modules)
- Scanning a `nginx -T` output and print a report.
- Handle runtime information from /proc/PID/cmdline instead of `nginx -V`
- Detect unsupported builds and modules (dynamic and static)
