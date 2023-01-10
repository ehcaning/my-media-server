# My Media Server Setup

## Deployment Instructions:

1. Create a VM and attach a volume (preferably name it `arr`) to it with at least 50GB under the `mnt/arr` directory.

2. Create a user name `arr`:

    ```sh
    sudo useradd -m arr
    ```

3. Get the `uid` and `gid` of the new user:

    ```sh
    su arr
    id
    uid=1000(arr) gid=1000(arr) groups=1000(arr)
    ```

    Insert these `uid` and `gid` into `docker-compose.yml` file for each service's environment: `PUID`, `PGID`

4. Run the whole stack, make sure to do it with `arr` user.

    ```sh
    docker-compose up -d
    ```

    If the `arr` user don't have permission to do so, add this user to `docker` group

5. Now we should adjust the ownership of files in case it is not right:

    ```sh
    cd /mnt/arr
    chown -R arr:arr *

    cd /home/arr
    chown -R arr:arr *
    ```

6. Now we want to have sub-domains pointing to all our services, create sub-domains and point them all to the IP of this server. And then edit the `nginx.conf` file and replace `server_name` for each service with the created sub-domain for your services. Now run the nginx service:

    ```sh
    docker-compose -f nginx.docker-compose.yml up -d
    ```

Now the whole thing is up and running. Let's setup everything else from the UI.

## Configs:

### Sonar & Radarr:

TODO

### Jackett:

TODO

### Transmission:

TODO

### jellyfin:

TODO
