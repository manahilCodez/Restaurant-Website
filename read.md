# Tokyo Pan Asian Cuisine Website ? User Guide

This package contains the Tokyo Pan Asian Cuisine customer ordering website and a staff dashboard preview. The pages are designed to work together as a front-end prototype.

## 1. Package contents

- `index.html` ? customer-facing website, menu, cart, checkout, payment receipt upload, and order tracking.
- `admin.html` ? staff dashboard preview for viewing and managing customer orders.
- `app.js` and `styles.css` ? customer-side behavior and styling.
- `admin.js` and `admin.css` ? dashboard behavior and styling.
- `assets/Tokyo_Asian_logo.png` ? the supplied original restaurant logo.
- `assets/menu-reference.jpeg` ? supplied menu reference image.
- `README.md` ? short project overview.
- `read.md` ? this detailed guide.

Keep this folder structure intact. The HTML pages load their styles, scripts, and images using relative paths.

## 2. Previewing the pages

### Quick local preview

1. Extract `tokyo-ordering.zip` to a folder.
2. Open `index.html` in a current desktop or mobile browser to see the customer website.
3. Open `admin.html` in the same browser to see the staff dashboard.

If there are no saved orders, the dashboard displays sample orders to demonstrate the layout. These are preview data and are not customer orders.

### Shared-browser-storage note

The prototype saves orders in browser `localStorage` and payment receipt files in `IndexedDB`. To see customer-created orders in the dashboard preview, open both pages from the same website origin and the same browser profile. Opening pages through different file paths, browsers, profiles, devices, or private windows may separate their storage. Hosting both pages under the same HTTPS origin is the recommended way to preview the shared flow.

## 3. Customer ordering flow

### Choose delivery or pickup

At the beginning of a browser session, the customer selects one of the following and presses **Done**:

- **Delivery** ? select Islamabad or Rawalpindi and enter the delivery address. The page explains that the customer arranges a rider using Bykea, a personal rider, or inDrive.
- **Pickup** ? the page displays the restaurant location: Commercial Market, B-Block, Satellite Town, Rawalpindi.

The selection is remembered in the browser and prefills checkout. The customer can access the cart from the floating button at the lower-right of the website without scrolling back to the header.

### Build a cart and submit an order

1. Browse menu categories or search dishes.
2. Use **Add to order** (or the quick-add button) to add dishes. Use the cart to change quantities or remove items.
3. Continue to checkout. Enter the customer's name and phone number.
4. For delivery, confirm or edit the prefilled address. For pickup, a delivery address is not required.
5. Add optional special instructions and submit the order request.
6. The order request number appears in the confirmation. Select **Track your order** to view its status.

Prices and dishes are represented in the supplied menu data in the website files. The checkout total reflects the food items in the cart. Delivery charges are not calculated by this prototype.

## 4. Payment and order progress

1. A staff member approves the order in the dashboard. This moves it to **Awaiting payment** and starts a 15-minute payment window.
2. The customer opens **Track order** to see the remaining payment time and restaurant Easypaisa instructions.
3. The customer uploads a PNG or JPG receipt no larger than 5 MB and presses **Done ? submit receipt**.
4. The order moves to **Payment verification**. The receipt is available for staff review in the admin dashboard.
5. Staff verifies payment to move the order to **Preparing**, or rejects the payment to send it back to **Awaiting payment** with a fresh payment window.
6. If the payment window expires before the customer submits a receipt, the order is set to **Rejected** and the event is timestamped. The countdown is visible on the customer and admin pages while they are open; after an inactive period, expiry is applied when one of the pages next runs.

Customer tracking is available from the **Track order** control in the header and the order confirmation. It displays the current order stage and relevant payment or fulfilment controls.

## 5. Staff dashboard workflow

Open `admin.html` to use the staff preview. Select an order in the order list to see its customer information, fulfilment choice, items, total, notes, and available actions.

Typical status flow:

- **Pending approval** ? approve or reject the request.
- **Awaiting payment** ? monitor the 15-minute countdown. A receipt can be submitted by the customer from their tracking page.
- **Payment verification** ? inspect the customer's uploaded receipt, then verify payment or reject it.
- **Preparing** ? review the order and mark it ready for pickup.
- **Ready for pickup** ? for delivery orders, review the rider details entered by the customer.
- **Handed to rider** ? confirm the rider handoff, then mark the order completed. For pickup orders, use the pickup completion action.
- **Completed** or **Rejected** ? final order states.

The **Progress updates** panel lists the order milestones. Select a milestone to show its details: payment verification includes the receipt when available, preparing shows the order items, ready for pickup shows rider details for delivery orders, and recorded milestones show their timestamps when present.

Other dashboard areas provide previews of menu management, customer lists, delivery methods, payment details, reports, staff, and settings. Menu management is not currently connected to the customer menu.

## 6. Data, limitations, and production setup

This is a front-end prototype, not a production ordering service. It has no server database, server-side order processing, live payment integration, or secure staff sign-in.

- Browser storage is local to an origin and browser profile. It does not synchronize between separate customer and staff devices.
- Receipt images are kept in browser `IndexedDB`; browser cleanup can remove them.
- The 15-minute expiry is checked by the customer/admin page scripts. A static browser-only website cannot run a background timer while all pages are closed. A production system should enforce expiry on a server.
- The Easypaisa payment details are displayed as instructions only; the prototype does not send or verify real payments.
- Delivery rider details are entered by the customer and displayed to staff. The prototype does not book a ride or contact the rider.
- The staff dashboard is not protected by authentication. Do not publish it for real staff use without adding server-side sign-in and access controls.

For a production launch, host the customer and staff interfaces under one HTTPS site and connect them to a server API and database. Add staff authentication, server-validated order transitions, server-side payment deadlines, secure receipt uploads, and a verified payment process before accepting real orders.

## 7. Updating and sharing the package

- Keep the original logo at `assets/Tokyo_Asian_logo.png` and preserve the relative asset paths.
- To share the complete prototype, send the ZIP file and have the recipient extract the entire folder before opening the pages.
- After any edits, re-create the ZIP from the contents of the `tokyo-ordering` folder so the guide and assets are included.
