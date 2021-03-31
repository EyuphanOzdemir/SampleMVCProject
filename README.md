# SampleMVCProject

===================GENERAL INFORMATION ABOUT THE SOLUTION===================
* The solution (named "RourieSolution") was developed as ASP NET CORE MVC application.
* The solution has 4 projects:
	-CommonLibrary: It includes a small number of methods and constants that can be/are used by other solutions/projects.
	-DBAccessLayer: It includes a data context, entity classes, their repository interfaces and the classes that implement these interfaces as well as a mock repository class for Company entity. I create the database with this project.
	-RourieWebAPI: The ASP NET CORE MVC application that performs the main tasks.
        	-UnitTestProject: A small test application that uses MSTest.
 
==================SETTING UP THE SOLUTION====================================
* There are two ways to create the database, which is named "Rourie" and stored in the LOCALDB SQL Server instance that comes with Visual Studio. 
1) Package Manager Console-> update-database
(DBAccessLayer project should be set as default both in solution explorer and package manager console)
2)In the root folder, there is a folder named "DB". That folder includes a DB creation SQL script (CreateDB.sql).

===================HOW TO LOGIN?=============================================
* There are two users stored in the database. "Admin" whose password is "admin123" and "testuser" whose password is "testuser123". As the names imply, Admin user is the admin and the other user is restricted. testuser is a restricted one and cannot do anything about users (create, list, delete). Other than that they are the same.

===================GENERAL FEATURES OF THE APPLICATION=======================
* Companies and contacts can be inserted, edited, deleted, listed, plus "details" can be seen obviously. To insert a contact, the company should be selected. (1-Many relation between them). There are links between companies and contacts (Show contacts of the company, add contact to the company, Go to the company of the contact)
* Uniqueness of Company name is checked. Similarly, uniqueness of email and mobile phone of contacts.
* If the user wants to delete a company that has some contacts, the user is informed and warned. After deleting, all the related contacts are automatically deleted.    
* There is a collapsible search panel in the Contacts view. There is also pagination for Contacts, which appears after adding more than 10 contacts. 
* A user whose type is admin can list users, add new users and delete the users (admins cannot be deleted).
* Users can change their passwords.
* Company and contact creation events (including who created those entities) as well as possible exceptions (including stack-traces) and 404 responses are logged. The log file is [shortdate].log and it is stored in the root folder of RourieWebAPI folder. Other information is also logged. To see the log records produced by the application, search "Special" in the file, please. 
* When a non-existent resource is demanded, a page/view named "PageNotFound" is shown to the user. When an exception occurs, AppError view is shown.
* Typical form authentication functions are performed. (such as keep-me-signed-in and redirection to the page the user originally demanded after successful login, etc.). If a restricted user calls any User-related view, she is directed to the AccessDenied page.
* The views are designed to be responsive via bootstrap, including drop-down navigation button when the screen is too small.
* Each Create/Edit view uses client-side validations (and as well as server side with the help of model-validity checking) 

===================TECHNICAL CONCEPTS APPLIED OR TARGETED====================
* Dependency injection
* Using repository interfaces 
* Using async CRUD methods in the repository classes and the related action methods in controllers 
(Repository classes include both sync and async versions of CRUD operations)
* Logging
* Error handling (Environment should be set to something other than "Development" to see AppError view, but exception logs will be in the log file in any case)
* Forms (i.e. cookie-based) Authentication and Authorization
* Unit testing (with only two example test methods)
* Code-first approach to design and create the database. (But not because I think this is the right way, but because I wanted to do this way this time)
