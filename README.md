## Sonarqube scanning Java Application using Pipeline

### Requirements
  - EC2 instance(AMZ linux)
  - install docker & docker compose
  - java 17 install
  - jenkins install
  - plugins - Maven
            - maven Integration Plugin
            - Sonarqube scanner
  - Credentials of sonarqube set in jenkins
    
## Steps
1. run docker compose file
2. log in sonarqube and create project,create token 
3. Install Plugins
   Manage jenkins > plugins - 
            - maven Integration Plugin
            - Sonarqube scanner
4. Store sonarqube credentials in jenkins
   manage jenkins > system - sonarqube 
            - environment variable
            - name
            - server url
            - server auth token - paste here token

5. create a pipline
6. check sonarqube dashboard


## Docker compose file for sonarqube installation
```
version: "3"
services:
  sonarqube:
    image: sonarqube:community
    restart: unless-stopped
    depends_on:
db
    environment:
      SONAR_JDBC_URL: jdbc:postgresql://db:5432/sonar
      SONAR_JDBC_USERNAME: sonar
      SONAR_JDBC_PASSWORD: sonar
    volumes:
sonarqube_data:/opt/sonarqube/data
sonarqube_extensions:/opt/sonarqube/extensions
sonarqube_logs:/opt/sonarqube/logs
    ports:
"9000:9000"
  db:
    image: postgres:12
    restart: unless-stopped
    environment:
      POSTGRES_USER: sonar
      POSTGRES_PASSWORD: sonar
    volumes:
postgresql:/var/lib/postgresql
postgresql_data:/var/lib/postgresql/data
volumes:
  sonarqube_data:
  sonarqube_extensions:
  sonarqube_logs:
  postgresql:
  postgresql_data:
```

