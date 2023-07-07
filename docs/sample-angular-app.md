1.- Run de application on the host

    - Install the node dependencies
         
         node i

    - Run the application 

        ng serve

2. Create the dockerfile and build the application

    Build stage
        - Use the lastest node stable base image as build
        - Set the working directory /src
        - Copy the package.json file to the image
        - Run the npm install command
        - Copy the rest of the file to the /src folder from the host
            - Add the docker ignore file, make sure the node_folder and dist is included
    
    Final stage
        - Use the latest nginx stable base image as final
        - Copy the application bundled generated from the build stage to the nginx start folder
    
3.- Extra configuration 

    # Install all the update on the nginx base image
    # Make sure the destination folder is empty
    # Add the tzdata package and change the time zone to Madrid 
    # Add the regional configurations
    # Remove curl and git packages because vulnerabilities
    # Create group and user
         

    docker build -t sergioacortes/sampleangularapp .



