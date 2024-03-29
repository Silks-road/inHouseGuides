# Callguard Hosted Panel Setup Guide : Part 1

The following is a project environment setup and installation guide, for developerss who are unfamiliar with Eckoh's **Callguard Hosted Panel** (CGH) project.

**CGHP Part 1** covers setup for the following:

1. Prerequisites & System Requirements
2. Import & local setup
3. Config.xml.install

## Prerequisites & System Requirements

Due to company wide PCI compliance standard procedures, please make sure you first have all the pre-approved company security software installed, and VPN access routes on your computer. This should have been part of your standard set up and induction upon first joining Eckoh. If you are unsure your computer meets full compliance standards, please see a member of the Network Security department before going any further.

Regarding the CG project specifically, this should include access to the following:

- The DEV and UAT databases.
  - *While MySQL is the preferred in-house database management system, it is not a prerequisite as such and you may use another compatible tool should you so wish.*
- VPN access to your departments relevant company servers.
- Account access to the Mande servers project.
- Account access to the Holly Management System.
- General understanding of JS, XML, PHP and GitHub.

### Import & local setup
---

Once you have the go ahead from your Project Manager please begin as follows:

You should already have access to the Dev servers you need as per the Prerequisites & System Requirements section above.

Following this please SSH into the company Dev servers, type in your credentials, and move into your pre-existing Developer Sandbox.

    ssh hhdevapp01.dev.eckoh.com
    user.name: ada.lovelace@eckoh.com
    password: **********
    cd /srv/share/sites/ada.lovelace/callguardProjects

#### Naming conventions & paths

Once in your Sandbox, create an _appropriately named_ directory for your soon to be forked project.

It is company practice to name your local project and project pathway, displayed the same way as shown in the client Github repo you will fork from. Please make sure to check with the [new company naming conventions](https://confluence.eckoh.com/pages/viewpage.action?spaceKey=PD&title=Development+Lifecycle) for best practices if you are unsure.

>**NOTE**: In some rare cases, your CGH client repo may still be hosted on SVN. Should this be the case, follow the procedures outlined [here](linktomydocsexplainingSVNmigration) in order to correctly migrate the project over to Github before going any further.

Once you can confirm your client is on Github, [fork](https://help.github.com/en/articles/fork-a-repo) the repo. Your local CGH project and pathway should take on the end two pathnames from the Github repo itself:

https://github.com/Eckoh/{company-brand}/{organisation-name}/{CGH-type}

https://github.com/Eckoh/shopping-channel/{clothing-line}/{callguard-panel}

Therefore your local directory project should resemble something like:

`pwd /srv/share/sites/ada.lovelace/callguardProjects/clothing-line/callguard-panel`

Next clone your forked repo and create a feature branch of the client Github repository you have been assigned to.

Feature branches can be named as you deem appropriate so long as they stay relevant to the project at hand.

```
  mkdir clothing-line clothing-line/callguard-panel
  cd clothing-line/callguard-panel
  git clone https://github.com/Eckoh/ada.lovelace/clothing-line/callguard-panel.git .
  git checkout feature/callguard-panel-update
```

#### Assets folder

Check if your local directory has imported an `assets` folder. It is usually found in the httpdocs directory: `callguard-panel/httpdocs/assets`, and should contain images, css files etc.

Some projects depending on their age, may not have one and you will therefore need to either import or copy an assets folder from a previous project you've worked on, or from another online CGH repository.

#### Cleanup & copy

Delete ALL the `.idea` folders and files within your local copy, and check for any remnant of `.svn` files within:

`rm -rf *.idea *.svn`

>**NOTE**: You may on occasion come across an “export” folder, with an “export.xml.install” file within... For the most part you can ignore this, but it is best to double check... Normally you would find this folder and file in the IVR section of the CGH projects, instead of the Panel. However if the IVR is configurable then you would find it in the Panel conf folder as well. On occasions it is also found in the API and Web versions depending on the client and situation. For more info search for export module and ETL in the company [Wiki](https://wiki.eckoh.com/export-module/).


### Config.xml.install
---

Open your text editor and go to your `conf.xml.install` file.

#### Client No. & Service ID tags

Access the Dev database and locate both your relevant **Client Number** and **Service ID**.

>**NOTE**: If you are unsure which client number or service ID is relevant, or cannot find these in the Dev database, follow the [database access guide](deadlink).

Once you have your client number (and service ID), locate all the `<CLIENT-##>` tags within this file. They will either already have the relevant client number attached, or have the Dev Database test number (21). Update as appropriate.

```
  </CLIENT-21> <!-- used only for setup: REMOVE &/ REPLACE as appropriate for project —>
```

This includes updating the `</CLIENT-##>` tags within the `<UAT>` and `<PROD>` sections also:

```xml
  <UAT extends="DEV">
    <CLIENT-##>
    </CLIENT-##>
  </UAT>
...
  <PROD extends="UAT">
    <CLIENT-##>
    </CLIENT-##>
  </PROD>
```

Repeat this process for the service ID tags:

```php
  </SERVICE-ID-21> <!-- used only for setup: REMOVE &/ REPLACE as appropriate for project —>
```

#### Error logger

Change the error email logger to your own email address and delete the verbose, fancy, and location DEV tags.

These are usually held within the same `<errorReport>` tags but may be in various locations throughout the config file so please make sure you do a thorough search:

```xml
  <errorReport>
    <mailto>your.name@eckoh.com</mailto>
    <!-- DELETE <verbose>1</verbose> These are automatically disabled in higher environments -->
    <!-- DELETE <fancy>1</fancy> Fancy reporting only available for verbose reporting -->
    <!-- DELETE <location>DEV</location> -->
  </errorReport>
```

#### Assets location

Within your `conf.xml.install` you must change your `assets` location to its default location within the `<SIT></SIT>` section of your config file.

You can find the pre-exsisting client [Mande](deadlink) URL, either by going directly through the Mande application itself or via the SIT servers:

```ssh hhccdevweb21.dev.eckoh.com
ssh hhccdevweb21.dev.eckoh.com
cd /srv/share/sites/Mande/mande/
ll
  ...
  aaaaa-cgh-panel.2.3.1.eckoh.com
  bbbbb-cgh-panel.4.1.1.eckoh.com
  clothing-line-cgh-panel.1.3.8.eckoh.com
  ddddd-cgh-panel.2.1.1.eckoh.com
  ddddd-cgh-panel.2.7.0.eckoh.com
  eeeee-cgh-panel.3.2.1.eckoh.com
  ...
cd clothing-line-cgh-panel.1-3-8.eckoh.com
pwd
/srv/share/sites/shopping-channel/clothing-line-cgh-panel.1-3-8.eckoh.com
```

Copy your URL path and paste it into your `location` tags, with the `assets` folder included.

Your location tags should end up look something like this:

```xml
  <SIT extends="DEV">
    <CLIENT-##>
      ...
      	<assets>
    			<location>/srv/share/sites/shopping-channel/clothing-line-cgh-panel.1-3-8.eckoh.com/assets/</location>
			  </assets>
      ...
    </CLIENT-##>
  </SIT>  

```

#### CSS location

Check that the  `css` tags are set to `default`.

>**NOTE**: Sometimes they will still misdirect, so you may have to use your local path instead.

```xml
  <style>
    <css>default</css>
  </style>
```

#### Query strings

Remove all instances of query strings/ question marks from the validation fields i.e. ``}?$ = }$`` as they are no longer relevant to the CGH verification tokens.

#### Logging

Print your working directory root pathway, and create then create a log directory to hold said project logs:

```git
pwd /srv/share/sites/ada.lovelace/callguardProjects/clothing-line/callguard-panel
mkdir /srv/share/service_files/clothing-line/callguard-panel/logs
```

#### Config.xml

Once this is completed, make a copy of the `conf.xml.install` file **WITHOUT the extention**, including all content:

```
cp config.xml.install config.xml
```

While you are here make sure you check and update the`location` tags within `assets` are correct, i.e directed towards your own path instead of the Eckoh Mande URL:

```xml
  <assets>
    <location>/assets/</location>
  </assets>
```



------

[CGHP: Part 2](https://github.com/Silks-road/inHouseGuides/blob/master/callguard/linktopart2)
