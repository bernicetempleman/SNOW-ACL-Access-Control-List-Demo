# SNOW-ACL-Access-Control-List-Demo

##ACL Demo - Table level 

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
