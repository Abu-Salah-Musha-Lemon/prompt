# Inventory Management Admin Dashboard — Regeneration Prompt

> Written for a developer or AI agent tasked with rebuilding this panel from scratch.

---

## 1. Project Overview

Build a full-featured, multi-page **Inventory Management & POS Admin Dashboard** as a static HTML/CSS/JS template. The system is aimed at retail/wholesale businesses and covers the entire inventory lifecycle — products, purchasing, sales, returns, transfers, expenses, quotations, people (customers & suppliers), reporting, and system settings.

The template must be **fully responsive** (mobile, tablet, desktop) and ship as standalone `.html` files with shared `assets/` — no build tools required.

---

## 2. Tech Stack

| Layer | Technology |
|---|---|
| Markup | HTML5, semantic elements |
| Styling | Bootstrap 5 + custom `style.css` |
| Icons | Font Awesome 5 Free + Feather Icons (via `feather.min.js`) |
| Charts | ApexCharts (`apexcharts.min.js` + `chart-data.js`) |
| Tables | jQuery DataTables with Bootstrap 4 skin |
| Date Picker | Bootstrap DateTime Picker |
| Select | Select2 |
| Carousel | Owl Carousel 2 |
| Scroll | jQuery SlimScroll |
| Utility JS | jQuery 3.6.0, Bootstrap Bundle 5 |
| Alerts | SweetAlert2 |
| Misc | Animate.css (entrance animations), global page loader (whirly spinner) |

---

## 3. Color System & Design Tokens

```css
/* Primary brand — used on CTAs, active states, links, accents */
--primary:      #FF9F43;
--primary-dark: #FE820E;

/* Sidebar active / dark backgrounds */
--dark-navy:    #1B2850;
--dark-bg:      #141432;   /* dark mode root */
--dark-card:    #1D1D42;   /* dark mode card */
--dark-border:  #353570;

/* Semantic */
--success:  #28C76F;
--danger:   #EA5455;
--info:     #00CFE8;
--warning:  #F90;
--purple:   #7367F0;

/* Text */
--text-primary:   #212B36;
--text-secondary: #637381;
--text-light:     #B8BCC9;

/* Surfaces */
--body-bg:    #FAFBFE;
--card-bg:    #FFFFFF;
--border:     #E8EBED;
--table-head: #FAFBFE;

/* Scrollbar — thin, #FF9F43 thumb */
```

**Typography:** `Nunito, sans-serif` — base size 14px, line-height 1.5.

---

## 4. Global Layout Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│  .header  (fixed, h=60px, white, box-shadow)                    │
│  ├── .header-left (w=260px, logo + toggle btn)                  │
│  ├── #mobile_btn (hamburger, visible < 992px)                   │
│  └── .user-menu (search, language flag, notifications, avatar)  │
├──────────────┬──────────────────────────────────────────────────┤
│  .sidebar    │  .page-wrapper                                   │
│  (fixed,     │  (margin-left: 260px, padding-top: 60px)        │
│   top=60px,  │  └── .content (padding: 25px)                   │
│   w=260px,   │       └── page-specific HTML                    │
│   white,     │                                                  │
│   border-r)  │                                                  │
└──────────────┴──────────────────────────────────────────────────┘
```

**Mini-sidebar mode** (`body.mini-sidebar`): sidebar collapses to 80px showing only icons; expands on hover (`body.expand-menu`).

**Dark mode:** toggled via `body[data-theme=dark]`. Surfaces flip to `--dark-bg / --dark-card / --dark-border`.

---

## 5. Header — Detailed Specification

- **Logo area** (`.header-left`, 260px wide, right border): two `<img>` variants — full logo (shown normally) and small square logo (shown in mini-sidebar). Toggle button (`#toggle_btn`) with a circular dot indicator when active.
- **Search bar** (`.top-nav-search`): 230px wide rounded input with SVG search icon button; on mobile collapses into a slide-down overlay triggered by `.responsive-search` icon.
- **Language switcher** (`.flag-nav` dropdown): flag thumbnail images for EN, FR, ES, DE.
- **Notifications dropdown** (`.notifications`): bell icon with an orange badge count; dropdown has a fixed-height (290px) scrollable list of notification items (avatar + message + relative time), a header with "Clear All" link, and a footer "View all" link → `activities.html`.
- **User menu** (`.main-drop`): avatar with green online dot; dropdown shows profile card (avatar + name "John Doe" + role "Admin"), "My Profile" → `profile.html`, "Settings" → `generalsettings.html`, "Logout" → `signin.html`.
- **Mobile fallback** (`.mobile-user-menu`, visible < 576px): ellipsis icon triggering a compact dropdown.

---

## 6. Sidebar — Navigation Tree

The sidebar uses `ul > li` with nested `ul` for submenus. Each top-level item has an SVG/PNG icon + text + optional `.menu-arrow` chevron.  
Active item: `background: #1B2850; border-radius: 5px; icon filter: brightness(0) invert(1)`.  
Submenu items: indented with a `::after` dot bullet; active dot = `#092C4C`.

**Full navigation structure:**

```
Dashboard                         → index.html

Product ▾
  Product List                    → productlist.html
  Add Product                     → addproduct.html
  Category List                   → categorylist.html
  Add Category                    → addcategory.html
  Sub Category List               → subcategorylist.html
  Add Sub Category                → subaddcategory.html
  Brand List                      → brandlist.html
  Add Brand                       → addbrand.html
  Import Products                 → importproduct.html
  Print Barcode                   → barcode.html

Sales ▾
  Sales List                      → saleslist.html
  POS                             → pos.html
  New Sales                       → pos.html
  Sales Return List               → salesreturnlists.html
  New Sales Return                → createsalesreturns.html

Purchase ▾
  Purchase List                   → purchaselist.html
  Add Purchase                    → addpurchase.html
  Import Purchase                 → importpurchase.html

Expense ▾
  Expense List                    → expenselist.html
  Add Expense                     → createexpense.html
  Expense Category                → expensecategory.html

Quotation ▾
  Quotation List                  → quotationList.html
  Add Quotation                   → addquotation.html

Transfer ▾
  Transfer List                   → transferlist.html
  Add Transfer                    → addtransfer.html
  Import Transfer                 → importtransfer.html

Return ▾
  Sales Return List               → salesreturnlist.html
  Add Sales Return                → createsalesreturn.html
  Purchase Return List            → purchasereturnlist.html
  Add Purchase Return             → createpurchasereturn.html

People ▾
  Customer List                   → customerlist.html
  Add Customer                    → addcustomer.html
  Supplier List                   → supplierlist.html
  Add Supplier                    → addsupplier.html
  Store List                      → storelist.html
  Add Store                       → addstore.html
  User List                       → userlist.html
  Add User                        → adduser.html

Reports ▾
  Purchase Order Report           → purchaseorderreport.html
  Inventory Report                → inventoryreport.html
  Invoice Report                  → invoicereport.html
  Sales Report                    → salesreport.html
  Purchase Report                 → purchasereport.html
  Supplier Report                 → supplierreport.html
  Customer Report                 → customerreport.html

Settings ▾
  General Settings                → generalsettings.html
  Email Settings                  → emailsettings.html
  Payment Settings                → paymentsettings.html
  Currency Settings               → currencysettings.html
  Tax Rates                       → taxrates.html
  Group Permissions               → grouppermissions.html
  Create Permission               → createpermission.html

UI Extras ▾
  Charts (Apex/JS/Morris/Flot/Peity)
  Forms (inputs, select2, wizard, upload, masks, validation)
  Tables (basic, DataTables)
  Icons (Feather, FA, Material, etc.)
  Pages (profile, activities, calendar, chat, email, notifications,
          timeline, blank, error-404, error-500)
```

---

## 7. Dashboard — `index.html`

### KPI Row 1 — `.dash-widget` cards (4 × col-lg-3)

Each card: white bg, 1px border `#E8EBED`, border-radius 6px, padding 20px, flex row (icon circle left + text right).

| # | Icon bg (rgba) | Metric | Value |
|---|---|---|---|
| 0 | `rgba(249,110,111,.12)` orange-red | Total Purchase Due | $307,144.00 |
| 1 | `rgba(40,199,111,.12)` green | Total Sales Due | $4,385.00 |
| 2 | `rgba(0,207,232,.12)` cyan | Total Sale Amount | $385,656.50 |
| 3 | `rgba(234,84,85,.12)` red | Total Sale Amount | $400.00 |

### KPI Row 2 — `.dash-count` cards (4 × col-lg-3)

Solid colored cards with large count + label + Feather icon (hover icon scales 1.25×).

| Class | Color | Label | Count | Icon |
|---|---|---|---|---|
| (default) | `#FF9F43` | Customers | 100 | `user` |
| `.das1` | `#00CFE8` | Suppliers | 100 | `user-check` |
| `.das2` | `#1B2850` | Purchase Invoice | 100 | `file-text` |
| `.das3` | `#28C76F` | Sales Invoice | 105 | `file` |

### Charts Row

- **Left (col-lg-7):** Card titled "Purchase & Sales" with a year selector dropdown (2022/2021/2020) and an ApexCharts area/line combo chart rendered in `#sales_charts`. Two legend items: "Sales" (green dot) and "Purchase" (red dot).
- **Right (col-lg-5):** Card titled "Recently Added Products" with a DataTable showing columns: Sno | Products (thumbnail + name link) | Price. Sample data: Apple Earpods $891.2, iPhone 11 $668.51, Samsung $522.29, Macbook Pro $291.01.

### Bottom Table

Full-width card titled "Expired Products". DataTable columns: SNo | Product Code | Product Name (thumbnail + name link) | Brand Name | Category Name | Expiry Date.

---

## 8. Authentication Pages

### `signin.html`
- Split layout: left 40% = form panel; right 60% = full-height image (`assets/img/login.jpg`). Below 992px image hides, form is full width.
- Form fields: Email (with mail icon addon) + Password (with toggle-visibility eye icon).
- "Forgot Password?" link → `forgetpassword.html`.
- Primary CTA: "Sign In" button → `index.html`.
- Social sign-up row: Google + Facebook buttons (icon + text).
- Logo at top, centered.

### `signup.html` — mirrors sign-in layout with registration fields.
### `forgetpassword.html` — email-only form with back-to-login link.

---

## 9. Product Module

### `productlist.html`
- Page header: title "Product List" + breadcrumb + action buttons: Filter (orange, 34×34), Import, Export (Excel/PDF/Print icons via `.wordset`), Add Product (orange, icon+text).
- Filter panel (`#filter_inputs`, initially hidden): warehouse, category, sub-category, brand, price range, status dropdowns in a card.
- Search row: text search input (200px, rounded, magnifier icon) + filter toggle button.
- DataTable columns: checkbox | Product | SKU | Category | Brand | Price | Unit | Qty | Created | Status (badge) | Action (view/edit/delete icons).
- Product thumbnails in table cells.

### `addproduct.html` / `editproduct.html`
- Card form with sections:
  - Product Information: Name, Category (Select2), Sub-Category, Brand, Unit (Select2), SKU (auto-generate button), Barcode Symbology (Select2).
  - Pricing & Stock: Cost (with calculator icon), Price, Tax % (Select2), Discount Type (Select2), Discount, Stock Alert, Expiry Date (calendar picker), Manufactured Date.
  - Image Upload: drag-and-drop zone (`.image-upload`) — displays thumbnail previews with remove (×) buttons.
  - Product Details: multiline text fields for description, notes.
- Submit / Cancel buttons (`.btn-submit`, `.btn-cancel`).

### `productlist.html` inline modals
- View product modal (`.product-details` full info)
- Delete confirmation (SweetAlert2 dialog)
- Barcode print modal: grid of barcode images

---

## 10. Sales Module

### `saleslist.html`
DataTable: Invoice # | Customer | Date | Status (Paid/Pending/Overdue badge) | Payment Status | Grand Total | Paid | Due | Action.

### `add-sales.html` / `edit-sales.html`
- Header fields: Customer (Select2 + add button), Date, Reference, Warehouse.
- Product search row: barcode scanner icon + text search + Select2 dropdown.
- Product line table: Product | Qty (increment/decrement input) | Price | Discount | Tax | Subtotal | Delete.
- Totals block (right-aligned): Sub Total, Tax, Discount, Shipping, Grand Total.
- Payment section: Payment Method (Cash/Card/etc.), Amount, Note.
- Footer: Submit / Cancel.

### `pos.html` — Point of Sale
Full-width, no sidebar. Special header (`.header-pos`).
- **Left panel:** product carousel (Owl Carousel) with category filter tabs (`.tab-set`), product cards (`.productset`) showing image, name, price; search input with barcode scanner; order list (`.order-list`) showing selected items with qty controls.
- **Right panel:** customer selector, totals card (`.total-order ul`), payment method buttons (`.btn-pos ul`: Hold, Quotation, Void, Payment, Recent Transaction), payment calculator (`.calculator-set`), cash/note/card payment modal.

---

## 11. Purchase Module

### `purchaselist.html`
DataTable: Date | Reference | Supplier | Status | Grand Total | Paid | Due | Action.

### `addpurchase.html`
Similar to add-sales but supplier-centric. Product lookup by barcode or name. Line items table. Totals block.

### `importpurchase.html`
File upload card: drag-and-drop CSV, download template link, upload/submit buttons.

---

## 12. People Module

### `customerlist.html` / `supplierlist.html`
DataTable: Avatar | Name | Code | Phone | Email | Country | Status (badge) | Action.

### `addcustomer.html` / `addsupplier.html`
Form: Name, Email, Phone, Country (Select2), City, Address, Tax Number, Description.

### `userlist.html`
DataTable: Name | Role | Email | Created | Status | Action.

### `adduser.html`
Form: username, email, password (with toggle), role (Select2), store (Select2), profile picture upload.

---

## 13. Settings Pages

All settings pages follow the same layout: left tab nav (General | Email | Payment | Currency | Tax | Permissions) or inline card sections.

### `generalsettings.html`
Fields: Site Name, Email, Phone, Address, Logo upload, Favicon upload, Currency Symbol, Currency Position, Language.

### `emailsettings.html`
SMTP fields: host, port, encryption, username, password, from email/name. Test email button.

### `paymentsettings.html`
Enable/disable toggles for payment gateways (Stripe, PayPal, etc.) with key/secret fields that reveal on toggle.

### `taxrates.html`
DataTable of tax rates (name + %) with add/edit/delete inline.

### `grouppermissions.html` / `createpermission.html`
Role → permission matrix with checkboxes per module (CRUD).

---

## 14. Reports Module

All report pages share the same pattern:
- Date range pickers (from/to) + optional filters (warehouse, supplier, customer, product).
- "Generate Report" / "Reset" buttons.
- DataTable of results.
- Export buttons: Excel, PDF, Print.

Pages: `salesreport.html`, `purchasereport.html`, `inventoryreport.html`, `supplierreport.html`, `customerreport.html`, `invoicereport.html`, `purchaseorderreport.html`.

---

## 15. Profile Page — `profile.html`

- Profile header banner (gradient `#EA5455 → #FF9F43`, height 109px).
- Avatar circle (130px, -40px margin-top, white border, box-shadow) with upload overlay button.
- Name + role displayed.
- Two-column form below: personal info (name, email, phone, DOB, role) + change password (old / new / confirm with visibility toggles).

---

## 16. Additional Pages

| File | Content |
|---|---|
| `activities.html` | Timeline-style activity feed (avatar + action + time) |
| `calendar.html` | FullCalendar integration with event modal |
| `chat.html` | Two-panel chat UI (contact list left, thread right, message composer) |
| `email.html` | Email client layout (folder list left, message list + preview right) |
| `notification.html` | Paginated notification list |
| `profile.html` | As above |
| `barcode.html` | Barcode print UI: Select product → generate barcode grid → print |
| `error-404.html` | Centred 404 with large orange `h1`, message, "Back to Home" button |
| `error-500.html` | Same pattern for 500 |
| `blankpage.html` | Empty page wrapper with header/sidebar only |

---

## 17. Shared Component Patterns

### Page Header
```html
<div class="page-header">
  <div class="page-title">
    <h4>Page Title</h4>
    <h6>Sub-description or breadcrumb</h6>
  </div>
  <div class="page-btn">
    <a href="add-page.html" class="btn btn-added">
      <img src="assets/img/icons/plus.svg" alt="img" class="me-1">Add New
    </a>
  </div>
</div>
```

### Search + Filter Toolbar
```html
<div class="table-top">
  <div class="search-set">
    <div class="search-input">
      <a class="btn btn-searchset"><img src="assets/img/icons/search-white.svg"></a>
      <input type="search" class="form-control form-control-sm" placeholder="Search...">
    </div>
    <a href="javascript:void(0);" id="collapse-header" class="btn btn-filter">
      <img src="assets/img/icons/filter.svg" alt="filter">
    </a>
  </div>
  <div class="wordset">
    <ul>
      <li><a href="#" title="excel"><img src="assets/img/icons/excel.svg"></a></li>
      <li><a href="#" title="pdf"><img src="assets/img/icons/pdf.svg"></a></li>
      <li><a href="#" title="print"><img src="assets/img/icons/printer.svg"></a></li>
    </ul>
  </div>
</div>
```

### Standard DataTable Card
```html
<div class="card">
  <div class="card-body">
    <div class="table-top"><!-- search + toolbar --></div>
    <div id="filter_inputs" class="card-body pb-0"><!-- filter fields --></div>
    <div class="table-responsive">
      <table class="table datatable">
        <thead>...</thead>
        <tbody>...</tbody>
      </table>
    </div>
  </div>
</div>
```

### Action Buttons in Table Rows
```html
<td>
  <a class="me-3" href="view-page.html"><img src="assets/img/icons/eye.svg"></a>
  <a class="me-3" href="edit-page.html"><img src="assets/img/icons/edit.svg"></a>
  <a href="javascript:void(0);" class="confirm-text">
    <img src="assets/img/icons/delete.svg">
  </a>
</td>
```

### Status Badges
```html
<span class="badges bg-lightgreen">Paid</span>
<span class="badges bg-lightred">Cancelled</span>
<span class="badges bg-lightyellow">Pending</span>
<span class="badges bg-lightpurple">Draft</span>
```

### Form Layout
```html
<div class="card">
  <div class="card-body">
    <div class="row">
      <div class="col-lg-6 col-sm-6 col-12">
        <div class="form-group">
          <label>Field Label <span class="manitory">*</span></label>
          <input type="text" class="form-control">
        </div>
      </div>
      <!-- more cols -->
    </div>
    <div class="col-lg-12">
      <a href="javascript:void(0);" class="btn btn-submit me-2">Submit</a>
      <a href="list-page.html" class="btn btn-cancel">Cancel</a>
    </div>
  </div>
</div>
```

---

## 18. JavaScript Initialisation (bottom of every page)

```html
<script src="assets/js/jquery-3.6.0.min.js"></script>
<script src="assets/js/feather.min.js"></script>
<script src="assets/js/jquery.slimscroll.min.js"></script>
<script src="assets/js/jquery.dataTables.min.js"></script>
<script src="assets/js/dataTables.bootstrap4.min.js"></script>
<script src="assets/js/bootstrap.bundle.min.js"></script>
<script src="assets/js/script.js"></script>
<!-- Page-specific -->
<script src="assets/plugins/apexchart/apexcharts.min.js"></script>  <!-- dashboard -->
<script src="assets/plugins/select2/js/select2.min.js"></script>     <!-- forms -->
<script src="assets/plugins/owlcarousel/owl.carousel.min.js"></script><!-- POS -->
```

`script.js` must handle:
- Sidebar toggle (`#toggle_btn`) → body class `mini-sidebar`
- Mobile nav (`#mobile_btn`) → `slide-nav` class
- Submenu expand/collapse (`.submenu > a` click)
- Active link detection on page load
- Feather icon replacement: `feather.replace()`
- DataTable auto-init: `$('.datatable').DataTable()`
- Select2 auto-init: `$('.select2').select2()`
- Delete confirm: SweetAlert2 on `.confirm-text` click
- Page loader hide on `$(window).load`
- Counter animation on `.counters` elements (count-up to `data-count`)
- Dark mode toggle (stored in localStorage)

---

## 19. Responsive Behaviour

| Breakpoint | Changes |
|---|---|
| ≥ 992px | Full sidebar (260px), page-wrapper margin-left 260px |
| < 992px | Sidebar off-canvas (margin-left: -575px), toggled by slide-nav; page-wrapper margin-left 0; header is full-width |
| < 576px | User menu hidden, mobile-user-menu shown; some flex columns stack vertically |

---

## 20. File & Folder Structure

```
project-root/
├── index.html
├── signin.html
├── signup.html
├── forgetpassword.html
├── [all other .html pages listed in Section 6]
└── assets/
    ├── css/
    │   ├── bootstrap.min.css
    │   ├── animate.css
    │   ├── dataTables.bootstrap4.min.css
    │   ├── bootstrap-datetimepicker.min.css
    │   └── style.css          ← primary custom stylesheet
    ├── js/
    │   ├── jquery-3.6.0.min.js
    │   ├── bootstrap.bundle.min.js
    │   ├── feather.min.js
    │   ├── jquery.slimscroll.min.js
    │   ├── jquery.dataTables.min.js
    │   ├── dataTables.bootstrap4.min.js
    │   └── script.js          ← custom JS (init + interactions)
    ├── plugins/
    │   ├── fontawesome/css/   ← fontawesome.min.css, all.min.css
    │   ├── apexchart/         ← apexcharts.min.js, chart-data.js
    │   ├── select2/css+js/
    │   ├── owlcarousel/
    │   └── ...
    └── img/
        ├── logo.png
        ├── logo-small.png
        ├── favicon.png
        ├── login.jpg
        ├── icons/             ← all SVG icons referenced in HTML
        ├── flags/             ← us.png, fr.png, es.png, de.png, us1.png
        ├── profiles/          ← avatar images
        ├── product/           ← product thumbnails
        ├── customer/          ← customer photos
        └── brand/             ← brand logos
```

---

## 21. Constraints & Notes

1. **No framework build required.** All CSS/JS is pre-compiled; the template is static HTML.
2. **DataTables `dataview` class** disables built-in pagination/length controls (custom controls used instead).
3. **Select2** must be initialised on all `<select>` elements with class `select2` or `select-one`.
4. **Image upload zones** use hidden `<input type="file">` overlaid by a styled drop zone; preview via JS FileReader.
5. **Barcode fields** use a scanner icon that fires a `keypress` listener; on Enter it searches the product table.
6. **POS page** does NOT use the standard `.sidebar` / `.page-wrapper` layout — it uses `.main-wrappers` with a stripped `.header-pos` instead.
7. **Dark mode** is body-attribute-driven: `body[data-theme="dark"]` only — no separate stylesheet.
8. **All modals** use Bootstrap 5 modal component. Delete confirmations use SweetAlert2.
9. Counter elements (`.counters`) should animate from 0 to the value in `data-count` on page load.
10. Every list/table page must have an empty-state row ("No records found") shown when DataTable has 0 rows.
