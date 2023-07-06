1.- Run de application on the host

    - Install the node dependencies
         
         node i

    - Run the application 

        ng serve

2. Create the dockerfile and build the application

    - Use the lastest node stable base image
    - Set the working directory /src
    - Copy the package.json file to the image
    - Run the npm install command
    - Copy the rest of the file to the /src folder from the host
        - Add the docker ignore file, make sure the node_folder is included
         

    docker build -t sergioacortes/sampleangularapp .



