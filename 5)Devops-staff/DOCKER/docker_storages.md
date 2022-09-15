# The Docker Storages

[![](../../images/types-of-mounts-volume.png)](../../images/types-of-mounts-volume.png)

**<ins>Docker volume</ins>** — механизм для постоянного сохранения данных генерируемых и используемых
контейнером. Так как после удаления контейнера удаляются все хранимые данные в этом контейнере
данный механизм позволяет сохранять данные в память (HARD) файловой системы.

Volumes are stored in a part of the host filesystem which is managed by Docker 
(/var/lib/docker/volumes/ on Linux).

**<ins>Bind mount</ins>** — файл или директория на диске host системы. Создает связь с папкой в файловой системе
и папкой в контейнере, при изменении содержимого папки локально, данные меняются во всех контейнерах.
(добавили новый файл и все контейнеры забрали этот файл себе).

**<ins>TMPFS</ins>** — механизм для временного сохранения данных генерируемых и используемых контейнером в
оперативной памяти host системы. Так как после удаления контейнера удаляются все хранимые данные в этом контейнере
данный механизм позволяет сохранять данные в память (RAM) файловой системы.

[![](../../images/volumes-shared-storage.svg)](../../images/volumes-shared-storage.svg)

### Console commands:
- **CREATE VOLUME:**
  ```text
     docker volume create <volume name>
  ```
  - **Directives:**
    - `--name`:
      ```text
        docker volume create --name <volume name>
      ```
    - `--label`:
      ```text
        docker volume create --label <label key='label value'>
      ```
    - `--driver`:  
      Volume drivers let you store volumes on remote hosts or cloud providers, to encrypt the
      contents of volumes, or to add other functionality.
      ```text
        docker volume create --driver <storage name> <volume name>
      
        //Example:
        docker volume create --driver local storage
      ```
    - `--opt` / **can be set in starting running container**:    
      <ins>Set options:</ins>
      - `type=`:   
        The type of the mount, which can be `bind`, `volume`, or `tmpfs`.
        ```text
          //Example:
          docker volume create --driver local \
            --opt type=tmpfs \
            --opt device=tmpfs \
            --opt o=size=100m \
          storage
        
        or
        
        docker container run -d \
          --mount type=bind,source="$(pwd)"/html,target=/usr/share/nginx/html,readonly \
          --publish 80:80 \
          --name webhost nginx:alpine
        ```
      - `source=` or `src=`:  
        The source of the mount. For named volumes, this is the name of the volume. For anonymous
        volumes, this field is omitted. May be specified as source or src
        ```text
          //Example volume:
          docker run -d \
            --mount source=nginx-vol,target=/usr/share/nginx/html,readonly \
            --name nginxtest \
          nginx:latest
        
          //Example bind:
          docker container run -d \
            --mount type=bind,source="$(pwd)"/index.html,target=/usr/share/nginx/html/index.html \
            --mount type=bind,source="$(pwd)"/about.html,target=/usr/share/nginx/html/about.html \
            --publish 80:80 \
            --name webhost nginx:alpine
        ```
      - `destination=`, `dst=`, or `target=`:  
        The destination takes as its value the path where the file or directory is mounted in the
        container.
        ```text
          //Example:
          docker run -d \
            --mount source=nginx-vol,target=/usr/share/nginx/html,readonly \
            --name nginxtest \
          nginx:latest
        ```
      - `readonly` or `ro`:
        Container can only read from the storage;
        ```text
          //Example:
          docker run -d \
            --mount source=nginx-vol,destination=/usr/share/nginx/html,readonly \
            --name nginxtest \
          nginx:latest
        ```
      - `volume-opt=key=value`:    
        The volume-opt option, which can be specified more than once, takes a key-value pair
        consisting of the option name and its value.
        ```text
          
        ```  
- **MAP VOLUME TO CONTAINER DIRECTORY:**  
  Bind container's directory to the certain volume;
  - **Directives:**
    - `-v` or `--volume`:
      ```text
        docker container run -d -v <volume name / local source>:<container directory>:<options> ...
      
        // Example volume:
        docker volume create storage
      
        docker container run -d -v storage:/usr/share/nginx/html:ro -p 80:80 nginx:alpine
      
        // Example bind:
        docker run -d \                                                                                        
           -it \
           --name webhost \
           --volume "$(pwd)"/target:/app \
        nginx:alpine
      ```
    - `--mount`:
       ```text
        docker container run -d --mount source=<volume name>,target=<container directory>,<options> ...

        // Example volume:
        docker volume create storage
      
        docker container run -d --mount source=storage,target=/usr/share/nginx/html --name webhost nginx:alpine
      
        // Example bind:
        docker run -d \
          -it \
          --name webhost \
          --mount type=bind,source="$(pwd)"/target,target=/app \
        nginx:alpine
      
        // Example tmpfs:
        docker run -d \
          -it \
          --name webhost \
          --mount type=tmpfs,destination=/app,tmpfs-size=100m \
        nginx:alpine
      ```
- **VOLUME INFORMATION:**  
  Show the information about volume:
  ```text
    docker volume inspect <volume name>
  ```
- **VOLUMES INFORMATION:**
   ```text
    docker volume ls
   ```
- **REMOVE VOLUMES:**  
  Remove all unused volumes;
   ```text
      docker volume prune -f
   ```
- **REMOVE VOLUME:**
   ```text
      docker volume rm <volume name>
   ```
