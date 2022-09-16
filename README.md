---
editor_options: 
  markdown: 
    wrap: 72
---

# Bloomberg Industry Group Investigations PFAS Litigation Open Data

## Terms of Use

By downloading the Dataset, you agree that you will attribute the
Dataset and any use of the Dataset to Bloomberg Law. You may use the
Dataset for personal or internal business purposes, and may make limited
use of the Dataset in connection with the provision of other services to
clients; provided that you may not monetize the Dataset or otherwise
make commercial use of the Dataset where the Dataset constitutes all, or
substantially all, of the commercial offering. The Dataset is provided
"as-is" and without any express or implied warranties.

## Introduction

This repository contains the database of PFAS-related lawsuits that was
used to produce the story [Companies Face Billions in Damages as PFAS
Lawsuits Flood
Courts](https://news.bloomberglaw.com/pfas-project/companies-face-billions-in-damages-as-pfas-lawsuits-flood-courts "Companies Face Billions in Damages as PFAS Lawsuits Flood Courts"),
which was published on May 23, 2022. The custom-built database includes
more than 6,400 PFAS-related lawsuits and was compiled using data from
the Bloomberg Law platform.

PFAS, which stands for per- and polyfluoroalkyl substances, are a group
of man-made chemicals that are distinguished by their durability and
water resiliency. They're often referred to as "forever chemicals"
because of their inability to naturally break down.

## How the Database was Constructed

PFAS case filings were found in one of two ways:

1.  **Search Results:** A string of keywords and regular expressions
    were used to find lawsuits relating to PFAS. The search was further
    narrowed down by limiting results to federal district courts,
    certain filing documents (complaints, petitions, and notices), and
    certain nature of suit codes most directly related to PFAS
    liability. Due to how searches are conducted on the Bloomberg Law
    platform, it's possible that many lawsuits related to PFAS did not
    appear in search results. To correct for this, we also included
    cases found using the below method.

2.  **Multidistrict Litigation Member Cases:** There are three known
    multidistrict litigation (MDL) cases that focused on PFAS
    litigation. The lead docket for these MDLs included information on
    member cases that were then included in our database of PFAS
    litigation.

Cases from as far back as could be accessed through Q1 2022 (ending
March 31, 2022) are included in the database. The earliest case in the
database was filed on July 20, 2005.

This database is not being updated and does not include any newly filed
cases past Q1 2022.

## Note on Database Structure

This dataset is organized such that each party to a lawsuit is an
individual observation, or row. Each lawsuit may contain many rows of
data where most data fields are duplicated aside from the `party_types`,
`party_names`, and `standardized_party_names` fields.

## Data Description

[pfas-litigation-2022Q1.csv](data/pfas-litigation-2022Q1.csv) - A
comma-separated values file of PFAS case filings through March 31, 2022,
containing 84,536 records plus a header row.

## Data Dictionary

| Data Field                 | Description                                                                                                                                                                                                                                                                            |
|-----------------------------------------|-------------------------------|
| `docket_ID`                | Unique case identifier assigned by the Bloomberg Law platform. Can be used to access dockets directly on Bloomberg Law with the following link syntax: <https://www.bloomberglaw.com/product/blaw/document/%60docket_ID>\`                                                             |
| `case_name`                | Lawsuit name, most commonly consisting of *plaintiff* v. *defendant*                                                                                                                                                                                                                   |
| `date_filed`               | Date lawsuit was filed                                                                                                                                                                                                                                                                 |
| `last_updated`             | Last time the docket on Bloomberg Law was synced to PACER to download additional docket entries or changes                                                                                                                                                                             |
| `docket_number`            | Court-assigned docket number, e.g. `1:05-cv-01818` *(Note: These are not unique identifiers. There could be multiple of the same docket number across various federal district courts.)*                                                                                               |
| `court_name`               | Federal district court where the case is located                                                                                                                                                                                                                                       |
| `judge`                    | Federal judge assigned to case                                                                                                                                                                                                                                                         |
| `party_type`               | Party's relationship to the lawsuit, most commonly *plaintiff* or *defendant*                                                                                                                                                                                                          |
| `party_names`              | Party's name                                                                                                                                                                                                                                                                           |
| `standardized_party_names` | Standardized naming convention for the top 20 defendants and the various iterations of DowDupont, DuPont de Nemours, and E.I. du Pont de Nemours & Co. If name wasn't standardized, this entry defaults to what is in `party_names`. See below for companies with standardized naming. |
| `money_demand`             | Money amount demanded by plaintiff in the case. This field is not unique per observation so will be repeated for each party in a case. *(Note: This number does not represent funds paid or a final judgment by the court, so be cautious in how this is used.)*                       |
| `doc_id`                   | Another unique case identifier assigned by the Bloomberg Law platform                                                                                                                                                                                                                  |
| `lead_case`                | If the case belongs to a multi-district litigation, this is the docket number of the lead case *(Note: Not all cases that belong to a multi-district litigation will necessarily have this field filled.)*                                                                             |
| `cause_of_action`          | Cause of action - this is the section of law that the plaintiff cites in their complaint as giving them the right to file the lawsuit                                                                                                                                                  |
| `nature_of_suit`           | Nature of suit code - this is a categorization tag that identifies the subject matter in a lawsuit                                                                                                                                                                                     |
| `in_AFFF_MDL`              | Tag that identifies if a lawsuit is part of the AFFF multidistrict litigation based in the District of South Carolina (lead case: 2:18-mn-02873). Default is `NA`; otherwise `Y` if true                                                                                               |
| `in_C_8_MDL`               | Tag that identifies if a lawsuit is part of the C-8 multidistrict litigation based in the Southern District of Ohio (lead case: 2:13-md-02433). Default is `NA`; otherwise `Y` if true                                                                                                 |
| `in_teflon_MDL`            | Tag that identifies if a lawsuit is part of the teflon multidistrict litigation based in the Southern District of Iowa (lead case: 4:06-md-1733). Default is `NA`; otherwise `Y` if true                                                                                               |

**Companies with standardized naming in the `standardized_party_names`
column:** - CHEMOURS - DOWDUPONT INC. - DUPONT DE NEMOURS INC. - E.I. DU
PONT DE NEMOURS & CO. - 3M - BUCKEYE FIRE EQUIPMENT COMPANY - TYCO FIRE
PRODUCTS - NATIONAL FOAM - DYNAX CORPORATION - CHEMGUARD INC -
KIDDE-FENWAL INC - CORTEVA INC - CLARIANT CORPORATION - CARRIER
CORPORATION - ARKEMA INC - AGC INC - UTC FIRE & SECURITY AMERICAS
CORPORATION INC - UNITED TECHNOLOGIES CORPORATION - NATION FORD CHEMICAL
COMPANY - AMEREX CORPORATION - DEEPWATER CHEMICALS INC - CHUBB FIRE &
SECURITY LTD
