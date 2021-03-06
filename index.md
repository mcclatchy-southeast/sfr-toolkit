---
layout: page
title: Single-family rental industry reporting toolkit
---

![A "For Rent" sign sits in the yard of a Raleigh home owned by Tricon Residential in early 2022. // Julia Wall](/assets/images/tricon_flag_jmw.JPG)
*A "For Rent" sign sits in the yard of a Raleigh home owned by Tricon Residential in early 2022. // Julia Wall, The News & Observer*

###### LAST UPDATED: June 9, 2022

In May 2022, reporters from The Charlotte Observer and The News & Observer [published a series of stories](https://www.charlotteobserver.com/topics/security_for_sale) highlighting the rise of the single-family home rental industry in North Carolina.

The work was funded in part by the [Pulitzer Center](https://pulitzercenter.org/), which invested not only in the journalism, but in the creation of a toolkit for newsrooms looking to replicate and expand upon the two papers' reporting in their own markets.

Not all of the lessons learned during the Observer and N&O's six months spent tracking and documenting large single-family rental companies in North Carolina will apply to every market. But because this industry has standardized the way it buys and manages homes across the country to increase its profit margins at scale, many techniques will be similar whether you're covering Charlotte or Chula Vista, Raleigh or Richmond.

Have questions or suggestions? Contact [N&O investigative reporter Tyler Dukes](mailto:mtdukes@newsobserver.com).

## Who this toolkit is for

We've designed this toolkit for local and national journalists at a variety of skill levels who are interested in probing the extent of corporate homeownership in their cities, regions and states.

Some experience working with data – and specifically the R statistical programming language – will be helpful, but we've written our tutorials to cover some entry-level concepts for people brand new to R.

Why R? Because most property record databases are a bit too large for common spreadsheet tools like Google Sheets, and can even cause Excel to move too slowly.

Our overarching goal is to make this guide as accessible as possible, so if you get stuck, let us know. We're continuing to improve the content here to make it easier to use.

Although this toolkit is geared toward journalists, its use isn't limited to newsrooms. Members of the public, academics and researchers are welcome.

## How to use this toolkit
This site is divided up into two broad sections: **tutorials** and **resources**.

**Resources** contain background materials, like readings lists and glossaries, that can help add context to your reporting and understanding of corporate homeownership.

**Tutorials** provide technical walkthroughs for different aspects of the project, like how to match the names of the various holding companies to their parent companies.

We'll add to these sections over time, and if there's something you want to see, let us know.

## What you'll need

Before you get started, make sure you have the data and software that can help you discover the scale of corporate homeownership in your community.

### Data and documents

#### Essential 
- **Property record data** Data on property ownership may be maintained on the county level, depending on your state. If it's not readily accessible your county website or GIS portal online, try requesting it from your local register of deeds or tax administration department.

#### Optional

- **Property sales/transaction data** Depending on the jurisdiction, data on property sales (like sale price and date) may be stored separately from data detailing the current owner of a parcel or property. You'll need this data if you plan to evaluate how many transactions involve a corporate landlord over a certain period of time. Even if property record data contains information on a home's sale price and date, if it sold multiple times over the time period you're studying (if the home was bought and flipped, for example), you'll miss every transaction before the most recent one.
 
- **Rental property/landlord registrations** Some jurisdictions may require landlords of certain sizes to register basic information, like contact details, addresses or unit counts, for the purposes of public safety or code enforcement (North Carolina, by contrast, forbids municipalities from collecting this information). Check to see if you can request this data, which might allow you to quickly identify large landlords.

- **Consumer complaints** States with consumer protection divisions (often housed within the office of the state attorney general), should be able to provide copies of complaints filed against corporate landlords. You'll probably have to submit a public records request for these documents for a specific list of companies over a specific time period. The records will provide the names of renters and, often, documentation of problems those renters have experienced.

- **Corporation registration database** Most states have an agency responsible for registering corporate entities doing business within state borders, and they track those registrations in a corporation database. In North Carolina, for example, this database is maintained by the [Office of the Secretary of State](https://www.sosnc.gov/online_services/search/by_title/_Business_Registration). These records can be incredibly valuable for verifying the links between companies and their subsidiaries. The amount of information available publicly depends on the state, but you should be able to submit a public records request for the entire database. [Another option is to use OpenCorporates](https://opencorporates.com/), a nonprofit that tracks business registrations across the country and makes its data available via an API.

### Technology

- **R** *(free)* A statistical programming language that is quickly becoming one of the standard tools for data journalists around the world.

- **RStudio** *(free)* A popular integrated development environment (IDE) that essentially functions as a user interface for the R language itself.

## Contributors
This site was primarily written and designed by News & Observer investigative reporter Tyler Dukes, with extensive contribution and editing from Charlotte Observer investigative reporter Payton Guion and Observer growth reporter Gordon Rago and McClatchy Southeast investigations editor Cathy Clabby.

Photos by Julia Wall, Jeff Siner and Khadejeh Nikoyeh.

Special thanks to the Pulizer Center for its generous support of this work.

Want to contribute to our toolkit? Want to share what you found? Contact [N&O investigative reporter Tyler Dukes](mailto:mtdukes@newsobserver.com).