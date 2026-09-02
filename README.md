
<p align="center"> <img src=Screenshots/logo.png  border="2px solid #555">

# SourcePoint
SourcePoint is a polymorphic C2 profile generator for Cobalt Strike C2s, updated for **Cobalt Strike 4.13**. SourcePoint allows unique C2 profiles to be generated on the fly that helps reduce our Indicators of Compromise ("IoCs") and allows the operator to spin up complex profiles with minimal effort. SourcePoint was designed with the intent of addressing the issue of how to make our C2 activity harder to detect, focusing on moving away from malicious IoCs to suspicious ones. The goal here is that it is harder to detect our C2 if our IoCs are not malicious in-nature and require additional research to discover the suspicious nature. SourcePoint contains numerous different configurable options to choose from to modify your profile (in most cases if left blank SourcePoint will randomly choose them for you). The generated profiles modify all aspects of your C2. The goal of this project is to not only aid in circumventing detection-based controls but also help blend C2 traffic and activity into the environment, making said activity hard to detect. 

Errors are bound to happen, I attempted to handle as many as I could find within this Fork from the original code. 


## Installation
```
go get gopkg.in/yaml.v2

go build SourcePoint.go
```
OR
```
go install https://github.com/waffl3ss/SourcePoint
```

## Usage

```
#./SourcePoint -h

	   _____                            ____        _       __
	  / ___/____  __  _______________  / __ \____  (_)___  / /_
	  \__ \/ __ \/ / / / ___/ ___/ _ \/ /_/ / __ \/ / __ \/ __/
	 ___/ / /_/ / /_/ / /  / /__/  __/ ____/ /_/ / / / / / /_
	/____/\____/\__,_/_/   \___/\___/_/    \____/_/_/ /_/\__/
  							(@Tyl0us)

                                                                                                                        
Usage of ./sourcepoint:
  -Allocation string
        Minimum amount of memory to request for injected content (must be higher than 4096)
  -BeaconGate string
        Specify beacon gate options (All, Comms, Core, Cleanup) or specific APIs
  -CDN string
        CDN cookie name (typically used for AzureEdge profiles)
  -CDN-Value string
        CDN cookie value (typically used for AzureEdge profiles)
  -CheckinDelay string
        Delay in milliseconds before Beacon's initial check-in
  -CopyPEHeader
        Copy PE Header
  -Customuri string
        The base URI for custom HTTP GET/POST profile - Cannot be used with CustomuriGET or CustomuriPOST
  -CustomuriGET string
        The base URI for custom HTTP GET profile - Must be used with CustomuriPOST
  -CustomuriPOST string
        The base URI for custom HTTP POST profile - Must be used with CustomuriGET
  -Datajitter string
        Appends a value to HTTP-Get and HTTP-Post server output (default "50")
  -EafBypass
        Enable EAF Bypass
  -Forwarder
        Enabled the X-forwarded-For header (Good for when your C2 is behind a redirector)
  -Host string
        Team server domain name
  -Httplib string
        Select the default HTTP Beacon library:
        [*] wininet
        [*] winhttp (default "winhttp")
  -InjectDriploadDelay string
        Delay in milliseconds between drip-load chunks for process injection
  -InjectUseDriploading
        Enable drip-loading for process injection
  -Injector string
        Select the preferred method to allocate memory in the remote process:
        [*] VirtualAllocEx (Great for cross architecture i.e x86 -> x64 and x64->x86)
        [*] NtMapViewOfSection (A more stealthly option, however fails over to VirtualAllocEx, generating more events when it does)
  -Jitter string
        Jitter percentage for beacon call home
  -Keylogger string
        Select the preferred method the beacon will use to log keystrokes: 
        [*] GetAsyncKeyState (Uses GetAsyncKeyState API (Separate DLL for x86/x64 process))
        [*] SetWindowsHookEx (Uses SetWindowsHookEx API)
  -Keystore string
        SSL keystore name
  -Metadata string
        Specifies how to transform and embed metadata into the HTTP request:
        [*] base64
        [*] base64url
        [*] netbios
        [*] netbiosu (default "base64url")
  -Outfile string
        Name of output file
  -PE_Clone string
        PE file beacon will mimic (Use the number):
        [1] ActivationManager.dll
        [2] audioeng.dll
        [3] AzureSettingSyncProvider.dll
        [4] BingMaps.dll
        [5] DIAGCPL.dll
        [6] EDGEHTML.dll
        [7] FILEMGMT.dll
        [8] FIREWALLCONTROLPANEL.dll
        [9] GPSVC.dll
        [10] gpupvdev.dll
        [11] libcrypto.dll
        [12] srvcli.dll
        [13] srvsvc.dll
        [14] Windows.Storage.Search.dll
        [15] Windows.System.Diagnostics.dll
        [16] Windows.System.Launcher.dll
        [17] Windows.System.SystemManagement.dll
        [18] Windows.UI.BioFeedback.dll
        [19] Windows.UI.BlockedShutdown.dll
        [20] Windows.UI.Core.TextInput.DLL
        [21] winsqlite3.dll
        [22] WMNetMgr.DLL
        [23] wwanapi.dll
        [24] WWANSVC.DLL
        [25] wow64win.dll
        [26] wow64.dll
        [27] ctiuser.dll (Carbon Black's DLL)
        [28] InProcessClient.dll (SentinelOne's DLL)
        [29] umppc.dll (CrowdStrike's DLL)
        [30] CyMemDef64.dll (Cylance's DLL)
  -Password string
        SSL certificate password
  -PostEX_Name string
        File Post-Ex activities will spawn and inject into (Use the number):
        [1] WerFault.exe
        [2] WWAHost.exe
        [3] choice.exe
        [4] bootcfg.exe
        [5] dtdump.exe
        [6] expand.exe
        [7] fsutil.exe
        [8] gpupdate.exe
        [9] gpresult.exe
        [10] logman.exe
        [11] mcbuilder.exe
        [12] mtstocom.exe
        [13] pcaui.exe
        [14] powercfg.exe
        [15] svchost.exe
        [16] dllhost.exe
  -Profile string
        HTTP GET/POST profile (Use the number):
        [1] Windowsupdate
        [2] Slack
        [3] Gotomeeting
        [4] Outlook.Live
        [5] Safebrowsing [Cloudfront Compatible]
        [6] AzureEdge [AzureEdge Compatible]
        [7] Field-Keyword [Cloudfront Compatible]
        [8] Custom (Used with ProfilePath)
  -ProfilePath string
        Path of custom HTTP GET/POST profile...
  -RdllDriploadDelay string
        Delay in milliseconds between drip-load chunks for RDLL
  -RdllUseDriploading
        Enable drip-loading for RDLL (allocates many small memory chunks instead of one large block)
  -RdllUseSyscalls
        Use Syscalls for Rdll
  -Sleep string
        Initial beacon sleep time
  -SleepMask
        Enable Sleep Mask (default true)
  -StartRWX
        Use RWX as initial permissions for injected content (default true, set to false for RW)
  -SmartInject
        Enable Smart Inject (post-ex)
  -Stage string
        Disable host staging (Default: False) (default "false")
  -Syscall string
        Defines the ability to use direct/indirect system calls:
        [*] None
        [*] Direct
        [*] Indirect (default "None")
  -TasksDnsProxyMaxSize string
        The maximum size (in bytes) of proxy data to transfer via the DNS communication channel at a check in
  -TasksMaxSize string
        The maximum size (in bytes) of task(s) and proxy data that can be transferred through a communication channel at a check in
  -TasksProxyMaxSize string
        The maximum size (in bytes) of proxy data to transfer via the communication channel at a check in
  -ThreadSpoof
        Sets post-ex DLLs to spawn threads with a spoofed start address (default true)
  -TransformObfuscate string
        Transform obfuscate options (comma-separated list):
        [*] lznt1
        [*] rc4 "64"
        [*] xor "32"
        [*] base64
  -Uri string
        The number URIs a profile for beacons to choose from
  -Useragent string
        UserAgent string for the beacon to use (Leave blank to randomly select one):
        [*] Win10Chrome
        [*] Win10Edge
        [*] Win10IE
        [*] Win10Firefox
        [*] Win10
        [*] Win6.3
        [*] Linux
        [*] Mac
  -Yaml string
        Path to the Yaml config file
```


## Important

SourcePoint primarily automates the build process of a profile. It's very important to know all the features modified in these profiles. Knowing these features can really help increase your success. 

## Options 

While there are a lot of settings and features described in the help function of SourcePoint, there are numerous important features baked into each profile that are important to be familiar with. These features are:

### Global Options
This part of your profile modifies how the beacon operates. Some of the features used to modify the behaviour are:

* Host Stage - Allows the team server to host staged shellcode for HTTP, HTTPS, DNS. If this is enabled, anyone sending a GET request with a specific value such has `/9ZXq` can pull the shellcode as well
* Sleep - The length of time that a beacon calls back home
* Jitter - Appends a percentage to the beacon call home time
* Useragent - The useragent string used when communicating HTTP and HTTPS traffic. Using the appropriate useragent string can help blend into the environment 
* Data Jitter - Adds a random-length string to all GET and POST requests to ensure incoming requests are not the same length
* Checkin Delay - Delays Beacon's initial check-in by the specified number of milliseconds, breaking event-correlation detection heuristics on reflective loading
* SMB Frame Header - Adds a header value to the SMB beacon messages
* Pipename - Sets the name of the SMB pipe the beacons is going to use for communication
* Pipename Stager - Sets the name of the SMB stager for the beacons
* TCP Frame Header - Adds a header value to the TCP beacon messages
* SSH Banner - The SSH banner used
* SSH Pipename - The name used for the SSH banner
* HttpLib - The library attribute allows the user to specify the default library used by the generated beacons. The value can be "wininet" or "winhttp"

### Stage
This part of your profile controls how beacon is loaded into memory and edits the content of the beacon DLL. Some of the features used to modify the behaviour are:

* Obfuscate - Obfuscates the import table of the reflective DLL
* Stomppe - Asks the payload to stomp MZ, PE and, e_lfanew values after loading
* Clean up - Tells the beacon to free up memory associated with the reflective DLL that initialized it
* UseRWX - Ensures shellcode does not use Read, Write Execute permissions
* Magic_MZ - Overrides the first bytes (MZ header included) of Beacon's Reflective DLL (currently only for x64)
* Magic_PE - Overrides the PE character marker used by Beacon's Reflective Loader with another value
* Syscall - Defines the ability to use direct/indirect system calls instead of the standard Windows API functions
* BeaconGate - Controls which API calls are routed through the beacon gate for evasion (All, Comms, Core, Cleanup, or specific APIs)
* Sleep Mask - Obfuscates beacon in memory while sleeping. TCP and SMB beacons will obfuscate themselves at rest while they wait for the connection to be established
* EAF Bypass - Enables Export Address Filtering bypass
* RDLL Use Syscalls - Uses indirect system calls when loading the payload
* Copy PE Header - Copies the PE header from the cloned DLL into beacon's memory
* RDLL Drip Loading - Allocates many small memory chunks instead of one large block, breaking event-correlation detection heuristics. Configurable delay between chunks via RdllDriploadDelay
* PE Header - Changes the characteristics of your beacon Reflective DLL to look like something else in memory
* Transform Obfuscate - Transforms beacon's Reflective DLL stage content using compression and encoding (lznt1, xor, rc4, base64)
* Transformation - Transform beacon's Reflective DLL stage by removing or adding strings to the .rdata 

### Process-Inject
This part of your profile controls how the beacon shapes injected content and controls process injection behavior. Some of the features used to modify the behaviour are:

* Allocator - Determines how the beacon's Reflective loader allocates memory 
* Minimum Allocation - Minimum amount of memory to request for injected content
* Userwx - Ensures shellcode does not use Read, Write Execute permissions (The alternative is RW)
* Startrwx - Use Read, Write Execute as initial permissions for injected content (The alternative is RW)
* Drip Loading - Enables drip-loading for process injection, allocating memory in small chunks. Configurable delay between chunks via InjectDriploadDelay
* Transformer - Adds a block of padding content injected by the beacon
* Execute - This section determines how to execute the injected code

### Post-Ex
This part of your profile controls how the beacon handles post-exploitation modules and commands. Some of the features used to modify the behaviour are:

* Spawnto - Determines the default temporary process beacon will spawn for its post-exploitation command and options
* Obfuscate - Obfuscates the import table of the reflective DLL
* Smart Inject - Pass key function pointers from beacon to its child jobs (moved from stage to post-ex in CS 4.13)
* AMSI disable - Disable AMSI for powerpick, execute-assembly, and psinject (Certain EDRs can detect this best avoid using these tools)
* Keylogger - Determines how the keystroke logging API is used to capture keystrokes
* Cleanup - Cleans up the post-ex User Defined Reflective DLL ("UDRL") memory when the post-ex DLL is loaded
* Threadhint - Allows post-ex DLLs to spawn threads with a spoofed start address


### Profiles
Currently SourcePoint provides you with 7 baked in options for HTTP/HTTPS traffic profiles, based on existing profiles. Of these 7, 4 of them are influenced by and based on:
* Microsoft Window's Update Communication
* Slack's Message Communication
* Gotomeeting's Active Meeting Communication 
* Microsoft Outlook's Email Communication

3 of the profile options (5, 6 and 7) are designed specifically for:
* Cloudfront.net
* AzureEdge.net

The last option (8) is designed to input a custom profile. This option is designed to allow an operator to utilize a completely custom traffic profile. There are many cases where a completely unique traffic profile will yield high success rather than one of these. This also allows operators to still utilize SourcePoint's malleability features with their go-to or favorite traffic profile. As this allows for unique profiles it's important to ensure you tweak and adjust the profile for SourcePoint to work. At a minimum:
* Replace - `header "Host" "acme.com";` with `header "Host" "{{.Variables.Host}}";`
* Replace - `/pathtolegitpage/` under the GET field with `{{.Variables.HTTP_GET_URI}}`
* Replace - `/pathtolegitpage/` under the POST field with `{{.Variables.HTTP_POST_URI}}`


To do so, use the following options `-Customuri` and `-ProfilePath` along with `-Profile 8`. To use a different URI base for GET and POST, `-CustomuriGET` and  `-CustomuriPOST` should be used in place of `-Customuri`. While developing a profile, it's highly recommended to use the native ./c2lint to verify everything is working. 

### Redirector Rules

When a profile is generated, SourcePoint automatically outputs Apache mod_rewrite `RewriteCond` rules matching the selected profile's URI patterns. These are ready to use in an Apache or Nginx redirector configuration to forward only matching beacon traffic to the team server and redirect everything else to a legitimate site.

Example output for the Slack profile:
```
[*] For redirector (if in use):
	# Profile: Slack
	RewriteCond %{REQUEST_URI} ^/messages/[A-Za-z0-9-]{5,} [NC]
```

## Sample Yaml Config

```yaml
Stage: "False"
Host: "acme-email.com"
Keystore:
Password:
Metadata: "base64url"
Injector: "VirtualAllocEx"
Outfile: "test.profile"
PE_Clone: 20
Profile: 4
Allocation: 5312
Jitter: 30
Debug: true
Sleep: 35
Uri: 3
Useragent: "Win10Chrome"
Post-EX Processname: 11
Datajitter: 40
Keylogger: "SetWindowsHookEx"
Customuri:
CustomuriGET:
CustomuriPOST:
CDN:
CDN_Value:
ProfilePath:
Syscall_method:
Httplib: winhttp
ThreadSpoof: True
Forwarder: False
TasksMaxSize:
TasksProxyMaxSize:
TasksDnsProxyMaxSize:
EafBypass: True
RdllUseSyscalls: True
CopyPEHeader: True
TransformObfuscate: "lznt1,xor \"32\""
SmartInject: True
BeaconGate: "All"
SleepMask: True
RdllUseDriploading: False
RdllDriploadDelay:
CheckinDelay:
InjectUseDriploading: False
InjectDriploadDelay:
StartRWX: True
```

## CS 4.13 Compatibility Notes

This fork has been updated for Cobalt Strike 4.13 compatibility. The following changes were made:

**Removed options (no longer valid in CS 4.13):**
* `RdllLoader` - Removed. The StompLoader architecture was removed in CS 4.12; PrependLoader is now the only loader and is used by default.
* `smartinject` in the stage block - Moved exclusively to the `post-ex` block (controlled via `-SmartInject` flag / `SmartInject` YAML key).
* `set name` in PE cloning - Removed from the stage block. PE header cloning still works via checksum, compile_time, entry_point, image_size, and rich_header fields.

**New options added:**
* `CheckinDelay` - Delays Beacon's initial check-in to break detection heuristics on reflective loading.
* `RdllUseDriploading` / `RdllDriploadDelay` - Enables drip-loading technique for the RDLL, allocating many small memory chunks instead of one large block.
* `InjectUseDriploading` / `InjectDriploadDelay` - Enables drip-loading for process injection.

**Bug fixes:**
* Fixed `CDN_Value` not being wired from YAML config to profile generation.
* Fixed off-by-one in random user agent selection that excluded the last Mac UA.
* Fixed duplicate `compile_time` and `entry_point` fields in PE clone #5 (DIAGCPL.dll).
* Removed debug print statement that leaked `TasksMaxSize` to stdout.
* Added `Win10Firefox` as a user agent selection option.
* Updated user agent strings with Chrome 136/137, Firefox 137/138, Edge 135-137, Safari 18.4 versions.
* Fixed WindowsUpdate profile (1) `http-post` uri-append collision between `id` and `output` blocks.
* Fixed WindowsUpdate profile (1) URI length exceeding 63-byte limit.
* Fixed GoToMeeting profile (3) extra closing brace causing mismatched braces error.
* Fixed GoToMeeting profile (3) duplicate `http-stager` URIs (x86/x64 now use different random values).
* Fixed GoToMeeting profile (3) `Content-Type` header in `http-config` block (not allowed by c2lint).
* Fixed PE clone `image_size` values for 11 entries that were too small for CS 4.13 beacon DLLs (x86 minimum 372736, x64 minimum 462848).
* Added missing `image_size_x86`/`image_size_x64` fields to 4 PE clone entries that lacked them.
* Fixed off-by-one in random selection for Post-EX process names (last entry `svchost.exe` was never picked).
* Fixed off-by-one in random selection for SSH banners (only 4 of 8 banners were ever used).
* Fixed off-by-one in random selection for pipe names (last entry never picked).
* Fixed off-by-one in random selection for thread hints (last entry never picked).
* Fixed off-by-one in random selection for Magic PE values (last entry never picked).

## SSL Certificate

Profiles mode 1-4 can be used without a valid SSL, SourcePoint will generate a self-signed certificate related to the profile type. However, valid SSL certificates are extremely important the success of any type of C2. For many reasons but obviously no certificate means the traffic is going to be unencrypted (i.e. HTTP WHICH SHOULD NEVER BE USED) but using a self-signed cert comes with its obvious limitations. Certbot/LetsEncrypt and converting to a .store is sufficient.
