---
description: Guide to manage your collection sale stages
---

# Manage Sale Stages

Collection is configure-able with multiple presale stages and public sale stage for minting. Most of the times, an NFT collection can include multiple sale stages, including an Presale phase (sometimes called a “pre-mint”, “allowlist mint” or “whitelist mint”) that gives early access to those who are on the allowlist. Freee collection comes with 2 types of sale stages (minting stages).&#x20;

* **Presale Stages**: Allocate your collection to a specific groups of audience, called an “allowlist” who get the privilege to mint earlier or at a special price. A collection can setup up to 5 presale stages.&#x20;
* **Public Sale**: Everyone can mint your collection until mint out.

Do note that, overlap minting schedule is not allowed for collection. Plan your minting schedule carefully to achieve the best result.\
\
To manage your sale stages, scroll to **Sales configuration** section in collection management page **Overview** tab.

<figure><img src="../../../.gitbook/assets/Screenshot 2024-08-19 at 16.54.50.png" alt=""><figcaption></figcaption></figure>

***

## Manage Presale Stages

To manage / confirgure Presale stages, click on the **Add Presale** or **Manage Presale** button on the right of Presale Stages section. Optionally, you can change to **Presale Stages** Tab, all presale stages related configuration will be done here.&#x20;

Collection support up to 5 presale stages, you can setup and update all presale stages before finalise it by performing **Save onchain** action.

### 1. Add a Presale Stage

Click on the **Add Presale** button located on the right side of the page. Configure and setup presale stage in the dialog popped out.

<figure><img src="../../../.gitbook/assets/Screenshot 2024-08-19 at 17.40.09.png" alt=""><figcaption></figcaption></figure>

\*Required Fields

1. Enter **Stage** **Name** for your presale. \*
2. \[Optional] Set a **Stage Supply** if applicable. This limit the number of NFT that can be mint during this stage.
3. Set a **Stage Price,** enter your desired amount in ETH (or other selected chain currency).&#x20;
4. Decide **Start & end time** of current presale stage. \*
5. Fill in **Mint limit per address** for current stage. This is **required**, presale stage need to have a default limit of number of NFT an allowlist address can mint. \*
6.  Setup **Allowlist** for current stage, setup list of wallet addresses that allow to mint at current stage. You have option to upload an CSV (follow specified format) or enter all addresses manually. This is **optional while configure presale**, but you are require to setup afterward, else your Presale stage is invalid, no one can mint from it.

    For allowlist setup, refer [section 3](manage-sale-stages.md#id-3.-manage-presale-stages-allowlist) below.
7. Click on **Confirm** button.

***

### 2. Update a Presale Stage

<figure><img src="../../../.gitbook/assets/Screenshot 2024-08-19 at 19.46.15.png" alt=""><figcaption></figcaption></figure>

To edit a Presale Stage, click on the **Edit** icon on the right side of desire Presale Stage (circled in red on above screenshot). On Edit dialog popped out, you will be able to edit every configuration of selected stage except the Allowlist.&#x20;

<figure><img src="../../../.gitbook/assets/Screenshot 2024-08-19 at 19.50.51.png" alt=""><figcaption></figcaption></figure>

Refer [section 1](manage-sale-stages.md#id-1.-add-a-presale-stage) above for detail explanation of each field.

**Note:** Presale stage config is not edit-able after presale started.

***

### 3. Manage Presale Stage's Allowlist

<figure><img src="../../../.gitbook/assets/Screenshot 2024-08-19 at 19.46.15 copy.png" alt=""><figcaption></figcaption></figure>

To manage Presale Stage's Allowlist, click on the **Allowlist** icon on the right side of desire Presale Stage (circled in red on above screenshot).

<figure><img src="../../../.gitbook/assets/Screenshot 2024-08-19 at 19.54.08.png" alt=""><figcaption></figcaption></figure>

There are two ways for you to setup/manage presale stage allowlist:

1. CSV upload
2. Manual Entry

### 3.1 CSV Upload Method

Recommended for large allowlist with more than 20 addresses, and support up to 10,000 addresses per stage.

1. Click on the **CSV upload** button.
2.  **Select** allowlist CSV file from your computer.

    Your allowlist CSV file must contains all  3 columns: 'Wallet Address, 'Price', and 'Mint Limit'.\


    <figure><img src="../../../.gitbook/assets/Screenshot 2024-08-19 at 19.57.23.png" alt=""><figcaption></figcaption></figure>
3.  Click **Next** button and review the first few lines of your allowlist.\


    <figure><img src="../../../.gitbook/assets/Screenshot 2024-08-19 at 20.00.38.png" alt=""><figcaption></figcaption></figure>
4. If everything looks fine, click on **Add items** button to proceed.
5.  Imported allowlist will show in table, click **Confirm** to add Allowlist into selected presale stage.\




    <figure><img src="../../../.gitbook/assets/Screenshot 2024-08-19 at 20.02.09.png" alt=""><figcaption></figcaption></figure>

### 3.2 Manual Entry Method

Recommended for small allowlist with a size of 10 to 20 addresses.

1.  Click on the **Manual entry** button\


    <figure><img src="../../../.gitbook/assets/Screenshot 2024-08-19 at 20.06.49 (1).png" alt=""><figcaption></figcaption></figure>
2. Enter **Wallet Addresses** of the accounts for your allowlist. ​
3. Set a **price** for all these wallet addresses.
4. Set a **mint limit** for all these wallet addresses. ​
5. Click on **Add items** button to proceed.
6.  Allowlist entries will list down in a table, click **Confirm** to add Allowlist into selected presale stage.\


    <figure><img src="../../../.gitbook/assets/Screenshot 2024-08-19 at 20.02.09 (1).png" alt=""><figcaption></figcaption></figure>

***

### 4. Remove Presale Stage

<figure><img src="../../../.gitbook/assets/remove stage.png" alt=""><figcaption></figcaption></figure>

To remove a Presale Stage, click on the **Trash** icon on the right side of desire Presale Stage (circled in red on above screenshot).

<figure><img src="../../../.gitbook/assets/Screenshot 2024-08-19 at 20.14.32.png" alt=""><figcaption></figcaption></figure>

1. **Check** carefully selected stage information.
2. Click on **Confirm** button to remove selected presale stage.

**Note:** Presale stage is not remove-able after presale started.

***

### 5. Save on chain

Once you done configure everything for your Presale Stages, you are require to save all changes on chain for it to take effect.&#x20;

<figure><img src="../../../.gitbook/assets/Screenshot 2024-08-19 at 20.12.57.png" alt=""><figcaption></figcaption></figure>

1. There will be a floating panel at the bottom of the page showing changes you make,  Save onchain  button and Discard button.\
   **Save onchain button:** Finalise your Presale Stages setup and save it on chain to take effect\
   **Discard button:** Discard whatever change you make and reset to it original state.
2. Click on **Save onchain** button after review your Presale Stages setup
3.  **Approve** the Gas fee.

    A message will appear within your connected wallet for you to approve the gas fee to complete the update. Gas fees are the cost of interacting with the blockchain. Gas fees are not set or collected by Freee.

***

## Manage Public Sale Stage

To manage / confirgure Public Sale stage, click on the **Edit** button on the right of Public Sale section in **Overview** Tab.

<figure><img src="../../../.gitbook/assets/Screenshot 2024-08-19 at 17.14.47.png" alt=""><figcaption></figcaption></figure>

On the Update Public Sale Config dialog popped out:

1. Set a **Price** for public sale, enter your desired amount in ETH (or selected chain currency).&#x20;
2. Decide **Start & end time** of public sale.&#x20;
3. Fill in **Mint limit per address** for public sale. This is **optional**, leave empty if don't want to limit number of NFT a user can mint.
4. Click on **Update** button once you confirm your Public Sale config
5.  **Approve** the Gas fee.

    A message will appear within your connected wallet for you to approve the gas fee to complete the update. Gas fees are the cost of interacting with the blockchain. Gas fees are not set or collected by Freee.
