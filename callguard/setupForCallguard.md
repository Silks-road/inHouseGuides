# Setting up your local Callguard Hosted Project

The following is a project environment setup and installation guide, for Devs who are completely unfamiliar with Eckoh's Callguard Hosted project (CGH).

Please note that due to the complexity of this legacy code project, and some of the individual file sizes themselves (i.e. the main project file being over 2200 lines long); each section below holds as much relevant information as possible per section in order to help navigate new Developers around the inherent pitfalls within said project.

As such, should you simply wish to be reminded of the most basic installation requirements, you may prefer to use the previous guide still available on the old company Wiki page. Though please be aware that it also contains outdated information.

### Prerequisites & System Requirements

Due to company wide PCI compliance standard procedures, please make sure you first have all the pre-approved company security software installed, and VPN access routes on your computer. This should have been part of your standard set up and induction upon first joining Eckoh. If you are unsure your computer meets full compliance standards, please see a member of the Network Security department before going any further.

Regarding the CG project specifically, this should include access to the following:

* Company DEV and UAT databases.

    * _While [MySQL](https://www.mysql.com/) is the preferred in-house database management system, it is not a prerequisite as such and you may use another compatible tool should you so wish._
* VPN access to your departments relevant company servers.
* Account access to the Mande project for deployment.
* Account access to the Holly Management System for testing.

### Callguard Hosted Project Overview

#### Understanding CGH

CGH is an Eckoh product which has been designed to remove all (or part of) company contact centres from the annual scope of the PCI DSS audit process – which in turn simplifies the compliance burden itself for the company in question.

<span style="color: #9E9E9E;"> _"...The Callguard project itself has many features to meet your company PCI compliant needs. Phone DTMF tones are intercepted by Eckoh, capturing the card data safely within our hosted environment. Agents can see card payment progress, but not the details themselves..."_</span>

CallGuard is PCI DSS Level One compliant, and no equipment is deployed on premises - it is completely software based. Tokenisation allows for repeat payments, and whether a company is using fully Hosted, On-Demand or On-Site versions of CGH, no changes are necessary within existing company infrastructures or networks.

**As a Developer, the most important information you need to understand is that the Callguard aspect of the project you are working on, is actually hosted BEHIND the browser panel that you see. Technically speaking, the visual panel and CGH are actually SEPARATE aspects of the same project.**

Added to this, due to the previous lack of naming consistency within Eckoh, and that the browser panel and CGH  are so closely interlinked; you may find individuals within Eckoh refer to them interchangeably, combined, or even under completely different names. Some older running projects still have naming inconsistencies within them, so bare this in mind when discussing CGH with your fellow Devs or project team.

All of the following examples can and may refer to the Eckoh CGH project: Config Panel, CGH, The Panels, Callguard Hosted Panel, Configurable Panel, Bespoke Panel, etc.  

### Import & Setup

Once you have the go ahead from your Project Manager begin as follows:

#### Access

You should already have access to the Dev servers you need as per the Prerequisites & System Requirements section above.

First SSH into the company Dev servers, type in your credentials, and move into your pre-existing Dev Sandbox.

    ssh hhdevapp01.dev.eckoh.com
    user.name: ada.lovelace@eckoh.com
    password: **********
    cd /srv/share/sites/ada.lovelace/callguardProjects

#### Naming conventions & paths

Once in your Sandbox, create an _appropriately named_ directory for your locally forked project.

It is company practice to name your local project the same way as the Github pathway is displayed, for the client repo that you intend to fork from. Please make sure to check with the [new company naming conventions](https://confluence.eckoh.com/pages/viewpage.action?spaceKey=PD&title=Development+Lifecycle) for best practices if you are unsure.

>**NOTE**: In some rare cases, your CGH client repo may still be hosted on SVN. Should this be the case, follow the procedures outlined [here](linktomydocsexplainingSVNmigration) in order to correctly migrate the project over to Github before going any further.

Once you can confirm your client is on Github, [fork](https://help.github.com/en/articles/fork-a-repo) the repo. Your local CGH project and pathway should take on the end two pathnames from the Github repo itself:

https://github.com/Eckoh/{company-brand}/{organisation-name}/{CGH-type}

https://github.com/Eckoh/shopping-channel/{clothing-line}/{callguard-panel}

Therefore your local directory project should resemble something like:

`pwd /srv/share/sites/ada.lovelace/callguardProjects/clothing-line/callguard-panel`

Next clone your forked repo and create a feature branch of the client Github repository you have been tasked to work on.

Feature branches can be named as you deem appropriate so long as they stay relevant to the project at hand.

```
  mkdir clothing-line clothing-line/callguard-panel
  cd clothing-line/callguard-panel
  git clone https://github.com/Eckoh/ada.lovelace/clothing-line/callguard-panel.git .
  git checkout feature/callguard-panel-update
```

#### Assets folder

Check if your local repo has imported an assets folder. It is usually found in the httpdocs directory: `callguard-panel/httpdocs/assets`, containing images, css files etc.

Some projects depending on their age, may not have one and you will therefore need to either import or copy an assets folder from a previous project you've worked on, or from another online CGH repo.

#### Cleanup & copy

Delete ALL the the `.idea` folders and files within your local copy, and check for any remnant of `.svn` files within:

`rm -rf .idea svn`

Now go to `vhost` folder within said project, and make a copy of the vhost file **WITHOUT the extention**, including all content:

    cd vhost
    pwd ...clothing-line/callguard-panel/vhost
    cp vhost.conf.install vhost.conf

Do the same again in your `conf` folder for both you config & syndication files, again with file extensions removed:

>**NOTE**: You may on occasion come across an “export” folder, with an “export.xml.install” file within... For the most part you can ignore this, but it is best to double check... Normally you would find this folder and file in the IVR section of the CGH projects, instead of the Panel; but if the IVR is configurable then you would find it in the Panel conf folder as well. On occasions it is also found in the API and Web versions depending on the client and situation. For more info search for export module and ETL in the docs or follow this [link](https://wiki.eckoh.com/export-module/)

    cd ../conf/
    cp config.xml.install config.xml
    cp syndication.xml.install syndication.xml

Print your file path and copy the path displayed and SAVE it - you will need it for updating the config in the next section

`pwd /srv/share/sites/ada.lovelace/callguardProjects/clothing-line/callguard-panel`

/////////////////////////////////////////////////////////////////////////////////////////
