# masa-exam

**Part I: Theory**
*Please, do NOT use online resources as an assistance for this part of the exam*

**Section A: Please, select the correct answer or the most close to the correct one**

 1. What is a PR?
 - [ ] Program Result: the outcome of a programming effort available for testing
 - [ ] Public Relations: a practice of managing and influencing an organizational info to the public
 - [x] Pull Request: a request to review the code of a developer prior to merging it main branch
 - [ ] Private Role: A security role that is used in internal system processing

2. What is the role of a service in nodejs server architecture?
 - [ ] Get the request from the router, treat the request parameters, prepare the response of the server to the consumer
 - [x] Keep state of a specific logic portion of the system, provide processing of the data passed from the different controllers, parse the data and returned the processed response
 - [ ] To be the first element in the system that should service the consumer for his CRUD request to the server
 - [ ] To provide services to the system that do not require a state but should be used across the whole system

3. What is INNER JOIN?
 - [ ] A mechanism to link between to tables in the SQL query to bring data based on the same value in two tables. Allows NULL values on one on the sides of the JOIN
 - [x] A mechanism to link between to tables in the SQL query to bring data based on the same value in two tables. Only non NULL values are accepted for both sides of the JOIN
 - [ ] A way of executing to `foreach` loops in JS/TS while the internal loop uses values of the external loop
 - [ ] Such a term does not exist

4. What is the code of a server error in HTTP protocol?
 - [ ] 2xx
 - [ ] 3xx
 - [ ] 4xx
 - [x] 5xx

5. What is the correct flow a story?
 - [ ] Software Detailed Design (SDD), Product design, QA review, UI design, Development, QA testing, Customer review
 - [x] Customer request, Product design, UI design, SDD, QA review, Development, QA testing, Customer User Acceptance Testing (UAT)
 - [ ] Product design, SDD, QA review, UI design, Development, QA testing, UAT
 - [ ] Customer request, UI design, Product design, UAT, QA review, Development, QA testing

6. Which tool would you use to test a nodejs server?
 - [ ] Browser
 - [ ] Postman
 - [ ] Fiddler
 - [x] All answers are correct

7. What is the most secure way to connect to SQL Server?
 - [ ] Integrated security
 - [x] Mixed mode
 - [ ] SQL Server login
 - [ ] Application role

8. What is the correct pair of a protocol and the port for secure HTTP communication?
 - [ ] HTTP:80
 - [ ] HTTPS:80
 - [x] HTTPS:443
 - [ ] HTTP:443

9. What is a trigger
 - [x] Trigger is a piece of code executed by the database engine whenever some action is performed on a database object like tables, view, etc.
 - [ ] Trigger is a method that is called JS/TS environment whenever a certain event is fired to complete an asynchronous code execution
 - [ ] Trigger is a processing being performed right after the merge of a code to main branch in order to run a build for the system
 - [ ] Trigger is the mechanism by which the router is sending its data to the controller in nodejs server

10. Why would you use the JWT token? (more than a single answer can be selected)
 - [ ] JWT tokens are encrypted
 - [ ] It's a more secure way of handling authentication and authorization data than username and password
 - [x] JWT tokens are signed and this signature can be verified uniquely
 - [ ] All answers are correct

**Section B: Please, explain the following terms the best way you can**

11. Authentication & Authorization
Authentication is a process of giving permission to a user to "enter" the system. An access to some functionality of the system is not guaranteed yet.

Authorization is a process of giving to an authenticated user an access to specific part of functionality of our system. We can do that while knowing a role that the user got. The role is often included in Javascript Web Token.

12. Stored procedure
Stored procedure is a piece of code predefined by the user with its unique name. It's executed by the database engine whenever it's called by the user or other procedure/trigger etc. It can perform DML, DDL and other commmands in the database.  

13. Git rebase
Git rebase command is used to move a sequence of commits from the first branch to the second branch as if we had created the first branch just from the last commit of the second branch. This operation has a significant drawback that the history of commits is not saved. However, it can be used to maintain a linear project history.

14. Generics
Generics is a convenient tool in TypeScript used to provide a way to create reusable functions (and other objects) that then can be used for different data types manipulation. 

15. Middleware
Generally, middleware is a function in the application request-response cycle used, for instance, to authorize a user. It's called in front of some other function in order to check whether a user has an access to this specific functionality in this case. Additionally, middleware function may perform other operations in the application request-response cycle as it has access to request, response and next objects.
 
**Part II: Practice on paper**
*No restrictions on online resources usage*

16. You received a bug stating the following: "Intermittently the following method results in a system getting stuck." You're required to find and fix the problem in this method:

		public  static  addMonths(date: Date, value: number): Date {
		    let expectedMonth: number = date.getMonth() + value;
		    if (expectedMonth  >  12) {
		        expectedMonth = expectedMonth % 12;
		    }
    
		    if (expectedMonth  <  0) {
		        expectedMonth += 12;
	        }
    
		    date.setMonth(date.getMonth() + value);
	        const daysToAdd: number = date.getMonth() >  expectedMonth ? -1 : 1;
	        while (date.getMonth() !== expectedMonth) {
		        date.setDate(date.getDate() + daysToAdd);
		    }
    
		    return  date;
	    }

		Fixed code:
		public  static  addMonths(date: Date, value: number): Date {
		    let expectedMonth: number = date.getMonth() + value;
		    while (expectedMonth  >  12) {
		        expectedMonth = expectedMonth % 12;
		    }
    
		    while (expectedMonth  <  0) {
		        expectedMonth += 12;
	        }
    
		    date.setMonth(date.getMonth() + value);
	        const daysToAdd: number = date.getMonth() >  expectedMonth ? -1 : 1;
	        while (date.getMonth() !== expectedMonth) {
		        date.setDate(date.getDate() + daysToAdd);
		    }
    
		    return  date;
	    }

17. **Having the following DB tables diagram:** *=> 10 points*

![](https://github.com/lentyaishe/masa-exam/blob/dev/resources/db-relations.jpg)

You need to write a query that returns for each student his/her parents' information/ Take into consideration that the amount of parents for the child can be different ("Orphan" comment should appear for any child that has no parents defined in the tables). The data should be returned in the following manner:

| Student | Parents |
| --- | --- |
| John Doe | Mark Doe (09-1231231), Jane Doe (09-4132123) |
| Mary Smith | Klark Smith (07-2134897) |
| Patrice Raymond | Orphan |

Answer:
SELECT tab1.student as Student,
	   (CASE 
			WHEN tab3.parent_cnt = 0 THEN 'Orphan'
			WHEN tab3.parent_cnt > 0 THEN CONCAT(tab1.parent, ', ', tab2.parent)
	   END) AS Parents 
FROM 
	(SELECT 
		id,
		CONCAT(s.first_name, ' ', s.last_name) AS student,
		CONCAT(p.first_name, ' ', p.last_name, ' ', p.phone) AS parent
	 FROM 
		student s
		LEFT JOIN parent_to_student ps ON s.id = ps.student_id
		LEFT JOIN parent p ON p.id = ps.parent_id) tab1
LEFT JOIN 
	(SELECT 
		id,
		CONCAT(s.first_name, ' ', s.last_name) AS student,
		CONCAT(p.first_name, ' ', p.last_name, ' ', p.phone) AS parent
	 FROM 
		student s
		LEFT JOIN parent_to_student ps ON s.id = ps.student_id
		LEFT JOIN parent p ON p.id = ps.parent_id) tab2 
ON tab1.student = tab2.student AND tab1.parent != tab2.student
LEFT JOIN 
(
	SELECT 
		s.id AS student_id,
		COUNT(p.id) AS parent_cnt
	FROM 
		student s
		LEFT JOIN parent_to_student ps ON s.id = ps.student_id
		LEFT JOIN parent p ON p.id = ps.parent_id	
	GROUP BY s.id
) tab3 
ON tab3.student_id = tab1.id = tab2.id;

18. **Write a method in JS/TS that gets as an argument an array of numbers and returns the sum of all array members**. *=> 5 points*
function sumArr (arr: number[]): number {
	if (arr.length === 0) {
		return 0;
	}
	else {
		return arr.reduce((finalSum, elem) => finalSum + elem, 0);
	}
}


19. **Explain the following piece of code:** *=> 5 points*

		public static padLeft(input: number, places: number): string {
			const zeroes: number = places - input.toString().length + 1;
			return Array(+(zeroes > 0 && zeroes)).join("0") + input.toString();
		}



20. **Fix the following code and fill the required gaps in it by the coding standards. The purpose of this code is to verify the user is a member of a specific role and in case the user is the user data is returned by the isUserPermitted() method. Treat the comments as actual code written that should not be changed:** *=> 15 points*

		interface user {
			id: number;
			firstName: string;
			lastName: string;
		}
		
		interface dbUser {
			id: number;
			first_name: string;
			last_name: string;
		}
		
		interface role {
			id: number;
			userIds: number[];
		}
		
		interface dbRole {
			id: number;
			user_id: number;
		}
		
		public isUserPermitted(userId: number, roleId: number): Promise<user> {
			return new Promise<user>((resolve, reject) => {
				Promise.all([
					this.getUser(userId),
					this.getRole(roleId)
				])
				.then((results: [user | role]) => {
					if (results[1].userIds.indexOf(results[0].id) > -1)
					{
						resolve(results[0]);
					}
					else {
						resolve([]);
					}
				})
				.catch((errorStr: string) => {
					reject(errorStr);
				});
			});
		}
		
		private getUser(userId: number): Promise<user> {
			return new Promise<user>((resolve, reject) => {
				// Access to the DB that returns the user data by id as dbUser or null
				const user: dbUser | undefined = fun(userId, ...);
				if (user === undefined) {
					const errorStr: string = 'User from DB didn't find';
					reject(errorStr);
				}
				else {
					resolve(parseDbUser(user));
				}
			});
		}
		
		private getRole(roleId: number): Promise<role> {
			return new Promise<user>((resolve, reject) => {
				// Access to the DB that returns the role data by id as array of dbRole or null
				const dbRoles: dbRole[] | undefined = fun(roleId, ...);
				if (dbRoles === undefined) {
					const errorStr: string = 'Role from DB didn't find';
					reject(errorStr);
				}
				else {
					reslove(parseDbRole(dbRoles));
				}
			});
		}

		private parseDbUser(dbUser: dbUser): user {
			return {
				id: dbUser.id,
				firstName: dbUser.first_name,
				lastName: dbUser.last_name
			};
		}

		private parseDbRoles(dbRoles: dbRole[]): role {
			let roleToReturn: role;
			roleToReturn.id = dbRoles[0].id;
			roleToReturn.userIds = [];
			dbRoles.forEach((elem: dbRole) => {
				roleToReturn.userIds.push(elem.user_id);
			})
			return roleToReturn;
		}


## Part III: Practice on dev machine *=> 33 points*

*No restrictions on online resources usage*

 - Clone the repository: https://github.com/lentyaishe/masa-exam;
 - Switch to `broken-server` branch;
 - Create a new git repository under your personal Github called `masa-exam`;
 - Load the `main` branch of your new repository with the contents of the `broken-server` branch;
 - Each bug in the list should be solved in designated branch.

The following is the list of currently existing problems with the system. :

21. **The server solution cannot be compiled. Fix all compilation issues accordingly.** *=> 10 points*

22. **An attempt to get a list of board types fails.** *=> 5 points*

23. **Any request to the server returns: "A token is required for authentication" even in case the token is supplied for the request.** *=> 5 points*

24. **Addition of the new user cannot be performed. Returned error message: "Incorrect query".** *=> 5 points*

25. **On an attempt to add a new board type an error: "not found" is returned.** *=> 8 points*

# Good luck!!
