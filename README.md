# Oracle Integration Cloud: The Tutorial

This document shows how to use Oracle Integration Cloud (OIC) at the very basic level.


## Purpose

Before you get started, please note that this tutorial is **meant for beginners**. Every step builds on all previous steps, so if you understand a step feel free to skip that step -- please still read all of this document to make sure you did not miss any key configuration steps. Here is a more detailed list of what this tutorial will cover:
- How to navigate to and from OIC, starting from the cloud login dashboard
- How to build a connection
- How to create and run a simple integration: REST endpoints
- How to track your integration instance
- Locations of various important pieces of information
	- e.g. Activity Log, Variable Tracking

Here is what you'll need for the tutorial that is **NOT** covered in this tutorial (i.e. prerequisites):
- Oracle Cloud tenancy
	- You can create a free trial account [starting here](https://www.oracle.com/cloud/free/). There will be a step in which you will need to provide your credit card information. This is for identity purposes; other FAQs are answered [here](https://www.oracle.com/cloud/free/faq.html).
- An application to integrate with (this is provided, but feel free to try to connect OIC to your own application after you complete this tutorial)

By the end of this tutorial, it is expected that you will be able to create your own integrations and know where to get help if you get stuck. Don't be afraid to search the internet for a specific error, the REST API catalog on OIC, or just general information on something you noticed while playing around with the OIC dashboard.


# Let's get started

## **STEP 1**: Navigating to and from OIC

In this step, you will navigate to and from OIC. You will need to travel along this path: (Oracle cloud)->(cloud dashboard)->(integration instance page)->(OIC home)->(integration dashboard). The multiple layers of nesting are for security reasons and/or due to the numerous PaaS products Oracle has to offer and/or the whims of the architects of the OCI gen 2 console, idfk.

### 1.1: Logging in to Oracle Cloud (OCI)
<!-- **NOTE**: Oracle, just like any other big business, is infamous for its numerous acronyms, of which number far more than its multi-thousand products. OCI refers to the cloud, usually the Gen 2 cloud (see the keynote addresses for Oracle Open World (OOW) 2016), whereas OIC refers to _integration_ cloud. Yes it's confusing but we get by and also we love our TLAs - three-lettered acronyms. We could have made it OCIPASS: Oracle Cloud Infrastructure, Platform, and Software Services. But who has time to read seven letters?? -->
- Open a web browser and navigate to [cloud.oracle.com](cloud.oracle.com).
<img src="images/OIC-1.01.png" width="100%" title="Oracle cloud home page">
- Enter the name of your account/tenancy.
<img src="images/OIC-1.02.png" width="100%" title="Also known as your identity domain">
- Enter your credentials for either basic authentication/user or using a federated account (i.e. Oracle SSO).
<img src="images/OIC-1.03.png" width="100%" title="username user.name@email.com, password password is NOT a default user/pass combination for OCI">

### 1.2: Navigating to the Integration Dashboard
- Once you login to your cloud tenancy, you will arrive at one of three pages: the PaaS dashboard, IaaS dashboard, or the classic dashboard.
	- If the Integration link appears for you (first image) then you can click **Integration**. Otherwise you can navigate to the same page by selecting the hamburger menu on the top left corner (it looks like three horizontal lines stacked vertically, or a capital Greek Xi Ξ in some type faces) and selecting **Integration** (second image). Note: this might take you to an intermediate page in which you will have to click **Open Service Console** (third image).
	<img src="images/OIC-1.04.png" width="100%" title="Platform Services dashboard">
	<img src="images/OIC-1.05.png" width="100%" title="PaaS to Integration via hamburger menu">
	<img src="images/OIC-1.06.png" width="100%" title="Open Service Console">
	- Alternatively, you might find yourself at the IaaS dashboard (first image). In that case, select the hamburger menu on the top left corner, scroll down to **Platform Services**, and select **Integration** (second image). This may open a new tab or window.
	<img src="images/OIC-1.07.png" width="100%" title="Infrastructure Services dashboard">
	<img src="images/OIC-1.08.png" width="100%" title="IaaS to Integration via hamburger menu">
	- TODO classic part
	<!-- - Finally, if you arrived at the classic dashboard...you screwed up. Game over. Just give up now. I don't usually say that OCI classic sucks but when I do I mean it. There's a whole multitude of memes I could make revolving around the fact that OIC classic is an embarrassment to Oracle that will make even the most design- and utilitarian-deaf wonder: is this a professional webpage? Actually, if you come here just try one of the webpages that you see in the previous 5 images, replacing my information with your information, and maybe one of them will work. -->
- Finally you will arrive at the Integration Instance page. It looks like this:
<img src="images/OIC-1.09.png" width="100%" title="Integration Instance page">
- If you see an instance you are authorized to create test integrations on, skip this step. Otherwise you will need to provision an OIC instance. Click **Create Instance** and fill in the details however you want with these constraints:
	- Satisfy all items that have an asterisk \* next to them.
	- Select your home region.
	- Make sure you select the proper license type: check with your Oracle representative and/or confirm that you own an integration software license (remember: THIS COSTS MONEY).
	- Leave the Details page as its defaults, selecting an integer between 1 and 3 for "Number of 20K Messages Per Hour Packs". You may opt to choose "Integration and Process" if you have purchased the Enterprise edition and if you plan on creating process automation some time in the future (e.g. with process applications and decision models), but this is potentially more expensive.
- Here's an example:
<img src="images/OIC-1.10.png" width="100%" title="Provisioning instance page 1">
<img src="images/OIC-1.11.png" width="100%" title="Provisioning instance page 2; defaults selected">
<img src="images/OIC-1.12.png" width="100%" title="Provisioning instance page 3">

**NOTE**: this instance was not actually created. For the remainder of this tutorial, all future graphics refer to the "OIC-NE-SC" instance.
- Once your instance is provisioned, you will see that the instance is ready to use. To navigate to OIC home, click the small hamburger menu indicated by the red arrow in the below image, then click **Open Oracle Integration Home Page**. You should see a similar screen as shown in the second image
<img src="images/OIC-1.13.png" width="100%" title="Navigating to OIC home">
<img src="images/OIC-1.14.png" width="100%" title="OIC home">
- Finally, click the hamburger menu in the upper left corner and select **Integrations**. This brings you to the Integration Dashboard. You may see only the sample integrations that are always included in every Integration instance.
<img src="images/OIC-1.15.png" width="100%" title="Navigating to Integration dashboard">
<img src="images/OIC-1.16.png" width="100%" title="Integration dashboard">


## **STEP 2**: Connections

A **connection** is 


## **STEP 3**: Integration components


## **STEP 4**: Build an integration


## **STEP 5**: Run and Track the integration


## Miscellaneous important information within OIC

### Activity Log

### Variable Tracking

### Designer menu vs Monitoring menu

