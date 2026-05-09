# ╔══════════════════════════════════════════════════════════════════╗
# ║   MASTER PROMPT — PRODUCTION ERP & INVENTORY ADMIN DASHBOARD   ║
# ║   Full-Stack UI Architect · Senior Frontend Engineer           ║
# ╚══════════════════════════════════════════════════════════════════╝

You are a **senior full-stack architect, frontend engineer, and UI/UX system designer**.

Generate a **COMPLETE, production-ready, MULTI-PAGE ERP + Inventory Management & POS Admin Dashboard** using HTML5, Bootstrap 5, and vanilla JavaScript. This must feel like a **real enterprise frontend system**, not a UI demo. Every page, component, and interaction must be consistent, polished, and scalable for future backend integration (Laravel / Django / Node.js).

---

## ═══════════════════════════════════════
## 1. OBJECTIVE
## ═══════════════════════════════════════

Build a modular ERP + Inventory/POS system UI that covers:

- ✔ Full inventory lifecycle (products, purchasing, sales, returns, transfers, expenses, quotations)
- ✔ ERP modules (HRMS, CRM, Finance, Warehouse, E-commerce, Reporting, Settings)
- ✔ POS (Point of Sale) terminal page
- ✔ Multiple standalone HTML pages — NO single-page app
- ✔ Shared reusable layout (sidebar + topbar) across all pages
- ✔ Fully responsive (mobile → tablet → desktop)
- ✔ No build tools required (pure static files, CDN only)

Apply:
- ✔ Golden Ratio layout balance
- ✔ 60% / 30% / 10% design hierarchy (neutral / containers / accent)

---

## ═══════════════════════════════════════
## 2. TECH STACK — STRICT (CDN ONLY)
## ═══════════════════════════════════════

| Layer          | Library / Version                              |
|----------------|------------------------------------------------|
| Markup         | HTML5, semantic elements                       |
| Styling        | Bootstrap 5.3 (CDN)                            |
| Icons          | Bootstrap Icons 1.11 + Font Awesome 6 Free     |
| Charts         | ApexCharts (CDN)                               |
| Tables         | jQuery DataTables 1.13 + Bootstrap 5 skin      |
| Notifications  | Toastr.js (CDN)                                |
| Alerts         | SweetAlert2 (CDN)                              |
| Select         | Select2 4.1 (CDN)                              |
| Date Picker    | Flatpickr (CDN)                                |
| Scroll         | jQuery SlimScroll (CDN)                        |
| Utility JS     | jQuery 3.7, Bootstrap Bundle 5.3               |
| Misc           | Animate.css (CDN), global whirly page loader   |

❌ No React / Vue / Angular  
❌ No backend code (but structure MUST support future integration)  
❌ No npm / webpack / build tools — CDN only

---

## ═══════════════════════════════════════
## 3. PROJECT FILE STRUCTURE (MANDATORY)
## ═══════════════════════════════════════

```
/erp-dashboard/
│
├── index.html              ← Dashboard (KPIs, charts, summary)
├── sales.html              ← Sales list, add sale
├── add-sales.html          ← Add/edit sale form
├── salesreturnlist.html    ← Sales returns
├── purchase.html           ← Purchase list
├── addpurchase.html        ← Add/edit purchase form
├── purchasereturnlist.html ← Purchase returns
├── pos.html                ← Point of Sale terminal
├── inventory.html          ← Products, stock levels
├── addproduct.html         ← Add/edit product form
├── categorylist.html       ← Product categories
├── brandlist.html          ← Brands
├── warehouse.html          ← Warehouse management
├── transfer.html           ← Stock transfers
├── expense.html            ← Expenses list
├── quotation.html          ← Quotations
├── hrms.html               ← Employees, attendance, payroll
├── crm.html                ← Leads, deals, contacts
├── ecommerce.html          ← Orders, customers, products
├── finance.html            ← Invoices, payments, expenses
├── reports.html            ← Charts, filters, exports
├── settings.html           ← Profile & system preferences
├── customerlist.html       ← Customer management
├── supplierlist.html       ← Supplier management
├── userlist.html           ← User management
├── barcode.html            ← Barcode print utility
├── profile.html            ← User profile
├── activities.html         ← Activity log / notifications
├── signin.html             ← Login page
├── signup.html             ← Registration page
├── error-404.html          ← 404 error page
├── error-500.html          ← 500 error page
│
└── assets/
    ├── css/
    │   └── style.css       ← All custom styles
    ├── js/
    │   └── script.js       ← All custom JS (init + interactions)
    └── img/
        ├── logo.png
        ├── logo-small.png
        └── favicon.png
```

> **Note on partials:** Since pure HTML has no native includes, duplicate the header/sidebar/footer structure consistently across every page. All shared JS lives in `assets/js/script.js` and is loaded on every page.

---

## ═══════════════════════════════════════
## 4. COLOR SYSTEM & DESIGN TOKENS
## ═══════════════════════════════════════

```css
:root {
  /* ── Primary Brand (10% accent) ── */
  --primary:        #FF9F43;
  --primary-dark:   #FE820E;
  --primary-light:  rgba(255, 159, 67, 0.12);

  /* ── Sidebar / Container (30%) ── */
  --sidebar-bg:     #FFFFFF;
  --dark-navy:      #1B2850;    /* active item bg */
  --dark-bg:        #141432;    /* dark mode root */
  --dark-card:      #1D1D42;    /* dark mode card */
  --dark-border:    #353570;

  /* ── Body / Neutral (60%) ── */
  --body-bg:        #FAFBFE;
  --card-bg:        #FFFFFF;
  --border:         #E8EBED;
  --table-head-bg:  #FAFBFE;

  /* ── Semantic ── */
  --success:        #28C76F;
  --danger:         #EA5455;
  --info:           #00CFE8;
  --warning:        #FF9F43;
  --purple:         #7367F0;

  /* ── Text ── */
  --text-primary:   #212B36;
  --text-secondary: #637381;
  --text-light:     #B8BCC9;

  /* ── Radius & Shadow ── */
  --radius-sm:      6px;
  --radius-md:      10px;
  --radius-lg:      12px;
  --shadow-sm:      0 2px 8px rgba(0,0,0,0.06);
  --shadow-md:      0 4px 20px rgba(0,0,0,0.08);
}
```

**Typography:** `Nunito, sans-serif` — base 14px, line-height 1.5.  
**Scrollbar:** thin, `#FF9F43` thumb, `#F1F1F1` track.

---

## ═══════════════════════════════════════
## 5. GLOBAL LAYOUT ARCHITECTURE
## ═══════════════════════════════════════

```
┌──────────────────────────────────────────────────────────────────────┐
│  .header  (fixed, h=60px, white, box-shadow)                         │
│  ├── .header-left  (w=260px — logo + toggle btn + mini dot)          │
│  ├── #mobile_btn   (hamburger — visible only < 992px)                │
│  └── .user-menu    (search · language · notifications · avatar)      │
├──────────────────┬───────────────────────────────────────────────────┤
│  .sidebar        │  .page-wrapper                                    │
│  (fixed,         │  (margin-left: 260px, padding-top: 60px)         │
│   top=60px,      │  └── .content  (padding: 25px)                   │
│   w=260px,       │       └── ← page-specific content here →         │
│   white bg,      │                                                   │
│   border-right)  │                                                   │
└──────────────────┴───────────────────────────────────────────────────┘
```

**Mini-sidebar** (`body.mini-sidebar`): collapses to 80px icons-only; expands on hover (`body.expand-menu`). State persists via `localStorage`.

**Dark mode**: `body[data-theme="dark"]` — surfaces swap to `--dark-bg / --dark-card / --dark-border`. Toggle persists via `localStorage`.

---

## ═══════════════════════════════════════
## 6. TOPBAR / HEADER — FULL SPEC
## ═══════════════════════════════════════

Same across **every page**.

| Element | Spec |
|---|---|
| `.header-left` | 260px wide, right border `#E8EBED`, logo + toggle button |
| Full logo | `assets/img/logo.png` — 140px wide, hidden in mini-sidebar |
| Small logo | `assets/img/logo-small.png` — 30px, shown only in mini-sidebar |
| `#toggle_btn` | Circular dot indicator when sidebar is active |
| `#mobile_btn` | Hamburger — 3 bars, orange color, visible < 992px |
| Search | `.top-nav-search` — 230px rounded input + SVG icon; collapses to overlay on mobile |
| Language | `.flag-nav` dropdown — flag images: EN, FR, ES, DE |
| Notifications | Bell icon + orange badge; 290px fixed-height scrollable dropdown (avatar + message + time), "Clear All" + "View all → activities.html" |
| User avatar | `.main-drop` — avatar + green online dot; dropdown: profile card (name "John Doe", role "Admin") + links to profile.html, settings, logout |
| Mobile fallback | `.mobile-user-menu` (visible < 576px) — ellipsis → compact dropdown |

---

## ═══════════════════════════════════════
## 7. SIDEBAR — FULL NAVIGATION TREE
## ═══════════════════════════════════════

Same sidebar on **every page**. Uses `ul > li` with nested `ul` for submenus.

**Active item style:** `background: #1B2850; border-radius: 5px; icon filter: brightness(0) invert(1)`  
**Active detection:** JS reads `window.location.pathname` and adds `.active` to matching `<a>` and its parent `<li>`.  
**Collapsed mode:** `.menu-arrow` chevron — rotates 90° when open (`.subdrop` class on `<a>`).  
**Mini-sidebar:** icons only; hover shows floating submenu panel.

```
Dashboard                             → index.html

Product ▾
  Product List                        → inventory.html
  Add Product                         → addproduct.html
  Category List                       → categorylist.html
  Add Category                        → categorylist.html#add
  Brand List                          → brandlist.html
  Add Brand                           → brandlist.html#add
  Import Products                     → inventory.html#import
  Print Barcode                       → barcode.html

Sales ▾
  Sales List                          → sales.html
  POS Terminal                        → pos.html
  Add New Sale                        → add-sales.html
  Sales Return List                   → salesreturnlist.html

Purchase ▾
  Purchase List                       → purchase.html
  Add Purchase                        → addpurchase.html
  Purchase Return List                → purchasereturnlist.html

Expense ▾
  Expense List                        → expense.html
  Add Expense                         → expense.html#add
  Expense Category                    → expense.html#categories

Quotation ▾
  Quotation List                      → quotation.html
  Add Quotation                       → quotation.html#add

Transfer ▾
  Transfer List                       → transfer.html
  Add Transfer                        → transfer.html#add

Return ▾
  Sales Return                        → salesreturnlist.html
  Purchase Return                     → purchasereturnlist.html

People ▾
  Customer List                       → customerlist.html
  Supplier List                       → supplierlist.html
  Store / Warehouse                   → warehouse.html
  User List                           → userlist.html

HRMS ▾
  Employees                           → hrms.html
  Attendance                          → hrms.html#attendance
  Payroll                             → hrms.html#payroll

CRM ▾
  Leads                               → crm.html#leads
  Deals Pipeline                      → crm.html#deals
  Contacts                            → crm.html#contacts

Finance ▾
  Invoices                            → finance.html#invoices
  Payments                            → finance.html#payments
  Expenses                            → finance.html#expenses

E-Commerce ▾
  Orders                              → ecommerce.html#orders
  Customers                           → ecommerce.html#customers
  Products                            → ecommerce.html#products

Reports                               → reports.html

Settings                              → settings.html

Logout                                → signin.html
```

---

## ═══════════════════════════════════════
## 8. DATATABLE — FULL FEATURE SPEC
## ═══════════════════════════════════════

**Every data table across every page** must use jQuery DataTables with the Bootstrap 5 skin and ALL of the following features configured:

### 8.1 Core DataTable Configuration (apply globally via `script.js`)

```javascript
$('.datatable').DataTable({
  // ── Pagination ──
  paging:       true,
  pageLength:   10,
  lengthMenu:   [[10, 25, 50, 100, -1], [10, 25, 50, 100, 'All']],
  lengthChange: true,

  // ── Search ──
  searching:    true,
  search: { smart: true, regex: false, caseInsensitive: true },

  // ── Ordering ──
  ordering:     true,
  order:        [[0, 'asc']],
  orderMulti:   true,        // shift+click multi-column sort

  // ── Info ──
  info:         true,        // "Showing X to Y of Z entries"

  // ── Responsive ──
  responsive:   true,        // collapses columns on small screens

  // ── Scroll ──
  scrollX:      true,        // horizontal scroll on overflow
  scrollCollapse: true,

  // ── Column Visibility ──
  colReorder:   true,        // drag-drop reorder columns
  buttons: [
    {
      extend:    'colvis',
      text:      '<i class="bi bi-layout-three-columns"></i> Columns',
      className: 'btn btn-sm btn-outline-secondary'
    },
    {
      extend:    'excel',
      text:      '<i class="bi bi-file-earmark-excel"></i> Excel',
      className: 'btn btn-sm btn-outline-success',
      exportOptions: { columns: ':visible' }
    },
    {
      extend:    'csv',
      text:      '<i class="bi bi-filetype-csv"></i> CSV',
      className: 'btn btn-sm btn-outline-info',
      exportOptions: { columns: ':visible' }
    },
    {
      extend:    'pdf',
      text:      '<i class="bi bi-file-earmark-pdf"></i> PDF',
      className: 'btn btn-sm btn-outline-danger',
      exportOptions: { columns: ':visible' }
    },
    {
      extend:    'print',
      text:      '<i class="bi bi-printer"></i> Print',
      className: 'btn btn-sm btn-outline-dark',
      exportOptions: { columns: ':visible' }
    },
    {
      extend:    'copy',
      text:      '<i class="bi bi-clipboard"></i> Copy',
      className: 'btn btn-sm btn-outline-secondary'
    }
  ],
  dom: "<'row mb-3'<'col-sm-6'l><'col-sm-6 text-end'B>>" +
       "<'row'<'col-sm-12'tr>>" +
       "<'row mt-3'<'col-sm-5'i><'col-sm-7'p>>",

  // ── State ──
  stateSave:    true,        // remember sort/page/length across refresh

  // ── Processing indicator ──
  processing:   true,
  language: {
    processing: '<div class="spinner-border text-warning" role="status"><span class="visually-hidden">Loading...</span></div>',
    search:          '',
    searchPlaceholder: 'Search...',
    lengthMenu:      'Show _MENU_ entries',
    info:            'Showing _START_ to _END_ of _TOTAL_ entries',
    infoEmpty:       'Showing 0 to 0 of 0 entries',
    infoFiltered:    '(filtered from _MAX_ total)',
    emptyTable:      '<div class="text-center py-4"><i class="bi bi-inbox fs-1 text-muted"></i><p class="mt-2 text-muted">No records found</p></div>',
    zeroRecords:     'No matching records found',
    paginate: {
      previous: '<i class="bi bi-chevron-left"></i>',
      next:     '<i class="bi bi-chevron-right"></i>'
    }
  }
});
```

### 8.2 Per-Row Features (required in every table)

Every table row must include:

```html
<!-- Row checkbox (bulk select) -->
<td><input type="checkbox" class="row-checkbox form-check-input"></td>

<!-- Status badge -->
<td><span class="badges bg-lightgreen">Active</span></td>

<!-- Action buttons -->
<td>
  <a href="#" class="action-btn view-btn"   title="View">
    <i class="bi bi-eye"></i>
  </a>
  <a href="#" class="action-btn edit-btn"   title="Edit">
    <i class="bi bi-pencil-square"></i>
  </a>
  <a href="#" class="action-btn delete-btn confirm-text" title="Delete">
    <i class="bi bi-trash3"></i>
  </a>
</td>
```

### 8.3 Bulk Actions Toolbar

Above every table, include a bulk-action bar (hidden until rows selected):

```html
<div id="bulk-actions" class="bulk-actions-bar d-none mb-3">
  <span class="selected-count me-3">0 selected</span>
  <button class="btn btn-sm btn-danger bulk-delete me-2">
    <i class="bi bi-trash3"></i> Delete Selected
  </button>
  <button class="btn btn-sm btn-warning bulk-status me-2">
    <i class="bi bi-toggle-on"></i> Change Status
  </button>
  <button class="btn btn-sm btn-secondary bulk-export">
    <i class="bi bi-download"></i> Export Selected
  </button>
</div>
```

### 8.4 Select-All Checkbox

Table header must include:

```html
<th><input type="checkbox" id="select-all" class="form-check-input"></th>
```

JS logic in `script.js`:
```javascript
// Select all / deselect all
$('#select-all').on('change', function () {
  const checked = this.checked;
  $('.row-checkbox').prop('checked', checked);
  updateBulkBar();
});
$('body').on('change', '.row-checkbox', updateBulkBar);

function updateBulkBar() {
  const count = $('.row-checkbox:checked').length;
  if (count > 0) {
    $('#bulk-actions').removeClass('d-none');
    $('.selected-count').text(count + ' selected');
  } else {
    $('#bulk-actions').addClass('d-none');
  }
}
```

### 8.5 Column-Level Filtering (below header row)

Each filterable table must have a second `<thead>` row with per-column filter inputs:

```html
<thead>
  <tr><!-- normal header --></tr>
  <tr class="column-filters">
    <th></th> <!-- checkbox col — no filter -->
    <th><input type="text"   class="form-control form-control-sm" placeholder="Filter..."></th>
    <th><input type="text"   class="form-control form-control-sm" placeholder="Filter..."></th>
    <th>
      <select class="form-select form-select-sm">
        <option value="">All Status</option>
        <option>Active</option>
        <option>Inactive</option>
      </select>
    </th>
    <th></th> <!-- action col — no filter -->
  </tr>
</thead>
```

Initialize column search in `script.js`:
```javascript
table.columns().every(function () {
  const col = this;
  $('input, select', col.footer() || $('.column-filters th').eq(col.index()))
    .on('keyup change', function () {
      if (col.search() !== this.value) col.search(this.value).draw();
    });
});
```

---

## ═══════════════════════════════════════
## 9. TOASTR NOTIFICATIONS — FULL SPEC
## ═══════════════════════════════════════

Use **Toastr.js** for all non-blocking user feedback. Configure globally in `script.js`:

### 9.1 Global Configuration

```javascript
toastr.options = {
  closeButton:       true,
  progressBar:       true,
  positionClass:     'toast-top-right',
  preventDuplicates: false,
  timeOut:           4000,
  extendedTimeOut:   1500,
  showEasing:        'swing',
  hideEasing:        'linear',
  showMethod:        'fadeIn',
  hideMethod:        'fadeOut',
  tapToDismiss:      true,
  newestOnTop:       true,
  maxOpened:         5,
  autoDismiss:       true
};
```

### 9.2 Toastr Trigger Points (use these everywhere)

```javascript
// ── CRUD operations ──
toastr.success('Record saved successfully!',   'Success');
toastr.success('Record updated successfully!', 'Updated');
toastr.success('Record deleted successfully!', 'Deleted');

// ── Validation errors ──
toastr.error('Please fill in all required fields.', 'Validation Error');
toastr.error('An unexpected error occurred.',       'Error');

// ── Info ──
toastr.info('Your session will expire in 5 minutes.', 'Session Warning');
toastr.info('Data is being loaded, please wait.',     'Loading');

// ── Warnings ──
toastr.warning('This action cannot be undone.',  'Warning');
toastr.warning('Stock level is below threshold.','Low Stock Alert');

// ── Form submit pattern ──
$('#save-btn').on('click', function (e) {
  e.preventDefault();
  // ... validate ...
  // on success:
  toastr.success('Record has been saved!', 'Success');
  // on failure:
  toastr.error('Save failed. Check your input.', 'Error');
});

// ── Delete pattern (with SweetAlert2 confirm → Toastr result) ──
$('.confirm-text').on('click', function () {
  Swal.fire({
    title:              'Are you sure?',
    text:               'This record will be permanently deleted.',
    icon:               'warning',
    showCancelButton:   true,
    confirmButtonColor: '#EA5455',
    cancelButtonColor:  '#637381',
    confirmButtonText:  'Yes, delete it!',
    cancelButtonText:   'Cancel'
  }).then(result => {
    if (result.isConfirmed) {
      // ... perform delete ...
      toastr.success('Record has been deleted.', 'Deleted');
    } else {
      toastr.info('Delete cancelled.', 'Cancelled');
    }
  });
});

// ── Bulk delete pattern ──
$('.bulk-delete').on('click', function () {
  const count = $('.row-checkbox:checked').length;
  Swal.fire({
    title: `Delete ${count} records?`,
    icon:  'warning',
    showCancelButton:   true,
    confirmButtonColor: '#EA5455',
    confirmButtonText:  'Delete All'
  }).then(r => {
    if (r.isConfirmed) toastr.success(`${count} records deleted.`, 'Bulk Delete');
  });
});

// ── Status toggle ──
$('.status-toggle').on('change', function () {
  const status = this.checked ? 'Active' : 'Inactive';
  toastr.info(`Status changed to ${status}`, 'Status Updated');
});

// ── Export feedback ──
$('.dt-button').on('click', function () {
  const label = $(this).text().trim();
  toastr.info(`Exporting as ${label}...`, 'Export');
});

// ── Import feedback ──
$('#import-btn').on('click', function () {
  toastr.success('File imported successfully! 24 records added.', 'Import Complete');
});

// ── Session warning (auto-trigger) ──
setTimeout(() => {
  toastr.warning('Your session will expire in 5 minutes.', 'Session Warning');
}, 55 * 60 * 1000); // 55 minutes
```

### 9.3 Toastr CDN Links

```html
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/toastr.js/latest/toastr.min.css">
<script src="https://cdnjs.cloudflare.com/ajax/libs/toastr.js/latest/toastr.min.js"></script>
```

---

## ═══════════════════════════════════════
## 10. DASHBOARD — index.html
## ═══════════════════════════════════════

### KPI Row 1 — `.dash-widget` (4 × col-lg-3)

White card, border `#E8EBED`, radius 6px, flex row: colored icon circle (left) + metric (right).

| # | Circle bg | Metric | Value |
|---|---|---|---|
| 0 | `rgba(255,159,67,.12)` | Total Purchase Due | $307,144 |
| 1 | `rgba(40,199,111,.12)` | Total Sales Due | $4,385 |
| 2 | `rgba(0,207,232,.12)` | Total Sale Amount | $385,656 |
| 3 | `rgba(234,84,85,.12)` | Total Expenses | $40,000 |

### KPI Row 2 — `.dash-count` (4 × col-lg-3)

Solid colored cards + Feather/BI icon (hover: scale 1.25×, 0.3s transition).

| Class | Color | Label | Count |
|---|---|---|---|
| default | `#FF9F43` | Customers | 100 |
| `.das1` | `#00CFE8` | Suppliers | 100 |
| `.das2` | `#1B2850` | Purchase Invoice | 100 |
| `.das3` | `#28C76F` | Sales Invoice | 105 |

### Charts Row

- **Left (col-lg-7):** "Purchase & Sales" — ApexCharts area/line combo in `#sales_charts`, year selector dropdown (2024/2023/2022), legend dots (green=Sales, red=Purchase).
- **Right (col-lg-5):** "Recently Added Products" — DataTable (Sno | Product | Price).

### Bottom Table

"Expired Products" — DataTable (SNo | Code | Product | Brand | Category | Expiry Date).

### Additional Dashboard Widgets

- **Mini stat cards row:** Total Revenue, New Orders, Pending Shipments, Low Stock Alerts
- **Recent Activities feed** (right column): avatar + action + timestamp list
- **Top Selling Products** bar chart (ApexCharts)
- **Revenue by Category** donut chart (ApexCharts)

---

## ═══════════════════════════════════════
## 11. PAGE-SPECIFIC CONTENT
## ═══════════════════════════════════════

### 11.1 sales.html
- Page header: "Sales List" + Add Sale button → `add-sales.html`
- Filter card: Date From/To (Flatpickr), Customer (Select2), Status dropdown, Apply/Reset
- DataTable columns: ☐ | Invoice # | Customer | Date | Payment Method | Status | Grand Total | Paid | Due | Action
- Status badges: Paid (green), Pending (yellow), Overdue (red), Cancelled (grey)

### 11.2 add-sales.html
- Header fields: Customer (Select2 + [+] add), Date (Flatpickr), Reference, Warehouse
- Product search: barcode scanner icon + text input + Select2 dropdown
- Line items table: Product | Qty (±) | Unit Price | Discount % | Tax % | Subtotal | [×]
- Totals block (right-aligned card): Sub Total / Tax / Discount / Shipping / Grand Total
- Payment: Method (Cash/Card/Bank), Amount Tendered, Note
- Footer: Submit → `toastr.success` / Cancel

### 11.3 purchase.html
- DataTable: ☐ | Reference | Supplier | Date | Status | Grand Total | Paid | Due | Action

### 11.4 addpurchase.html
- Same structure as add-sales but supplier-centric

### 11.5 pos.html
- NO sidebar / NO standard page-wrapper — standalone full-screen layout
- **Left panel:** category tabs, product cards grid (image + name + price), qty controls, barcode search
- **Right panel:** order list (product + qty + subtotal), customer select, totals, payment methods calculator
- POS-specific header (logo + search + user only — no nav)

### 11.6 inventory.html (Products)
- Filter card: Category, Brand, Warehouse, Status, Price Range
- DataTable: ☐ | Image | Name | SKU | Category | Brand | Price | Stock Qty | Status | Action
- Inline stock level badge: `<10` = red "Low", `10-50` = yellow "Medium", `>50` = green "Good"

### 11.7 addproduct.html
- **Product Info section:** Name, Category (Select2), Sub-Category, Brand, Unit, SKU (auto-generate), Barcode Symbology
- **Pricing & Stock:** Cost, Sell Price, Tax % (Select2), Discount Type, Discount, Reorder Qty, Expiry Date (Flatpickr), Mfg Date
- **Image Upload:** Drag-and-drop zone with FileReader preview + remove (×) button per image
- **Description / Notes:** textarea fields

### 11.8 hrms.html — 3-tab layout
- **Employees tab:** DataTable (☐ | Avatar | Name | Department | Role | Email | Phone | Join Date | Status | Action)
- **Attendance tab:** Month/year filter + DataTable (Employee | Mon | Tue | ... | Sun | Present | Absent | Late)
- **Payroll tab:** DataTable (Employee | Base | Bonus | Deductions | Net Pay | Month | Status | Action)

### 11.9 crm.html — 3-tab layout
- **Leads tab:** DataTable (☐ | Name | Company | Email | Phone | Source | Stage | Value | Action)
- **Deals Pipeline:** Kanban-style 5-column board: Prospecting → Qualification → Proposal → Negotiation → Closed; each card shows deal name + value + owner avatar
- **Contacts tab:** DataTable (☐ | Avatar | Name | Company | Email | Phone | Country | Action)

### 11.10 warehouse.html
- DataTable: ☐ | Warehouse Name | Code | City | Country | Manager | Phone | Status | Action
- "Add Warehouse" button → Bootstrap modal with full form

### 11.11 ecommerce.html — 3-tab layout
- **Orders tab:** DataTable (☐ | Order # | Customer | Date | Items | Total | Payment | Shipping Status | Action)
- **Customers tab:** DataTable (☐ | Avatar | Name | Email | Phone | Total Orders | Total Spent | Status | Action)
- **Products tab:** DataTable (☐ | Image | Name | Category | Price | Stock | Sold | Rating | Status | Action)

### 11.12 finance.html — 3-tab layout
- **Invoices tab:** DataTable (☐ | Invoice # | Client | Date | Due Date | Amount | Paid | Balance | Status | Action)
- **Payments tab:** DataTable (☐ | Payment # | Invoice # | Client | Date | Amount | Method | Status | Action)
- **Expenses tab:** DataTable (☐ | Category | Description | Date | Amount | Paid By | Status | Action) + Expense summary donut chart

### 11.13 reports.html
- Filter bar: Module (dropdown), Date Range (Flatpickr range), Warehouse, Format (PDF/Excel)
- 4 chart cards (2×2 grid): Sales Trend (line), Purchase vs Sales (bar), Inventory Value by Category (donut), Revenue by Month (area)
- Summary DataTable below charts

### 11.14 customerlist.html
- DataTable: ☐ | Avatar | Name | Code | Email | Phone | Country | Total Orders | Total Spent | Status | Action

### 11.15 supplierlist.html
- DataTable: ☐ | Avatar | Name | Code | Email | Phone | Country | Total Purchase | Balance | Status | Action

### 11.16 userlist.html
- DataTable: ☐ | Avatar | Name | Email | Role | Warehouse | Last Login | Status | Action

### 11.17 expense.html — 2-tab layout
- **Expense List tab:** DataTable (☐ | Category | Reference | Date | Amount | Note | Status | Action)
- **Expense Categories tab:** DataTable (☐ | Name | Description | Count | Action)

### 11.18 quotation.html
- DataTable: ☐ | Quote # | Customer | Date | Valid Until | Amount | Status | Action

### 11.19 transfer.html
- DataTable: ☐ | Reference | From Warehouse | To Warehouse | Date | Products | Status | Action

### 11.20 salesreturnlist.html / purchasereturnlist.html
- DataTable: ☐ | Return # | Original # | Customer/Supplier | Date | Amount | Reason | Status | Action

### 11.21 barcode.html
- Select product (Select2), select barcode symbology, set quantity
- Generate button → renders barcode image grid
- Print button → `window.print()` on barcode area

### 11.22 profile.html
- Banner gradient (`#EA5455 → #FF9F43`, 109px)
- Avatar (130px, −40px offset, white border, upload overlay button)
- Two-column form: Personal Info (name, email, phone, DOB, role, bio) | Change Password (current, new, confirm + eye toggles)

### 11.23 activities.html
- Timeline feed: avatar + event description + relative time
- Filter by type (All / Sales / Purchase / System / HR)

### 11.24 settings.html — Tab layout
- **General:** Site name, email, phone, address, logo/favicon upload, timezone, language, currency
- **Email:** SMTP host/port/encryption/username/password, from name/email, test send button
- **Payment:** Toggle cards per gateway (Stripe, PayPal, Bank Transfer) with key/secret reveal
- **Tax & Currency:** Tax rates DataTable (name + %), currency settings
- **Permissions:** Role → module permission matrix with checkboxes (CRUD per module)
- **Preferences:** Dark mode toggle, notification prefs, sidebar default state

### 11.25 signin.html
- Split: left 40% = form, right 60% = full-height image
- Fields: Email (mail icon addon) + Password (eye toggle)
- "Forgot Password?" link, Sign In CTA, Google + Facebook social buttons
- Below 992px: image hides, form goes full-width

### 11.26 error-404.html / error-500.html
- Centred: large orange `h1` (404/500), message text, "Back to Dashboard" button (→ index.html)

---

## ═══════════════════════════════════════
## 12. SHARED COMPONENT PATTERNS
## ═══════════════════════════════════════

### Page Header
```html
<div class="page-header">
  <div class="page-title">
    <h4>Page Title</h4>
    <h6>Breadcrumb / description</h6>
  </div>
  <div class="page-btn">
    <a href="add-page.html" class="btn btn-added">
      <i class="bi bi-plus-circle me-1"></i> Add New
    </a>
  </div>
</div>
```

### Filter Card (collapsible)
```html
<div class="card filter-card mb-3" id="filter-card" style="display:none;">
  <div class="card-body">
    <div class="row g-3">
      <div class="col-lg-3 col-md-6">
        <label class="form-label">From Date</label>
        <input type="text" class="form-control flatpickr-date" placeholder="Select date">
      </div>
      <div class="col-lg-3 col-md-6">
        <label class="form-label">Status</label>
        <select class="form-select select2">
          <option value="">All</option>
          <option>Active</option>
          <option>Inactive</option>
        </select>
      </div>
      <div class="col-lg-3 col-md-6 d-flex align-items-end">
        <button class="btn btn-primary me-2">Apply</button>
        <button class="btn btn-secondary">Reset</button>
      </div>
    </div>
  </div>
</div>
```

### Table Toolbar (above DataTable)
```html
<div class="table-top d-flex justify-content-between align-items-center mb-3">
  <div class="search-set d-flex gap-2">
    <div class="search-input position-relative">
      <i class="bi bi-search search-icon"></i>
      <input type="search" class="form-control ps-4" placeholder="Search...">
    </div>
    <button class="btn btn-filter" id="toggle-filter" title="Filter">
      <i class="bi bi-funnel"></i>
    </button>
  </div>
  <div class="wordset d-flex gap-2">
    <!-- Export buttons injected by DataTables buttons extension -->
  </div>
</div>
```

### Status Badges
```html
<span class="badges bg-lightgreen">Active / Paid</span>
<span class="badges bg-lightred">Inactive / Cancelled</span>
<span class="badges bg-lightyellow">Pending</span>
<span class="badges bg-lightpurple">Draft</span>
<span class="badges bg-lightblue">Processing</span>
```

CSS:
```css
.badges { font-size:12px; font-weight:500; padding:4px 10px; border-radius:5px; display:inline-block; }
.bg-lightgreen  { background: rgba(40,199,111,.15); color: #28C76F; }
.bg-lightred    { background: rgba(234,84,85,.15);  color: #EA5455; }
.bg-lightyellow { background: rgba(255,159,67,.15); color: #FF9F43; }
.bg-lightpurple { background: rgba(115,103,240,.15);color: #7367F0; }
.bg-lightblue   { background: rgba(0,207,232,.15);  color: #00CFE8; }
```

### Add/Edit Form Card
```html
<div class="card">
  <div class="card-body">
    <div class="row g-3">
      <div class="col-lg-6 col-md-6 col-12">
        <div class="form-group mb-3">
          <label class="form-label">Field Label <span class="text-danger">*</span></label>
          <input type="text" class="form-control" placeholder="Enter value">
        </div>
      </div>
    </div>
    <div class="d-flex gap-2 mt-3">
      <button type="submit" class="btn btn-submit">Save</button>
      <a href="list-page.html" class="btn btn-cancel">Cancel</a>
    </div>
  </div>
</div>
```

### Delete Confirmation (SweetAlert2 + Toastr)
```javascript
document.querySelectorAll('.confirm-text').forEach(btn => {
  btn.addEventListener('click', function(e) {
    e.preventDefault();
    Swal.fire({
      title:              'Delete this record?',
      text:               'This action cannot be undone.',
      icon:               'warning',
      showCancelButton:   true,
      confirmButtonColor: '#EA5455',
      cancelButtonColor:  '#637381',
      confirmButtonText:  'Yes, delete!'
    }).then(result => {
      if (result.isConfirmed) {
        btn.closest('tr').remove();
        toastr.success('Record deleted successfully!', 'Deleted');
      }
    });
  });
});
```

---

## ═══════════════════════════════════════
## 13. JAVASCRIPT — script.js FULL SPEC
## ═══════════════════════════════════════

`assets/js/script.js` must handle ALL of the following — loaded on every page:

```javascript
$(function () {

  // 1. PAGE LOADER — hide on window load
  $(window).on('load', function () {
    $('#global-loader').fadeOut(500);
  });

  // 2. FEATHER ICONS
  if (typeof feather !== 'undefined') feather.replace();

  // 3. SIDEBAR TOGGLE (mini-sidebar)
  const SIDEBAR_KEY = 'erp_sidebar_collapsed';
  function applySidebarState() {
    if (localStorage.getItem(SIDEBAR_KEY) === 'true') {
      $('body').addClass('mini-sidebar');
    }
  }
  applySidebarState();
  $('#toggle_btn').on('click', function () {
    $('body').toggleClass('mini-sidebar');
    localStorage.setItem(SIDEBAR_KEY, $('body').hasClass('mini-sidebar'));
  });

  // 4. MOBILE SIDEBAR
  $('#mobile_btn').on('click', function () {
    $('body').toggleClass('slide-nav');
    $('.sidebar-overlay').toggleClass('opened');
  });
  $('.sidebar-overlay, #dismiss').on('click', function () {
    $('body').removeClass('slide-nav');
    $('.sidebar-overlay').removeClass('opened');
  });

  // 5. SIDEBAR SUBMENU
  $('.sidebar .submenu > a').on('click', function (e) {
    e.preventDefault();
    const $li = $(this).parent();
    if ($li.hasClass('open')) {
      $li.removeClass('open');
      $li.children('ul').slideUp(200);
    } else {
      $li.siblings('.open').removeClass('open').children('ul').slideUp(200);
      $li.addClass('open');
      $li.children('ul').slideDown(200);
    }
    $(this).toggleClass('subdrop');
  });

  // 6. ACTIVE MENU DETECTION
  const currentPage = window.location.pathname.split('/').pop() || 'index.html';
  $('.sidebar a').each(function () {
    const href = $(this).attr('href');
    if (href && href.split('#')[0] === currentPage) {
      $(this).addClass('active');
      $(this).closest('li').addClass('active');
      $(this).closest('.submenu').addClass('open').children('a').addClass('subdrop active');
      $(this).closest('.submenu ul').show();
    }
  });

  // 7. DARK MODE
  const DARK_KEY = 'erp_dark_mode';
  if (localStorage.getItem(DARK_KEY) === 'true') {
    $('body').attr('data-theme', 'dark');
    $('#dark-toggle').prop('checked', true);
  }
  $('#dark-toggle').on('change', function () {
    if (this.checked) {
      $('body').attr('data-theme', 'dark');
      localStorage.setItem(DARK_KEY, 'true');
      toastr.info('Dark mode enabled', 'Theme');
    } else {
      $('body').removeAttr('data-theme');
      localStorage.removeItem(DARK_KEY);
      toastr.info('Light mode enabled', 'Theme');
    }
  });

  // 8. DATATABLES — global init
  if ($.fn.DataTable) {
    $('.datatable').each(function () {
      if (!$.fn.DataTable.isDataTable(this)) {
        $(this).DataTable({
          paging: true, pageLength: 10,
          lengthMenu: [[10,25,50,100,-1],[10,25,50,100,'All']],
          searching: true, ordering: true, info: true,
          responsive: true, scrollX: true, stateSave: true,
          processing: true, colReorder: true,
          buttons: [
            { extend:'colvis', text:'<i class="bi bi-layout-three-columns"></i> Columns', className:'btn btn-sm btn-outline-secondary' },
            { extend:'excel',  text:'<i class="bi bi-file-earmark-excel"></i> Excel',   className:'btn btn-sm btn-outline-success',  exportOptions:{columns:':visible'} },
            { extend:'csv',    text:'<i class="bi bi-filetype-csv"></i> CSV',           className:'btn btn-sm btn-outline-info',     exportOptions:{columns:':visible'} },
            { extend:'pdf',    text:'<i class="bi bi-file-earmark-pdf"></i> PDF',       className:'btn btn-sm btn-outline-danger',   exportOptions:{columns:':visible'} },
            { extend:'print',  text:'<i class="bi bi-printer"></i> Print',              className:'btn btn-sm btn-outline-dark',     exportOptions:{columns:':visible'} },
            { extend:'copy',   text:'<i class="bi bi-clipboard"></i> Copy',             className:'btn btn-sm btn-outline-secondary' }
          ],
          dom: "<'row mb-3'<'col-sm-6'l><'col-sm-6 text-end'B>>" +
               "<'row'<'col-sm-12'tr>>" +
               "<'row mt-3'<'col-sm-5'i><'col-sm-7'p>>",
          language: {
            processing:      '<div class="spinner-border text-warning" role="status"></div>',
            search:          '', searchPlaceholder: 'Search...',
            emptyTable:      '<div class="text-center py-4"><i class="bi bi-inbox fs-1 text-muted"></i><p class="mt-2 text-muted">No records found</p></div>',
            paginate: { previous:'<i class="bi bi-chevron-left"></i>', next:'<i class="bi bi-chevron-right"></i>' }
          }
        });
      }
    });
  }

  // 9. SELECT2
  if ($.fn.select2) {
    $('.select2').select2({ theme: 'bootstrap-5', width: '100%' });
  }

  // 10. FLATPICKR DATE PICKERS
  if (typeof flatpickr !== 'undefined') {
    flatpickr('.flatpickr-date', { dateFormat: 'd-m-Y', allowInput: true });
    flatpickr('.flatpickr-datetime', { enableTime: true, dateFormat: 'd-m-Y H:i' });
    flatpickr('.flatpickr-range', { mode: 'range', dateFormat: 'd-m-Y' });
  }

  // 11. TOASTR CONFIG
  toastr.options = {
    closeButton: true, progressBar: true,
    positionClass: 'toast-top-right',
    timeOut: 4000, extendedTimeOut: 1500,
    showMethod: 'fadeIn', hideMethod: 'fadeOut',
    newestOnTop: true, maxOpened: 5
  };

  // 12. COUNTER ANIMATION
  $('.counters').each(function () {
    const target = parseFloat($(this).data('count'));
    $(this).prop('Counter', 0).animate({ Counter: target }, {
      duration: 1500, easing: 'swing',
      step: function (now) {
        $(this).text(parseFloat(now.toFixed(2)).toLocaleString());
      },
      complete: function () {
        $(this).text(parseFloat(target.toFixed(2)).toLocaleString());
      }
    });
  });

  // 13. FILTER CARD TOGGLE
  $('#toggle-filter').on('click', function () {
    $('#filter-card').slideToggle(200);
    $(this).toggleClass('active');
  });

  // 14. SELECT ALL (bulk)
  $(document).on('change', '#select-all', function () {
    $('.row-checkbox').prop('checked', this.checked);
    updateBulkBar();
  });
  $(document).on('change', '.row-checkbox', updateBulkBar);
  function updateBulkBar() {
    const count = $('.row-checkbox:checked').length;
    if (count > 0) {
      $('#bulk-actions').removeClass('d-none');
      $('.selected-count').text(count + ' selected');
    } else {
      $('#bulk-actions').addClass('d-none');
    }
    $('#select-all').prop('indeterminate',
      count > 0 && count < $('.row-checkbox').length
    );
  }

  // 15. DELETE CONFIRM (SweetAlert2 + Toastr)
  $(document).on('click', '.confirm-text', function (e) {
    e.preventDefault();
    const $row = $(this).closest('tr');
    Swal.fire({
      title: 'Delete this record?', text: 'This cannot be undone.',
      icon: 'warning', showCancelButton: true,
      confirmButtonColor: '#EA5455', cancelButtonColor: '#637381',
      confirmButtonText: 'Yes, delete!'
    }).then(r => {
      if (r.isConfirmed) {
        $row.fadeOut(300, function () { $(this).remove(); });
        toastr.success('Record deleted successfully!', 'Deleted');
      }
    });
  });

  // 16. SLIMSCROLL for sidebar
  if ($.fn.slimScroll) {
    $('.slimscroll').slimScroll({ height: 'auto', width: '100%', position: 'right', size: '5px', color: '#FF9F43' });
  }

  // 17. TOOLTIP init
  $('[data-bs-toggle="tooltip"]').tooltip();

  // 18. IMAGE UPLOAD PREVIEW
  $(document).on('change', '.image-upload input[type=file]', function () {
    const files = this.files;
    const $container = $(this).siblings('.image-uploads');
    Array.from(files).forEach(file => {
      const reader = new FileReader();
      reader.onload = e => {
        const $thumb = $(`<div class="preview-thumb position-relative me-2 mb-2 d-inline-block">
          <img src="${e.target.result}" style="width:80px;height:80px;object-fit:cover;border-radius:6px;">
          <button type="button" class="remove-img btn btn-sm btn-danger position-absolute top-0 end-0" style="padding:0 4px;font-size:10px">×</button>
        </div>`);
        $container.append($thumb);
      };
      reader.readAsDataURL(file);
    });
  });
  $(document).on('click', '.remove-img', function () {
    $(this).closest('.preview-thumb').remove();
  });

  // 19. STATUS TOGGLE TOASTR
  $(document).on('change', '.status-toggle', function () {
    toastr.info(`Status changed to ${this.checked ? 'Active' : 'Inactive'}`, 'Updated');
  });

  // 20. FORM SAVE (generic — override per page)
  $(document).on('click', '.btn-submit', function (e) {
    const $form = $(this).closest('form, .card-body');
    const empty = $form.find('[required]').filter(function () { return !this.value.trim(); });
    if (empty.length) {
      toastr.error('Please fill all required fields.', 'Validation Error');
      empty.first().focus();
      return;
    }
    toastr.success('Record saved successfully!', 'Saved');
  });

});
```

---

## ═══════════════════════════════════════
## 14. CDN SCRIPT LOAD ORDER
## ═══════════════════════════════════════

### `<head>` — CSS

```html
<!-- Bootstrap 5 -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css">
<!-- Bootstrap Icons -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.3/font/bootstrap-icons.min.css">
<!-- Font Awesome 6 -->
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
<!-- DataTables + Bootstrap 5 skin -->
<link rel="stylesheet" href="https://cdn.datatables.net/1.13.8/css/dataTables.bootstrap5.min.css">
<link rel="stylesheet" href="https://cdn.datatables.net/buttons/2.4.2/css/buttons.bootstrap5.min.css">
<link rel="stylesheet" href="https://cdn.datatables.net/responsive/2.5.0/css/responsive.bootstrap5.min.css">
<link rel="stylesheet" href="https://cdn.datatables.net/colreorder/1.7.0/css/colReorder.bootstrap5.min.css">
<!-- Select2 -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/select2@4.1.0-rc.0/dist/css/select2.min.css">
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/select2-bootstrap-5-theme@1.3.0/dist/select2-bootstrap-5-theme.min.css">
<!-- Flatpickr -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/flatpickr/dist/flatpickr.min.css">
<!-- Toastr -->
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/toastr.js/latest/toastr.min.css">
<!-- SweetAlert2 -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/sweetalert2@11/dist/sweetalert2.min.css">
<!-- Animate.css -->
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css">
<!-- Custom -->
<link rel="stylesheet" href="assets/css/style.css">
```

### Before `</body>` — JS

```html
<!-- jQuery (MUST be first) -->
<script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
<!-- Bootstrap Bundle -->
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"></script>
<!-- DataTables core -->
<script src="https://cdn.datatables.net/1.13.8/js/jquery.dataTables.min.js"></script>
<script src="https://cdn.datatables.net/1.13.8/js/dataTables.bootstrap5.min.js"></script>
<!-- DataTables extensions -->
<script src="https://cdn.datatables.net/buttons/2.4.2/js/dataTables.buttons.min.js"></script>
<script src="https://cdn.datatables.net/buttons/2.4.2/js/buttons.bootstrap5.min.js"></script>
<script src="https://cdn.datatables.net/buttons/2.4.2/js/buttons.html5.min.js"></script>
<script src="https://cdn.datatables.net/buttons/2.4.2/js/buttons.colVis.min.js"></script>
<script src="https://cdn.datatables.net/buttons/2.4.2/js/buttons.print.min.js"></script>
<script src="https://cdn.datatables.net/responsive/2.5.0/js/dataTables.responsive.min.js"></script>
<script src="https://cdn.datatables.net/responsive/2.5.0/js/responsive.bootstrap5.min.js"></script>
<script src="https://cdn.datatables.net/colreorder/1.7.0/js/dataTables.colReorder.min.js"></script>
<!-- PDF / Excel export deps -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/jszip/3.10.1/jszip.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/pdfmake/0.2.7/pdfmake.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/pdfmake/0.2.7/vfs_fonts.js"></script>
<!-- Select2 -->
<script src="https://cdn.jsdelivr.net/npm/select2@4.1.0-rc.0/dist/js/select2.min.js"></script>
<!-- Flatpickr -->
<script src="https://cdn.jsdelivr.net/npm/flatpickr"></script>
<!-- ApexCharts -->
<script src="https://cdn.jsdelivr.net/npm/apexcharts"></script>
<!-- SlimScroll -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/jQuery-slimScroll/1.3.8/jquery.slimscroll.min.js"></script>
<!-- Toastr -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/toastr.js/latest/toastr.min.js"></script>
<!-- SweetAlert2 -->
<script src="https://cdn.jsdelivr.net/npm/sweetalert2@11"></script>
<!-- Custom (always last) -->
<script src="assets/js/script.js"></script>
```

---

## ═══════════════════════════════════════
## 15. DESIGN SYSTEM — style.css SPEC
## ═══════════════════════════════════════

```css
/* ── Global Reset & Base ── */
body { font-family: 'Nunito', sans-serif; font-size: 14px;
       color: var(--text-primary); background: var(--body-bg);
       overflow-x: hidden; line-height: 1.5; }

/* ── Page Loader ── */
#global-loader { position:fixed; inset:0; background:#fff; z-index:999999; }
.whirly-loader { /* animated spinner — orange #FF9F43 */ }

/* ── Header ── */
.header { position:fixed; top:0; left:0; right:0; height:60px;
          background:#fff; border-bottom:1px solid var(--border);
          box-shadow: var(--shadow-sm); z-index:1000; display:flex; align-items:center; }
.header-left { width:260px; padding:0 20px; border-right:1px solid var(--border);
               display:flex; align-items:center; justify-content:space-between;
               height:100%; flex-shrink:0; transition: width .2s ease; }
.header-left .logo img  { width:140px; }
.header-left .logo-small { display:none; }
.header-left .logo-small img { width:30px; }

/* ── Sidebar ── */
.sidebar { position:fixed; top:60px; left:0; bottom:0; width:260px;
           background:var(--sidebar-bg); border-right:1px solid var(--border);
           z-index:999; transition: width .2s ease; overflow:hidden; }
.sidebar .slimscroll { height:100%; overflow:hidden; }
.sidebar-menu { padding:20px 15px; }
.sidebar-menu > ul > li { margin-bottom:4px; }
.sidebar-menu > ul > li > a { display:flex; align-items:center; gap:10px;
  padding:10px 15px; border-radius:var(--radius-sm); color:var(--text-primary);
  font-weight:500; font-size:14px; transition:all .2s ease; }
.sidebar-menu > ul > li > a:hover,
.sidebar-menu > ul > li > a.active,
.sidebar-menu > ul > li.active > a {
  background: var(--dark-navy); color:#fff; }
.sidebar-menu > ul > li > a:hover img,
.sidebar-menu > ul > li.active > a img { filter:brightness(0) invert(1); }
.sidebar-menu > ul > li > a i,
.sidebar-menu > ul > li > a .menu-icon { width:18px; flex-shrink:0; }
.sidebar-menu > ul > li > a .menu-arrow { margin-left:auto; transition:transform .2s; }
.sidebar-menu > ul > li > a.subdrop .menu-arrow { transform:rotate(90deg); }
/* Submenu */
.sidebar-menu .submenu ul { background:#FAFBFE; border-radius:5px;
  padding:8px 0; display:none; margin-top:2px; }
.sidebar-menu .submenu ul li a { display:block; padding:7px 10px 7px 40px;
  font-size:13px; font-weight:500; color:var(--text-primary);
  border-radius:4px; position:relative; }
.sidebar-menu .submenu ul li a::before { content:'';
  width:6px; height:6px; border-radius:50%; border:1px solid #aaa;
  position:absolute; left:18px; top:50%; transform:translateY(-50%); }
.sidebar-menu .submenu ul li a:hover,
.sidebar-menu .submenu ul li a.active { color:var(--primary); }
.sidebar-menu .submenu ul li a.active::before { background:var(--primary); border-color:var(--primary); }

/* ── Mini Sidebar ── */
.mini-sidebar .header-left { width:80px; justify-content:center; }
.mini-sidebar .header-left .logo { display:none; }
.mini-sidebar .header-left .logo-small { display:block; }
.mini-sidebar .sidebar { width:80px; }
.mini-sidebar .sidebar-menu > ul > li > a span:not(.menu-icon) { display:none; }
.mini-sidebar .sidebar-menu > ul > li > a .menu-arrow { display:none; }
.mini-sidebar .page-wrapper { margin-left:80px; }
/* expand on hover */
.mini-sidebar:not(.expand-menu) .sidebar:hover { width:260px; box-shadow:var(--shadow-md); }
.mini-sidebar:not(.expand-menu) .sidebar:hover .sidebar-menu > ul > li > a span { display:inline; }
.mini-sidebar:not(.expand-menu) .sidebar:hover .menu-arrow { display:inline !important; }

/* ── Page Wrapper ── */
.page-wrapper { margin-left:260px; padding-top:60px; transition:margin .2s ease; min-height:100vh; }
.page-wrapper .content { padding:25px; }
@media (max-width:991px) { .page-wrapper { margin-left:0; } }

/* ── Cards ── */
.card { border:1px solid var(--border); border-radius:var(--radius-md);
        box-shadow:var(--shadow-sm); background:var(--card-bg); margin-bottom:25px; }
.card-header { border-bottom:0; background:transparent; padding:20px; }
.card-body { padding:20px; }

/* ── Dash Widgets ── */
.dash-widget { display:flex; align-items:center; padding:20px;
               background:var(--card-bg); border:1px solid var(--border);
               border-radius:var(--radius-md); margin-bottom:25px; }
.dash-widgetimg span { width:48px; height:48px; border-radius:50%;
  display:flex; align-items:center; justify-content:center; flex-shrink:0; }
.dash-widgetcontent { margin-left:15px; }
.dash-widgetcontent h5 { font-size:20px; font-weight:700; color:var(--text-primary); margin-bottom:4px; }
.dash-widgetcontent h6 { font-size:13px; color:var(--text-secondary); margin:0; }
.dash-count { border-radius:var(--radius-md); padding:20px; color:#fff;
              display:flex; align-items:center; justify-content:space-between;
              margin-bottom:25px; cursor:pointer; transition:transform .2s; }
.dash-count:hover { transform:translateY(-2px); }
.dash-count h4 { font-size:26px; font-weight:700; margin:0; }
.dash-count h5 { font-size:13px; margin:0; opacity:.9; }
.dash-count .dash-imgs i, .dash-count .dash-imgs svg { font-size:36px; opacity:.8;
  transition:transform .3s; }
.dash-count:hover .dash-imgs i { transform:scale(1.2); }

/* ── Buttons ── */
.btn-submit { background:var(--primary); color:#fff; font-weight:700; padding:10px 24px; border-radius:6px; }
.btn-submit:hover { background:var(--primary-dark); color:#fff; }
.btn-cancel { background:#637381; color:#fff; font-weight:700; padding:10px 24px; border-radius:6px; }
.btn-cancel:hover { background:#424b52; color:#fff; }
.btn-added  { background:var(--primary); color:#fff; font-weight:700; padding:7px 16px; }
.btn-added:hover { background:var(--dark-navy); color:#fff; }
.btn-filter { background:var(--primary); color:#fff; width:34px; height:34px; padding:0; border-radius:5px; }
.btn-filter.active { background:var(--danger); }

/* ── Tables ── */
.table thead { background:var(--table-head-bg); }
.table thead th { font-weight:600; color:var(--text-primary); padding:12px 10px;
  white-space:nowrap; border-bottom:2px solid var(--border); }
.table tbody td { padding:10px; color:var(--text-secondary); vertical-align:middle;
  border-bottom:1px solid var(--border); white-space:nowrap; }
.table tbody tr:hover { background:#F8F9FA; }
.action-btn { display:inline-flex; align-items:center; justify-content:center;
  width:28px; height:28px; border-radius:50%; margin:0 2px;
  font-size:13px; text-decoration:none; transition:all .2s; }
.view-btn   { background:rgba(0,207,232,.12); color:var(--info); }
.edit-btn   { background:rgba(255,159,67,.12); color:var(--primary); }
.delete-btn { background:rgba(234,84,85,.12);  color:var(--danger); }
.view-btn:hover   { background:var(--info);    color:#fff; }
.edit-btn:hover   { background:var(--primary); color:#fff; }
.delete-btn:hover { background:var(--danger);  color:#fff; }

/* ── DataTables overrides ── */
div.dataTables_wrapper div.dataTables_length select { min-width:70px; }
div.dataTables_wrapper .dt-buttons { display:flex; flex-wrap:wrap; gap:4px; }
div.dataTables_wrapper div.dataTables_paginate .paginate_button.current,
div.dataTables_wrapper div.dataTables_paginate .paginate_button.current:hover {
  background:var(--primary) !important; border-color:var(--primary) !important; color:#fff !important; }
div.dataTables_wrapper div.dataTables_paginate .paginate_button:hover {
  background:var(--primary-light) !important; color:var(--primary) !important; }
.column-filters input, .column-filters select { font-size:12px; }

/* ── Toastr overrides ── */
.toast-top-right { top:70px !important; } /* below fixed header */
#toast-container > .toast { border-radius:var(--radius-sm) !important; }

/* ── Page Header ── */
.page-header { display:flex; align-items:center; justify-content:space-between;
  margin-bottom:25px; flex-wrap:wrap; gap:10px; }
.page-header h4 { font-size:18px; font-weight:700; color:var(--text-primary); margin:0; }
.page-header h6 { font-size:13px; color:var(--text-secondary); margin:0; }

/* ── Dark Mode ── */
[data-theme="dark"] { --body-bg:#141432; --card-bg:#1D1D42; --border:#353570;
  --text-primary:#fff; --text-secondary:#B8BCC9; --sidebar-bg:#141432;
  --table-head-bg:#141432; }
[data-theme="dark"] .header { background:#1B2850; border-color:#353570; }
[data-theme="dark"] .sidebar { background:#141432; border-color:#353570; }
[data-theme="dark"] .table thead { background:#141432; }
[data-theme="dark"] .table tbody tr:hover { background:#1D1D42; }

/* ── Mobile ── */
@media (max-width:991px) {
  .sidebar { left:-300px; transition:left .3s; }
  .slide-nav .sidebar { left:0; }
  .sidebar-overlay { display:none; position:fixed; inset:0; background:rgba(0,0,0,.5); z-index:998; }
  .sidebar-overlay.opened { display:block; }
  .page-wrapper { margin-left:0; }
}
@media (max-width:575px) {
  .user-menu { display:none; }
  .mobile-user-menu { display:block; }
}

/* ── Scrollbar ── */
::-webkit-scrollbar { width:5px; height:5px; }
::-webkit-scrollbar-track { background:#F1F1F1; }
::-webkit-scrollbar-thumb { background:var(--primary); border-radius:10px; }

/* ── Misc ── */
#global-loader { display:flex; align-items:center; justify-content:center; }
.bulk-actions-bar { background:#FFF3E0; border:1px solid var(--primary);
  border-radius:6px; padding:8px 15px; display:flex; align-items:center; flex-wrap:wrap; gap:8px; }
```

---

## ═══════════════════════════════════════
## 16. RESPONSIVENESS
## ═══════════════════════════════════════

| Breakpoint | Behaviour |
|---|---|
| ≥ 1200px | Full sidebar (260px), full topbar, all columns visible |
| 992–1199px | Full sidebar, some table columns collapse (DataTables responsive) |
| 768–991px | Sidebar off-canvas (slide-in on hamburger tap), tables scroll |
| < 768px | All cards stack, KPI grid 2-col, sidebar overlay |
| < 576px | User menu hidden → mobile-user-menu, 1-col card layout |

---

## ═══════════════════════════════════════
## 17. ACCESSIBILITY
## ═══════════════════════════════════════

- Semantic HTML: `<nav>`, `<main>`, `<header>`, `<aside>`, `<section>`
- `aria-label` on nav, sidebar, dropdowns
- `aria-expanded` on submenu toggles (updated by JS)
- `aria-current="page"` on active nav link
- `role="alert"` on toastr container
- Keyboard: Tab navigable sidebar, Enter/Space activates dropdowns
- Focus trap in modals (Bootstrap handles this)
- Sufficient color contrast (WCAG AA minimum)

---

## ═══════════════════════════════════════
## 18. CONSTRAINTS & IMPLEMENTATION NOTES
## ═══════════════════════════════════════

1. **No build tools.** All CDN. No npm, webpack, or transpilation required.
2. **POS page** (`pos.html`) uses its own layout — no `.sidebar` / `.page-wrapper`. Uses `.main-wrappers` with `.header-pos` (stripped header).
3. **DataTables `stateSave: true`** — each table remembers its last sort/page/length in `sessionStorage`.
4. **Select2** must be initialized on every `<select class="select2">` element.
5. **Flatpickr** replaces all date inputs — class `flatpickr-date` (single), `flatpickr-range` (range picker).
6. **Image upload** zones use hidden `<input type="file">` overlaid by styled drop zone; preview via JS `FileReader`. Multiple files supported.
7. **Barcode scanner** inputs fire on `keypress` Enter — searches product table and auto-fills line item row.
8. **Dark mode + sidebar state** persist across all pages via `localStorage`.
9. **All modals** use Bootstrap 5 modal. Delete = SweetAlert2 confirm → Toastr result.
10. **Counter elements** (`.counters[data-count="X"]`) animate 0 → X on page load via jQuery `.animate()`.
11. **Every list/table page** must show an empty-state (icon + "No records found") when DataTable has 0 rows.
12. **Toastr position** `toast-top-right` offset by 70px top to clear the fixed header.
13. **Export buttons** (Excel, PDF, CSV, Print, Copy, Column Visibility) are injected by DataTables Buttons extension into the DOM layout defined by `dom:` option — do not hand-code export buttons.
14. **Column-level filter inputs** in the second `<thead>` row must NOT be included in DataTables' own search (use `column().search()` API instead).
15. **Bulk action bar** is hidden by default (`d-none`) and only appears when ≥ 1 row checkbox is checked.
16. **apexcharts** — all charts use `var(--primary)` (`#FF9F43`) as the primary series color, `#28C76F` as secondary.

---

## ═══════════════════════════════════════
## 19. OUTPUT FORMAT
## ═══════════════════════════════════════

- Output **ALL files** clearly labeled with their filename as a comment header:
  ```
  --- index.html ---
  --- sales.html ---
  --- assets/css/style.css ---
  --- assets/js/script.js ---
  ```
- Each file must be **complete and self-contained** — no placeholders like `<!-- content here -->`.
- Every HTML file must include the **full header, sidebar, and footer** markup (no server-side includes).
- Every page must have **realistic sample data** in its tables (minimum 8–10 rows).
- **No explanations or commentary outside the code blocks.**
