---
layout: page
title: Clean up property owner names
---
One of the files resulting from The Charlotte Observer and The News & Observer's investigation is a "lookup table" – basically just a spreadsheet that can help us match the hundreds of subsidiaries and holding companies big corporate landlords use to buy and manage property with their respective parent firms.

These holding companies can sometimes be distinct entities, or they can just be mistyped into the property record system.

Either way, the text in your property records must be an exact match to one of the firms in our lookup table, or it won't match to a corresponding parent company.

In this walkthrough, you'll learn:
 - How to create a function in R

## Prepare your data

For this walkthrough, you'll need two main datasets:
- The property record data for your market (we'll be using Wake County, N.C.)
	- If this file isn't available online for your county, city or state, you may need to request it, probably from your local register of deeds. *Example: Wake County [real estate data](https://services.wakegov.com/realdata_extracts/)*
	- Make sure you get the field layout/data dictionary that describes the columns of the data. *Example: Wake County [record layout](https://s3.us-west-2.amazonaws.com/wakegov.com.if-us-west-2/prod/documents/2020-10/Record%20Layout.pdf)*

- The [corporate landlord lookup spreadsheet](https://github.com/mcclatchy-southeast/security_for_sale/tree/main/data) created by The Charlotte Observer/The News & Observer
	- [How to download the data](https://github.com/mcclatchy-southeast/security_for_sale#data)
	- [Field layout/data dictionary](https://github.com/mcclatchy-southeast/security_for_sale#corporate_landlord_lookup-1)

Store both of these files in the working directory containing your R project file (Skip that step? [Review the Setting Up tutorial](/_pages/bg_setting_up_r.html)).

Take note of the filetype extension. Is it a comma-separate value, or CSV? A text file with data defined by its position on each line (a fixed-width file)? Or is it a giant Excel file (.xlsx)? Depending on the filetype, you'll have to use slightly different import options below.

You'll also need to identify, from your field layout, which column contains the property owner name in your property record database. Some datasets may split this into a first name and last name for individuals (but not for corporate entities, which is what we care about), or across multiple columns if there are multiple owners.

In our Wake County data, our property owner name is contained in the `OWNER1` column and is not split by first and last name. We'll note that for later.

## Getting started
Start RStudio and in the top menu, click `File` > `Open Project...` and select the R Project file you started. This will automatically change your working directory.

Then start a new R script by clicking `File` > `New File` > `R Script` and click `File` > `Save As...` to name your work. We're going to call ours `clean_names.R`.

If everything is where it's supposed to be, you'll notice your Files pane should include your script, your R project and the data files you stored in your directory. Check to make sure everything's here.

![A working directory in R Studio with the data files appropriately placed.](/assets/images/working_directory.png)

At the top of your script, write a quick comment that tells you something about what your new script does. Starting each line with a `#` character will ensure this line is not executed when you run your code.

```R
# A script containing cleaning steps for owner names
# in property records data
# created 6/1/2022 by @mtdukes
```

For organizational purposes, create a section label with the keyboard shortcut <kbd>Command</kbd> + <kbd>Shift</kbd> + <kbd>R</kbd>. Section labels are visible in the Document Outline, which you can toggle with the button in the upper right of the script pane. Using section labels allows you to navigate through sections of your code with a point and click.

Use them whenever it makes sense as you organize your code.

![Creating a section label](/assets/images/section_label.gif)

Here, we'll do some initial setup, like loading up our packages into our workspace if they're already installed.

```R
#load up our packages
library(tidyverse)
library(readxl)
```

Remember: Execute each line of code by clicking `Run` or with <kbd>CMD</kbd> + <kbd>Enter</kbd>.

## Importing your data

Your next step depends on what type of property records file you're importing. Click to jump to directly to the corresponding instructions:
- [Excel file (.xlsx extension)](#a-importing-an-excel-file)
- [Fixed-width file (.txt extension with a set number of characters per line)](#b-importing-a-fixed-width-file)
- [Comma-separated value file (.csv extension)](#c-importing-a-csv-file)
- [Tab-delimited file (.tsv extension or .txt extension with tabs between columns)](#d-importing-a-tab-delimited-file)

The code blocks below are examples based on the data we're using from Wake County. You'll have to adjust for your specific dataset.

---

### A.) Importing an Excel file
The `readxl` package, part of the Tidyverse, makes it pretty easy to import Excel files into R.

We'll use the `read_excel()` function from that package to store the resulting dataframe in a variable with the assignment symbol, `<-`. You can use the keyboard shortcut <kbd>Option</kbd> + <kbd>-</kbd> to input that symbol at your cursor.

```R
#import xlsx of wake county property records
wake_properties <- read_excel('RealEstData05312022.xlsx')
```

###### [JUMP TO THE NEXT STEP](#importing-the-lookup-table)

### B.) Importing a fixed-width file

Tidyverse has a specific function for importing fixed-width files called `read_fwf()`. It does require a bit of extra code, since you're having to explicitly tell the function where each field begins and ends. Consult the field layout for your dataset to help you.

Use the assignment symbol, `<-`, to store your imported data to a variable. You can use the keyboard shortcut <kbd>Option</kbd> + <kbd>-</kbd> to input that symbol at your cursor.

When we load the data, we'll go ahead and assume everything is a character string (letters and numbers that R treats as plain text) to reduce import errors.

```R
#import fwf of wake county property records
wake_properties <- read_fwf('RealEstData06012022.txt',
                            trim_ws = TRUE, #trim errant white space
                            fwf_cols(owner_1 = c(1, 35), #positions based on data dictionary
                                     owner_2 = c(36, 70),
                                     mailing_address_1 = c(71, 105),
                                     mailing_address_2 = c(106, 140),
                                     mailing_address_3 = c(141, 175),
                                     real_estate_id = c(176, 182),
                                     card_number = c(183, 185),
                                     number_of_cards = c(186, 188),
                                     street_number = c(189, 194),
                                     street_prefix = c(195, 196),
                                     street_name = c(197, 221),
                                     street_type = c(222, 225),
                                     street_suffix = c(226, 227),
                                     planning_jurisdiction = c(228, 229),
                                     street_misc = c(230, 234),
                                     township = c(235, 236),
                                     fire_district = c(237, 238),
                                     land_sale_price = c(239, 250),
                                     land_sale_date = c(251, 260),
                                     zoning = c(261, 265),
                                     deeded_acreage = c(266, 273),
                                     total_sale_price = c(274, 284),
                                     total_sale_date = c(285, 294),
                                     assessed_building_value = c(295, 305),
                                     assessed_land_value = c(306, 316),
                                     parcel_identification = c(317, 335),
                                     special_district_1 = c(336, 338),
                                     special_district_2 = c(339, 341),
                                     special_district_3 = c(342, 344),
                                     billing_class = c(345, 345),
                                     property_description = c(346, 385),
                                     land_classification = c(386, 386),
                                     deed_book = c(387, 392),
                                     deed_page = c(393, 398),
                                     deed_date = c(399, 408),
                                     vcs = c(409, 415),
                                     property_index = c(416, 455),
                                     year_built = c(456, 459),
                                     no_of_rooms = c(460, 465),
                                     units = c(466, 471),
                                     heated_area = c(472, 482),
                                     utilities = c(483, 485),
                                     street_pavement = c(486, 486),
                                     topography = c(487, 487),
                                     year_of_addition = c(488, 491),
                                     effective_year = c(492, 495),
                                     remodeled_year = c(496, 499),
                                     unused = c(500, 501),
                                     special_write_in = c(502, 509),
                                     story_height = c(510, 510),
                                     design_style = c(511, 511),
                                     foundation_basement = c(512, 512),
                                     foundation_basement_pct = c(513, 514),
                                     exterior_wall = c(515, 515),
                                     common_wall = c(516, 516),
                                     roof = c(517, 517),
                                     roof_floor_system = c(518, 518),
                                     floor_finish = c(519, 519),
                                     interior_finish = c(520, 520),
                                     interior_finish_1 = c(521, 521),
                                     interior_finish_1_pct = c(522, 523),
                                     interior_finish_2 = c(524, 524),
                                     interior_finish_2_pct = c(525, 526),
                                     heat = c(527, 527),
                                     heat_pct = c(528, 529),
                                     air = c(530, 530),
                                     air_pct = c(531, 532),
                                     bath = c(533, 533),
                                     bath_fixtures = c(534, 536),
                                     built_in_1_description = c(537, 551),
                                     built_in_2_description = c(552, 566),
                                     built_in_3_description = c(567, 581),
                                     built_in_4_description = c(582, 596),
                                     built_in_5_description = c(597, 611),
                                     city = c(612, 614),
                                     grade = c(615, 619),
                                     assessed_grade_difference = c(620, 622),
                                     accrued_assessed_condition_pct = c(623, 625),
                                     land_deferred_code = c(626, 626),
                                     land_deferred_amount = c(627, 635),
                                     historic_deferred_code = c(636, 636),
                                     historic_deferred_amount = c(637, 645),
                                     recycled_units = c(646, 651),
                                     disqualifying_qualifying_flags = c(652, 652),
                                     land_disqualify_qualify_flag = c(653, 653),
                                     type_use = c(654, 656),
                                     physical_city = c(657, 706),
                                     physical_zip_code = c(707, 711)
                            ),
                            col_types = cols(.default = col_character()) #import data as characters
)
```

###### [JUMP TO THE NEXT STEP](#importing-the-lookup-table)

### C.) Importing a CSV file
Use the Tidyverse function `read_csv()` to import a comma-separate value file, storing it in a variable with the assignment symbol, `<-`. You can use the keyboard shortcut <kbd>Option</kbd> + <kbd>-</kbd> to input that symbol at your cursor.

When we load the data, we'll go ahead and assume everything is a character string (letters and numbers that R treats as plain text) to reduce import errors.

```R
#import a csv of wake county property records
wake_properties <- read_csv('RealEstData06012022.csv',
                            col_types = cols(.default = col_character()) #import data as characters
                            )
```

###### [JUMP TO THE NEXT STEP](#importing-the-lookup-table)

### D.) Importing a tab-delimited file
Use the Tidyverse function `read_csv()` to import a comma-separate value file, storing it in a variable with the assignment symbol, `<-`. You can use the keyboard shortcut <kbd>Option</kbd> + <kbd>-</kbd> to input that symbol at your cursor.

When we load the data, we'll go ahead and assume everything is a character string (letters and numbers that R treats as plain text) to reduce import errors.

```R
#import a tsv of wake county property records
wake_properties <- read_tsv('RealEstData06012022.tsv',
                            col_types = cols(.default = col_character()) #import data as characters
                            )
```
###### [JUMP TO THE NEXT STEP](#importing-the-lookup-table)
---

Regardless of the method you use, this may take a few minutes, depending on the size of your property record file. You should see the data show up in your Environment pane in the top right.

Take note of any error messages or warnings, as these may be the result of import errors that can skew your analysis.

### Importing the lookup table

The Observer/N&O lookup table is provided as a CSV file, so we'll use `read_csv()` to import it.

```R
#import the corporate lookup table
investors_labeled <- read_csv('corporate_landlord_lookup202204301254.txt')
```

If both datasets imported correctly, you should see them in your Environment pane, where you you can click to view them as tables. 