---
hide:
  - toc
---
???+ danger
    
    **Quickstart is in early development.** Please provide feedback via the 
    [quickstart-feedback Discord channel](https://discord.com/channels/822460010649878528/1335372922306695198)

    Quickstart is incomplete in that it does not expose every possible setting in `config.yml`.
    
    Notably, template variables on the default collections are not available, so you cannot generally modify the behavior of the default collections within Quickstart.

    Quickstart also does not provide any support for manipulating external YAML files like collection, overlay, and metadata files.
    

{%
  include-markdown "https://raw.githubusercontent.com/Kometa-Team/Quickstart/refs/heads/develop/README.md"
  comments=false
  start="<!--logo-start-->"
  end="<!--logo-end-->"
  rewrite-relative-urls=false
%}

{%
  include-markdown "https://raw.githubusercontent.com/Kometa-Team/Quickstart/refs/heads/develop/README.md"
  comments=false
  start="<!--body1-start-->"
  end="<!--body1-end-->"
  replace='{
    "(docs/plex-security.md)": "(https://github.com/Kometa-Team/Quickstart/blob/develop/docs/plex-security.md)",
    "(#-features)": "(#features)",
    "(#config-management--history)": "(#config-management-history)",
    "(#live-previews--assets)": "(#live-previews-assets)",
    "(#themes--personalization)": "(#themes-personalization)",
    "(#logscan-analyzer--analytics-page)": "(#logscan-analyzer-analytics-page)",
    "(#support--troubleshooting)": "(#support-troubleshooting)",
    "(#data--privacy-quickstart)": "(#data-privacy-quickstart)",
    "(#1---installing-on-windows)": "(#1-installing-on-windows)",
    "(#2---installing-on-mac)": "(#2-installing-on-mac)",
    "(#3---installing-on-ubuntu-linux)": "(#3-installing-on-ubuntu-linux)",
    "(#4---running-in-docker)": "(#4-running-in-docker)",
    "(#5---installing-locally)": "(#5-installing-locally)",
    "(#debugging--changing-ports)": "(#debugging-changing-ports)"
}'
  rewrite-relative-urls=false
%}

???+ danger

    **We strongly recommend running this yourself rather than relying on someone else to host Quickstart.**

    This ensures that connection attempts are made exclusively to services and machines accessible only to you. Additionally, all credentials are stored locally, safeguarding your sensitive information from being stored on someone else's machine.

{%
  include-markdown "https://raw.githubusercontent.com/Kometa-Team/Quickstart/refs/heads/develop/README.md"
  comments=false
  start="<!--body2-start-->"
  end="<!--body2-end-->"
  replace='{
    "(docs/plex-security.md)": "(https://github.com/Kometa-Team/Quickstart/blob/develop/docs/plex-security.md)",
    "(#-features)": "(#features)",
    "(#config-management--history)": "(#config-management-history)",
    "(#live-previews--assets)": "(#live-previews-assets)",
    "(#themes--personalization)": "(#themes-personalization)",
    "(#logscan-analyzer--analytics-page)": "(#logscan-analyzer-analytics-page)",
    "(#support--troubleshooting)": "(#support-troubleshooting)",
    "(#data--privacy-quickstart)": "(#data-privacy-quickstart)",
    "(#1---installing-on-windows)": "(#1-installing-on-windows)",
    "(#2---installing-on-mac)": "(#2-installing-on-mac)",
    "(#3---installing-on-ubuntu-linux)": "(#3-installing-on-ubuntu-linux)",
    "(#4---running-in-docker)": "(#4-running-in-docker)",
    "(#5---installing-locally)": "(#5-installing-locally)",
    "(#debugging--changing-ports)": "(#debugging-changing-ports)"
}'
  rewrite-relative-urls=false
%}

???+ tip

    You will likely need to perform these steps first to have a system tray icon show up:

    ```shell
    sudo apt update
    sudo apt install -y libxcb-xinerama0 libxcb-xinerama0-dev libxcb-icccm4 libxcb-image0 libxcb-keysyms1 libxcb-render-util0
    ```

{%
  include-markdown "https://raw.githubusercontent.com/Kometa-Team/Quickstart/refs/heads/develop/README.md"
  comments=false
  start="<!--body3-start-->"
  end="<!--body3-end-->"
  replace='{
    "(docs/plex-security.md)": "(https://github.com/Kometa-Team/Quickstart/blob/develop/docs/plex-security.md)",
    "(#-features)": "(#features)",
    "(#config-management--history)": "(#config-management-history)",
    "(#live-previews--assets)": "(#live-previews-assets)",
    "(#themes--personalization)": "(#themes-personalization)",
    "(#logscan-analyzer--analytics-page)": "(#logscan-analyzer-analytics-page)",
    "(#support--troubleshooting)": "(#support-troubleshooting)",
    "(#data--privacy-quickstart)": "(#data-privacy-quickstart)",
    "(#1---installing-on-windows)": "(#1-installing-on-windows)",
    "(#2---installing-on-mac)": "(#2-installing-on-mac)",
    "(#3---installing-on-ubuntu-linux)": "(#3-installing-on-ubuntu-linux)",
    "(#4---running-in-docker)": "(#4-running-in-docker)",
    "(#5---installing-locally)": "(#5-installing-locally)",
    "(#debugging--changing-ports)": "(#debugging-changing-ports)"
}'
  rewrite-relative-urls=false
%}
