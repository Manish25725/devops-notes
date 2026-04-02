ocker Image & Dockerfile Notes
🔹 1. What is a Docker Image?
A Docker Image is a blueprint/template to create containers.
It contains:
Application code
Dependencies
Runtime (Node, Python, etc.)
OS libraries

👉 Example:

Image = Recipe 🍔
Container = Cooked burger
🔹 2. What is a Dockerfile?
A Dockerfile is a text file with instructions to build an image.

👉 Think:

“Step-by-step instructions to build my app environment”

🔹 3. Basic Dockerfile Structure

Example (Node.js app):

# 1. Base Image
FROM node:18

# 2. Set working directory
WORKDIR /app

# 3. Copy package files
COPY package*.json ./

# 4. Install dependencies
RUN npm install

# 5. Copy rest of code
COPY . .

# 6. Expose port
EXPOSE 3000

# 7. Start app
CMD ["npm", "start"]
🔹 4. Important Dockerfile Instructions
1. FROM
Defines base image
FROM node:18
2. WORKDIR
Sets working directory inside container
WORKDIR /app
3. COPY
Copies files from local → container
COPY . .
4. RUN
Runs commands during build time
RUN npm install
5. CMD
Default command when container starts
CMD ["node", "server.js"]
6. EXPOSE
Defines port (just documentation)
EXPOSE 3000
🔹 5. How to Build Docker Image

Run this command:

docker build -t my-app .
Explanation:
-t my-app → image name
. → current directory (Dockerfile location)
🔹 6. How to Run Container from Image
docker run -p 3000:3000 my-app
Explanation:
-p 3000:3000 → map local port to container port