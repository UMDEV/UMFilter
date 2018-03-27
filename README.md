# UMFilter

Sample C++ ISAPI filter and extension for debugging issues with filters related to other extensions (or ASP.net) eating POSTS requests.

This is a sample IIS filter & extension that prints out a custom header and echos the post back. It is also a simple example of creating a combo filter & extension for IIS 7.0, 7.5, 8.0, 8.5.

## Installation Requirements
In order to use the UMFilter.dll ISAPI filter+extension you need to install the [Visual C++ 2017 redistributable](https://aka.ms/vs/15/release/VC_redist.x64.exe).

## Build Settings
The git repo holding the source code can be found on github.
This UMFilter.dll was built using [Visual Studio 2017 (Community Edition)](https://www.visualstudio.com/downloads/) using the following settings:
- Configuration: 64bit Release build
- Target Platform: Windows 10
- Windows SDK Version: 10.0.16299.0
- Platform Toolset: Visual Studio 2017 (v141)
- Use of MFC: Use Standard Windows Libraries
- Common Language Runtime Support: No Common Language Runtime Support

## How To Use This Filter
Using a utility that can make POST http requests (like curl), you need to POST data to a url that matches the ISAPI script mapping you setup. 

An example would be if you are testing your local IIS that has mapped the dll to `*.sso`  then you would POST `"param1=test1&param2=test2"` to `http://localhost/Shibboleth.sso` 

using curl: `curl -v -d "param1=test&param2=test2" "http://localhost/Shibboleth.sso"` 

The successful response back would be: 
`<html><body><pre>param1=test1&param2=test2</pre></body></html>` showing that all your POSTed data is printed in the pre element tag, you would also see the custom header in the response headers.
