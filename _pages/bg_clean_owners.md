---
layout: page
title: Clean up property owner names
---
One of the files resulting from The Charlotte Observer and The News & Observer's investigation is a "lookup table" – basically just a spreadsheet that can help us match the hundreds of subsidiaries and holding companies big corporate landlords use to buy and manage property with their parent firms.

These holding companies can sometimes be distinct entities, or they can just be mistyped into the property record system. Either way, the text in your property records must be an exact match to one of the firms in our lookup table, or it won't match to a corresponding parent company.

In this walkthrough, you'll learn:
 - How to install/import a packtimport a 
 - How to create a function in R

## Prepare your data

For this walkthrough, you'll need two main datasets:
- The property record data for your market (we'll be using Wake County, N.C.)
	- If this file isn't available online for your county, city or state, you may need to request it, probably from your local register of deeds<br />*Example: Wake County [real estate data](https://services.wakegov.com/realdata_extracts/)*
	- Make sure you get the field layout/data dictionary that describes the columns of the data<br />*Example: Wake County [record layout](https://s3.us-west-2.amazonaws.com/wakegov.com.if-us-west-2/prod/documents/2020-10/Record%20Layout.pdf)*

- The [corporate landlord lookup spreadsheet](https://github.com/mcclatchy-southeast/security_for_sale/tree/main/data) created by The Charlotte Observer/The News & Observer
	- [How to download the data](https://github.com/mcclatchy-southeast/security_for_sale#data)
	- [Field layout/data dictionary](https://github.com/mcclatchy-southeast/security_for_sale#corporate_landlord_lookup-1)

## Importing your data into Sheets
