# Installation Guide


Catalog Quality Analyzer


This document provides step-by-step instructions to install, configure, and deploy the Catalog Quality Analyzer App using Adobe App Builder.


## 1. Prerequisites


### System Requirements
- Node.js v24
- Adobe I/O CLI (`npm install -g @adobe/aio-cli`)
- A hosted Adobe Commerce instance (SaaS, or PaaS 2.4.5 to 2.4.9) with App Management.
- Adobe Admin UI SDK 4.2.0 or later


### Access Requirements
- Adobe App Builder
- Adobe Developer Console
- Adobe Commerce Admin



## 2. Quick Start Installation
1. Download the Catalog Quality Analyzer App code from Adobe Exchange
2. Create an App Builder Project in Developer Console (section 3)
3. Create the .env file from env.dist (section 4)
4. Initialize and Deploy App Builder Actions to the workspace (sections 7 and 8)
5. Associate,Configure and Install the app in Commerce Admin → Apps → App Management (sections 9,10 and 11)
6. Run the first scan (section 12)



---
## 3. Configure Required Services

Create an App Builder Project in Developer Console along with required services.

1. Log in to the Adobe Developer Console
2. Click **Create project from template**
3. Select **App Builder**. The Set up templated project page displays
4. Specify a project title and app name. Keep the **Include Runtime with each workspace** checkbox selected
5. Click **Save**. The project is created with two workspaces: **Stage** and **Production**
6. Make sure the workspace has the following services:
   - **I/O Runtime**: required for SaaS and PaaS. Added to each workspace by the checkbox in step 4. All app actions run on it
   - **Adobe Commerce as a Cloud Service** API  with an **OAuth Server-to-Server** credential: required for SaaS. Add it as described in section 3.1
   - PaaS: the **Adobe Commerce as a Cloud Service** API is not used. The app uses the Commerce Integration credentials (section 6)

For screenshots of these steps, see [**Creating your First App Builder Application**](https://developer.adobe.com/app-builder/docs/get_started/app_builder_get_started/first-app/).

### 3.1 Add the OAuth Server-to-Server Credential (SaaS only)
1. Open the workspace and click **+ Add Service** → **API**
2. Select **Adobe Commerce as a Cloud Service** and click **Next**
3. Select **OAuth Server-to-Server** and click **Next**
4. Select at least one product profile and click **Save configured API**
5. The credential is shown under **Credential details** tab in OAuth Server-to-Server in the workspace. Its values are added to .env automatically by `aio app use` and `aio app deploy`


## 4. Environment Configuration


### 4.1 Create .env File
```bash
cp env.dist .env
```
Run this command in the project root directory, once, before `npm install`.

Values added to .env automatically:
- `npm install`: AIO_COMMERCE_CONFIG_ENCRYPTION_KEY
- `aio app use --merge`: AIO_runtime_auth, AIO_runtime_namespace, AIO_runtime_apihost and the workspace credential
- `aio app deploy`: AIO_COMMERCE_AUTH_IMS_* (SaaS)

Values the developer will set: none are required. The optional ones are listed in section 4.2.

Do not run `cp env.dist .env` again after `npm install`. It overwrites .env and removes the generated encryption key.


### 4.2 Environment Variables


Only  values given below are set  manually, and all of them are optional. Everything else in .env is added automatically (section 4.1).


### SaaS
```bash
COMMERCE_WEBSITE_CODE=
COMMERCE_STORE_CODE=
COMMERCE_STORE_VIEW_CODE=
```
- Leave empty to use the default codes: website `base`, store `main_website_store`, store view `default`
- Set them only if your store uses other codes (Commerce Admin → Stores → All Stores) or a scan finds no or wrong products


### PaaS
```bash
COMMERCE_CONSUMER_KEY=
COMMERCE_CONSUMER_SECRET=
COMMERCE_ACCESS_TOKEN=
COMMERCE_ACCESS_TOKEN_SECRET=
```
- **Do not add these to .env.** They are the Integration credentials from section 6, and you enter them in App Management → **Configure** after associating the app (section 10.3). The app stores them encrypted


### Store URL (SaaS and PaaS)
```bash
COMMERCE_BASE_URL=
```
- **Do not add this to .env.** The store URL is detected automatically when you associate the app with your Commerce instance (section 9), and shown in the app configuration (section 10)
- For reference, the formats are:
  - SaaS: `https://(region).api.commerce.adobe.com/[tenant-id]/`
  - PaaS: `https://(your-domain)/` (the store root, without `/rest/`)


## 5. Authentication: PaaS vs SaaS


### Base URL Differences


- PaaS: https://(your-domain)/
- SaaS: https://(region).api.commerce.adobe.com/[tenant-id]/



### Authenticate with IMS


- For PaaS, this process requires a Commerce instance with [**Adobe Identity Management Service (IMS) for Adobe Commerce**](https://experienceleague.adobe.com/en/docs/commerce-admin/start/admin/ims/adobe-ims-integration-overview) configured.
- For SaaS, IMS configuration is included by default.



## 6. Obtain Credentials


### Adobe Commerce (PaaS)
- System → Extensions → Integrations → Add New Integration
- Grant API access and activate integration


### Adobe App Builder
- Developer Console → Project → Workspace → OAuth Server-to-Server



## 7. Initialize


```bash
npm install
aio login
aio console org select
aio console project select
aio console workspace select
aio app use --merge
```
## 8. Deploy
```bash
aio app deploy


```


## 9. App Management


### 9.1 Associate the App
1. Log in to the Commerce Admin
2. Go to Apps → App Management
3. Click **Associate App**
4. Select the Project and Workspace you deployed to in step 8 (for example Stage or Production)
5. Click **Associate**. The app card shows Associated



## 10. Configuration


### 10.1 Configure the App
1. Go to Apps → App Management
2. On the **Catalog Quality Analyzer** card, click **Configure**
3. Fill in the fields for your Commerce type and click **Save**


### 10.2 SaaS Configuration
- Store Base URL: filled in automatically. Leave it as it is
- No other fields are required


### 10.3 PaaS Configuration
- Integration Consumer Key
- Integration Consumer Secret
- Integration Access Token
- Integration Access Token Secret

Use the values from the Integration created in section 6. Fill in all four.

## 11. Install the App

### 11.1 Install the App
1. On the app card in Apps → App Management, click **Install**
2. Confirm the installation. The app adds the **Catalog Quality Analyzer** menu to the Commerce Admin
3. When it finishes, the card shows Installed
4. If the card shows Partially Installed, open the details, check the failed step and click **Install** again


---



## 12. Run First Scan
1. Go to Apps → Catalog Quality Analyzer
2. Click **Scan & Export** → **Start Scan**
3. When the status shows completed, open **Dashboard**

