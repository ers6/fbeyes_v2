# Bulk Upload Workflow 
Adapted from Washington University University Libraries bulk upload documentation.
- Ensure that you have downloaded the [Internet Archive python library](https://archive.org/developers/index.html). 
- Sign into your Internet Archive account via terminal. To do so, open your terminal and enter the following: 
    `ia configure`
- When prompted, enter the email address and password for your Internet Archive account.
- Use the create folders script to create the folders that you need for the individual items you are creating.
- Move the items into the folders.
- Navigate to the directory in terminal containing the folders.
- Zip the folders with the following script in Terminal. Make sure that _images is added to the end for proper ingest:
    `for i in *; do zip -r "$i.zip" $i; done;` 

- Add “_images” to the end of your zip files and move it to the #4_zip folder
- Copy your completed [record-creation-template](https://github.com/ers6/fbeyes_v2/blob/192dca805321069ca26a6e39e096eb180a450011/ia_workflow/record-creation-template.csv) spreadsheet and populate to create the records for each item. You do not need full metadata at this stage, just select fields.
- In terminal, navigate to the directory and run with uploading.csv being the name of your .csv:
  `$ ia upload --spreadsheet=your_record_creation_sheet.csv`
- Once ingest is complete, you can fill out your [metadata template sheet](https://github.com/ers6/fbeyes_v2/blob/94dbbad1a75eda3b495be48145ec50671f535cdc/ia_workflow/sample-IA-metadata-sheet.csv) and then ingest that with the following command:
    `$ ia metadata --spreadsheet=your_metadata_sheet.csv`
- Check that ingest worked properly by visiting Internet Archive. 
  
