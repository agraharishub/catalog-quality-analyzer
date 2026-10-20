# Catalog Quality Analyzer

The **Catalog Quality Analyzer** checks every product in your Adobe Commerce catalog (SaaS and PaaS) for content
problems and gives each one a quality score from 0 to 100.

It finds missing images, thin descriptions, missing attributes, weak SEO and duplicate content, and shows the results
on a catalog health dashboard in the Commerce Admin. You can fix SEO and description text directly from the app.
Merchants get it on Adobe Exchange and set it up in the Commerce Admin. You don't need to download code or use a
command line, and no store credentials are needed to scan.

---

## 🚀 Features

- **Catalog health dashboard:** an overall health score plus products scanned, critical issues, SEO issues, missing
  images and missing attributes, issues by audit and the lowest-scoring products. Click an issue tile to see the
  products behind it
- **Five audits, one score:** Image (25%), SEO (25%), Description (20%), Attribute (20%) and Duplicate content (10%)
  combine into a 0–100 score per product, graded Excellent, Good, Fair or Poor
- **Product Scores page:** search by SKU or name, filter by grade, by audit, by **critical issues**, by stock
  (in stock, out of stock, unknown) or by status (enabled, disabled), sort by score or number of issues, and see
  every issue for a product with its severity
- **Fix in the app:** edit the meta title, meta description, short description or description and save it straight
  to Commerce. The product is re-scored immediately
- **Re-check a product:** after editing a product in the Admin, refresh just that product's score without a full scan
- **Automatic daily scan:** the catalog is scanned once a day, and you can start a scan from **Scan & Export**
  whenever no scan is running
- **Export:** download the full report as CSV or Excel (Excel includes a summary sheet and colour-coded scores)
- **Works on SaaS and PaaS:** the app detects your Commerce type and store automatically
- **Secure by default:** every request to the app needs a valid Adobe sign-in. The app can only change the four
  text fields above, never prices, stock or other data, and Integration credentials are stored encrypted

---

## ✅ Requirements

- Adobe Commerce (SaaS or PaaS) with **Apps → App Management**, on a hosted environment (App Management doesn't
  support local Commerce installations)
- **Admin UI SDK 4.2.0 or later** (needed for the app's Admin menu entry; App Management itself needs 3.3.0+)
- An Admin user with the **App Management** permission (Admin UI SDK resources in the user's role)
- An Adobe organization entitled to **Adobe App Builder**
- Your storefront GraphQL must be reachable from the internet. The app reads the catalog through it. If your store
  uses an IP allowlist, allow the Adobe I/O Runtime egress IPs
- PaaS only, optional: a **Commerce Integration** with access to products, to save fixes from the app and scan the
  full catalog (without it, only storefront-visible products are scanned)

---

## 📦 Installation at a Glance

| # | Step                                                   | Where                                           | Guide                                                             | SaaS / PaaS |
| - | ------------------------------------------------------ | ----------------------------------------------- | ----------------------------------------------------------------- | ----------- |
| 1 | Get **Catalog Quality Analyzer**                       | Adobe Exchange                                  | [Section 2](INSTALL.md#2-get-the-app-on-adobe-exchange)           | Both        |
| 2 | Approve it, add an environment and **Deploy**          | Adobe Exchange → Manage (System Admin)          | [Section 3](INSTALL.md#3-approve-and-deploy-it)                   | Both        |
| 3 | Create an Integration (optional; SaaS: skip)           | Commerce Admin → System → Integrations          | [Section 4](INSTALL.md#4-create-a-commerce-integration-paas-only) | PaaS only   |
| 4 | **Associate** the app                                  | Commerce Admin → Apps → App Management          | [Section 5](INSTALL.md#5-associate-the-app-in-the-commerce-admin) | Both        |
| 5 | **Configure** the app                                  | Commerce Admin → Apps → App Management          | [Section 6](INSTALL.md#6-configure-the-app)                       | Both        |
| 6 | **Install**                                            | Commerce Admin → Apps → App Management          | [Section 7](INSTALL.md#7-install-the-app)                         | Both        |
| 7 | Press **Start Scan**                                   | Apps → Catalog Quality Analyzer → Scan & Export | [Section 8](INSTALL.md#8-run-your-first-scan)                     | Both        |
| 8 | Review the dashboard and fix low-scoring products      | Apps → Catalog Quality Analyzer                 | [Sections 9–10](INSTALL.md#9-read-the-dashboard)                  | Both        |

See [**INSTALL.md**](INSTALL.md) for every step in detail, everyday use and troubleshooting.

Settings in **Configure**: on **PaaS**, the four Integration keys and tokens that let the app save fixes (stored
encrypted). On **SaaS** there is nothing to fill in. The store URL and whether you're on SaaS or PaaS are sent by
Commerce when you associate the app, so you never enter them.

### ⚠️ Good to Know

- **Every product in the catalog is scanned** when the app has Admin API credentials (the ones used for saving
  fixes), including disabled products and products not visible individually (for example, the simple products
  inside a configurable). Products the storefront shows are scored from storefront data; the rest from their Admin
  data. Without working credentials, only storefront-visible products are scanned, and the scan page says so.
- **Fixes are saved as the default value (All Store Views).** Store views that have their own value for that field
  keep it.
- **Scan results are stored for 30 days.** The app shows only the latest finished scan (no history); a scan in
  progress doesn't replace it until it completes.
- **Dashboard tiles count issues, the lists show products**, so the numbers differ. For example, **Missing Images**
  opens every product with any image issue.
- **Duplicate content is checked across the whole catalog** at the end of each scan. Re-checking a single product keeps
  its duplicate flags until the next scan, unless you changed that field.
- **Very large catalogs:** exports above 2,000 products are prepared in the background and downloaded from a link
  when ready, which can take a minute or two. Storefront search often stops at about 10,000 products; above that the scan
  reads the product list through the Admin API, which needs the same credentials as saving fixes.
- **If part of a scan fails** (for example the store doesn't answer, or a part runs into the time limit), the scan
  still finishes with the products it could read and is marked **completed with some worker errors**.
- **SaaS:** category checks are skipped, because the SaaS catalog service doesn't return product categories to the app.

---

## 🛠️ For Developers

Build, run and deploy instructions, environment variables and the architecture are in
[**docs/DEVELOPMENT.md**](docs/DEVELOPMENT.md). See also [docs/API.md](docs/API.md) and
[docs/ARCHITECTURE.md](docs/ARCHITECTURE.md).

---

## 📩 Support

18th Digitech Pvt Ltd: **support@18dapps.com**
