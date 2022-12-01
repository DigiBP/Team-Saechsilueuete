# CliniPharm

**Team Members**\
Bönhof Berenice\
Buholzer Michael Andreas\
Lykovas Andrejus\
Santome Bragado Ruben\
Schwander Sandro

## Table of Contents




## Introduction


## Background
The Veterinary Drug Compendium is published by the CliniPharm Team at the Institute for Veterinary Pharmacology and Toxicology, Vetsuisse Faculty, University of Zurich. Every veterinary drug marketed in Switzerland needs its official information published online (according to law). Pharma companies who are authorization holders for veterinary drugs pay the foundation Refdata for this service, while Refdata currently has given the contract for this publication to the above mentioned Institute.

## Description of the Workflow-Steps in the As-Is-Process

**Documents Received:**

The process starts when an authorisation holder uploads files to the dedicated Dropbox. The current system sends a mail to the Entry Team’s inbox reporting uploaded documents every two hours during working hours.

**File Documents:**

In this step, an Entry Team member moves the received documents from the folder of the dedicated Dropbox to local filing. Locally all the documents belonging to one entry are stored in a folder with the following naming convention: “Swissmedic number”_”name of the drug”_”date of receipt”
Review Document Completeness:
Next, the filed documents are checked for completeness. The Entry Team member looks at the received documents and determines if they are complete and correct. To determine completeness, the worker reads in the documents if this is a new entry or what type of change needs to be done and which information texts have been approved by Swissmedic. Depending on this, the required documents can vary. To determine correctness, the worker looks at the content of the received documents and checks if it fulfills specific criteria (e.g. in the PDF-files, there is no Swissmedic logo or stamp allowed).

**Request missing documents or information:**

If documents or information are incomplete, an Entry Team member sends a mail to the contact at the authorisation holder, requesting the missing documents or information.

**Create or update data entry:**

For a new data entry, the Entry Team member creates a new entry in the database program (Paradox 4.5), labeling it with the unique Swissmedic-Number of the drug. Then firstly, the complete German version of the specialist information on the drug (called Fachinformation (FI)) is copied into the required fields. Secondly, the link(s) to the information page(s) about the active substance(s) of the drug is/are created. (These information pages are a separate service also provided by the CliniPharm team.) Thirdly, the species and route of application of the drug are entered into the system, and also – where this applies - the dosage of the drug per kg bodyweight. Fourthly, the duration of the withdrawal periods is entered into the system for drugs that are given to livestock. As the last step, PDF files of the specialist information and package leaflet are copied to the dedicated folder and renamed according to the internal convention (so they are linked to the published entry).
For changing an existing data entry, the necessary changes are done in the above-mentioned sections.

**Send Review Request:**

A mail is sent to a Review Team member asking for double-checking the created/revised entry.

**Review Data Entry:**

The Review Team member checks the documents and the entry per a dual control principle.

**Send feedback:**

Then the Review Team member emails their reply.

**Review feedback:**

The Entry Team member reads the mail and decides on the next step.
In case of non-minor changes needed to the entry or missing documents, the process goes back to “Create or update data entry” or “Request missing documents or information”.
In case of only minor changes:

**Revise data entry:**

The Entry Team member adds the requested small change(s) to the entry.

Request approval:

The Entry Team member sends an email to the contact at the authorization holder containing a link to the entry and asking for approval.

**Approved / Not Approved:**

Depending on the answering mail of the authorization holder, the process continues or goes back to “Review feedback”.

**File documents:**

The Entry Team member files the approval mail together with the other documents in the folder mentioned above. This folder is then moved into the local archive folder.

**Publish entry:**

The Entry Team member marks the approved entry in the system as OK. The entry will then automatically be published with the next update. (The update is started manually by a member of the Entry Team or Revision Team once or twice a week.)

