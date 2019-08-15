# Callguard Hosted Panel Specific Setup Guide

The following is a project environment setup and installation guide, for developerss who are unfamiliar with Eckoh's **Callguard Hosted Panel** (CGH) project.

Please note that due to the complexity of this legacy code project, and some of the individual project file sizes (i.e. the main project file being over 2200 lines long); each section holds as much relevant information as possible per section, in order to help new Developers naviagte around the inherent pitfalls within said project. This is also why the setup guide has been divided into subsections.

As such, should you simply wish to be reminded of the most basic installation requirements, you may prefer to use the [previous guide](deadlink) still available on the old company Wiki page. However please be aware that it also contains outdated information.

> **NOTE**: The CGH Web and/ or Integrated Voice Recognition (IVR) project setup guides can be found [here](deadlink). Again, please be aware that some of the information in these guides is now outdated.



##The Callguard Hosted project overview

###Understanding CGH

CGH is an Eckoh product which has been designed to remove all (or part of) company contact centres from the annual scope of the PCI DSS audit process – which in turn simplifies the compliance burden itself for the company in question. It is available in Web, IVR, and Panel format (the latter of which this article focuses on).

<span style="color: #9E9E9E;"> _"...The Callguard project itself has many features to meet your company PCI compliant needs. Phone DTMF tones are intercepted by Eckoh, capturing the card data safely within our hosted environment. Agents can see card payment progress, but not the details themselves..."_</span>

CallGuard is PCI DSS Level One compliant, and no equipment is deployed on premises - it is completely software based. Tokenisation allows for repeat payments, and whether a company is using fully Hosted, On-Demand or On-Site versions of CGH, no changes are necessary within existing company infrastructures or networks.

**As a Developer, the most important information you need to understand is that the Callguard aspect of the panel project you will be working on, is actually hosted BEHIND the browser panel that you see. Technically speaking, the visual panel and CGH are actually SEPARATE aspects of the same project.**

Added to this, due to the previous lack of naming consistency within Eckoh, and that the browser panel and CGH  are so closely interlinked; you may find individuals within Eckoh refer to them interchangeably, combined, or even under completely different names. Some older running projects still have naming inconsistencies within them so bare this in mind when discussing CGH with your fellow Devs or project team.

_All of the following examples can and may refer to the Eckoh CGH project: Config Panel, CGH, The Panels, Callguard Hosted Panel, Configurable Panel, Bespoke Panel, etc._



Please read through the setup guide carefully and defer to either the company [Wiki](deadlink) site or your manager should you have any further questions.

### 