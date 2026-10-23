# Catalog Quality Analyzer

The **Catalog Quality Analyzer** checks every product in your Adobe Commerce catalog (SaaS and PaaS) for content
problems and gives each one a quality score from 0 to 100.

It finds missing images, thin descriptions, missing attributes, weak SEO and duplicate content, and shows the results
on a catalog health dashboard in the Commerce Admin. You can fix SEO and description text directly from the app.
You deploy it to your own Adobe App Builder project with the Adobe I/O CLI, then associate and install it in the
Commerce Admin through App Management.

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

- Node.js v24
- Adobe I/O CLI v10+ (`npm install -g @adobe/aio-cli`)
- A hosted Adobe Commerce instance (SaaS, or PaaS 2.4.5 to 2.4.9) with App Management. Local installations are not supported
- Adobe Admin UI SDK 4.2.0 or later

---

## 📦 Installation at a Glance

See [**INSTALL.md**](INSTALL.md) for every step in detail.

### ⚠️ Good to Know

- **Fixes are saved as the default value (All Store Views).** Fixes are applied to the default (All Store Views) value. Store views with their own custom value are not changed.
- **Scan results are stored for 30 days.** The app shows only the latest finished scan (no history); a scan in
  progress doesn't replace it until it completes.
- **Dashboard tiles count issues, the lists show products**, Dashboard card counts differ from the product lists. For example, the Missing Images card counts products with missing images, but the list shows all products with any image-related issue.
- **Duplicate content is checked across the whole catalog** at the end of each scan. Re-checking a single product keeps
  its duplicate flags until the next scan, unless you changed that field.
- **Very large catalogs:** exports above 2,000 products are prepared in the background and downloaded from a link
  when ready, which can take a minute or two. Storefront search often stops at about 10,000 products; above that the scan
  reads the product list through the Admin API, which needs the same credentials as saving fixes.
- **SaaS:** category checks are skipped, because the SaaS catalog service doesn't return product categories to the app.

---

## 📩 Support

18th Digitech Pvt Ltd: **support@18dapps.com**