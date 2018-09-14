## Building a Full Stack Polls app similar to twitter polls with Spring Boot, Spring Security, JWT, React and Ant Design

### Live Demo
 	 
The application is hosted on AWS free tier. Check out the live demo at https://polls.callicoder.com

### Tutorials

I've written a complete tutorial series for this application on The CalliCoder Blog -

+ [Part 1: Bootstrapping the Project and creating the basic domain models and repositories](https://www.callicoder.com/spring-boot-spring-security-jwt-mysql-react-app-part-1/)

+ [Part 2: Configuring Spring Security along with JWT authentication and Building Rest APIs for Login and SignUp](https://www.callicoder.com/spring-boot-spring-security-jwt-mysql-react-app-part-2/)

+ [Part 3: Building Rest APIs for creating Polls, voting for a choice in a Poll, retrieving user profile etc](https://www.callicoder.com/spring-boot-spring-security-jwt-mysql-react-app-part-3/)

+ [Part 4: Building the front-end using React and Ant Design](https://www.callicoder.com/spring-boot-spring-security-jwt-mysql-react-app-part-4/)

## Steps to Setup the Spring Boot Back end app (polling-app-server)

1. **Clone the application**

	```bash
	git clone https://github.com/callicoder/spring-security-react-ant-design-polls-app.git
	cd polling-app-server
	```

2. **Create MySQL database**

	```bash
	create database polling_app
	```

3. **Change MySQL username and password as per your MySQL installation**

	+ open `src/main/resources/application.properties` file.

	+ change `spring.datasource.username` and `spring.datasource.password` properties as per your mysql installation

4. **Run the app**

	You can run the spring boot app by typing the following command -

	```bash
	mvn spring-boot:run
	```

	The server will start on port 5000. The spring boot app includes the front end build also, so you'll be able to access the complete application on `http://localhost:5000`.

5. **Add the default Roles**
	
	The spring boot app uses role based authorization powered by spring security. Please execute the following sql queries in the database to insert the `USER` and `ADMIN` roles.

	```sql
	INSERT INTO roles(name) VALUES('ROLE_USER');
	INSERT INTO roles(name) VALUES('ROLE_ADMIN');
	```

	Any new user who signs up to the app is assigned the `ROLE_USER` by default.

## The APIs
<table style="width:100%">
    <tr>
      <th>URL</th>
      <th>Method</th>
      <th>Description</th> 
      <th>Input Example</th>
      <th>Response Example</th>
    </tr>
    <tr>
      <td>http://localhost:5000/leavemanagement/auth/signup</td>
      <td>POST</td>
      <td>create a new user</td> 
      <td>{<br>
            "name": "name", <br>
            "username": "username", <br>
            "email": "example@example.com", <br>
            "password": "password" <br>
          }
      </td>
      <td>{<br>
            "success": true, <br>
            "message": "User registered successfully"<br>
          } <br>
          or <br>
          {<br>
              "success": false,<br>
              "message": "Username is already taken!"<br>
          }
      </td>
    </tr>
    <tr>
      <td>http://localhost:5000/leavemanagement/auth/signin</td>
      <td>POST</td>
      <td>login to the website</td> 
      <td>{<br>
            "usernameOrEmail": "value", <br>
            "password": "password" <br>
          }
      </td>
      <td>{<br>
            "accessToken": "eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiIzIiwiaWF0IjoxNTM2Mzk1ODkwLCJleHAiOjE1MzcwMDA2ODl9.xhE_xpesC8Pi6mFqNTMvUy6qiqEPpbhW20-Ky7by-CC4vwj6NNM6Bb0sB17fi1hg5xBy2yHWttGDvOh9De1d9w",<br>
            "tokenType": "Bearer"<br>
          }
      </td>
    </tr>
     <tr>
      <td>http://localhost:5000/leavemanagement/user/checkUsernameAvailability?username=</td>
      <td>GET</td>
      <td>see if the username is already taken</td> 
      <td>
      </td>
      <td>{<br>
            "available": false<br>
          }
      </td>
    </tr>
    <tr>
      <td>http://localhost:5000/leavemanagement/users/{username}</td>
      <td>GET</td>
      <td>pass in the username and remove the {} s</td> 
      <td>
      </td>
      <td>{<br>
            "id": 3,<br>
            "username": "username",<br>
            "name": "name",<br>
            "joinedAt": "2018-09-08T08:28:40Z",<br>
            "active": true<br>
          }
      </td>
    </tr>
    <tr>
      <td>http://localhost:5000/leavemanagement/user/checkEmailAvailability?email=</td>
      <td>GET</td>
      <td>see if the email is already taken</td> 
      <td>
      </td>
      <td>{<br>
            "available": true<br>
          }
      </td>
    </tr>
    <tr>
      <td>http://localhost:5000/leavemanagement/users/{username}/activate</td>
      <td>PUT</td>
      <td>deactivate the user</td> 
      <td>
      </td>
      <td>
      </td>
    </tr>
    <tr>
      <td>http://localhost:5000/leavemanagement/users/{username}/deactivate</td>
      <td>PUT</td>
      <td>activate the user</td> 
      <td>
      </td>
      <td>if there is an error:<br>
        {<br>
          "timestamp": "2018-09-14T13:43:08.455+0000",<br>
          "status": 404,<br>
          "error": "Not Found",<br>
          "message": "User not found with username : '{username}'",<br>
          "path": "/leavemanagement/users/%7Busername%7D/deactivate"<br>
        }
      </td>
    </tr>
    <tr>
      <td>http://localhost:5000/leavemanagement/users/{id}/byID/activate</td>
      <td>PUT</td>
      <td></td> 
      <td>
      </td>
      <td>
      </td>
    </tr>
    <tr>
      <td>http://localhost:5000/leavemanagement/users/{id}/byID/deactivate</td>
      <td>PUT</td>
      <td></td> 
      <td>
      </td>
      <td>
      </td>
    </tr>
    <tr>
      <td>http://localhost:5000/leavemanagement/users/byID/{id}</td>
      <td>GET</td>
      <td>get user information by providing the id</td> 
      <td>
      </td>
      <td>
        {<br>
            "id": 3,<br>
            "username": "username",<br>
            "name": "name",<br>
            "joinedAt": "2018-09-08T08:28:40Z",<br>
            "active": true<br>
        }
      </td>
    </tr>
    <tr>
      <td>http://localhost:5000/leavemanagement/users/delete/{username}</td>
      <td>POST</td>
      <td>delete the user</td> 
      <td>
      </td>
      <td></td>
    </tr>
  </table>
