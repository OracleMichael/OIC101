# Oracle Integration Cloud: The Tutorial

This document shows how to use Oracle Integration Cloud (OIC) at the very basic level.


## Purpose

Before you get started, please note that this tutorial is **meant for beginners**. Every step builds on all previous steps, so if you understand a step feel free to skip that step - please still read all of this document to make sure you did not miss any key configuration steps. Here is a more detailed list of what this tutorial will cover:
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

## **STEP 1**: Navigating to OIC

In this step, you will navigate to and from OIC. You will need to travel along this path: (Oracle cloud)->(cloud dashboard)->(integration instance page)->(OIC home)->(integration dashboard).

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

### Creating a connection
Remember to ***FREQUENTLY SAVE YOUR CONNECTIONS***. There will only be an initial and final reminder to save in this tutorial; OIC does not have an "autosave" feature for connections or integrations.
1. If you haven't already, click the upper left hamburger menu and select **Connections**.
<img src="images/OIC-2.02.png" width="100%" title="Navigating to Connections">
<img src="images/OIC-2.03.png" width="100%" title="Connections">
2. Click **Create** in the upper right corner, then scroll down or search for REST. Select REST to proceed to the configuration page.
<img src="images/OIC-2.04.png" width="100%" title="Initializing REST connection">
3. Enter a descriptive name for the connection. For the purpose of the tutorial you can enter "OIC101-connection". Make sure the Role is set to **Trigger and Invoke**.
<img src="images/OIC-2.05.png" width="100%" title="Connection configuration 1">
**NOTE**: Trigger means that if this connection is added to an integration, the application configured in this connection will _trigger_ the integration to begin. Invoke means that if this connection is added to an integration, that integration will be able to _invoke_ the application configured in this connection while OIC is running through the process flow of the integration. In some cases it makes more sense to only trigger or only invoke - in this case it makes the most sense to only invoke - but for the most part it is safe to create connections that can serve both incoming and outgoing requests.

4. Click **Configure Connectivity**. A dialog box will pop up with two required properties to be set. Set **Connection Type** to be "REST API Base URL" and set **Connection URL** to the **base URL** of the heroku application, `https://oic101.herokuapp.com`.
<img src="images/OIC-2.06.png" width="100%" title="Connection configuration 2">
5. Scroll down to **Configure Security**. The application is pretty basic and does not require authentication; select "No Security Policy" for **Security Policy**.
<img src="images/OIC-2.07.png" width="100%" title="Connection configuration 3">
6. You do not need to configure an Agent for this connection. Scroll to the top and click **Test**. Once you see the green bar appear, or that the REST Connection becomes 100% configured (second image), click **Save** and then **Close**.
<img src="images/OIC-2.08.png" width="100%" title="Connection configuration completed">
<img src="images/OIC-2.09.png" width="100%" title="Testing completed">
7. The connection should be ready to use, indicated by the green check mark on the right side of the window.
<img src="images/OIC-2.10.png" width="100%" title="Connection ready to use">


## **STEP 3**: Integrations

An **Integration** describes a process flow that performs a group of functions. Integrations can be triggered either by an application or by a schedule, called **Application-Driven Orchestrations** and **Scheduled Orchestrations** respectively. Integrations that are app-driven always use a defined connection that is configured as a trigger. Let's say that the connection is a Salesforce connection. Then in the integration, you would define the trigger to look for some kind of signal or API call, for instance when a contact is created in Salesforce. After some configuration on the Salesforce end, the integration will trigger whenever a contact is created in Salesforce. On the other hand, integrations that are scheduled rely on some schedule that will trigger the integration based on a frequency, for instance every day or every hour. This is more often used on a "gather-bulk-data" basis than a "one-action-one-trigger" basis, for instance moving all the logs between five minutes ago and last week to a backup server.

### Creating an integration
Remember to ***FREQUENTLY SAVE YOUR INTEGRATIONS***. There will only be an initial and final reminder to save in this tutorial; OIC does not have an "autosave" feature for connections or integrations.
1. Navigate to the integration dashboard. It should look like the last image of section 1. If you are on the Connections page, click on the upper left hamburger menu and select **Integrations**.
2. Click **Create** in the upper right corner. This brings up a dialog box with six types of integrations you can build. Select **App Driven Orchestration**.
<img src="images/OIC-3.01.png" width="100%" title="Create Integration - Select a Style">
3. Enter a descriptive name for the integration. For the purpose of the tutorial you can enter "OIC101-integration".
<img src="images/OIC-3.02.png" width="100%" title="Create Integration - Enter Important Information And Stuff">
4. Now the trigger must be configured.
	1. For the trigger, select **Sample REST Endpoint Interface**, the same one mentioned earlier in **STEP 2**. There are two ways to do this: click the + in the empty trigger slot under "START" and find **Sample REST Endpoint Interface** (first image); or open the trigger menu on the right side, find **Sample REST Endpoint Interface** under the list of REST endpoints, and drag/drop the endpoint onto the empty trigger slot (second image).
	<img src="images/OIC-3.03.png" width="100%" title="The click and find method">
	<img src="images/OIC-3.04.png" width="100%" title="The click and drag method, aka the fun method">
	2. A dialog box will appear. You will now enter the following information to finish configuring the initial REST trigger: **call the endpoint** whatever you wish (for instance, "start"), set the **relative resource URI** to "/", and leave the **action to be performed** as "GET". Click **Next** and then **Done** (no more configuration is required).
	<img src="images/OIC-3.05.png" width="100%" title="A very simple REST trigger">
	3. After configuring, you should see a screen similar to this one.
	<img src="images/OIC-3.06.png" width="100%" title="Finished configuring trigger">
**What's going on here?** The connection added to the integration is one that uses the URL of the integration as the trigger. This means that whenever an application makes a GET request to the URL of the integration, the integration will fire. Since the relative resource URI was set to "/", no additional endpoint is being hit. For instance if the base URL of the integration were something like `https://integration.oracle.com` then any application that makes a GET request to that URL or technically `https://integration.oracle.com/` will trigger the integration. However, since searching a URL on a web browser will make a GET request to that URL, you will use this to manually trigger the integration.

5. Now the connection to the application will be configured.
	1. You will add `OIC101-connection` between the trigger and its associated Map. There are two ways to do this. You can either hover your cursor over the grey arrow from the trigger to the Map, click the +, and find **OIC101-connection** (first image); or open the invoke menu on the right side, find **OIC101-connection** under the list of REST endpoints, and drag/drop the endpoint onto the + between the trigger and its associated Map. Then click **Next**.
	<img src="images/OIC-3.07.png" width="100%" title="The click and find method, revisited">
	<img src="images/OIC-3.08.png" width="100%" title="The click and drag method, also revisited and also equally more fun than the immediately above">
	2. A dialog box will appear. Enter the following information:
	| Field name                | Value                              |
	|---------------------------|------------------------------------|
	| Endpoint name             | sendToApp                          |
	| Description (optional)    | Sends a payload to the Express App |
	| Relative Resource URI     | /callOic                           |
	| Action to perform         | POST                               |
	| Configure request payload | (check this box)                   |
	<img src="images/OIC-3.09.png" width="100%" title="A substantially more complex REST trigger">
	3. Since this connection is a POST request, and since **Configure a request payload for this endpoint** is checked, you will have to define the format that the application will recognize. In this case, the format that is recognized is a JSON payload consisting of a single `message` (String) object. Here is a valid body that would be sent over to the application:
	```
	"body": {
		"message": "some string value"
	}
	```
	To configure this, first select "JSON Sample" for the **request payload format**. You will see an option to **enter sample JSON**; click `<<< inline >>>` (first image). Once inside, paste this minified version of the body above and click **Ok**: `{"message":""}` (second image). Then click **Next** and **Done**.
	<img src="images/OIC-3.10.png" width="100%" title="Request payload configuration 1">
	<img src="images/OIC-3.11.png" width="100%" title="Request payload configuration 2">
	4. After configuring, you should see a screen similar to this one. Note: you can click the icon pointed out below to automatically center and zoom out to fit all integration components.
	<img src="images/OIC-3.12.png" width="100%" title="Finished configuring invoke">
**What's going on here?** This connection was configured originally to contact the base URL, or `https://oic101.herokuapp.com`. When the connection was added to the integration, the relative resource URI was `callOic`. This means that when the integration reaches this component, OIC will make a POST call to `https://oic101.herokuapp.com/callOic`, which is precisely the URL to hit. Also, the payload/body sent along with the POST request was of the form `{ "message": ""}`, which is the format that the application recognizes (a single object called "message" of type string, as indicated by the empty double quotes). Even though the format has been defined, the actual payload has yet to be sent over. You will hard-code this string first, then modify the integration to dynamically accept any string based on a parameter.

6. Configure the map called "Map to sendToApp".
	1. Click on the map and select the pencil icon. For reference, the eyeball icon allows you to view the map, the pencil icon allows you to edit the map, and the menu/details opens a menu with more options.
	<img src="images/OIC-3.13.png" width="100%" title="How to edit a map">
	2. The map dialog opens, detailing all elements prior to this map on the left side and all inputs to the immediate next element on the right side. In this case, the immediate next element is the REST connection to the application, sendToApp, and it was defined to have a payload containing a single "message" object of type string. Click "\*message" (first image), click on the line that says "-- Drag and Drop or Type value here...", and enter a random value (second image), for instance "This is a message from OIC." Click **Save**, then **Close**, and finally **Validate** and then **Close**.
	<img src="images/OIC-3.14.png" width="100%" title="Contents of a map">
	<img src="images/OIC-3.15.png" width="100%" title="Hard-code the value of message">
7. All working parts of the integration are now configured properly. Before activation, all integrations must have one of the initial variables enabled for tracking. What this means is that when a user checks all instances of integrations that have been triggered, the user will be able to find the (usually) unique instance he/she is looking for, especially if there are errors in any of the tracked instances. You can see that there is an error, denoted by the red oval with a number 1 in it; this error is exactly the lack of a tracked variable. First, select the most hamburger-looking menu in the upper right corner, then click **Tracking** (first image). This opens a dialog box for tracking variables. **Click and drag** the only variable - `execute` - to the **Tracking Field** column (second image). Then click **Save**, and then **Save** and **Close** out of the integration (upper right corner).
<img src="images/OIC-3.16.png" width="100%" title="Where is the tracking menu?">
<img src="images/OIC-3.17.png" width="100%" title="Just track any variable that you see">

## **STEP 4**: Run and Track the integration

### 4.1: Activate the integration

### 4.2: Track instances and view the application


## **STEP 5**: Modify the integration

### 5.1: Modify the integration

### 5.2: Run and Track the integration


## Miscellaneous important information within OIC
<div id="misc"/>

### Integration components

### Activity Log

### Variable Tracking

### Designer menu vs Monitoring menu

