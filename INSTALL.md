# Installation Guide

Catalog Quality Analyzer

This guide takes you from getting **Catalog Quality Analyzer** on Adobe Exchange to your first catalog health report
in the Commerce Admin. The app runs in your own Adobe organization and is set up entirely from Adobe Exchange and the
Commerce Admin. You don't need to download code, use a command line or edit configuration files.

**Contents**

- [SaaS or PaaS: which steps are for you](#saas-or-paas-which-steps-are-for-you)

1. [Before you start](#1-before-you-start)
2. [Get the app on Adobe Exchange](#2-get-the-app-on-adobe-exchange)
3. [Approve and deploy it](#3-approve-and-deploy-it)
4. [Create a Commerce Integration (PaaS only)](#4-create-a-commerce-integration-paas-only)
5. [Associate the app in the Commerce Admin](#5-associate-the-app-in-the-commerce-admin)
6. [Configure the app](#6-configure-the-app)
7. [Install the app](#7-install-the-app)
8. [Run your first scan](#8-run-your-first-scan)
9. [Read the dashboard](#9-read-the-dashboard)
10. [Review and fix products](#10-review-and-fix-products)
11. [Export the report](#11-export-the-report)
12. [How scores are calculated](#12-how-scores-are-calculated)
13. [Everyday use](#13-everyday-use)
14. [Change settings or remove the app](#14-change-settings-or-remove-the-app)
15. [Troubleshooting](#15-troubleshooting)
16. [Developer setup (from source)](#16-developer-setup-from-source)
17. [Support](#17-support)

---

## SaaS or PaaS: which steps are for you

**How to tell which you have:**

- **SaaS** (Adobe Commerce as a Cloud Service): you open the Commerce Admin from
  [Adobe Experience Cloud](https://experience.adobe.com/) (Commerce → your instance), and the REST API address looks
  like `https://na1.api.commerce.adobe.com/<tenant-id>/`.
- **PaaS** (Adobe Commerce on cloud infrastructure or on-premises): you open the Admin at your own address, for
  example `https://mystore.com/admin` or `https://<environment>.magentosite.cloud/admin`.

| Section                                  | SaaS                              | PaaS                                                        |
| ---------------------------------------- | --------------------------------- | ----------------------------------------------------------- |
| 1. Before you start                      | ✅                                | ✅ plus App Management / Admin UI SDK on 2.4.5 to 2.4.7     |
| 2. Get the app on Adobe Exchange         | ✅                                | ✅                                                          |
| 3. Approve and deploy it                 | ✅                                | ✅                                                          |
| 4. Create a Commerce Integration         | ❌ skip (automatic)               | ✅ optional: to save fixes and scan the full catalog        |
| 5. Associate the app                     | ✅                                | ✅ (in the backend Admin)                                   |
| 6. Configure the app                     | ✅ nothing to fill in             | ✅ the 4 Integration settings (optional)                    |
| 7. Install the app                       | ✅                                | ✅                                                          |
| 8 to 13. Scan, dashboard, fix, export    | ✅                                | ✅                                                          |
| 14 to 16. Changes, troubleshooting, help | ✅                                | ✅                                                          |

---

## 1. Before you start

**Applies to:** ✅ SaaS · ✅ PaaS (a few requirements differ, marked below)

### What you need

| What                       | Details                                                                                                                                                                 |
| -------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Adobe Commerce             | **SaaS** (Adobe Commerce as a Cloud Service) or **PaaS** (Adobe Commerce on cloud infrastructure or on-premises)                                                         |
| App Management             | **Apps → App Management** in the Commerce Admin. Included on SaaS and on PaaS 2.4.8+. On PaaS 2.4.5 to 2.4.7, your Commerce developer installs the Admin UI SDK first. Not supported on local Commerce installations |
| Admin UI SDK               | **4.2.0 or later**, needed for the app's Admin menu entry (App Management itself needs 3.3.0+). See [App Management requirements](https://developer.adobe.com/commerce/extensibility/app-management/) |
| Adobe App Builder          | Your Adobe organization must be entitled to App Builder (ask your Adobe account manager if you aren't sure)                                                             |
| A reachable storefront API | The app reads your catalog through the storefront GraphQL API, so it must be reachable from the internet. If your store uses an IP allowlist, allow the Adobe I/O Runtime egress IPs. Sites behind a password can't be scanned |
| PaaS: Commerce Integration | Optional (section 4): needed to save fixes and to scan the full catalog with stock status. Without it, only storefront-visible products are scanned. Not needed on SaaS |

### Who does what

| Step                             | Who                                                                         |
| -------------------------------- | --------------------------------------------------------------------------- |
| Get the app on Adobe Exchange    | Anyone in your Adobe organization                                           |
| Approve and deploy it            | A **System Administrator** of your Adobe organization (Adobe Admin Console) |
| Create the Integration (PaaS)    | A Commerce Admin user with access to **System → Integrations**              |
| Associate, configure and install | A Commerce Admin user whose role includes the **App Management** permission |
| Scan, review and fix products    | Your catalog or merchandising team                                          |

Have these open in your browser: [Adobe Exchange](https://exchange.adobe.com/) and your Commerce Admin.

---

## 2. Get the app on Adobe Exchange

**Applies to:** ✅ SaaS · ✅ PaaS

1. Go to [Adobe Exchange](https://exchange.adobe.com/) and sign in with the Adobe ID of your **company organization**
   (the one your Commerce store belongs to). If you belong to several organizations, switch to the right one using
   the profile menu at the top right.
2. Search for **Catalog Quality Analyzer** (filter the app type to **App Builder** if needed) and open the listing.
3. Read the description and the required products (**App Builder** and **Adobe Commerce**). The app is free.
4. Click the button at the top right of the listing to get the app. There is no checkout or payment.
5. In the next dialogs, confirm that your organization has the required Adobe products (**Yes, continue**), then
   read and accept the license agreement (**Accept and continue**).
6. When it's done, the listing button changes to **Manage** and the status shows **Acquired**.

---

## 3. Approve and deploy it

**Applies to:** ✅ SaaS · ✅ PaaS

A System Administrator of your Adobe organization does this step.

### 3.1 Approve the app

1. In Adobe Exchange, open **Manage → App Builder Applications**.
2. Click **Catalog Quality Analyzer**, then **Review**.
3. Add a note if you like and **approve** it. The status changes to **Approved**.

### 3.2 Create an environment and deploy

Deploy once for each Commerce environment you want to analyze. We recommend a **Stage** environment first for your
staging store, and **Production** once you've tested it.

1. On the app's page in **Manage**, click **Add environment**, give it a name (for example `Stage` or `Production`)
   and confirm.
2. Click the environment's card and open the **Configuration** tab. Leave the defaults unless your Adobe administrator
   uses specific product profiles.
3. Click **Deploy**. It takes a few minutes. When the status shows **Deployed**, the app is running in your
   organization.

Deploying creates a project and a workspace (with the environment's name) in the
[Adobe Developer Console](https://developer.adobe.com/developer-console/) of your organization. You'll pick them in
section 5.

---

## 4. Create a Commerce Integration (PaaS only)

**Applies to:** ❌ SaaS (skip) · ✅ PaaS only, optional

**SaaS stores: skip this section.** The app saves fixes with its own Adobe credential automatically.

**PaaS stores:** scanning works without credentials, but then only products visible on the storefront are scanned.
With the Integration the app also scans disabled and not-visible products, looks up stock status, reads catalogs
above about 10,000 products, and can save fixes when you click **Save to Commerce** (section 10). You can add it
later.

1. In the Commerce Admin, go to **System → Extensions → Integrations** and click **Add New Integration**.
2. Enter a **Name** (for example `Catalog Quality Analyzer`) and your Admin password in **Your Password**. Leave the
   other fields empty.
3. Open the **API** tab. Set **Resource Access** to **Custom** and select **Catalog → Inventory → Products**. The
   app only reads and updates products.
4. Click **Save**.
5. In the list, click **Activate** on the new integration, then **Allow**.
6. Copy the four values shown: **Consumer Key**, **Consumer Secret**, **Access Token** and **Access Token Secret**.
   Keep them for section 6, then click **Done**.

> **Keep these values secret.** Paste them straight into **Configure** (section 6), where they are stored encrypted.
> Don't email them or share them in support requests.

---

## 5. Associate the app in the Commerce Admin

**Applies to:** ✅ SaaS · ✅ PaaS

This connects the deployed app to your store. Your store's address and whether it is SaaS or PaaS are passed to the
app automatically: you never enter them.

1. In the Commerce Admin, go to **Apps → App Management**. (SaaS: the Commerce Admin of your instance. PaaS: the
   backend Admin.)
2. Click **Associate App**.
3. Select the **Project** (**Catalog Quality Analyzer**) and the **Workspace** (the environment name from section 3.2,
   for example `Production`). Choose the environment that matches this store: Stage for a staging store, Production
   for the live store.
4. Click **Associate**. The app card shows **Associated**.

---

## 6. Configure the app

**Applies to:** ✅ SaaS (nothing to fill in) · ✅ PaaS (optional Integration settings)

**SaaS:** there are no settings to fill in. Continue with section 7.

**PaaS:** on the **Catalog Quality Analyzer** card, click **Configure**, fill in the settings below and click **Save**.
Values apply within about a minute and are stored encrypted.

The app uses one value for the whole store, so set the values at the default scope only. Values saved on a website or
store view can override the default, and if several store views have different values, it isn't defined which one
the app uses.

### Commerce Integration (PaaS only)

Only if you created one in section 4: **Integration Consumer Key**, **Integration Consumer Secret**, **Integration
Access Token** and **Integration Access Token Secret**. Fill in all four, or leave all four empty to scan only
storefront-visible products without saving fixes.

---

## 7. Install the app

**Applies to:** ✅ SaaS · ✅ PaaS

1. Back on the app card in **Apps → App Management**, click **Install** and confirm.
2. The installation adds the **Catalog Quality Analyzer** page to the Commerce Admin menu. This takes a few minutes.
3. When it finishes, the card shows **Installed**.

If the card shows **Partially Installed**, open the details to see the failed step and click **Install** again. If it
keeps failing, contact support (section 17).

---

## 8. Run your first scan

**Applies to:** ✅ SaaS · ✅ PaaS

1. Open **Apps → Catalog Quality Analyzer** in the Commerce Admin.
2. In the left menu, click **Scan & Export**, then **Start Scan**.
3. The page shows the status, the products scanned so far and a progress bar. The **Workers** table shows each part
   of the catalog being scanned in parallel.
4. When the status shows **completed**, open **Dashboard**.

While a scan is running, **Start Scan** is disabled.

How long a scan takes depends on the size of your catalog and how fast your store answers. A small catalog finishes in
a minute or two. After the first scan, the catalog is also scanned automatically once a day.

---

## 9. Read the dashboard

**Applies to:** ✅ SaaS · ✅ PaaS

**Dashboard** shows the latest finished scan:

- **Catalog health score:** the average score of all scanned products, with a short verdict and the share of products
  in each grade (Excellent, Good, Fair, Poor).
- **Tiles:** **Products Scanned**, **Critical Issues**, **SEO Issues**, **Missing Images** and **Missing Attributes**.
  Click an issue tile to open the matching products:
  - **Critical Issues** opens the products that have at least one issue marked **critical** (for example a missing
    main image, missing description or missing name).
  - **SEO Issues**, **Missing Images** and **Missing Attributes** open the products with any issue in that audit.

  The tiles count **issues**, while the list shows **products**, so the numbers differ: one product can have several
  issues, and **Missing Images** opens every product with an image issue (for example too few gallery images), not
  only products without an image.
- **Issues by Module:** the number of issues found by each audit. Click a bar to see those products.
- **Lowest-scoring products:** the six products with the lowest scores. **View all** opens every product graded
  **Poor**.

**Audit Modules** shows each audit with its issue count, and **View affected products** for each one.

---

## 10. Review and fix products

**Applies to:** ✅ SaaS · ✅ PaaS (saving fixes on PaaS needs the Integration from section 4)

### Find products

Open **Product Scores**. You can:

- **Search** by SKU or product name.
- Filter by **Grade** (Excellent 90–100, Good 70–89, Fair 50–69, Poor 0–49).
- Filter by **Module with issue**: **Critical issues** (products with at least one critical issue), or one audit
  (Image, Description, Attribute, SEO, Duplicate).
- Filter by **Stock** (In stock, Out of stock, Stock unknown) or **Status** (Enabled, Disabled).
- **Sort** by lowest score, highest score or most issues.

The **Issues** column shows the number of issues and, in brackets, how many are critical, for example `5 (1 crit)`.
Tags show whether a product is **Available**, **Disabled**, **Out of stock** or **Not visible** on the storefront.

### See and fix the issues

1. Click **View** on a product. The dialog lists its issues by audit, each with its severity (critical, high, medium
   or low).
2. Issues about the **meta title**, **meta description**, **short description** or **description** have a **Fix**
   button. Click it: the editor opens with the current value from Commerce and a counter against the recommended
   length.
3. Edit the text and click **Save to Commerce**. The product is re-scored straight away and the new score is shown.

Other issues (images, price, categories, URL key, stock) are fixed in the Commerce Admin: go to **Catalog →
Products**, search for the SKU and edit the product. Then click **Re-check from Commerce** in the app (below).

> **Where fixes are saved:** as the default value (**All Store Views**). Store views that have their own value for that
> field keep it.

### Re-check a product

After changing a product in the Commerce Admin, click **Re-check from Commerce** in its dialog. The app fetches the
product again and updates its score without a full scan. Changes can take a few minutes to reach the storefront
catalog, so if the score hasn't changed yet, try again shortly.

---

## 11. Export the report

**Applies to:** ✅ SaaS · ✅ PaaS

On **Scan & Export**, click **Export CSV** or **Export Excel** to download the full report for the latest scan.

- Each row is one product: SKU, name, quality score, grade, number of issues and critical issues, the score of each
  audit and the list of issues.
- The Excel file also has a **Summary** sheet with the dashboard figures, and colour-codes the score column.

For catalogs above 2,000 products the file is prepared in the background first. The page shows **Preparing the …
file** and the download starts by itself when it is ready, usually within a minute or two. Keep the page open until
then.

---

## 12. How scores are calculated

**Applies to:** ✅ SaaS · ✅ PaaS

Each product gets a score from 0 to 100 in five audits. The product's quality score is the weighted average:

| Audit             | Weight | What it checks                                                                                                    |
| ----------------- | ------ | ----------------------------------------------------------------------------------------------------------------- |
| Image             | 25%    | A real main image (not a placeholder), at least 3 gallery images, image labels (alt text)                         |
| SEO               | 25%    | Meta title 15–60 characters, meta description 70–160 characters, a clean URL key, a meta title that differs from the product name |
| Description       | 20%    | A description of 20+ words (50+ recommended) and a short description of 5+ words                                   |
| Attribute         | 20%    | Name, price, URL key, categories and stock status are filled in. **SaaS:** the categories check is skipped         |
| Duplicate content | 10%    | The name, description or meta description isn't identical to another product's                                    |

Issues marked **critical**: no main image, no description, no product name. The **catalog health score** is the
average of all product scores.

**Good to know:**

- With working Admin API credentials (the Integration on PaaS), **every product** is scanned, including disabled
  products and products not visible individually (for example simple products inside a configurable). Without them,
  only products **visible on your storefront** are scanned, and **Scan & Export** says so.
- Duplicate content is compared across the whole catalog at the end of each scan. For a minute or two after the
  progress bar reaches 100%, the page shows **Checking for duplicates across the whole catalogue…**

---

## 13. Everyday use

**Applies to:** ✅ SaaS · ✅ PaaS

- **Daily scan:** the catalog is scanned automatically once a day. The dashboard always shows the latest finished
  scan; a scan in progress doesn't replace it until it completes.
- **Start a scan when needed:** **Scan & Export → Start Scan** (available whenever no scan is running), for example
  after a large import.
- **Work through the list:** use **Product Scores** with **Critical issues** first, then **Sort by → Lowest score
  first**.
- **After fixing products in the Admin:** use **Re-check from Commerce** for single products, or start a new scan for
  many.
- **Storage:** scan results are stored for 30 days. The app shows only the latest finished scan; there's no
  history of earlier scans.

---

## 14. Change settings or remove the app

**Applies to:** ✅ SaaS · ✅ PaaS

- **Change a setting:** **Apps → App Management → Configure**, change it and click **Save**. It applies within about
  a minute.
- **Add or replace the Integration (PaaS):** create it as in section 4, enter all four values in **Configure** and
  save.
- **Remove the app from a store:** **Apps → App Management**, click **Unassociate** on the app and confirm. This
  disconnects the app from the store. Scan results expire automatically after 30 days.
- **Stop using the app in your organization:** after unassociating every store, a System Administrator can undeploy
  the environments in **Adobe Exchange → Manage**.

---

## 15. Troubleshooting

**Applies to:** ✅ SaaS · ✅ PaaS (rows that differ say SaaS or PaaS)

| Problem                                                                                  | What to do                                                                                                                                                                                                       |
| ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Catalog Quality Analyzer** isn't listed in App Management                              | Check in **Adobe Exchange → Manage** that the app is **Approved** and the environment is **Deployed**, and that you're associating with the same Adobe organization.                                              |
| The app isn't in the Admin menu                                                          | Check that the card in **Apps → App Management** shows **Installed** (section 7). Sign out of the Admin and back in.                                                                                              |
| "Not authorized" or 401 errors                                                           | Open the app from the Commerce Admin menu, not from a bookmarked direct link. Sign out and back in to refresh your Adobe sign-in.                                                                                  |
| **Dashboard** says "No scan data yet"                                                    | No scan has finished yet. Run one in **Scan & Export** (section 8).                                                                                                                                              |
| **Start Scan** fails with "COMMERCE_GRAPHQL_ENDPOINT or COMMERCE_BASE_URL must be configured" | The app isn't associated with this store. Associate it (section 5).                                                                                                                                         |
| **Start Scan** fails with a connection or GraphQL error                                  | The storefront GraphQL API isn't reachable from the internet. PaaS: check that the site isn't behind a password, IP allowlist or maintenance mode.                                                                 |
| The scan shows **completed** with "Scan completed with some worker errors"               | Part of the catalog couldn't be read; the scan kept every product it did read. The **Workers** table shows each failed part and why. Run the scan again; if the same part keeps failing, contact support with that error. |
| The scan stays at **running** and the **Done** counts stop changing                      | Keep the page open: a part that stops reporting is marked failed after about 12 minutes and the scan then finishes on its own (see the row above). |
| Fewer products scanned than in the catalog                                               | Without Admin API credentials only storefront-visible products are scanned, and storefront search stops at about 10,000 products (section 12). PaaS: fill in the Integration in **Configure** (section 6). |
| **Configure** doesn't load or save (error 500 "Failed to decrypt value")                  | The saved settings were encrypted with a different key, usually after the app was redeployed with a new `AIO_COMMERCE_CONFIG_ENCRYPTION_KEY`. Contact support (section 17) to clear the saved settings, then enter the values again. |
| **Fix** shows "Could not load the current value from Commerce"                           | PaaS: fill in all four Integration values in **Configure** (section 6) and check that the integration is **Active** with access to **Products**. SaaS: contact support.                                           |
| **Save to Commerce** fails with "Saving fixes needs the Integration credentials…"        | PaaS: create the Integration (section 4) and enter its four values in **Configure**.                                                                                                                             |
| **Save to Commerce** fails with "Commerce API 401" or "403"                              | PaaS: the Integration is inactive, was re-generated, or lacks access to **Catalog → Inventory → Products**. Re-activate it or update the four values in **Configure**.                                              |
| The score doesn't change after editing a product in the Admin                            | The storefront catalog can take a few minutes to update. Click **Re-check from Commerce** again later, or wait for the next scan.                                                                                 |
| **Re-check** says the product was "not found in Commerce"                                | The product is disabled, not visible on the storefront, or not indexed yet.                                                                                                                                       |
| **Export** fails                                                                         | Click the export button again to retry. If it keeps failing, contact support (section 17) with the error shown.                                                                                                   |

---

## 16. Developer setup (from source)

**Applies to:** developers who build and deploy the app themselves, not merchants installing it from Adobe Exchange.

Requirements: Node.js 24, the Adobe I/O CLI (`npm install -g @adobe/aio-cli`) and an App Builder project with an
OAuth Server-to-Server credential.

1. Install the dependencies:

   ```bash
   npm install
   ```

2. Select your organization, project and workspace. This writes the Runtime and credential values into `.env`:

   ```bash
   aio app use
   ```

3. Create your environment file from the template and fill in the empty values (each one is explained in the file):

   ```bash
   cp env.dist .env
   ```

   If `aio app use` already created `.env`, copy only the missing variables from `env.dist` into it instead of
   overwriting it.

   Generate `AIO_COMMERCE_CONFIG_ENCRYPTION_KEY` once with `npx aio-commerce-lib-config encryption setup` and keep
   it. If you change it after settings were saved in **Configure**, the saved values can no longer be decrypted and
   the Configure page fails until they are cleared and entered again.

4. Run the tests and deploy:

   ```bash
   npm test
   aio app deploy
   ```

5. Associate, configure and install the app in your Commerce Admin (sections 5 to 7).

Build details, local UI development and the architecture are in [docs/DEVELOPMENT.md](docs/DEVELOPMENT.md).

---

## 17. Support

**Applies to:** ✅ SaaS · ✅ PaaS

18th Digitech Pvt Ltd: **support@18dapps.com**

Please include: your Adobe organization name, the environment (for example `Production`), the store URL, what you
did, what you expected and a screenshot of the error (for a scan problem: **Scan & Export**, including the **Workers**
table). Never send your Commerce Integration keys or tokens.
