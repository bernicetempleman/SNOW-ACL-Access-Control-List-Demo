# SNOW-ACL-Access-Control-List-Demo

- Security Rules defined and set at the Row Level (access to the record) and at the Column Level (access to the field) and is executed when attempting to access any ServiceNow table to perform CRUD (create, read, update and delete)  operations. 
- Admins are except from the Access Controls when the Admin overrides checkbox is checked.

-Note: By default, the system provides ACL rules to restrict access to all database and configuration operations. 

## ACL rules can be defined in three ways:
- Conditional Expressions
- Scripts
- Roles

- After finding a matching ACL rule, the system evaluates if the user has the permissions required to access the object and operation.
-  If a user meets the ACL rule permissions, the instance grants the user access to the listed operation on the object.
-   If a user does not meet the ACL rule permissions of the first matching rule, the system evaluates the next matching ACL rule. 
-   If the user fails to meet the ACL rule permissions of any matching ACL rule, the system denies the user access to the operation on the object. 
![image](https://user-images.githubusercontent.com/12488769/148687615-25af632f-543d-48b4-b5df-27879d28894f.png)

Review: Table Rows and fields
‘Table.None’ applies to the whole table including records. (Green Color)

‘table.field’ applies to only one field on a record. (Red Color)

‘table.*’ applies to every field on a record without a table.field rule (Purple Color)

![image](https://user-images.githubusercontent.com/12488769/148687643-8fb5e95d-00d5-4ba3-bff2-1f4dea787c14.png)

## Search order for a field level rule
![image](https://user-images.githubusercontent.com/12488769/148687664-5fb82608-1c59-465e-aceb-16138be76bcd.png)

If you define a READ ACL with Table.None for Admin & ITIL

Result: Both Admin and ITIL will be able to view all records because they have access to all record with no field restrictions.


If you define a READ ACL with Table.None for Admin & ITIL & Table.* for Admin

Result: Only Admin will have read access because the Table.* is an explicit rule at the field level that grants only Admin read access to all fields.


If you define a READ ACL with Table.None for Admin & Table.* for ITIL

Result: ITIL will not be able to view any records because they only have access at the field level and not at the Record/Row level.

## * vs None
To grant read access to fields 1-10 for Admin and only Fields 1-9 for ITIL:

Table.None read Access Control granted to Admin and ITIL
Table.Field10 read Access Control granted to only Admin



To grant read access to fields 1-10 for Admin and only Fields 9-10 for ITIL:

Table.None read Access Control granted to Admin and ITIL
Table.* read Access Control granted to only Admin
Table.Field9 read Access Control granted to only ITIL
Table.Field10 read Access Control granted to only ITIL


## ACL Demo - Table level 

- Access c (Access control under system security) 
- No new button (need to elevate permissions/ security admin role/ only specific amount of time) 
- Check user/roles/ can’t see role 
- Need to login as admin// only visible to someone who already has it 
- Can’t impersonate
-  Elevate roles to add the security admin role
-  Create 2 tables (Parent and child) 
- Table-> tables and columns -> new
 
 ### Name: Parent - ACL demo
-  Check create module and create mobile module 
- Add to module: self-service 
- Add 2 col 
• Group reference group 
• Title string 
- Controls: make extensible 
- Create access control checked- creates 4 ACLs with table (only table acl and 1 role to access) 
- Save- see 4 ACLs 
![image](https://user-images.githubusercontent.com/12488769/147889337-ff74cdf3-0c77-40ca-949c-4177402025cc.png)

### Name: Child - ACL demo
-  Extends: Parent - ACL demo 
- Check create module and create mobile module
-  Add to module: self-service 
- Add 1 col Description string 
- Controls: 
- Create access control checked- creates 4 ACLs with table (only table acl and 1 role to access) 
- Save- > see 4 ACLs 
- Check acl list 
- Save - 4 ACLs

### See self service modules 
- Create 2 records for each table 
- Parent sees all 4 records 

### Create user to test/ can change theme color for testing 
- Acl.demo 
- No roles 
- Impersonate acl.demo 
- Can’t see tables 
-  end impersonate 


Give child table role to user
 Impersonate / can see child table // all 4 crud
 End impersonate 

Elevate access 
Inactivate acls for child table
 Remove role for child
 Impersonate 
Can’t see because of parent table.none stil exist and has role/ user denied access
 End impersonate

 ### Elevate 
- Enable READ ACL for child
-  Remove role from read acl child(no role on acl for child table- Click u_child_demo_acl.list )
-  Impersonate /can’t see child module/ module still has role// role not on table 
- Search: u_child_demo_acl.list // can see table /only read access/ write prevent by parent acl 
- End impersonate

### Elevate/ Access controls
-  make write access true for child 
- remove role from write acl on child
-  impersonate/ have read and write/ not create and delete// can edit 
- end impersonate


## ACL Demo -field level 
- //go to user acl.demo and add parent role
-  Impersonate
-  Can see parent module and records 
- End impersonate

### Create field level that only child role can edit access 
- Access c 
- Elevate
-  New 
- Title field on parent 
- Operation – write 
- Name: parent acl demo ( None : table level *Field level ) 
- Title (specific field) 
- Required role: u_child_demo_acl_user// blocking others 
- Can also give conditions 
- Or Advanced script 

###See new acl in list 
- Impersonate/ can’t edit title / can edit group// have parent role / not child role 
- End impersonate 

### Give child role 
- Impersonate 
- Can edit title field
