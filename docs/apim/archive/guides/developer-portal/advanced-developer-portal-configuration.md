---
description: The administrator's guide to the Developer Portal
---

# Configuration

## Introduction

Configuration of the Developer Portal takes place through the Management Console **Settings** page as highlighted in the image below.

<figure><img src="../../.gitbook/assets/dev_portal_settings.png" alt=""><figcaption><p>Developer portal settings</p></figcaption></figure>

The Developer Portal settings can be broken into the following major categories:

* General settings
* User management
* Layout and theme customization
* Documentation

## General settings

This section details how to configure high-level settings for the Developer Portal. Select the **Settings** tab in the secondary sidebar and scroll down to the **Portal** subheader where you have the following configuration options:

{% hint style="info" %}
`gravitee.yml` override

The top of the **Settings** page states "Depending on your architecture, this configuration may be overridden by a local configuration file. See documentation for more information."

All of the general settings can be overridden with the `gravitee.yaml` file. You can learn more about the `gravitee.yaml` file in the [APIM Configuration documentation.](../../getting-started/configuration/)
{% endhint %}

* **Api-key Header:** Modify the `api-key` header shown in the Developer Portal's CURL commands

{% hint style="warning" %}
Note, this only impacts what is displayed in the Developer Portal's UI. You must modify the `gravitee.yaml` file to impact how the Gateway handles the `api-key` header.
{% endhint %}

* **Portal URL:** Provide the URL of the Developer Portal. This will add a link to the Developer Portal on the top navigation bar of the Management Console as shown in the image below. Additionally, the [theme editor](advanced-developer-portal-configuration.md#theme-customization) will have a live preview of the Developer Portal.

<figure><img src="../../.gitbook/assets/dev_portal_link.png" alt=""><figcaption><p>Link to Developer Portal from Management Console</p></figcaption></figure>

* **Override homepage title:** Activating this toggle allows you to change the Developer Portal title from "Unleash the power of your APIs." to a custom title
* **Options**
  * **Use Tiles Mode:** Sets the default all APIs view to tiles as opposed to a list view
  * **Activate Support:** Adds a **Contact** and **Tickets** tab to each API. Email must be configured as detailed in the [Email configuration](advanced-developer-portal-configuration.md#email-notifications) section for the contact form to work
  * **Activate Rating:** Allow API consumers to leave written reviews and ratings
  * **Force user to fill comment:** Requires all subscription requests to have a comment
  * **Allow User Registration:** Allow API consumers to create an account from the Developer Portal. Email must be configured as detailed in the [Email configuration](advanced-developer-portal-configuration.md#email-notifications) section for registration to work.
    * **Enable automatic validation:** Automatically approve all accounts created on the Developer Portal
  * **Add Google Analytics:** Add a Google Analytics tracking ID to the Developer Portal
  * **Allow Upload Images:** Allows documentation owners to attach images as additional resources
  * **Max size upload file (bytes):** Controls the size of images documentation owners are allowed to attach
* **OpenAPI Viewers:** Select the viewer you would like to use to display your API documentation
* **Schedulers:** Configure the frequency the Developer Portal runs background tasks such as syncing data and sending/receiving notifications
* **Documentation URL:** Set the URL shown at the end of the v2 API creation flow. Note, this currently only applies to v2 APIs.

<figure><img src="../../.gitbook/assets/documentation_url.png" alt=""><figcaption><p>Documentation URL setting for v2 API creation flow</p></figcaption></figure>

## User management

Accessing the Developer Portal directly from the Management Console automatically signs you in with the same account. However, the power of the Developer Portal revolves around exposing your APIs to both internal and external API consumers. This necessitates the ability to create new accounts which requires some additional configuration.

### User sign-up

The ability to create new user accounts has two requirements:

1. Enabling the **Allow User Registration** option
2. Simple mail transfer protocol (SMTP) configuration to confirm user account creation

As detailed in [General settings](advanced-developer-portal-configuration.md#general-settings), the **Allow User Registration** option is already enabled by default.

To view SMTP settings, navigate to **Settings** in the Management Console. Then, in the secondary sidebar, select **Settings** under the **Portal** header in the submenu. The **SMTP** settings are at the bottom of the page; however, for many deployments, these settings will be greyed out. This is due to the `gravitee.yml` configuration file disabling email by default since it requires configuring an SMTP email service. This [SMTP configuration guide](../../getting-started/configuration/) will walk you through setting up email for your APIM deployment.

<figure><img src="../../.gitbook/assets/Screenshot 2023-06-05 at 12.03.55 PM.png" alt=""><figcaption><p>SMTP default settings</p></figcaption></figure>

After configuring SMTP, you should be able to create a new user in the Developer Portal. You can test this by opening the Developer Portal in an incognito window to avoid being automatically signed in with the same account being used in the Management Console. In the new incognito window, select **Sign up** at the bottom of the modal. Provide the required information and select the **Sign Up** button.

<figure><img src="../../.gitbook/assets/Screenshot 2023-06-05 at 12.14.03 PM.png" alt=""><figcaption><p>Developer portal sign up page</p></figcaption></figure>

You should receive a registration confirmation and an email to the address you provided. Open the email and click the link. Make sure the link opens in the incognito tab; otherwise, it will just open the Developer Portal with the account signed into the Management Console.

You will be taken to a page to finalize your account and add a password. By default, the password must meet the following requirements:

* 8 to 32 characters
* no more than 2 consecutive equal characters
* min 1 special characters (@ & # …)
* min 1 upper case character

{% hint style="info" %}
**Password customization**

Password requirements can be modified by changing the regex pattern under **User Management Configuration** in the `gravitee.yml` file or by using environment variables.
{% endhint %}

Once you finish creating your password, you will be able to sign in.

### User overview

All users can be viewed in APIM's Management Console by anyone with administrator privileges. To view users, select **Organization** at the bottom of the sidebar. Once there, navigate to the **Users** tab in the sidebar. Here, you will see a list of all current users tied to the organization. As an administrator, you can select any user for more details and to apply administrative policies. Additionally, admins can pre-register users by clicking the **Add user** button in the top right.

<figure><img src="../../.gitbook/assets/image (3) (1) (1).png" alt=""><figcaption><p>Management Console user overview</p></figcaption></figure>

{% hint style="info" %}
**Detailed user administration**

For a more detailed look at managing users including roles, groups, and permissions, head over to the [Administration guide.](../administration/#introduction)
{% endhint %}

## Layout and theme customization

This section will detail how to modify how APIs are presented to API consumers.

### API Sidebar

Administrators can modify what is shown in the sidebar of an API's **General information**.

<div data-full-width="false">

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-31 at 1.57.16 PM.png" alt=""><figcaption><p>Developer portal API sidebar</p></figcaption></figure>

</div>

To modify the access URL, select **Organization** in the sidebar of the Management Console. Next, select **Sharding tags** in the sidebar under the **Gateway** subheader. This page allows you to modify the **Default entrypoint** of the Gravitee Gateway. The access URL for each API in the Developer Portal will display the default entrypoint followed by that API's contect path.

<figure><img src="../../.gitbook/assets/Screenshot 2023-07-28 at 12.51.56 PM.png" alt=""><figcaption><p>Modify the access URL</p></figcaption></figure>

{% hint style="info" %}
&#x20;**Sharding Tags and Gateway Entrypoint Mappings**

At a high-level, sharding tags are assigned to APIs and Gravitee Gateways to provide a method to deploy an API to a subset of gateways. Adding a mapping between these sharding tags and a gateway’s entrypoint URL allows the developer portal to intelligently display different entrypoints depending on the API’s sharding tags.

Sharding tags are used to help manage complex distributed architectures. Check out the [Sharding Tags guide](../../getting-started/configuration/configure-sharding-tags-for-your-gravitee-api-gateways.md) to learn more.
{% endhint %}

For the rest of the sidebar settings, return to the Console's homescreen then select **Settings >** **API Portal Information** to display the following options:

<figure><img src="../../.gitbook/assets/dev_portal_api_display_settings.png" alt=""><figcaption><p>Developer portal API sidebar display settings</p></figcaption></figure>

* **Add extra information**
  * **Show tags list in the API header:** Display all API labels in the Developer Portal
  * **Show categories list in the API header:** Display all API categories in the Developer Portal
* **Configure the information list:** Display custom values in the Developer Portal. Use the **+ icon** in the bottom right to add new values.
* **API Page list options:** Detailed in the [catalog tabs](advanced-developer-portal-configuration.md#catalog-tabs) section below

### API Catalog

Administrators can also modify how API consumers browsing experience in the Developer Portal's API catalog.

#### Promotion banner

In APIM, select **API Portal Information** in the secondary sidebar to display the following options shown below.

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption><p>Developer portal API display settings</p></figcaption></figure>

* The other options are detailed in the [API sidebar](advanced-developer-portal-configuration.md#api-sidebar) section above.
*   **API Page list options**

    * **Display promotion banner:** Adds a banner to the top of each page in the API catalog to promote a particular API. The API that is promoted is determined automatically based on the tab. For example, the **Starred** tab will show the API that was most recently reviewed in the promotion banner.

    <figure><img src="../../.gitbook/assets/Screenshot 2023-05-31 at 2.21.47 PM.png" alt=""><figcaption><p>Developer portal promotion banner</p></figcaption></figure>

#### Categories tab

Administrators have the option to include a **Categories** tab in the API catalog. This organizes APIs based on the category applied to a Gateway API. Categories can be added on the **General** page of a Gateway API as shown below:

<figure><img src="../../.gitbook/assets/api_categories.png" alt=""><figcaption><p>Applying categories to a Gateway API</p></figcaption></figure>

To enable the Categories tab in the Developer Portal, go to APIM and select **Categories** in the secondary sidebar. Here you can also create new categories and modify or delete existing categories.

<figure><img src="../../.gitbook/assets/Screenshot 2023-06-01 at 1.59.06 PM.png" alt=""><figcaption><p>APIM categories settings page</p></figcaption></figure>

With the toggle enabled, users accessing the Developer Portal will have access to the page shown below:

<figure><img src="../../.gitbook/assets/dev_portal_categories.png" alt=""><figcaption><p>Dev portal categories page</p></figcaption></figure>

#### Top/featured APIs

Administrators also have control over what is displayed on the **Featured** page of the API catalog by modifying the top APIs. Navigate to APIM **Settings** and select **Top APIs** in the secondary sidebar.

<figure><img src="../../.gitbook/assets/Screenshot 2023-06-01 at 2.10.58 PM.png" alt=""><figcaption><p>Top APIs settings</p></figcaption></figure>

From here, administrators can add new APIs with the **+ icon**, reorder the top APIs, and remove APIs from the list. APIs added here are displayed on both the Developer Portal's homepage and on the API catalog's **Featured** page as shown below.

<figure><img src="../../.gitbook/assets/dev_portal_homepage.png" alt=""><figcaption><p>Developer portal homepage displaying top APIs</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/Screenshot 2023-06-01 at 2.14.32 PM.png" alt=""><figcaption><p>Developer portal Featured page in API catalog</p></figcaption></figure>

{% hint style="info" %}
**Top API visibility**

If you are having issues seeing Gateway APIs you added to the Top APIs list, make sure the API is public or the user logged into the Developer Portal has access to that API. Administrators can see all the APIs but individual users are restricted to public APIs and APIs they have been granted access to through user and group access settings.
{% endhint %}

### Custom navigation

Administrators can customize the Developer Portal navigation in the header and footer. This is done by creating link pages in Gravitee's system folders. There are three kinds of links:

* External link
* Link to an existing documentation page
* Link to a category

Each link is treated as a new documentation page. To learn about all the features and functionality of Developer Portal documentation, head to the[ Documentation section](advanced-developer-portal-configuration.md#documentation) of this page.

#### System folders

Gravitee's system folders are accessible in the Management Console under **Settings > Documentation** and can be identified by their padlock icon as shown below.

<figure><img src="../../.gitbook/assets/Screenshot 2023-06-05 at 10.44.36 AM.png" alt=""><figcaption><p>Gravitee's system folders</p></figcaption></figure>

There are three system folders: `Header`, `TopFooter` and `Footer`. Each system folder corresponds to an area of the Developer Portal:

<figure><img src="https://docs.gravitee.io/images/apim/3.x/api-publisher-guide/documentation/graviteeio-page-link-portal-zones.png" alt=""><figcaption><p>Developer portal - system folder mapping</p></figcaption></figure>

{% hint style="warning" %}
**`TopFooter`system folder nesting**

The`TopFooter`system folder is the only system folder that accepts nested folders. As shown in the image above, folders nested under the `TopFooter` system folder are used to group links together.

It is important to note that nested folders must be published to be seen in the Developer Portal.

<img src="../../.gitbook/assets/Screenshot 2023-06-05 at 11.24.49 AM.png" alt="" data-size="original">
{% endhint %}

#### Manage Links <a href="#manage_links" id="manage_links"></a>

To create a link, open a system folder and select the **+ icon** then select the **Link** icon. This will take you to a new page to select your link type and provide some additional information about your link.

<figure><img src="../../.gitbook/assets/dev_portal_create_a_link.png" alt=""><figcaption><p>Create a new Developer Portal link</p></figcaption></figure>

Select **Save**, and navigate to the Developer Portal to see your new link in action.

<figure><img src="../../.gitbook/assets/dev_portal_custom_link_example.png" alt=""><figcaption><p>Sample "Gravitee Homepage" custom link</p></figcaption></figure>

Each custom link has additional features such as translations and access control that you can learn more about in the [Documentation section](advanced-developer-portal-configuration.md#documentation).

{% hint style="warning" %}
**Publishing`TopFooter`nested folders**

The`TopFooter`system folder is the only system folder that accepts nested folders. It is important to note that nested folders must be published to be seen in the Developer Portal.

<img src="../../.gitbook/assets/Screenshot 2023-06-05 at 11.24.49 AM.png" alt="" data-size="original">
{% endhint %}

### Theming

Administrators can change the default theme of the Developer Portal to their own custom theme. To modify the theme, in the APIM settings select **Theme** in the secondary sidebar.

<figure><img src="../../.gitbook/assets/Screenshot 2023-06-01 at 2.50.54 PM.png" alt=""><figcaption><p>Developer portal theme settings</p></figcaption></figure>

This page allows the administrator to customize every aspect of the Developer Portal's look and feel. Edits made are shown in a live preview to the right.

{% hint style="warning" %}
**Enable live preview**

If you are not seeing a live preview, this is due to not providing a Portal URL as detailed in the [General settings section](advanced-developer-portal-configuration.md#general-settings).
{% endhint %}

#### Top menu

The top menu provides the following options:

* **Fullscreen:** This button opens the preview in a new window, making it easier to edit if you have several screens
* **Reset:** This button allows you to reset the theme from the last backup. Backups occur when you select the **Save** button
* **Save:** This button saves your theme
* **Enabled:** This toggle activates the theme in APIM Portal
* **Import:** Upload a custom theme in `JSON` format. To see the required structure of the `JSON` file, export the current theme
* **Export:** Download your current theme in `JSON` format
* **Restore Default Theme:** This button overwrites your modifications with the theme provided by default

## Documentation

Outside of APIs and applications, administrators can also provide site-wide documentation for API publishers and consumers. This documentation creates a direct line of communication with your developer community through a single channel. For example, you can use it to communicate your best practices, configure your own homepage, or even reference it in links when using [custom navigation](advanced-developer-portal-configuration.md#custom-navigation). All published documentation can be accessed in the Developer Portal's **Documentation** page as shown below.

{% hint style="info" %}
Site-wide documentation is separate from API documentation which can be added to an API by an API publisher.
{% endhint %}

<figure><img src="../../.gitbook/assets/Screenshot 2023-06-05 at 10.24.20 AM.png" alt=""><figcaption><p>Developer portal documentation page</p></figcaption></figure>

### Documentation types

To add some documentation, you can either create new pages or import them from a file or external source.

APIM supports multiple types of documentation:

* Markdown (for more information, see [Markdown documentation](https://docs.gravitee.io/apim/3.x/apim\_publisherguide\_publish\_documentation\_markdown.html) and [Markdown templates](https://docs.gravitee.io/apim/3.x/apim\_publisherguide\_publish\_documentation\_markdown\_template.html))
* AsciiDoc (for more information, see [AsciiDoc documentation](https://docs.gravitee.io/apim/3.x/apim\_publisherguide\_publish\_documentation\_asciidoc.html))
* OpenAPI (Swagger) (for more information, see [OpenAPI documentation](https://docs.gravitee.io/apim/3.x/apim\_publisherguide\_publish\_documentation\_openapi.html))
* AsynAPI (for more information, see [AsycAPI documentation](https://www.asyncapi.com/docs))

### Create documentation

To create documentation, go to **Settings > Documentation** in the Management Console.

<figure><img src="../../.gitbook/assets/Screenshot 2023-06-05 at 3.22.29 PM.png" alt=""><figcaption><p>Documentation settings page</p></figcaption></figure>

{% hint style="info" %}
**System folders**

Header, TopFooter, and Footer are known as system folders. They can be used to customize the Developer Portal's navigation by adding custom links. For more information, see [Custom navigation.](advanced-developer-portal-configuration.md#custom-navigation)
{% endhint %}

From here, you can create a new documentation page by selecting the **+ icon** in the bottom right. This presents you with the following options:

<figure><img src="../../.gitbook/assets/Screenshot 2023-06-05 at 3.45.43 PM.png" alt=""><figcaption><p>Create new documentation options</p></figcaption></figure>

* **Folder:** Generate a folder to organize your documentation. This also allows you to quickly generate translations of the entire folder by selecting **Translate Folder**. More information is provided on [translations below](advanced-developer-portal-configuration.md#translate-a-page).

<figure><img src="../../.gitbook/assets/Screenshot 2023-06-05 at 3.49.15 PM.png" alt=""><figcaption><p>Sample documentaion folder</p></figcaption></figure>

* **Markdown Template:** Create templates to be re-used for both site-wide and API markdown documentation.
* **Markdown:** Use the Markdown syntax for the documentation page
* **Asciidoc:** Use the Asciidoc syntax for the documentation page
* **OpenAPI (Swagger):** Use the OpenAPI syntax for the documentation page
* **AsyncAPI:** Use the AsyncAPI syntax for the documentation page

Regardless of your selection, each documentation type provides similar configuration options followed by a text editor matching the type of document you selected.

<figure><img src="../../.gitbook/assets/new_docs_page.png" alt=""><figcaption><p>Creating a documentation page</p></figcaption></figure>

* **Name:** Provide a label for your documentation page
* **Set as homepage:** Use the documentation page on the homepage of the Developer Portal

<figure><img src="../../.gitbook/assets/Screenshot 2023-06-07 at 3.04.50 PM.png" alt=""><figcaption><p>Custom homepage example</p></figcaption></figure>

{% hint style="info" %}
If you set multiple documentation pages as the homepage, only the page most recently set as the homepage will be active.
{% endhint %}

* **Publish this page:** Make the page available in the Developer Portal
* **Make private:** Make the page private to you and the users you explicitly allow through access control. Access control is detailed in the [Page configuration](advanced-developer-portal-configuration.md#configure-a-page) section.

The rest of the settings revolve around generating content for your new documentation page. APIM provides three main methods for generating documentation content

* Fill the content inline
  * Supports templating with API properties
* Import from file
* Import from an external source (Gitlab, Bitbucket, etc.)

### Fill the content inline (templating support)

This method is mostly self-explanatory as you will use the text editor to generate content based on the documentation type you selected. However, APIM also supports templating with API properties.

#### Templating with API properties

You can access your API data in your API documentation with the following syntax: `${api.name} or ${api.metadata['foo-bar']}`. This example shows how to create documentation templates based on the Apache [FreeMarker template engine](https://freemarker.apache.org/). Below the example, you can find a full reference table of available API properties.

{% code overflow="wrap" fullWidth="false" %}
```ftl
<#if api.picture??>
<img src="${api.picture}" style="float: right;max-width: 60px;"/>
</#if>

# Welcome to the API ${api.name}(${api.version})!

The API is <span style="text-transform: lowercase;color: <#if api.state=='STARTED'>green<#else>red</#if>">${api.state}</span>.

This API has been created on ${api.createdAt?datetime} and updated on ${api.updatedAt?datetime}.

<#if api.deployedAt??>
This API has been deployed on ${api.deployedAt?datetime}.
<#else>
This API has not yet been deployed.
</#if>

<#if api.visibility=='PUBLIC'>
This API is publicly exposed.
<#else>
This API is not publicly exposed.
</#if>

<#if api.tags?has_content>
Sharding tags: ${api.tags?join(", ")}
</#if>

## Description

${api.description}

## How to access

The API can be accessed through https://api.company.com${api.proxy.contextPath}:

curl https://api.company.com${api.proxy.contextPath}

## Rating

You can rate and put a comment for this API <a href='/#!/apis/${api.id}/ratings'>here</a>.

## Contact

The support contact is <a href="mailto:${api.metadata['email-support']}">${api.metadata['email-support']}</a>.

The API owner is <#if api.primaryOwner.email??><a href="mailto:${api.primaryOwner.email}">${api.primaryOwner.displayName}</a><#else>${api.primaryOwner.displayName}</#if>.
```
{% endcode %}

This has the following result in the Developer Portal:

<figure><img src="https://docs.gravitee.io/images/apim/3.x/api-publisher-guide/documentation/graviteeio-page-documentation-template.png" alt=""><figcaption><p>Result of templating engine example</p></figcaption></figure>

#### API properties reference

<table data-full-width="false"><thead><tr><th>Field name</th><th>Field type</th><th>Example</th></tr></thead><tbody><tr><td>id</td><td>String</td><td>70e72a24-59ac-4bad-a72a-2459acbbad39</td></tr><tr><td>name</td><td>String</td><td>My first API</td></tr><tr><td>description</td><td>String</td><td>My first API</td></tr><tr><td>version</td><td>String</td><td>1</td></tr><tr><td>metadata</td><td>Map</td><td>{"email-support": "<a href="mailto:support.contact@company.com">support.contact@company.com</a>"}</td></tr><tr><td>createdAt</td><td>Date</td><td>12 juil. 2018 14:44:00</td></tr><tr><td>updatedAt</td><td>Date</td><td>12 juil. 2018 14:46:00</td></tr><tr><td>deployedAt</td><td>Date</td><td>12 juil. 2018 14:49:00</td></tr><tr><td>picture</td><td>String</td><td>data:image/png;base64,iVBO…​</td></tr><tr><td>state</td><td>String</td><td>STARTED/STOPPED</td></tr><tr><td>visibility</td><td>String</td><td>PUBLIC/PRIVATE</td></tr><tr><td>tags</td><td>Array</td><td>["internal", "sales"]</td></tr><tr><td>proxy.contextPath</td><td>String</td><td>/stores</td></tr><tr><td>primaryOwner.displayName</td><td>String</td><td>Firstname Lastname</td></tr><tr><td>primaryOwner.email</td><td>String</td><td><a href="mailto:firstname.lastname@company.com">firstname.lastname@company.com</a></td></tr></tbody></table>

### Import from file

This method allows you to import a file matching the documentation type to generate the content.

### External source

The final method allows you to import your documentation from external sources. APIM includes five types of fetchers:

* **GitHub:** fetch your documentation from a GitHub repository
* **GitLab:** fetch your documentation from a GitLab repository
* **Git:** fetch your documentation from any Git repository
* **WWW:** fetch your documentation from the web
* **Bitbucket:** fetch your documentation from a Bitbucket repository

<figure><img src="https://docs.gravitee.io/images/apim/3.x/api-publisher-guide/documentation/graviteeio-page-documentation-external-source-auto-fetch.png" alt=""><figcaption><p>Documentation fetcher configuration</p></figcaption></figure>

The documentation is fetched and stored locally in APIM in the following three scenarios:

1. Documentation is fetched a single time after you finish configuring your fetcher
2. Any time you select **Fetch All**

<figure><img src="../../.gitbook/assets/Screenshot 2023-06-07 at 4.02.38 PM.png" alt=""><figcaption><p>Update all documentation from external sources</p></figcaption></figure>

3. At regular intervals if you configure auto-fetch

#### Import multiple pages

If you have an existing documentation set for your API in a GitHub or GitLab repository, you can configure the GitHub or GitLab fetcher to import the complete documentation structure on a one-off or regular basis.

Additionally, you can import the documentation into APIM in a different structure from the source repository structure. To do this, you need to create a Gravitee descriptor file (`.gravitee.json`), at the root of the repository, describing both the source and destination structure.

You can then configure a fetcher in APIM to read the JSON file and import the documentation according to the structure defined in the file.

{% hint style="warning" %}
The Gravitee descriptor file must be named `.gravitee.json` and must be placed at the root of the repository.
{% endhint %}

The following Gravitee descriptor describes a documentation set that includes:

* A home page in Markdown format in a folder called `/newdoc` to be placed at the root of the APIM documentation structure
* A JSON file containing a Swagger specification at the root of the repository, to be placed in a folder called `/technical` in the APIM documentation structure.

{% code title=".gravitee.json" %}
```json
{
    "version": 1,
    "documentation": {
        "pages": [
            {
                "src": "/newdoc/readme.md",
                "dest": "/",
                "name": "Homepage",
                "homepage": true
            },
            {
                "src": "/test-import-swagger.json",
                "dest": "/technical",
                "name": "Swagger"
            }
        ]
    }
}
```
{% endcode %}

The following steps detail how to actually configure a fetcher to import multiple files:

1. Select **Import multiple files**

<figure><img src="../../.gitbook/assets/Screenshot 2023-06-07 at 4.04.23 PM.png" alt=""><figcaption><p>Import multiple documentation files</p></figcaption></figure>

2. If you want to publish the pages on import, select **Publish all imported pages**

<figure><img src="https://docs.gravitee.io/images/apim/3.x/api-publisher-guide/documentation/import-multiple-files.png" alt=""><figcaption></figcaption></figure>

3. Select the **GitHub** or **GitLab** fetcher
4.  Specify the details of the external source, such as the URL of the external API, the name of the repository, and the branch. The fields vary slightly depending on the fetcher.

    <figure><img src="https://docs.gravitee.io/images/apim/3.x/api-publisher-guide/documentation/import-multiple-file-dets.png" alt=""><figcaption><p>Configure a fetcher</p></figcaption></figure>
5. In **Filepath**, enter the path to your JSON documentation specification file
6. Enter an access token, which you need to generate in your GitHub or GitLab user profile
7. Select **Auto Fetch** and specify the `crontab` update frequency, if you want the pages to be updated at regular intervals.

{% hint style="info" %}
**`cron` expressions**

A `cron` expression is a string consisting of six fields that describe the schedule (representing seconds, minutes, hours, days, months and weekdays).

For example:

* Fetch every second: `* * */1 * * *`
* At 00:00 on Saturday : `0 0 0 * * SAT`

If the APIM administrator [configured a maximum fetch frequency](advanced-developer-portal-configuration.md#general-settings), the value configured by the APIM administrator will override the frequency you specify.
{% endhint %}

8. Select **IMPORT** and APIM adds the files to your documentation set.

<figure><img src="https://docs.gravitee.io/images/apim/3.x/api-publisher-guide/documentation/import-multiple-files-result.png" alt=""><figcaption><p>Import technical folder documentation with fetcher</p></figcaption></figure>

### Page management

You can select a page from the list and configure the settings below. For

* [**Page:**](advanced-developer-portal-configuration.md#create-documentation) Manage the content of the documentation page by using the inline editor or importing files
* [**Translations:**](advanced-developer-portal-configuration.md#translate-a-page) Add translations of your page
* **Configuration:** Toggle options to publish your page and use it as the homepage
* [**External Source:**](advanced-developer-portal-configuration.md#external-source) Configure a fetcher for the page
* [**Access Control:**](advanced-developer-portal-configuration.md#access-control) Fine-grained access control over your page
* **Attached Resources:** Add additional files to your documentation page. This [setting must be enabled](advanced-developer-portal-configuration.md#general-settings) by the administrator.

#### Translations

You can add translations for your pages. In the **Translations** tab:

1. Select **Add a translation**
2. Enter your 2-character language code (FR for French, CZ for Czech, IT for Italian, etc.)
3. Enter the translated title
4. (Optional) You can edit the content to add translated content by toggling on the switch
5. Click **Save Translation** at the bottom of the page

<figure><img src="https://docs.gravitee.io/images/apim/3.x/api-publisher-guide/documentation/graviteeio-page-documentation-translations-1.png" alt=""><figcaption><p>Translate a page</p></figcaption></figure>

#### Access control

In the **Access Control** tab, you can mark a page as **Private** if you want to deny access to anonymous users.

For private pages, you can configure access lists by required or to be excluded roles/groups. You can learn more about creating roles/groups in our [Administration Guide](../administration/).

<figure><img src="https://docs.gravitee.io/images/apim/3.x/api-publisher-guide/documentation/graviteeio-page-documentation-access-control.png" alt=""><figcaption><p>Documentation access control</p></figcaption></figure>