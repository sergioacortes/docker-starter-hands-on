1.- Create an ASP.NET MVC application using Visual Studio

2.- Add linux docker support to the application

3.- Using Visual Studio Code, open the project an build de docker image

    - Why it does not work?
    - Fix the paths and rebuild the docker image

        docker build -t sergioacortes/sampleaspnetmvcapp .
    
4.- Optimize the docker image

    - Pass build arguments on build process
        - Pass the BuildConfiguration build argument and update the docker image

            docker build --build-arg BuildConfiguration=Release -t sergioacortes/sampleaspnetmvcapp .

        - Pass the AspnetVersion build argument and update the docker image
        - Pass the SdkVersion build argument and update the docker image

            docker build --build-arg AspnetVersion=6.0-alpine --build-arg SdkVersion=6.0-alpine --build-arg BuildConfiguration=Release -t sergioacortes/sampleaspnetmvcapp .

    - Change the base image and use the alpine version

    - Update the image to not restore package on build step

        - Why it does fail? Add the dockerignore file

    - Update the image to not build on publish step

    - Add the HttpPort build argument and Add ASP.NET environment variables

        ARG HttpPort=8080
        ENV ASPNETCORE_ENVIRONMENT=Production
        ENV ASPNETCORE_URLS=http://+:$HttpPort

5.- Security 
    
    - Create a group and an user and assign readonly permission to the /app folder where the application is going to be executed

        RUN addgroup --gid 1000 a3software && adduser -G a3software -D -s /bin/false -u 1000 a3innuva
        RUN chown -R a3innuva:a3software /app

6.- Run the docker image