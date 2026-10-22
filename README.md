# Tokyo Pan Asian Cuisine Website

## Pages
- `index.html` — customer ordering site and order tracking.
- `admin.html` — restaurant staff dashboard.

## Customer fulfilment
At the start of a browser session, customers choose delivery in Islamabad or Rawalpindi (with address) or pickup. The delivery form explains that the customer arranges the rider through Bykea, a personal rider, or inDrive. The choice and address prefill checkout; pickup does not require a delivery address. A floating cart button remains available while browsing.

## Payment and receipt flow
1. A customer submits an order request. Staff approval moves it to `Awaiting payment`.
2. Staff approval starts a 15-minute payment window. The customer sees a live countdown in order tracking and the staff see the same countdown in the dashboard. If payment is not submitted before the deadline, the order is automatically rejected and timestamped.
3. The customer sees the restaurant Easypaisa details (0313-5780250) in order tracking, uploads a PNG/JPG receipt (up to 5 MB), then submits it with **Done**.
4. The order moves to `Payment verification`. The receipt image is stored in IndexedDB and its metadata is attached to the shared `tokyo-orders` record.
5. Staff opens the order in `admin.html`, reviews/downloads the uploaded receipt, then verifies payment to move the order to `Preparing`. Staff can also reject payment back to `Awaiting payment`.
6. When staff marks a delivery order `Ready for pickup`, the customer enters the rider name, bike/car, vehicle number, and optional WhatsApp number in order tracking. Staff sees those details and confirms `Handed to rider`, then marks the order `Completed`. Self-pickup orders use a pickup-completion step instead.

## Deployment
Host both pages under the same HTTPS site origin. This lets their shared browser storage synchronize order statuses and receipts across customer and staff sessions. Browser file previews may isolate storage by page. A production multi-device restaurant workflow should use a server database and authenticated API instead of browser storage.

The staff dashboard is a front-end preview and has no secure sign-in. Protect `admin.html` with server-side staff authentication and role permissions before deployment. Sample orders appear when there are no saved customer orders; they are preview data only.

## Menu and assets
The supplied Tokyo logo is preserved unchanged in `assets/Tokyo_Asian_logo.png`. The customer menu is transcribed from the supplied menu reference. The staff menu-management preview is not yet connected to that live menu.


