1. In the Workspace, click on 'New Item' and select 'Data pipeline'.
<img width="978" alt="Screenshot 2024-12-19 at 9 22 23 AM" src="https://github.com/user-attachments/assets/2223d019-9751-4044-aef2-9328f192194b" />

2. Click on 'Pipeline activity'.  Select 'Copy data'.
<img width="1440" alt="Screenshot 2024-12-19 at 9 25 50 AM" src="https://github.com/user-attachments/assets/bfc57aad-1734-4b23-95fd-aa86df0f7cd5" />

3. At the pipeline canvas area, the 'copy data' activity is created.  Click on the 'copy data' activity and select 'clone' to make seven 'copy data' activities for the following files to be ingested:
   - Calendar
   - Customers
   - Products
   - Regions
   - Returns
   - Stores
   - Transactions 1997
   - Transactions 1998
  
For each activity under 'Name', type 'Copy (respective File Name)'.  Make sure that the 'Activity State' is selected as 'Activated'.
<img width="1440" alt="Screenshot 2024-12-19 at 9 25 13 AM" src="https://github.com/user-attachments/assets/fdab596a-2386-46e0-b45a-04f351daaade" />

4. Under 'Source', select 'Connection' for the Lakehouse created previously (MavenMarket_Lakehouse).  For the 'File path', browse to select the CSV file respective to the 'copy data' activity.  For the 'File format', select 'DelimitedText'.
<img width="1371" alt="Screenshot 2024-12-19 at 9 27 08 AM" src="https://github.com/user-attachments/assets/550c333b-9c7b-4c9a-af72-9c033c108b85" />

5. Under 'Destination', select 'Connection' for the Warehouse created previously (MavenMarket_Warehouse). For the 'Table', make sure the schema is named from the schema created previously in the Warehouse (mavenmarket) and the table name is named after the respective files to be sent down the pipeline.
<img width="1373" alt="Screenshot 2024-12-19 at 9 27 47 AM" src="https://github.com/user-attachments/assets/dd1e961a-ce96-4c2c-bca5-49c625b44f2a" />

6. Click 'Validate' to see if there are any errors.  After, click 'Run'.  If there are no errors, the 'copy data' activities should be successful.
<img width="1440" alt="Screenshot 2024-12-19 at 2 02 46 PM" src="https://github.com/user-attachments/assets/6166959c-7084-4649-9a0e-628199d70b9e" />
