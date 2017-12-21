# spring-cloud-config-server
spring cloud server app , which uses the git backed configuration properties and make it available to the clients .

This appication starts @ tomcat 8888 port 

Use the Below Endpoints to query the properties 

http://localhost:8888/s1rates/qa
http://localhost:8888/s1rates/dev
http://localhost:8888/s1rates/default

Adding spring security to block the unAuthorized request querying the App

	<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-security</artifactId>
		</dependency>
    
After Adding above dependency , if you try quering the endpoints for properties you would get below response

{
    "timestamp": 1513881191780,
    "status": 401,
    "error": "Unauthorized",
    "message": "Full authentication is required to access this resource",
    "path": "/s1rates/qa"
}

To fix the above issue pass the Authorization header in the request 

curl -H "Authorization: Basic d29ya0Bob21lOndvcmtAaG9tZQ==" http://localhost:8888/s1rates/qa

d29ya0Bob21lOndvcmtAaG9tZQ== : This is Base 64 encoded of value being passed in via security.user.name : security.user.password
