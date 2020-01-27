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
	- You can create a free trial account [starting here](https://www.oracle.com/cloud/free/). There will be a step in which you will need to provide your credit card information. This is for identity purposes, and your card will never be charged without your approval; other FAQs are answered [here](https://www.oracle.com/cloud/free/faq.html). If you do create a free trial account, you do not have to worry about anything money related mentioned in this tutorial, and know that you have either 30 days or until your trial account money is used up to keep any non-free-tier items running on your trial account.
- An application to integrate with (this is provided, but feel free to try to connect OIC to your own application after you complete this tutorial)
- Basic Javascript and REST knowledge

By the end of this tutorial, it is expected that you will be able to create your own integrations and know where to get help if you get stuck. Don't be afraid to search the internet for a specific error, the REST API catalog on OIC, or just general information on something you noticed while playing around with the OIC dashboard.


# Let's get started

## **STEP 1**: Navigating to and from OIC

In this step, you will navigate to and from OIC. You will need to travel along this path: (Oracle cloud)->(cloud dashboard)->(integration instance page)->(OIC home)->(integration dashboard). The multiple layers of nesting are for security reasons and/or due to the numerous PaaS products Oracle has to offer and/or the whims of the architects of the OCI gen 2 console, idfk.

### 1.1: Logging in to Oracle Cloud (OCI)
<!-- **NOTE**: Oracle, just like any other big business, is infamous for its numerous acronyms, of which number far more than its multi-thousand products. OCI refers to the cloud, usually the Gen 2 cloud (see the keynote addresses for Oracle Open World (OOW) 2016), whereas OIC refers to _integration_ cloud. Yes it's confusing but we get by and also we love our TLAs - three-lettered acronyms. We could have made it OCIPASS: Oracle Cloud Infrastructure, Platform, and Software Services. But who has time to read seven letters?? -->
1. Open a web browser and navigate to [cloud.oracle.com](cloud.oracle.com).
<img src="images/OIC-1.01.png" width="100%" title="Oracle cloud home page">
2. Enter the name of your account/tenancy.
<img src="images/OIC-1.02.png" width="100%" title="Also known as your identity domain">
3. Enter your credentials for either basic authentication/user or using a federated account (i.e. Oracle SSO).
<img src="images/OIC-1.03.png" width="100%" title="username user.name@email.com, password password is NOT a default user/pass combination for OCI">

### 1.2: Navigating to the Integration Dashboard
1. Once you login to your cloud tenancy, you will arrive at one of three pages: the PaaS dashboard, IaaS dashboard, or the classic dashboard.
	1. If the Integration link appears for you (first image) then you can click **Integration**. Otherwise you can navigate to the same page by selecting the hamburger menu on the top left corner (it looks like three horizontal lines stacked vertically, or a capital Greek Xi Ξ in some type faces) and selecting **Integration** (second image). Note: this might take you to an intermediate page in which you will have to click **Open Service Console** (third image).
	<img src="images/OIC-1.04.png" width="100%" title="Platform Services dashboard">
	<img src="images/OIC-1.05.png" width="100%" title="PaaS to Integration via hamburger menu">
	<img src="images/OIC-1.06.png" width="100%" title="Open Service Console">
	2. Alternatively, you might find yourself at the IaaS dashboard (first image). In that case, select the hamburger menu on the top left corner, scroll down to **Platform Services**, and select **Integration** (second image). This may open a new tab or window.
	<img src="images/OIC-1.07.png" width="100%" title="Infrastructure Services dashboard">
	<img src="images/OIC-1.08.png" width="100%" title="IaaS to Integration via hamburger menu">
	3. TODO classic part
	<!-- 3. Finally, if you arrived at the classic dashboard...you screwed up. Game over. Just give up now. I don't usually say that OCI classic sucks but when I do I mean it. There's a whole multitude of memes I could make revolving around the fact that OIC classic is an embarrassment to Oracle that will make even the most design- and utilitarian-deaf wonder: is this a professional webpage? Actually, if you come here just try one of the webpages that you see in the previous 5 images, replacing my information with your information, and maybe one of them will work. -->
2. Finally you will arrive at the Integration Instance page. It looks like this:
<img src="images/OIC-1.09.png" width="100%" title="Integration Instance page">
3. If you see an instance you are authorized to create test integrations on, skip this step. Otherwise you will need to provision an OIC instance. Click **Create Instance** and fill in the details however you want with these constraints:
	- Satisfy all items that have an asterisk \* next to them.
	- Select your home region.
	- Make sure you select the proper license type: check with your Oracle representative and/or confirm that you own an integration software license (remember: THIS COSTS MONEY).
	- Leave the Details page as its defaults, selecting an integer between 1 and 3 for "Number of 20K Messages Per Hour Packs". You may opt to choose "Integration and Process" if you have purchased the Enterprise edition and if you plan on creating process automation some time in the future (e.g. with process applications and decision models), but this is potentially more expensive.

Here's an example:
<img src="images/OIC-1.10.png" width="100%" title="Provisioning instance page 1">
<img src="images/OIC-1.11.png" width="100%" title="Provisioning instance page 2; defaults selected">
<img src="images/OIC-1.12.png" width="100%" title="Provisioning instance page 3">
**NOTE**: this instance was not actually created. For the remainder of this tutorial, all future graphics refer to the "OIC-NE-SC" instance.

4. Once your instance is provisioned, you will see that the instance is ready to use. To navigate to OIC home, click the small hamburger menu indicated by the red arrow in the below image, then click **Open Oracle Integration Home Page**. You should see a similar screen as shown in the second image
<img src="images/OIC-1.13.png" width="100%" title="Navigating to OIC home">
<img src="images/OIC-1.14.png" width="100%" title="OIC home">
5. Finally, click the hamburger menu in the upper left corner and select **Integrations**. This brings you to the Integration Dashboard. You may see only the sample integrations that are always included in every Integration instance.
<img src="images/OIC-1.15.png" width="100%" title="Navigating to Integration dashboard">
<img src="images/OIC-1.16.png" width="100%" title="Integration dashboard">

**Note**: you should automatically be brought to the "Designer" menu. You can confirm this by selecting the upper left hamburger menu to bring up a grey left sidebar with seven items: Integrations, Connections, Lookups, Packages, Agents, Adapters, and Libraries. Please view the [Miscellaneous important information within OIC](#misc) section below for more information.


## **STEP 2**: Connections

A **connection** is a way for OIC to connect to some application, including third-party applications, applications running on Oracle software, or even other integrations on OIC. A connection is based off of an **Adapter**. By default, you should see under the list of Connections (upper-left hamburger menu -> Connections) that there are already some sample connections built, including but not limited to the **Sample REST Endpoint Interface**. You will use the **Sample REST Endpoint Interface** and you will also create your own connection. First, however, you will need to define what exactly OIC is connecting to.

At [https://oic101.herokuapp.com/](https://oic101.herokuapp.com/), you will see a very simple application that has exposed two REST endpoints: `/callOic` and `/responseFromOic`. You can see this in the code below:
<img src="images/OIC-2.01.png" width="100%" title="Exposed REST endpoints of this application">
- The `callOic` endpoint is a POST call: this means that this application is configured to receive a payload from somewhere. In this case, that somewhere is OIC. For now, the only piece of information you need is that the endpoint to call is `https://oic101.herokuapp.com/callOic`.
- The `responseFromOic` endpoint is a GET call: this means that this application will return some information when you enter the address `https://oic101.herokuapp.com/callOic` in a web browser (since web browsers by default make a GET request to any website you enter). OIC does not call this endpoint; instead, you can view the information stored in the application when you invoke `https://oic101.herokuapp.com/responseFromOic` in a web browser.

### 2.1: Creating a connection
Remember to ***FREQUENTLY SAVE YOUR CONNECTIONS***. There will only be an initial and final reminder to save in this tutorial; OIC does not have an "autosave" feature for connections or integrations.
1. If you haven't already, click the upper left hamburger menu and select **Connections**.
<img src="images/OIC-2.02.png" width="100%" title="Navigating to Connections">
<img src="images/OIC-2.03.png" width="100%" title="Connections">
2. Click **Create** in the upper right corner, then scroll down or search for REST. Select REST to proceed to the configuration page.
<img src="images/OIC-2.04.png" width="100%" title="Initializing REST connection">
3. Enter a descriptive name for the connection. For the purpose of the tutorial you can enter "OIC101-connection". Make sure the Role is set to **Trigger and Invoke**.
<img src="images/OIC-2.05.png" width="100%" title="Connection configuration 1">
**NOTE**: Trigger means that if this connection is added to an integration, the application configured in this connection will _trigger_ the integration to begin. Invoke means that if this connection is added to an integration, that integration will be able to _invoke_ the application configured in this connection while OIC is running through the process flow of the integration. In some cases it makes more sense to only trigger or only invoke -- in this case it makes the most sense to only invoke -- but for the most part it is safe to create connections that can serve both incoming and outgoing requests.

4. Click **Configure Connectivity**. A dialog box will pop up with two required properties to be set. Set **Connection Type** to be "REST API Base URL" and set **Connection URL** to the POST endpoint of the heroku application, `https://oic101.herokuapp.com/callOic`.
<img src="images/OIC-2.06.png" width="100%" title="Connection configuration 2">
5. Scroll down to **Configure Security**. The application is pretty basic and does not require authentication; select "No Security Policy" for **Security Policy**.
<img src="images/OIC-2.07.png" width="100%" title="Connection configuration 3">
6. You do not need to configure an Agent for this connection. Scroll to the top and click **Test**. Once you see the green bar appear, or that the REST Connection becomes 100% configured (second image), click **Save** and then **Close**.
<img src="images/OIC-2.08.png" width="100%" title="Connection configuration completed">
<img src="images/OIC-2.09.png" width="100%" title="Testing completed">
7. The connection should be ready to use, indicated by the green check mark on the right side of the window.
<img src="images/OIC-2.10.png" width="100%" title="Connection ready to use">


## **STEP 3**: Integration components


## **STEP 4**: Build an integration


## **STEP 5**: Run and Track the integration


## Miscellaneous important information within OIC
<div id="misc"/>

### Activity Log

### Variable Tracking

### Designer menu vs Monitoring menu

