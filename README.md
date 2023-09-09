# isec6000-assignment1-task1
Saleor Platform
About
What is Saleor Platform?
Saleor Platform is the easiest way to start local development with all the major Saleor services:

Core GraphQL API
Dashboard
Mailpit (Test email interface)
Jaeger (APM)
The necessary databases, cache, etc.
Keep in mind this repository is for local development only and is not meant to be deployed in any production environment! If you're not a developer and just want to try out Saleor you can check our live demo.

Requirements
Docker
How to clone the repository?
To clone the repository, run the following command

git clone https://github.com/saleor/saleor-platform.git
How to run it?
We are using shared folders to enable live code reloading. Without this, Docker Compose will not start:

Windows/MacOS: Add the cloned saleor-platform directory to Docker shared directories (Preferences -> Resources -> File sharing).
Windows/MacOS: Make sure that in Docker preferences you have dedicated at least 5 GB of memory (Preferences -> Resources -> Advanced).
Linux: No action is required, sharing is already enabled and memory for the Docker engine is not limited.
Go to the cloned directory:

cd saleor-platform
Build the application:
docker compose build
Apply Django migrations:
docker compose run --rm api python3 manage.py migrate
Populate the database with example data and create the admin user:
docker compose run --rm api python3 manage.py populatedb --createsuperuser
Note that --createsuperuser argument creates an admin account for admin@example.com with the password set to admin.

Run the application:
docker compose up
Where is the application running?
Saleor Core (API) - http://localhost:8000
Saleor Dashboard - http://localhost:9000
Jaeger UI (APM) - http://localhost:16686
Mailpit (Test email interface) - http://localhost:8025
Troubleshooting
How to solve issues with lack of available space or build errors after an update
How to run application parts?
How to update the subprojects to the newest versions?
How to solve issues with lack of available space or build errors after an update
Most of the time both issues can be solved by cleaning up space taken by old containers. After that, we build again whole platform.

Make sure docker stack is not running
docker compose stop
Remove existing volumes
Warning! Proceeding will remove also your database container! If you need existing data, please remove only services that cause problems! https://docs.docker.com/compose/reference/rm/

docker compose rm
Build fresh containers
docker compose build
Now you can run a fresh environment using commands from How to run it? section. Done!
Still no available space
If you are getting issues with lack of available space, consider pruning your docker cache:

Warning! This will remove:

all stopped containers
all networks not used by at least one container
all dangling images
all dangling build cache
More info: https://docs.docker.com/engine/reference/commandline/system_prune/

I've been warned
Issues with migrations after changing the versions - resetting the database
Please submit an issue ticket if you spot issues with database migrations during the version update.

When testing developer releases or making local changes, you might end up in a state where you would like to reset the database completely. Since its state is persisted in the mounted volume, you'll need to use a dedicated command.

Warning! This command will remove all data already stored in the database.

I've been warned
How to run application parts?
docker compose up api worker for backend services only
docker compose up for backend and frontend services
Feedback
If you have any questions or feedback, do not hesitate to contact us via GitHub Discussions.

License
Disclaimer: Everything you see here is open and free to use as long as you comply with the license. There are no hidden charges. We promise to do our best to fix bugs and improve the code.

