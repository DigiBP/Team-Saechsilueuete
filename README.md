# Veterinary Drug Compendium

**Team Members**\
Bönhof Berenice\
Buholzer Michael\
Lykovas Andrejus\
Santome Bragado Ruben\
Schwander Sandro

## Table of Contents




## Introduction

A team must digitalise processes based on an own project idea or a selected pre-defined project case. An own project idea is recommended and appreciated.

The following deliverables are mandatory:
* Link to GitHub repositories containing:
  * Modelling artefacts (such as BPMN, DMN, CMMN, etc.) and, if required, other project artefacts (such as configuration files, source code, etc.)
  * Documentation about project and processes (as GitHub markdown files (e.g., Readme and interlinked .md files)).
* Link to a running workflow(s) and/or instantiation(s) of a: 
  * Link to start form(s) and/or cloud-based deployment(s)
  * Link to presentation slides

## Background
For every veterinary drug marketed in Switzerland each Swissmedic approved drug information must be published online, according to law. Pharma companies who are authorization holders for veterinary drugs pay the foundation Refdata for this service, while Refdata currently has given the contract for this publication to the Institute for Veterinary Pharmacology and Toxicology at the University of Zurich. There the Veterinary Drug Compendium (VDC) is published by the CliniPharm Team. Whenever a new drug comes to market, leaves the market, or the approved information of an existing drug is changed, the respective entry of this drug in the VDC has to be created, deleted or changed. For these purposes the CliniPharm Team receives new documents from authorization holders on a regular basis. The CliniPharm personel is split into the Entry Team whose members create, change or delete entries in the VDC, and the Review Team who ensure quality by reviewing the Entry Team's work.

## The 'As-Is-Process':
![VDC_as-is_20221218](https://user-images.githubusercontent.com/115710100/208304796-c8482ae9-cb6f-4f60-ac74-11744d09a648.png)

## Description of the Workflow-Steps

### Documents Received:

The process starts when an authorization holder uploads documents to the dedicated file hosting service. The current system sends an email to the Entry Team’s inbox reporting uploaded documents every two hours during working hours.

### File Documents:

In this step, an Entry Team member moves the received documents from the folder of the dedicated file hosting service to local filing. Locally all the documents belonging to one process are stored in one folder. These folders are named by convention to enable retrieval of information for specific amendments in the VDC.

### Review Document Completeness:

Next, the filed documents are checked for completeness. The Entry Team member looks at the received documents and determines if they are complete and correct. To determine completeness, the worker reads in the documents if this is a new entry or what type of change needs to be done and which information texts have been approved by Swissmedic. Depending on this, the required documents can vary. To determine correctness, the worker looks at the content of the received documents and checks if it fulfills specific criteria (e.g. in the PDF-files, there is no Swissmedic logo or stamp allowed).

### Request missing documents or information:

If documents or information are incomplete, an Entry Team member sends an email to the contact at the authorization holder, requesting the missing documents or information.

### Create or update data entry:

For a new data entry, the Entry Team member creates a new entry in the database program (Paradox 4.5), labeling it with the unique Swissmedic-Number of the drug. Then firstly, the complete German version of the specialist information on the drug (called Fachinformation (FI)) is copied into the required fields. Secondly, the link(s) to the information page(s) about the active substance(s) of the drug is/are created. (These information pages are a separate service also provided by the CliniPharm team.) Thirdly, the species and route of application of the drug are entered into the system, and also – where this applies - the dosage of the drug per kilogram bodyweight. Fourthly, the duration of the withdrawal periods is entered into the system for drugs that are given to livestock. As the last step, PDF files of the specialist information and package leaflet are copied to the dedicated folder and renamed according to the internal convention (so they are linked to the published entry).
For changing an existing data entry, the necessary changes are done in the above-mentioned sections.

### Send Review Request:

An email is sent to a Review Team member asking for the review of the created/revised entry.

### Review Data Entry:

The Review Team member checks the documents and the entry per a four-eye principle.

### Send feedback:

Then the Review Team member emails their reply.

### Review feedback:

The Entry Team member reads the reply and proceeds accordingly.

### Revise data entry:

The Entry Team member adds the requested change(s) to the entry.

### Request approval:

The Entry Team member sends an email to the contact at the authorization holder containing a link to the entry and asking for approval via email.

### Review response:

The Entry Team member reads the response of the authorization holder and proceeds accordingly.

### File documents:

The Entry Team member files the approval email together with the other documents in the folder mentioned above. This folder is then moved into the local archive folder.

### Publish entry:

The Entry Team member marks the approved entry in the system as OK. The entry will then automatically be published with the next update. (VDC updates are started manually by a member of the Entry Team or Revision Team once or twice a week.)

## The 'To-Be-Process': 
![image](https://user-images.githubusercontent.com/8128472/208300798-1371d125-2083-4f52-9e9c-f679538d3e20.png)

## Description of the Workflow-Steps

### Documents Received and Filed:

The original process only provides for the upload of documents. Now, the upload is done via an online form where additional information can be requested (e.g. email, case type, affected animals, active ingredient, Swissmedic ID of the drug, etc.), which already helps with the pre-selection. In the future the form could be managed via an online portal. This would allow the partners to initiate a new case via personal login credentials, track the current status and even secure communication could be ensured. 

In the demo version, email address of the requester, Swissmedic ID, case type and the upload of the Approved Drug Information document (docx) are provided via a Google Forms form. Then, with Make.com, the entries of the Google Sheets linked to the form are watched and as soon as a new entry (row) appears, the information is extracted, enriched by an automatically generated unique case id and a pre-generated approval_url. Google Sheets linked to the Google Forms act as a simple form of database. The step of renaming the file is also automatized via Make.com. After, the entries are transferred to Camunda, where they trigger a start event.

For security reasons, so that bad actors do not use the process to spam emails we forced the <a href=https://docs.google.com/forms/d/e/1FAIpQLSc4paGeoj6DRHrGdoJBFstS9N8GzVEoykw593UdGz7M0UPcqw/viewform>Document Submission Form</a> to request a Google mail log-in. In the productive environment, the form would also be available after log-in. If the partner wishes to get notified under a personal email address insted of a general company one they would enter their email address manually in the form.

<img width="250" src="https://user-images.githubusercontent.com/8128472/208304224-301ef8da-149e-4dad-b0cb-d1a6cb318894.png">

For demonstration purposes, only one document is submitted in the form and the upload of e.g. other language versions was forgone. In the productive environment, the form would be designed to help the partners upload correctly, by determining all the required documents through the requested additional information.

Once the form is submitted, the data will apear in the central data base (google sheet in the demo case):
![image](https://user-images.githubusercontent.com/8128472/208304197-cb752c1f-fa23-4ace-877a-121acf000c5d.png)


Process of document uploading, filing and renaming through Make.com:
<img width="923" alt="Bildschirmfoto 2022-12-15 um 17 26 23" src="https://user-images.githubusercontent.com/102740850/207914631-bb694711-3f27-4c56-aee7-95f4c2475b4a.png">

The first step in the Make **Document received** scenario is a watch rows step. In the demo the scenario is scheduled to check every 15 minutes or triggered manually, but if the process would be deployed in a productive environment a periodic review every couple of hours would be implemented, similar to the as-is process.

<img width="250" src="https://user-images.githubusercontent.com/8128472/208289070-25d276a0-c224-41b4-a302-c8847c4d0ae0.png">

The second step is to generate a unique case_id which will be carried accross the process and used to identify the business process instances. The generated case_id later will be sent to the Camunda instance and used as a Business Key there. For the sake of the demo the case_id is a simple randomly generated number. It is calculated by taking a randomly generated number, multiplied by the mathematical constant pi then multiplied by 10'000 to make the number at least five digits long and of course multiplied by the answer to the ultimate question of life, the universe and everything (42). The generated number is rounded to a natural number for consistency. The generated case_id has a slight chance to not be unique, but for the sake of a demo it is sufficient. In a productive environment several different options could be discussed with different used cases. A running number could be used as a counter of submitted cases, a running number per holder of authorization could help identify the requestor etc. 

<img width="250" src="https://user-images.githubusercontent.com/8128472/208289058-11b4ed6a-f82c-4ab7-a17d-568dd84957fa.png">

The next step in Make is to create a link to a prefilled approval form that will be sent to the requestor at a later step. The form is prefilled with the submitted swissmedic_id and the generated case_id. Technically this information could be added manually, but prefilling significantly reduces human mistakes, thus the process is less likely to get stuck. 

<img width="250" src="https://user-images.githubusercontent.com/8128472/208289466-661cd137-ace0-43cb-ba92-31960ed7cd79.png">

Once the form along with the required document is submitted, Make automatically renames the documents to the required format and stores it in Google Drive. 

<img width="250" src="https://user-images.githubusercontent.com/8128472/208298797-5a09d638-ffe7-450f-bd5a-01343cac63bc.png">

Once the previous steps are finalised, the Make scenario appends all the generated details into the same google sheet database for further usage.
The format of the renamed file is as follows: "CaseID_" + the generated case_id + "-SwissMedicID_" + swissmedic_id.

<img width="250" src="https://user-images.githubusercontent.com/8128472/208289628-1c2aecd1-0764-4633-885c-dcadfe9774c5.png">

As its last step this Make scenario sends all of the information to Camunda to trigger the start event.
Here the Camunda businessKey is set to match the case_id number so that the process can be tracked across the process steps and different Make scenarios.
By using a message from Make we send several variables used by the other steps in the process to Camunda. The following information is sent as strings:
* timestamp - the time stamp value of the submission
* doc_url - the google doc location of the submitted file
* email - the email address of the submitter
* swissmedic_id - the official Swissmedic ID of the drug
* case_type - if it is a new request or change request (for the demo version we did not explore the usage any further)
* approval_form - a generated approval form link with the prefilled information.

<img width="250" src="https://user-images.githubusercontent.com/8128472/208289746-4c865bfd-d017-45ae-8346-ecb3454afd9d.png">

### Review Document Completeness:

In the As-Is-Process, within the check document completeness phase, there are a few checks being done (e.g. the user reads documents, checks what has to be provided and checks for some basic requirements). The team believes that at least a part of that process step could be automated. Since the uploaded documents correspond to a certain recurring structure (form as well as content, e.g. for comparable substances and animals), a document similarity comparison could be used to decide whether the uploaded documents match the information provided. For the demo, we made use of the statistical measure “term frequency-inverse document frequency“ (TF-IDF). TF-IDF was invented for document search and can be used to deliver results that are most relevant to e.g. a search enquiry. The “term frequency” is, what the name says, a count of the number of appearances of a specific term, while the “inverse document frequency” measures how common or rare a word is across a set of documents. The output of TF-IDF is a score between 0 and 1, where 1 means a complete match with the compared document(s) and 0 means no match at all. This algorithm could be used to compare the uploaded document to multiple documents of the same category, e.g. the same active component for the same animal(s). Thresholds could be implemented, where cases below a certain score could be transferred to an exception and thus be checked manually. On the other side, cases above a certain threshold could again be transferred to an exceptional sub-process, as possible duplicates of existing entries might apply. 

In our demo, we compare the uploaded document with a baseline document that only contains the pre-defined structure (titles). The threshold as based on experiences is set to a score of 0.6. This document completeness check was implemented using an external task worker running a python script. This would make it relatively easy to extend for further reviews or to extend the document check to other documents. To simplify matters, the code for document verification is executed locally. In a real implementation, of course, a cloud instance or a company server would be used for this purpose (the source code is provided on this github repo (https://github.com/DigiBP/Team-Saechsilueuete/tree/main/External%20Worker).

### Review exception

If the uploaded document’s TF-IDF score is below 0.6, the document needs to be checked by a member of the Entry Team (user task). There might be cases where the structure does not fit the baseline but is still in order. Then the exception is accepted and the next task in the process is triggered through Camunda. If the submitted document is truly not correct the exception is rejected, the Entry Team member contacts the customer and the process ends. 

### Create or update date entry:

Because of the previous step automation we decided to keep a four-eyes principle and kept the publishing of the data entry as a user task. In this step an Entry Team member would ensure the four-eyes principle and catch the majority of mistakes or inconsistencies from the automated steps. To show that this task is assigned to the Entry Team the variable "entry_team" was entered under candidate group in Camunda.
In a productive environment, the entry team member would enter the received drug information in the Paradox 4.5 system which would then be reviewed and published after the final approval in the last steps of the process.

For the demo set-up we used a google sites service and created a dummy website where we manually embed the received drug information and mark the page as "Not approved".
![image](https://user-images.githubusercontent.com/8128472/208302688-505be29b-f922-4bc3-b62d-8f4816e38a7e.png)

Once the information is published to the page, the Entry Team member can finish the task in Camunda and provide the published information link which will be further used in the process.

<img width="1419" alt="image" src="https://user-images.githubusercontent.com/106996493/209012000-480d2cb8-62bd-41df-9166-1c641db81c27.png">

### Review data entry:

The review team receives the link to the website via Camunda and reviews the page. The goal is to review whether the right file has been published and if it looks aesthatically acceptable. The reviewer then clicks on the checkbox in Camunda and completes the task to trigger the next task. 

<img width="1419" alt="image" src="https://user-images.githubusercontent.com/106996493/209011677-cc37abf7-6eb9-43f9-b69f-e44ba2038607.png">

### Revise data entry:

If the data entry is not correct, a member of the Entry Team takes over this user task and makes the required correction. The user is provided with the necessary information in the Form fields of Camunda and adds the information if major changes were required. The last information determines whether the process goes back to be reviewed again or continues.

### Request approval:

Once the entry is created or updated and the four-eyes principle is satisfied the system autoamtically triggers an email approval request to the authorization holder. The email is sent to the original requestor and contains one link to the published information and another link to a pre-filled approval form.

![image](https://user-images.githubusercontent.com/8128472/208302958-e93430f4-760d-4b03-ab02-e3cddf0e80be.png)

Camunda triggeres this scenario via http-connector to a custom webhook in Make, which includes the communication of the required variables.

<img width="250" src="https://user-images.githubusercontent.com/115710100/208379589-600f8af4-6c51-4f92-9b87-08aadd921a71.png">

<img width="250" src="https://user-images.githubusercontent.com/8128472/208303149-8cf06d61-dd2d-4668-8333-5d5b2fe122e5.png">

The email is then generated by Make using the information provided previously throughout the process (swissmedic_id, VDC_link, approval_form). To allow the sending of the email via Gmail an OAuth for Make's Gmail API was set up.

<img width="250" src="https://user-images.githubusercontent.com/8128472/208303223-6737a1bf-7e42-4dba-b6d0-09fa0733ffe0.png">

<img width="600" alt="image" src="https://user-images.githubusercontent.com/106996493/209012290-bcb63658-74ba-4720-8282-ee8b18eb8df4.png">

As the approval form is already prefilled with the additional needed information, the approver only has to enter their email and click "Approve" or "Reject". In case of rejection, the form has a field where additional information can be entered.

<img width="250" src="https://user-images.githubusercontent.com/8128472/208303722-ca927927-b638-4786-ad21-6796aec6f6d1.png">

### Response received:

Once the approval form is filled the information will appear in the Approval sheet in the master database.

![image](https://user-images.githubusercontent.com/8128472/208303856-966f691c-3220-4d50-b936-757b4477ffe7.png)

Same as in the Make scenario before the start event, Make is looking for new data entries and kicks off the further steps to send the information back to Camunda with all the required information:

* BusinessKey
* approved or rejected key
* Additional information in case of rejection
* case_id
* swissmedic_id

![image](https://user-images.githubusercontent.com/8128472/208303906-750cd96d-e301-48dc-9479-3cc704491990.png)

<img width="250" src="https://user-images.githubusercontent.com/8128472/208303919-aa13ca86-40d1-46ad-b521-6b4e45840f68.png">


<img width="250" src="https://user-images.githubusercontent.com/8128472/208303961-65c7c27e-be64-4cb3-ad35-ca2839ddbfe9.png">


### Publish entry:

The final step of the process, is a simple user task, where the user access the website and removes the ribbon saying "Not Approved". This indicated to the end users that the document is approved. 

![publish entry](https://user-images.githubusercontent.com/106996493/208474404-b3ec1f90-8c59-4ca2-8216-4e8c1cb3ce2f.png)
