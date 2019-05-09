## Use Vcpkg to build third application.

Before doing this, download git cmake, and add them to Environment PATH

Open PowerShell, 

```
PS> git clone https://github.com/Microsoft/vcpkg.git
PS> cd vcpkg
PS> .\bootstrap-vcpkg.bat
```

Add the vcpkg path to Environment PATH.

Reopen PowerShell with administrator,

```
PS> vcpkg integrate install
```

Then, at any time, you can download the packages managed by vcpkg.
For example:

```
PS> vcpkg install curl # install specific package
```

You can use vcpkg to search packages:
```
PS> vcpkg search # View all packages
PS> vcpkg search tesseract # Search specific packages
```

## install tesseract

```
vcpkg install tesseract
```
