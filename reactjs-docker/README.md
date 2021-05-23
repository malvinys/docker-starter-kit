**How to run**
- Open this project directory
- Run in terminal `docker build -t reactjs-docker .`
- Run in terminal `docker run -d --name reactjs-docker -p 8080:80 reactjs-docker`
- Open `http://localhost:8080`
<br>

**Stacks in this project**
- Docker
- Reactjs using `npx create-react-app project-name`
- Node using image docker `node:14-alpine`
- Nginx using image docker `nginx:alpine`
<br>

**Core Docker Files**
- .dockerignore `Defines the files/folders which should be ignored and not be copied into our Docker image when building it`
- Dockerfile `Defines the commands which are sequentially run to generate a new Docker image.`
<br>

**Explanation from** <a href="https://github.com/malvinys/docker-starter-kit/blob/master/reactjs-docker/Dockerfile" target="_blank">Dockerfile</a>
<br>
```
For the Dockerfile the first part (line 1–19) is pretty straightforward.
- Copy the definitions, including the dependencies, to the build stage
- Install all of the production dependencies (no need for dev dependencies here)
- Copy the sources
- Create the production build

The reason why we first copy and install our dependencies instead of copying them together with all of the other sources
is also already a build optimization. Because when the package.json and yarn.lock doesn’t change
and thus neither your dependencies Docker can take these steps from the cache and won’t have to fetch
and install all the node_modules again if you only changed something in your source code.
Which speeds up your docker builds by a lot.

Coming back to the Dockerfile line 22–34:
- Use nginx:alpine as the base image.
- Set the current working directory to the folder that NGINX uses to serve the files /usr/share/nginx/html.
- Remove all of the already existing assets from NGINX.
- Copy the production-ready build from the previous build stage to the current working directory.
- Start nginx with daemon off so the Docker container doesn’t stop after the command finishes. See StackOverflow

Now that our configuration part is done let's build and run our Docker image!
```
<br>

**Explanation from step** `docker build -t reactjs-docker .`
<br>
```
That commands searches for a Dockerfile in the current directory and use it to build a new Docker image.
The -t parameter is being used to define a name and an optional tag in the “name:tag” format.

You might have multiple Dockerfile‘s for different purposes or if you want to test different configurations
you can always use the --file PATH/TO/FILE parameter on thedocker build command
to specify the path to the Dockerfile you want to use.
```
<br>

**Explanation from step** `docker run -d --name reactjs-docker -p 8080:80 reactjs-docker`
<br>
```
- -d
  Tells Docker to run your container in “detached”-mode so it won’t need your terminal open but is running in the background
- --name
  Name for the container as reactjs-docker
- -p
  Provides a port mapping. Here Docker is being told that we want to map our port 8080 to the internal port 80.
  80 is the default HTTP port where NGINX is serving our React App.
- reactjs-docker
  The image name that was defined via docker build
```
<br>

**You can see full documentation from this awesome articel:**
<br>
https://levelup.gitconnected.com/easy-optimization-of-your-react-docker-image-down-to-22mb-9d9e3a06870