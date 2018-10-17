# Build image local
	```
  docker build -t jenkins-app .
  ```
  
# Run docker locally to test
  ```
  docker run -p 8080:8080/tcp jenkins-app
  ```