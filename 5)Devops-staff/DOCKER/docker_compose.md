# The Docker Compose

**Docker Compose** используется для одновременного управления несколькими контейнерами, входящими
в состав приложения. Этот инструмент предлагает те же возможности, что и Docker, но позволяет
работать с более сложными приложениями.

[![](../../images/85948940715022ca196b8ad6f1e810d0.png)](../../images/85948940715022ca196b8ad6f1e810d0.png)

### File commands:
  - **SET THE IMAGE:**  
    ```yaml
      version: "2.4"
    
      services:
        webhost: # name of the container
          image: nginx:alpine # docker image
    ```
  - **SET THE PORTS:**  
    ```yaml
      version: "2.4"
  
      services:
        webhost:
          image: nginx:alpine
          ports:
            - 80:80
    ```   
  - **SET THE VOLUMES:**  
      ```yaml
        version: "2.4"

        services:
          webhost:
            image: nginx:alpine
            ports:
              - 80:80
            volumes:
              - <local directory>:<container directory> # bind
              - <container directory> # volume
      ```   
  - **SET THE CONTAINER NAME:**  
     ```yaml
        version: "2.4"

        services:
          webhost:
            image: nginx:alpine
            container_name: webhost # set the container name
            ports:
              - 80:80
            volumes:
              - ./html:/usr/share/nginx/html
     ```   
  - **SET THE RESTART CONFIG:**  
    ```yaml
      version: "2.4"

      services:
        webhost:
          image: nginx:alpine
          container_name: webhost
          ports:
            - 80:80
          restart: always # no / on-failure[:max-retries] / unless-stopped
          volumes:
            - ./html:/usr/share/nginx/html
    ```   
  - **SET THE ENV VARIABLES:**  
    Set own env vars in each container;
    ```yaml
      version: "2.4"

      services:
        webhost:
          image: nginx:alpine
          container_name: webhost
          ports:
            - 80:80
          restart: always
          environment:
            - MODE=dev 
          volumes:
            - ./html:/usr/share/nginx/html
    ``` 
  - **SET THE COMMAND:**  
    Overrides the default command declared by the container image (i.e. by Dockerfile’s CMD);
    ```yaml
      version: "2.4"

      services:
        db:
          image: mongo:4
          container_name: storage
          command: mongod --auth
          ports:
            - 27017:27017
          volumes:
            - ./data:/data/db
          
          # CMD ['mongod']
    ``` 
  - **HEALTHCHECK:**
    ```yaml
    version: "2.4"

    services:
      webhost:
        image: nginx:alpine
        container_name: webhost
        ports:
          - 80:80
        healthcheck:
          test: "curl http://localhost/"
          interval: 10s
          timeout: 5s
          retries: 3
        volumes:
          - ./html:/usr/share/nginx/html
    ```
  - **DEPENDS ON:**  
    First service will wait till the service that it depends on wil run or its condition;  
    **Conditions:**  
      - **service_started:** is an equivalent of the short syntax described above
      - **service_healthy:** specifies that a dependency is expected to be "healthy"
        (as indicated by healthcheck) before starting a dependent service.
      - **service_completed_successfully:** specifies that a dependency is expected to run
        to successful completion before starting a dependent service.
    ```yaml
    version: "2.4"

    services:
      webhost:
        image: nginx:alpine
        container_name: webhost
        ports:
          - 80:80
        depends_on:
          db:
            condition: service_started
            #condition: service_healthy
        volumes:
          - ./html:/usr/share/nginx/html
      db:
        image: mongo:4
        container_name: storage
    ```
  - **USE 2 SERVICES IN THE CONTAINER:**  
    ```yaml
        version: "2.4"

        services:
          webhost:
            image: nginx:alpine
            container_name: webhost
            ports:
              - 80:80
            depends_on:
              - db
            volumes:
              - ./html:/usr/share/nginx/html
        
          db:
            image: mongo:4
            container_name: storage
            volumes:
              - ./data:/data/db
     ```
  - **SET THE NETWORKS:**
    ```yaml
        version: "2.4"

        services:
          webhost:
            image: nginx:alpine
            container_name: webhost
            ports:
              - 80:80
            depends_on:
              - db
            volumes:
              - ./html:/usr/share/nginx/html
            networks: # container access to network
              - back
          
          db:
            image: mongo:4
            container_name: storage
            volumes:
              - ./data:/data/db
            networks: # container access to network
              - db
        
        networks: # networks
          back:
            driver: bridge
          db:
            driver: bridge
     ```
  - **SET THE LINKS:**  
    Aliases for the network (IP) name of the service;
    ```yaml
      links:
        - <server IP name>:<server port name>
    
      #Example:    
      version: "2.4"

      services:
        webapp:
          image: nginx:alpine
          container_name: webapp
          build: ./webapp # path to the dockerfile
          ports:
            - 80:80
          links:
            - webapp
          volumes:
            - ./html:/usr/share/nginx/html
          networks:
            - back
        
        webhost:
          image: nginx:alpine
          container_name: webhost
          build: ./webhost # path to the dockerfile
          links:
            - webhost
          ports:
            - 8080:80
          volumes:
            - ./html:/usr/share/nginx/html
          networks:
            - back
      
      networks:
        back:
          driver: bridge
    ```
  - **SET THE DOCKER FILE PATH:**  
    For big projects cna be useful separate configs in different dockerfiles;
    ```yaml
        version: "2.4"

        services:
          webapp:
            image: nginx:alpine
            container_name: webapp
            build: ./webapp # path to the dockerfile
            ports:
              - 80:80
            volumes:
              - ./html:/usr/share/nginx/html
            networks:
              - back
          
          webhost:
            image: nginx:alpine
            container_name: webhost
            build: ./webhost # path to the dockerfile
            ports:
              - 8080:80
            volumes:
              - ./html:/usr/share/nginx/html
            networks:
              - back
        
        networks:
          back:
            driver: bridge
     ```
### Console commands:
https://docs.docker.com/engine/reference/commandline/compose/
