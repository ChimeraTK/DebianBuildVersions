# DebianBuildVersions
Control repository for storing build version numbers for Debian packages. The content of this repository is parsed and changed by the getDebianBuildVersion script from the DebainPackagingScripts repository. Do not modify manually unless you know exactly what you are doing! Our Debian package repositories might break otherwise.

The structure is as follows:
* The first three directories in the hierarchy are: PACKAGE_NAME/MAJOR.MINOR_PACKAGE_VERSION/DEBIAN_CODENAME
* In that directory, a file LATEST_BUILD contains the subdirectory for the build with the highest build number
* The subdirectories names contain the names and versions of the dependencies, one directory hierarchy per dependency
* In the deepest subdirectory (fully describing all dependencies) a single file called BUILD_NUMBER contains the build number assigned to this build

Example:

The package DeviceAccess-DoocsBackend depends on DeviceAccess, DOOCS and DoocsServerTestHelper. If this package is built as version 0.1 on xenial against DeviceAccess-0.14, DOOCS-18.10.5 and DoocsServerTestHelper-0.1, the file DeviceAccess-DoocsBackend/0.1/xenial/DeviceAccess-0.14/DOOCS-18.10.5/DoocsServerTestHelper-0.1/BUILD_NUMBER will contain the build version.

If this file does not yet exist, because this is the first build in this exact combinations of versions, the file DeviceAccess-DoocsBackend/0.1/xenial/LATEST_BUILD is examined. This file contains information about the last build.

Let's assume, the last build was identical but against DeviceAccess-0.13. Then the file will contain the following string:
<pre>./DeviceAccess-0.13/DOOCS-18.10.5/DoocsServerTestHelper-0.1/BUILD_NUMBER</pre>

The script will then take the build number from the file DeviceAccess-DoocsBackend/0.1/xenial/DeviceAccess-0.14/DOOCS-18.10.5/DoocsServerTestHelper-0.1/BUILD_NUMBER, increase it by 1, add the file DeviceAccess-DoocsBackend/0.1/xenial/DeviceAccess-0.14/DOOCS-18.10.5/DoocsServerTestHelper-0.1/BUILD_NUMBER and update the file DeviceAccess-DoocsBackend/0.1/xenial/LATEST_BUILD.
