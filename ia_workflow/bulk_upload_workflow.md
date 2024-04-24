# Bulk Upload Workflow 
Adapted from Washington University University Libraries bulk upload documentation.
- Sign into your Internet Archive account via terminal. To do so, open your terminal and enter the following: 
`ia configure`
- When prompted, enter the email address and password for your Internet Archive account.
- Use the create folders script to create the folders that you need for the individual items you are creating.
- Move the items into the folders
- Zip the folders with the following script in Terminal. Make sure that _images is added to the end for proper ingest:
  `for i in *; do zip -r "$i.zip" $i; done;` 

