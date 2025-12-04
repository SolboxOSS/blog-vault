---
id: pcld7a9f21
title: pCloud White Label Explorer (Preview)
description: Private preview of a fully branded pCloud Explorer desktop experience powered by RcloneView.
hide_title: true
hide_table_of_contents: true
unlisted: true
---
<meta name="robots" content="noindex" />

# pCloud White Label Explorer (Preview)

This page is a private preview of how RcloneView can be delivered as a fully branded **pCloud Explorer** desktop application for your users.

The goal of this white-label proposal is to:

- Put the **pCloud brand front-and-center** across the entire product.
- Make it **effortless for users to connect their pCloud account** immediately after installation.
- Ensure **pCloud is the first choice** in every management and navigation workflow.
- Provide **priority support and maintenance** specifically for pCloud-branded deployments.

---

## 1. Brand Kit & Visual Integration

We provide a brand kit where pCloud is the primary and visible brand throughout the product. All RcloneView branding is removed or kept only where legally required (e.g., internal version strings).

Key elements:

- Application name set to **“pCloud Explorer”** (or another agreed label).
- All RcloneView logos replaced by **pCloud logo**:
  - Desktop shortcuts and taskbar icons.
  - Installer icons.
  - In-app header and window icon.
- Color accents adjusted to match pCloud’s brand palette where appropriate.

<img src="/support/images/en/howto/remote-storage-connection-settings/pcloud-brandkit-examples.png" alt="pcloud brandkit examples" class="img-large img-center" />


---

## 2. Post‑Install pCloud Remote Wizard

Immediately after installation, users are guided to connect their pCloud account so they can start using the service without additional setup steps.

Main behaviors:

- At the end of the setup wizard, launching the app opens **“Add pCloud Remote”** as the default onboarding flow.
- The wizard is simplified and pre-configured for pCloud:
  - Provider type is pre-selected as **pCloud**.
  - Only pCloud‑specific options are shown by default.
  - Advanced options remain available behind an **“Show advanced options”** link.

<img src="/support/images/en/howto/remote-storage-connection-settings/post-install-pcloud-remote-wizard.png" alt="post install pcloud remote wizard" class="img-large img-center" />

### On-Home Quick Access Wizard

If the user skips the initial connection or closes the wizard:

- The right-hand panel of the home screen shows a **large pCloud tile**.
- Clicking the tile reopens the **“Add pCloud Remote”** wizard at any time.

<img src="/support/images/en/howto/remote-storage-connection-settings/on-home-quick-access-wizard.png" alt="on home quick access wizard" class="img-large img-center" />


This ensures that connecting pCloud is always the most visible next action for new or returning users.

---

## 3. pCloud‑First Navigation & Management

Once a pCloud remote is added, the UI is optimized to keep pCloud prominently visible across all key navigation and management screens.

### 3.1 pCloud Drive in RcloneView Explorer

When the pCloud remote is mounted as a local drive:

- The pCloud drive (for example, `pCloud Drive (P:/)`) is shown at the **top of the RcloneView local remotes list**.
- The drive uses the **pCloud icon** so that it is visually distinct from other drives.

<img src="/support/images/en/howto/remote-storage-connection-settings/pcloud-first-in-explorer.png" alt="pcloud first in explorer" class="img-medium img-center" />

### 3.2 pCloud Panel Pinned on Re‑Launch

After a pCloud remote has been configured:

- On subsequent launches, the UI opens with a **pCloud panel pinned** by default.
- Typical layout:
  - Left side: local disk or another source.
  - Right side: the user’s **MYpCloud** remote.
- This makes repeated sync or copy operations between local folders and pCloud a one-click action.

<img src="/support/images/en/howto/remote-storage-connection-settings/pcloud-panel-pinned-on-re-launch.png" alt="pcloud panel pinned on re launch" class="img-large img-center" />


### 3.3 pCloud First in “New Remote” & “Remote Manager”

To highlight pCloud as a primary storage provider:

- In the **New Remote** dialog:
  - pCloud appears at the **top of the provider list**.
  - pCloud tile is visually highlighted to encourage selection.
- In **Remote Manager**:
  - The pCloud remote (e.g., `MYpCloud`) is displayed at the **top of the remote list**.
  - In both list and card views, the pCloud remote is visually emphasized for quicker access.


<img src="/support/images/en/howto/remote-storage-connection-settings/pcloud-first-in-management-dialog.png" alt="pcloud first in management-dialog" class="img-large img-center" />

---

## 4. Priority Support & Maintenance for pCloud

For the pCloud white-label deployment, we provide a dedicated support and maintenance track.

Included services:

- **Dedicated documentation**  
  - Separate manual pages specifically for **pCloud Explorer** users.  
  - Step-by-step guides for connecting, syncing, and troubleshooting with pCloud.

- **Priority incident handling**  
  - pCloud user issues are prioritized in the support queue.  
  - **Emergency response** for critical incidents affecting pCloud users (e.g., connection failures, data access issues).

- **Ongoing product updates**  
  - Regular desktop client upgrades included as part of the maintenance agreement.  
  - Ability to roll out new RcloneView features behind pCloud branding after joint approval.

---

## 5. Next Steps

If you would like to move forward with this white-label product:

1. **Branding alignment**
   - Confirm pCloud logo usage guidelines and brand colors.
   - Decide final product name (e.g., *pCloud Explorer*).
2. **Experience definition**
   - Validate the onboarding flow and pCloud-first behaviors described above.
   - Adjust any default settings (e.g., default sync mode, default mount path).
3. **Pilot build**
   - We deliver a private pilot build and pCloud-specific documentation for internal testing.

This page and its URL are intended for pCloud and partner stakeholders only and will not appear in public navigation or search. It can be safely shared as a direct link during evaluation and pilot discussions.

