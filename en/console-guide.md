## Security > Security Advisor > Console Guide

This document explains Security Advisor features and how to use.

## Dashboard

You can check the inspection results in Inspection Item of Security Advisor.
The results of checking organizations are shown regardless of the selected region, and project resources show the results of checking resources created in the selected region.

* Click **Save as Excel** to download the inspection results to an excel file.
* Summary of Inspection Result displays the number of inspection items by Alert Criteria.
* Short List of Inspection Result displays the items of detected resources with **Critical, High, Moderate, and Low** criteria.

## Inspection Item

You can run inspection by selecting inspection items and get the result and recommended actions.
You can check the details of inspection results and exclude unnecessary items from inspection.

### Basic Information

* Provides descriptions of the inspection items.
* Allows you to confirm alert criteria and take action on detected resources through recommendations.

### Detected Resource

* You can view the details of the resources detected based on the alert criteria for each item.
* If you check any of the detected resources and click **Except Selected**, those resources will be excluded on the next inspection.

### Exception List

* You can find the items excluded from inspection.
* If you check any of the excluded items and click **Disable Exception**, the item can be included in inspection.

## Settings

You can run inspection periodically at a desired time by setting up auto inspection.
If you enter an email address, the auto inspection result is sent to the address. When you set up auto inspection but don’t enter an email address, the inspection result is reflected only in the console.

### Admin Settings

* Set the email address of the administrator who will receive the inspection results. Make sure to enter the email address correctly.
* The email is not a required field.

### Inspection Settings
* You can enable auto inspection by setting **Inspection Cycle**. The inspection result is automatically reflected in the console, and sent to the email address if set.
* You can select **Auto Inspection Item**.
