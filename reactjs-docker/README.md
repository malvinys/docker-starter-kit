How to run
- Open this project directory
- Run in terminal `docker build -t reactjs-docker .`
- Run in terminal `docker run -d --name reactjs-docker -p 8080:80 reactjs-docker`
- Open `http://localhost:8080`

Stacks in this project
- Docker
- Reactjs using `npx create-react-app project-name`
- Node using image docker `node:14-alpine`
- Nginx using image docker `nginx:alpine`

Core Docker Files
- .dockerignore `Defines the files/folders which should be ignored and not be copied into our Docker image when building it`
- Dockerfile `Defines the commands which are sequentially run to generate a new Docker image.`

You can see full documentation from this awesome articel:
https://levelup.gitconnected.com/easy-optimization-of-your-react-docker-image-down-to-22mb-9d9e3a06870