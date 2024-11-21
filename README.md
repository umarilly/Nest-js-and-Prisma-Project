
# Nest.js & Prisma Project

Nest.js & Prisma Project is a simple CRUD application built using Nest.js and Prisma, designed for practice. It leverages a MySQL Docker image for database management, making it easy to set up and run in a containerized environment. The app provides basic Create, Read, Update, and Delete operations for managing entities, demonstrating the integration of Prisma as an ORM with Nest.js for seamless database interactions.

## Install the Nest.js CLI and Prerequisites:
- Install Node.js first. If you have already installed Node.js, then enter `node --version` and `npm --version` to verify their installation.
- Then run the following command: `npm install -g @nestjs/cli`
- Verify the Nest.js CLI: `nest -v` or `nest --version`
- Create a new project: `nest new <project-name>` (e.g., `nest new my-project`)
- Use the package manager: `npm`, `yarn`, or `pnpm` - I am choosing npm for now. (If you want to use yarn or pnpm, then install them first.)
- Switch to the project directory: `cd <directory-name>`
- To run the server, enter `npm run start` - (There are different startup scripts, and you can also set them from the package.json file.)

## Setup Prisma
- Enter `npm install prisma --save-dev` to install Prisma.
- Then enter `npx prisma init` or `npx prisma init --datasource-provider <database-name>`.
- For instance, `npx prisma init --datasource-provider <SQLite or PostgreSQL or MySQL>`.
- After this, a prisma folder and a .env file will be created.
- The prisma folder will contain a migrations folder and schema.prisma, and the .env file will contain the Database URL.
- Open the schema.prisma inside the prisma folder and start writing your model.
- After writing the model, just save the file and close it.

## Database Source Provider
- Choose the database, e.g., MySQL, PostgreSQL, or any other.
- I am choosing MySQL for now; the process is quite similar for all other databases.
- Then, go to the .env file and create the following:
  - MYSQL_DATABASE=""
  - MYSQL_ROOT_PASSWORD=""
- Name your database and also create a password for your database.

## Dockerization
- Install Docker Desktop, or you can use any other method if you have a different OS.
- Create a docker-compose.yaml file in the root of your project directory and write the service for MySQL.
- After creating it, go to the root of the project, open the terminal, and run `docker-compose up`.

## Database URL Changes
- Change the database URL in .env.
- It looks like the following:
```bash
DATABASE_URL="mysql://root:password@127.0.0.1:3306/nest_prisma_project"
```
- Also, change the database provider in the prisma.schema file if your provider is not PostgreSQL.
- Then, you can write the schema of your tables inside the schema.prisma file.
- Then enter `npx prisma migrate dev --name init` to generate the schema and create the first migration, i.e., `init`.
- To push and deploy the schema, use `npx prisma migrate push` and `npx prisma migrate deploy`.

## Implementation
- Here, I am writing the implementation of my project.

### Creating Modules, Service, and Resource
- Also known as database service, I have named it database service.
- Create a new database module:
  - `nest g module database` - This will create a new database module file in the database directory within the src folder.
  - This will also update the `app.module.ts` to add the `database.module.ts` to it.
- Create a new database service:
  - Enter `nest g service database`
  - This will create `database.service.spec.ts` and `database.service.ts` and update the `database.module.ts` to add the service.
- Now create a resource - a resource basically creates a module, service, and controller file in one go.
- Enter `nest g resource products`
- This will create a complete CRUD structure (products directory: module, service, and controller).
- Change these according to your requirements.

### Working with Relations
- Create different models according to your requirements. I am creating description, reviews, and tag models.
- For 1-to-1, 1-to-many, and many-to-many relations with the products model respectively.
- Migrate the database using `npx prisma migrate dev --name relations`.
- This will create a new migration with the name `relations`.

## Running the Application
- To start the application, run `npm run start`
- The application will be available at `http://localhost:3000`.
- Use tools like Postman or Insomnia to test the API endpoints.

## Testing
- Nest.js provides a robust testing framework.
- Create unit tests for your services and controllers using Jest.
- Run tests using `npm run test`.

## Conclusion
- This project demonstrates a basic CRUD application using Nest.js and Prisma.
- It covers setting up the environment, creating modules and services, and working with database relations.
- For more advanced features, refer to the official documentation of Nest.js and Prisma.