# otobo-dark-skin
A dark skin for OTOBO

![OTOBO Dark Skin](/screenshot.png?raw=true)

OTOBO is a fork based on the ((OTRS)) Community Edition.

https://otobo.de

## Motivation
At the time of this release, only one default skin is included in OTOBO, and the colors used there are way too bright and shiny for me personally. So I decided to create a dark skin for OTOBO based on the files included in the default skin.

It's possible that it doesn't work well with all add-on packages, since I focused exclusively on packages I use, which are the following so far:
- FAQ
- Survey

## Installation
Copy the files of this repository to ```$OTOBO_HOME/var/httpd/htdocs/skins/Agent/otobo-dark-skin``` and adjust the permissions.

**Example:**
```
chown -R otobo:www-data $OTOBO_HOME/var/httpd/htdocs/skins/Agent/otobo-dark-skin
```

Then create the file ```$OTOBO_HOME/Kernel/Config/Files/XML/CustomSkin.xml``` with the following contents:
```
<?xml version="1.0" encoding="utf-8" ?>
<otobo_config version="2.0" init="Application">
        <Setting Name="AgentLogoCustom###otobo-dark-skin" Required="0" Valid="1">
                <Description Translatable="1">The logo shown in the header of the agent interface for the skin "OTOBO Dark". See "AgentLogo" for further description.</Description>
                <Navigation>Frontend::Agent</Navigation>
                <Value>
                        <Hash>
                                <Item Key="URL">skins/Agent/otobo-dark-skin/img/your_logo.png</Item>
                                <Item Key="StyleTop">16px</Item>
                                <Item Key="StyleRight">24px</Item>
                                <Item Key="StyleHeight">60px</Item>
                                <Item Key="StyleWidth">194px</Item>
                        </Hash>
                </Value>
        </Setting>
        <Setting Name="Loader::Agent::Skin###001-otobo-dark-skin" Required="0" Valid="1">
                <Description Translatable="1">OTOBO Dark Skin</Description>
                <Navigation>Frontend::Base::Loader</Navigation>
                <Value>
                        <Hash>
                                <Item Key="InternalName">otobo-dark-skin</Item>
                                <Item Key="VisibleName" Translatable="1">OTOBO Dark Skin</Item>
                                <Item Key="Description" Translatable="1">A dark skin for OTOBO</Item>
                                <Item Key="HomePage">www.example.com</Item>
                        </Hash>
                </Value>
        </Setting>
</otobo_config>
```
Don't forget to adjust the logo and homepage parameters according to your needs.

Now execute the following command as "otobo" user:
```
$OTOBO_HOME/bin/otobo.Console.pl Maint::Config::Rebuild
```

If you want this skin to be the default one for all new users, change the following system configuration setting to ```otobo-dark-skin```:
```
Loader::Agent::DefaultSelectedSkin
```

Now you should be able to switch to this new skin in your personal settings.
