## Update PgAdmin4 docker image

1. Pull the latest docker image

```
 sudo docker pull dpage/pgadmin4
```

2. Stop the running container

```
sudo docker stop pgadmin
```

3. Remove existing container

```
 sudo docker rm pgadmin
 or 
 sudo docker rm --force pgadmin
```

4. Run the latest images

```
 sudo docker run --name pgadmin -p 80:80 -v /var/lib/pgadmin:/var/lib/pgadmin  -e 'PGADMIN_DEFAULT_EMAIL=m.thirumal@hotmail.com' -e 'PGADMIN_DEFAULT_PASSWORD=thirumal' -d dpage/pgadmin4
```
or the below command for reverse proxy with ngnix
```
sudo docker run --name pgadmin -p 5050:80 -v /var/lib/pgadmin:/var/lib/pgadmin  -e 'PGADMIN_DEFAULT_EMAIL=m.thirumal@hotmail.com' -e 'PGADMIN_DEFAULT_PASSWORD=thirumal' -d dpage/pgadmin4
```

Auto start the `PgAdmin4` during the system boot

```
sudo docker run --restart always --name pgadmin -p 5050:80 -v /var/lib/pgadmin:/var/lib/pgadmin  -e 'PGADMIN_DEFAULT_EMAIL=m.thirumal@hotmail.com' -e 'PGADMIN_DEFAULT_PASSWORD=thirumal' -d dpage/pgadmin4
```

5. To start docker container

```
sudo docker start pgadmin
```
	
![Pgadmin4.png](Pgadmin4.png)
