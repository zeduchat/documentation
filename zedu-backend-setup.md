**Zedu Telex Backend Local Setup Guide  - this guide explains how to clone, install, configure, and run the Zedu Telex backend locally, the backend is a Go application and uses Docker Compose to run its development dependencies such as PostgreSQL, Redis, RabbitMQ, MongoDB, Elasticsearch, MinIO, and Centrifugo** 

Repository:
Zedu Telex Backend — https://github.com/zeduchat/zedu-be

**1. What You Need**
Before starting, you need:
Git
Go
Docker
Docker Compose
Make
VS Code (recommended)
Internet connection
Enough disk space for Docker images
The backend repository currently requires:
Go 1.24.0
Go toolchain 1.24.7

The development Docker setup requires:
Docker = 24
Docker Compose = 2


**2. Clone the Backend**
Open a terminal. This guide assumes the project is located in your Documents folder.
Go to the directory containing the frontend:
cd ~/Documents/Zedu

Clone the backend:
git clone https://github.com/zeduapp/telex_be.git

Enter the backend:
cd telex_be

Confirm the location:
pwd


Check the repository:
git status

**3. Check the Required Go Version**
Run:
head -20 go.mod

The repository currently specifies:
go 1.24.0
toolchain go1.24.7

Therefore, Go 1.24.7 is a good local version to use.
**4. Install Go 1.24.7**
If Go is not installed, first check:
go version

install Go 1.24.7.
For an x86_64 computer, check your architecture:
uname -m

Expected:
x86_64

Download Go:
cd /tmp
wget https://go.dev/dl/go1.24.7.linux-amd64.tar.gz

Remove an existing /usr/local/go installation if necessary:
sudo rm -rf /usr/local/go

Install Go:
sudo tar -C /usr/local -xzf go1.24.7.linux-amd64.tar.gz

Add Go to PATH:
echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.bashrc

Reload the shell:
source ~/.bashrc

Verify:
go version

Expected:
go version go1.24.7 linux/amd64

Also check:
go env GOPATH

**5. Install Docker**
The backend's development environment is designed to use Docker Compose.
Check whether Docker is installed:
docker --version

If Docker is not installed:
sudo apt update

Then:
sudo apt install -y docker.io docker-compose-v2

Start Docker:
sudo systemctl enable --now docker

Check Docker:
sudo systemctl status docker --no-pager

You want:
Active: active (running)

**6. Allow Your User to Run Docker**
Add your Linux user to the Docker group:
sudo usermod -aG docker $USER

Apply the group change:
newgrp docker

Test:
docker ps

**7. Verify Docker**
Run:
docker --version

Example:
Docker version 29.1.3

Check Docker Compose:
docker compose version

Example:
Docker Compose version 2.40.3

Check running containers:
docker ps

If no containers are running, an empty table is normal:
CONTAINER ID   IMAGE   COMMAND   CREATED   STATUS   PORTS   NAMES

**8. Install/Check Make**
Check Make:
make --version

Example:
GNU Make 4.3

Make is useful because the repository provides commands such as:
make start-dev
make dev-clean

**9. Check the Docker Compose Configuration**
Open:
cd ~/Documents/Zedu/telex_be
nano docker-compose.dev.yml

Or simply inspect it:
cat docker-compose.dev.yml

You can also list the services:
grep -E '^  [a-zA-Z0-9_-]+:' docker-compose.dev.yml

You should see services similar to:
postgres
redis
elasticsearch
rabbitmq
mongodb
mongo-express
minio
centrifugo
backend

**10. Correct the Docker Compose Database Script**
If your Compose file contains:
./scripts/init-database-local.sql:/docker-entrypoint-initdb.d/init-databases.sql

change it to:
./scripts/init-databases.sql:/docker-entrypoint-initdb.d/init-databases.sql

During our setup, the correct PostgreSQL mount was already present around line 16:
./scripts/init-databases.sql:/docker-entrypoint-initdb.d/init-databases.sql

There was another incorrect reference later in the backend service.
The duplicate/incorrect backend mount should be removed.
The backend volumes should therefore look like:
volumes:
  - .:/app

while PostgreSQL handles the initialization script.
**11. Verify the Database Script**
Run:
grep -n "init-database" docker-compose.dev.yml

Ideally, you should only have the valid PostgreSQL initialization reference:
./scripts/init-databases.sql:/docker-entrypoint-initdb.d/init-databases.sql

**12. Validate Docker Compose Before Starting**
Before starting the entire backend:
docker compose -f docker-compose.dev.yml config

If the command completes without an error and returns to your terminal prompt, the Compose YAML is valid.
This is a useful habit:
Edit configuration
       ↓
docker compose ... config
       ↓
Start services

rather than immediately starting a broken configuration.
**13. Check Available Disk Space**
Because the development environment contains several Docker services, check disk space:
df -h

**14. Start the Backend**
Once Docker Compose has been validated, run:
cd ~/Documents/Zedu/telex_be
docker compose -f docker-compose.dev.yml up --build

This command:
Builds the Go backend image.
Downloads required Docker images.
Starts PostgreSQL.
Starts Redis.
Starts RabbitMQ.
Starts Elasticsearch.
Starts MongoDB.
Starts Mongo Express.
Starts MinIO.
Starts Centrifugo.
Starts the Go backend.
**15 Leave the Backend Terminal Running**
When the backend is running, leave that terminal open.
You will see logs from multiple services.
For example:
postgres
redis
rabbitmq
mongodb
minio
centrifugo
telex-backend

Do not close the terminal while developing unless you intentionally stop the stack.
**16. Start the Backend Using Make**
The repository's Makefile contains:
start-dev:
    docker compose -f docker-compose.dev.yml up --build

Therefore, once the environment is correctly configured, you can also use:
make start-dev

However, inspect the Makefile first.
The current Makefile begins with:
include app.env
export

If your repository does not contain app.env, make start-dev may have an environment-file issue.
For this reason, the direct Docker Compose command is the safer first startup command:
docker compose -f docker-compose.dev.yml up --build

**17. Completely Clean the Development Environment**
The repository provides:
make dev-clean

which executes:
docker compose -f docker-compose.dev.yml down -v

You can also run it directly:
docker compose -f docker-compose.dev.yml down -v

Warning
The -v option removes Docker volumes.
That means local database data can be deleted.
Do not use:
docker compose ... down -v

**18. Backend Port**
The Go backend is configured to use:
8019

Therefore the API should be available at:
http://localhost:8019

The Compose file maps:
8019:8019

**19. Test the Backend**
Once the backend is running, test its API.
A useful health/status endpoint for this project is:
curl -i http://localhost:8019/api/v1/api-status

A successful response should start with something similar to:
HTTP/1.1 200 OK

If you receive a 200 response, the backend API is responding.
**20. Running Frontend and Backend Together**
Use two terminals.
Terminal 1 — Backend
cd ~/Documents/Zedu/telex_be
docker compose -f docker-compose.dev.yml up --build

Terminal 2 — Frontend
cd ~/Documents/Zedu/telex_fe

Then start the frontend using the command defined by its package.json.
For example:
pnpm dev

or:
npm run dev

**21. Frontend → Backend Communication**
The frontend should communicate with:
http://localhost:8019

The frontend should not connect directly to PostgreSQL, MongoDB, Redis, etc.
22 Check Frontend Environment Variables
Go to the frontend:
cd ~/Documents/Zedu/telex_fe

Look for environment files:
find . -maxdepth 2 -type f \( -name ".env*" -o -name "*env*" \) -print

Search for API configuration:
grep -R "API_URL\|API_BASE\|BASE_URL\|NEXT_PUBLIC\|VITE_" . \
  --exclude-dir=node_modules \
  --exclude-dir=.git \
  --exclude-dir=.next

**23. OneSignal Frontend Error**
During frontend testing, an error appeared:
[OneSignal] Failed to initialize
You need to provide your OneSignal appId.

This is a frontend configuration issue, not proof that the Go backend is broken.
The frontend was running at:
http://localhost:3001

The error originated from:
src/components/layout/onesignal/onesignal-provider.tsx

To investigate:
cd ~/Documents/Zedu/telex_fe

Run:
grep -R "OneSignal\|ONESIGNAL" src \
  --exclude-dir=node_modules \
  --exclude-dir=.next


**24. Checking Running Docker Containers**
Open another terminal and run:
docker ps

You should eventually see containers for services such as:
telex-backend
postgres
redis
rabbitmq_telex
mongodb_telex
minio_telex
centrifugo

You can see all containers, including stopped ones:
docker ps -a

**25. Checking Backend Logs**
The backend container is called:
telex-backend

You can inspect logs with:
docker logs telex-backend

For live logs:
docker logs -f telex-backend

Press:
Ctrl + C

to stop following the logs.

**26. Database Migrations**
The repository contains migrations under:
db/migrations/

The Makefile contains commands such as:
make migrate-up

make migrate-down

make migrate-version

make migrate-force version=<version>

make fix-dirty

make migrate-safe-up

However, the Makefile currently includes:
include app.env

Therefore, before using these Make commands, verify that the expected app.env exists and contains the required DB_URL.
Do not run migration commands blindly against the wrong database.

Once everything has been configured successfully, your normal workflow becomes simple.
Terminal 1 — Backend
cd ~/Documents/Zedu/telex_be
docker compose -f docker-compose.dev.yml up

Terminal 2 — Frontend
cd ~/Documents/Zedu/telex_fe
pnpm dev

Use the package manager specified by the frontend repository.
Then open the frontend:
http://localhost:3001

The frontend communicates with:
http://localhost:8019


**27. The Complete Setup in Short**
For an experienced developer who already has the prerequisites installed:
cd ~/Documents/Zedu

git clone https://github.com/zeduapp/telex_be.git

cd telex_be

go version

docker --version

docker compose version

docker ps

docker compose -f docker-compose.dev.yml config

docker compose -f docker-compose.dev.yml up --build

Then, in another terminal:
cd ~/Documents/Zedu/telex_fe

Start the frontend using its configured development command.
Test the backend:
curl -i http://localhost:8019/api/v1/api-status



**Final Setup Checklist**
Use this checklist when setting up the backend on a new Ubuntu machine.
Clone telex_be
Confirm backend location
Install Go 1.24.7
Run go version
Install Docker
Install Docker Compose
Add user to Docker group
Confirm docker ps works without sudo
Confirm Make is installed
Inspect app-sample.env
Inspect docker-compose.dev.yml
Check scripts/init-databases.sql
Fix any incorrect init-database-local.sql reference
Run docker compose ... config
Check available disk space
Start Docker Compose
Wait for PostgreSQL and other dependencies
Check docker ps
Check telex-backend logs if necessary
Test http://localhost:8019/api/v1/api-status
Start the frontend
Configure frontend API URL
Configure local frontend origin/CORS if required
Configure OneSignal if required
Test login
Test API calls
Test messaging/realtime functionality
Test file uploads
Test other application features

