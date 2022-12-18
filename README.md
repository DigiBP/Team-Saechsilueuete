# Veterinary Drug Compendium

**Team Members**\
Bönhof Berenice\
Buholzer Michael\
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

**Review Document Completeness:**

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

**Request approval:**

The Entry Team member sends an email to the contact at the authorization holder containing a link to the entry and asking for approval.

**Approved / Not Approved:**

Depending on the answering mail of the authorization holder, the process continues or goes back to “Review feedback”.

**File documents:**

The Entry Team member files the approval mail together with the other documents in the folder mentioned above. This folder is then moved into the local archive folder.

**Publish entry:**

The Entry Team member marks the approved entry in the system as OK. The entry will then automatically be published with the next update. (The update is started manually by a member of the Entry Team or Revision Team once or twice a week.)

The 'As-Is-Process':
![TAK-BPMN_Redrafted_is_20221117](https://user-images.githubusercontent.com/102740850/206895665-90c7bd45-595a-49ba-ac82-25e64eec8f7f.png)

## The 'To-Be-Process': 

**Documents Received and Filed:**

The original process only provides for the upload of documents. Now, the upload is done via an online form, which already helps with the pre-selection. With this, additional form fields can be requested (e.g. e-mail, case type, affected animals, active ingredient, Swissmedic ID of the drug, etc.). In the future, this form could be managed via an online portal. This would allow the partners to initiate a new case via personal login credentials, track the current status and even secure communication (if needed) could be ensured. 

In the demo version, e-mail address of the requester, Swissmedic ID, case type and the upload of the Approved Drug Information document (docx) are provided via a Google Forms Form. Then, with Make.com, the entries of the Google Sheets linked to the form are watched and as soon as a new entry (row) appears, the information is extracted, enriched by an autoamtically generated unique case id and a pre-generated approval_url. The Google Sheets provided by/linked to the Google Forms acts in this case as a simple form of database. The second process step is also automatized via Make.com. After, the entries are transferred to Camunda, where a new case is opened.

For security reasons, so that bad actors do not use the process to spam e-mails we forced the Document Suibmission Form to request a Google mail log-in.

https://docs.google.com/forms/d/e/1FAIpQLSc4paGeoj6DRHrGdoJBFstS9N8GzVEoykw593UdGz7M0UPcqw/viewform

Process of document uploading and filing/renaming through Make.com:
<img width="923" alt="Bildschirmfoto 2022-12-15 um 17 26 23" src="https://user-images.githubusercontent.com/102740850/207914631-bb694711-3f27-4c56-aee7-95f4c2475b4a.png">

The first step in the Make **Document received** sequence is a watch rows step.. In the demo the step will be activated manually, but if the process would be deployed in a productive environment it would make most sense to activate a periodic review. Based on the discussion with the process expert Berenice, a period of every couple of hours should be more than enough. It is not time critical to review the files imediately as the information is received.

<img width="250" src="https://user-images.githubusercontent.com/8128472/208289070-25d276a0-c224-41b4-a302-c8847c4d0ae0.png">

The second step is to generate a unique case_id which will be carried accross the process and used to identify the business process instances. The generated case_id later will be sent to the Camunda instance and used as a Business Key there. 
For the sake of the demo the case_id is a simple randomly generated number. It is calculated by taking a randomly generated number, muliplied by the mathematical constant pi then multiplied by 10000 to make the number at least 5 digits long and of course multiplied by the answer to the ultimate question of life, the universe and everything (42). The generated number is rounded to a natural number for consistency. The generated case_id has a slight chance to not be unique, but foir the sake of a demo it is suficient. In a productive environment several different options could be diiscussed with different used cases. A running number could be used as a counter of submitted cases, a running number per holder of authorisation could help identify the requestor etc. 

<img width="250" src="https://user-images.githubusercontent.com/8128472/208289058-11b4ed6a-f82c-4ab7-a17d-568dd84957fa.png">

The next step in Make is to use the submitted swissmedic_id and the generated case_id and create an approval form link with prefilled details. Technically the person could add the details themselves, but a prefilled form significantly cuts on the human mistakes, thus the process is less likely to get stuck. 

<img width="250" src="https://user-images.githubusercontent.com/8128472/208289466-661cd137-ace0-43cb-ba92-31960ed7cd79.png">

Once the form along with the required document is submitted, Make automatically renames the documents to the required format and stores it in the google drive. 

<img width="250" src="https://user-images.githubusercontent.com/8128472/208298797-5a09d638-ffe7-450f-bd5a-01343cac63bc.png">

Once the previous steps are finalised, the Make sequence appends all the generated details into the same google sheet database for further usage.
The format of the renamed file is as follows: "CaseID_" + the generated case_id + "-SwissMedicID_" + swissmedic_id.

<img width="250" src="https://user-images.githubusercontent.com/8128472/208289628-1c2aecd1-0764-4633-885c-dcadfe9774c5.png">

As a last step of this Make sequence is sending all of the information back to Caunda for the process to run further.
In this step we set the Camunda businessKey to match the case_id nummber so that the process can be tracked across the process steps and different make scenarios.
By using a message from Make we send several variables used by the oither steps in the process to Camunda. The following information is send as strings:
* timestamp - the tie stamp value of the submission
* doc_url - the google doc location of the submitted file
* email - the e-mail of the submitter
* swissmedic_id - the official Swissmedic ID of the drug
* case_type - if it is a new request or change request (for the demo version we did not explore the usage any further)
* approval_form - a generated approval form link with the prefilled information.

<img width="250" src="https://user-images.githubusercontent.com/8128472/208289746-4c865bfd-d017-45ae-8346-ecb3454afd9d.png">

**Review Document Completeness:**

In the As-Is-Process, within the check document completeness phase, there are a few checks being done (e.g. the user reads documents, checks what has to be provided and checks for some basic requirements). The team believes that at least a part of that process step could be automated. Since the uploaded documents correspond to a certain recurring structure (form as well as content, e.g. for comparable substances and animals), a document similarity comparison could be used to decide whether the uploaded documents match the information provided. For the demo, we made use of the statistical measure “term frequency-inverse document frequency“ (TF-IDF). TF-IDF was invented for document search and can be used to deliver results that are most relevant to e.g. a search enquiry. The “term frequency” is, what the name says, a count of the number of appearances of a specific term, while the “inverse document frequency” measures how common or rare a word is across a set of documents. The output of TF-IDF is a score between 0 and 1, where 1 means a complete match with the compared document(s) and 0 means no match at all. This algorithm could be used to compare the uploaded document to multiple documents of the same category, e.g. the same active component for the same animal(s). Thresholds could be implemented, where cases below a certain score could be transferred to an exception and thus be checked manually. On the other side, cases above a certain threshold could again be transferred to an exceptional sub-process, as possible duplicates of existing entries might apply. 

In our demo, we compare the uploaded document with a baseline document that only contains the pre-defined structure (titles). The threshold as based on experiences is set to a score of 0.6. If the uploaded document’s TF-IDF score is below, the document needs to be checked by a user (user task). This document completeness check was implemented using an external task worker running a python script. This would make it relatively easy to extend for further reviews or to extend the document check to other documents. To simplify matters, the code for document verification is executed locally. In a real implementation, of course, a cloud instance or a company server would also be used for this purpose (the source code is provided on this github repo).
