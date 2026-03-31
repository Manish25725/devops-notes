🐳 Docker + httpd (Apache) Notes
🔹 What is httpd?
httpd = Apache HTTP Server
It is a web server used to serve:
HTML files
CSS / JS
Static websites
Runs on port 80 (default)

👉 Simple:

httpd is software that takes a request from browser and returns a webpage.

🔹 What is Docker httpd Image?
Official image: httpd
Available on Docker Hub
Used to quickly run Apache server inside a container

👉 No need to install Apache manually on system

🔹 Basic Docker httpd Command
Run httpd container
docker run -d -p 8080:80 httpd
Explanation:
-d → run in background (detached mode)
-p 8080:80 → map:
host port: 8080
container port: 80
httpd → image name

👉 Access in browser:

http://localhost:8080
🔹 Serving Your Own Website
Step 1: Create HTML file
<h1>Hello from Docker</h1>
Step 2: Run container with volume
docker run -d -p 8080:80 \
-v $(pwd):/usr/local/apache2/htdocs/ \
httpd
Explanation:
-v → mount volume
$(pwd) → current directory
/usr/local/apache2/htdocs/ → Apache's default web folder

👉 Now your HTML file is served

🔹 Important Folder in httpd Container
/usr/local/apache2/htdocs/

👉 This is where:

All website files are stored
Apache serves content from here
🔹 Check Running Container
docker ps
🔹 Stop Container
docker stop <container_id>
🔹 Remove Container
docker rm <container_id>
🔹 Logs
docker logs <container_id>

👉 Useful for debugging server issues

🔹 Custom Configuration (Advanced)
Copy config file
docker cp httpd.conf <container_id>:/usr/local/apache2/conf/

👉 You can:

Change port
Enable modules
Modify server behavior
🔹 Dockerfile for httpd
FROM httpd:latest
COPY . /usr/local/apache2/htdocs/
Build Image
docker build -t my-httpd .
Run
docker run -d -p 8080:80 my-httpd
🔹 Interview Explanation (Simple)

👉 If interviewer asks:

"How do you use httpd in Docker?"

Answer:

I use the official httpd Docker image to quickly run an Apache web server.
I map port 80 of the container to a local port and mount my project folder to /usr/local/apache2/htdocs so Apache serves my files directly.
This avoids installing Apache locally and ensures consistency across environments.

🔹 Real-Life Use Case
Hosting static websites
Testing frontend builds (React, Angular)
Serving landing pages
Quick local server for development
🔹 Key Points to Remember
httpd = Apache web server
Default port = 80
Docker makes setup instant
Use volumes to serve custom files
Lightweight and fast for static content
🔹 Common Mistakes

❌ Forgetting port mapping
❌ Wrong folder mount
❌ Editing files but not refreshing container
❌ Using wrong path instead of /htdocs