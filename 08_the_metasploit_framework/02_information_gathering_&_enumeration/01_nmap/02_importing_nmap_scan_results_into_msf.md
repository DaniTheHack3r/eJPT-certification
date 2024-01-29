# Importing Nmap Scan Results into MSF

This is a practical demostration only, no presentation attached.

## Laboratory

- Start the postgresql server by running `service postgresql start`.

- Start the msfconsole and check the database status.

- Create a new workspace and import your nmap scan results. We can name it Win2k12 for this example.

- To import the nmap results, run `db_import $PATH_TO_NMAP_SCAN`.

- To check if the data was properly imported, we can run `hosts`. That will show the host we recently scanned with nmap.

- We can also check the services by running `services`. All the services found in the nmap scan will be displayed in the list, with its corresponding host on the first column.

**Note**: This information can be used in conjunction with auxiliary modules to perform different types of scans or exploit modules for those specific services.

### Using nmap from an auxiliary module in MSF

- Change to a new workspace, we can call it Nmap_MSF.

- To run nmap, we can use the command `db_nmap -Pn -sV -O $TARGET_IP`. You don't need to export the file into a certain format, it will be directly saved to the database.
