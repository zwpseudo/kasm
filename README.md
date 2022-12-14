# KasmVNC - Linux Web Remote Desktop

<a href="https://kasmweb.com"><img src="https://kasm-static-content.s3.amazonaws.com/logo_kasm.png" width="300"><a/>
  
[Kasm Technologies](https://www.kasmweb.com) developed Kasm Workspaces, the Containerized Streaming Platform. Kasm has open-sourced the Workspace docker images, which include containerized [full desktops and apps](https://github.com/kasmtech/workspaces-images) and [base images](https://github.com/kasmtech/workspaces-core-images) intended for developers to create custimized streaming containers. These containers can be used standalone or within the [Kasm Workspaces Platform](https://www.kasmweb.com) which provides a full Enterprise feature set. KasmVNC is used as the streaming tech for our container images, however, you can use KasmVNC for individual servers. While the term VNC is in the name, KasmVNC is not intended to remain compliant with the RFB spec and has different goals than other VNC projects:

  - Web-based - KasmVNC is designed to provide a web accessible remote desktop. It comes with a web server and websocket server built in. There is no need to install other components. Simply run and navigate to your desktop's URL on the port you specify. While you can still tun on the legacy VNC port, it is disabled by default.
  - Security - The RFB specification (VNC) limits the password field to 8 characters, so while the client may take a longer password, only the first 8 characters are sent. KasmVNC defaults to HTTPS with HTTP Basic Auth and disables the legacy VNC authentication method which is not sufficiently secure for internet accessible systems.
  - Simplicity - KasmVNC aims at being simple to deploy and configure.

# Releases

Since this is a fast evolving project, the documents on the tip of master are chaning rapidly and will not match releases. Be sure to use the README and other documentation from the release branch that matches the version of KasmVNC you are using. Do not use the README from the master branch, unless you are compiling KasmVNC yourself from the tip of master. All releases starting at 0.9.3 have a branch named in the format 'release/0.9.3', for example. 

# New Features!

  - Webp image compression for better bandwidth usage
  - Automatic mixing of webp and jpeg based on CPU availability on server
  - Multi-threaded image encoding for smoother frame rate for servers with more cores
  - [Full screen video detection](https://github.com/kasmtech/KasmVNC/wiki/Video-Rendering-Options#video-mode), goes into configurable video mode for better full screen videoo playback performance.
  - [Dynamic jpeg/webp image coompression](https://github.com/kasmtech/KasmVNC/wiki/Video-Rendering-Options#dynamic-image-quality) quality settings based on screen change rates
  - Seemless clipboard support (on Chromium based browsers)
  - Binary clipboard support for text, images, and formatted text (on Chromium based browsers)
  - Allow client to set/change most configuration settings
  - [Data Loss Prevention features](https://github.com/kasmtech/KasmVNC/wiki/Data-Loss-Prevention)
    - Key stroke logging
    - Clipboard logging
    - Max clipboard transfer size up and down
    - Min time between clipboard operations required
    - Keyboard input rate limit
    - Screen region selection
  - Deb packages for Debian, Ubuntu, and Kali Linux included in release.
  - RPM packages for CentOS, Oracle, OpenSUSE, Fedora. RPM packages are currently not updatable and not released, though you can build and install them. See build documentation.
  - Web [API](https://github.com/kasmtech/KasmVNC/wiki/API) added for remotely controlling and getting information from KasmVNC
  - Multi-User support with permissions that can be changed via the API
  - Web UI uses a webpack for faster load times.
  - Network and CPU bottleneck statistics
  - Relative cursor support (game pointer mode)
  - Cursor lock
  - IME support for languages with extended characters
  - Better mobile support

Future Goals:

  - UDP transport for faster frame rates
  - H264 encoding

### Installation

#### Debian-based

```sh
# Please choose the package for your distro here (under Assets):
# https://github.com/kasmtech/KasmVNC/releases
wget <package_url>

sudo apt-get install ./kasmvncserver_*.deb

# Add your user to the ssl-cert group
sudo addgroup $USER ssl-cert
# You will need to re-connect in order to pick up the group change

# On the first run, vncserver will ask you to create a KasmVNC user and choose a desktop
# environment you want to run. It can detect Cinnamon, Mate, LXDE, LXQT, KDE, Gnome,
# XFCE. You can also choose to manually edit xstartup.
# After you chose a desktop environment or to manually edit xstartup,
# vncserver won't ask you again, unless you run it as:
vncserver -select-de

# You can select a specific Desktop Environment like this:
vncserver -select-de mate

# Tail the logs
tail -f ~/.vnc/*.log
```

Now navigate to your system at the urls printed by `vncserver`.

To stop the KasmVNC you started earlier on display 10:

```sh
vncserver -kill <display_number>
```

Settings can be modified via editing `/etc/kasmvnc/kasmvnc.yaml` or `~/.vnc/kasmvnc.yaml`.

The options for vncserver:

| Argument | Description |
| -------- | ----------- |
| depth | Color depth, for jpeg/webp should be 24bit |
| geometry | Screensize, this will automatically be adjusted when the client connects. |
| websocketPort | The port to use for the web socket. Use a high port to avoid having to run as root. |
| cert | SSL cert to use for HTTPS |
| sslOnly | Disable HTTP |
| interface | Which interface to bind the web server to. |

### Development
Would you like to contribute to KasmVNC? Please reachout to us at info@kasmweb.com. We have investigated or are working on the following, if you have experience in these fields and would like to help please let us know.

Real-time H264 encoding using NVIDIA and Intel encoding technology.

Windows version of KasmVNC. We have been able to get it to compile for Windows and increased the performance, but still not releasable. Experienced Windows developers with a background in cross compiling would help.
  
ARM version of KasmVNC, we have had requests for this and at one point we did have an ARM build of KasmVNC but it takes dev cycles to mainain and bring it back to life.

### Compiling From Source
See the [builder/README.md](https://github.com/kasmtech/KasmVNC/blob/master/builder/README.md). We containerize our build systems to ensure highly repeatable builds.

### License and Acknowledgements
See the [LICENSE.TXT](https://github.com/kasmtech/KasmVNC/blob/master/LICENSE.TXT) and [ACKNOWLEDGEMENTS.MD](https://github.com/kasmtech/KasmVNC/blob/master/LICENSE.TXT)
