# Simple UI Information App

This is a simple Node.js application that serves a basic HTML page displaying some information on the UI. The purpose of this repository is to demonstrate a simple web application and how to dockerize it.

## Prerequisites

Before you begin, ensure you have the following installed on your machine:
- Node.js
- Docker

## Getting Started

1. Clone this repository to your local machine:

> git clone <repository_url>


2. Navigate to the project directory:

cd simpleNodeApp/


3. Build the Docker image:

docker build -t node-app .


4. Run the Docker container:

docker run -p 3000:3000 simple-ui-app



5. Access the application in your web browser at [http://localhost:3000]

## Project Structure

- `app.js`: Node.js application code.
- `Dockerfile`: Dockerfile for containerization.
- `package.json`: Project metadata and dependencies.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
