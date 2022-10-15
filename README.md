# authelia for traefik
This project offer you an empty shell to start your Authelia container and link it with traefik

You will need to change a few values in the compose file for it to work smoothly

## configuration options you should look into :

### docker-compose.yml

- the secrets file you will use
- in the service section
  - the version of the image
  - the secrets you want to actualy use, for now I'm not using redis for exemple 
  - the labels the value of :
    - traefik.http.routers.authelia.rule (the URL you chose to register for authelia)
    - traefik.http.routers.authelia.entrypoints (if you did not use my traefik docker compose files)
    - traefik.http.middlewares.authelia.forwardauth.address (at lest the end of the line it's where authelia will redirect you after you athenticate yourself)
  - the name of the nework
  - the environment variable for the secrets (if not using them all)
- in the network section the name 
- in the volume sections the volume you will need

### configuration.yml

Then the application configuration in the file : ```data/config/configuration.yml```

- the jwt secret : If you want to fill the jwt directly in the configuration file let the comment if you will use the secret file as I did
- The authelia URL you registered : should be the same as the label traefik.http.routers.authelia.rule
- The log configuration : If you want a log file ...
- The theme : For me it's always dark
- The dua api configuraiton : if you want to use it, I did not...
- The authentication backend : for me it was a file easy to maintain as I'm alone on my lab ;)
- The access control configuration : This one sohuld be changed EVERY time you add a service that should be protected by authelia !
- The session confiugation : 
  - The secret : if you want to use the file or directly put it in the configuration file
  - The timeout of your session
  - The domain
- The redis configuration if you will use it
- The regulation rules : max bad password in an amount of time in seconds before you are banned the amount of time defined
- The storage configuration : an encryption key and a  path for the sqlite database
- The notifier conifugaration : this part will be needed for the MFA activation

### user_database (optional)

If you want to use a file as your user database as you are less than 10 :
You will want to change the user(s) informations in the ```data/config/user_database.yml``` )

But you can choose another method (see technotim presentation on youtube)

### the secrets files

Now that you checked all the conifuration files, you should create your secrets in the files inside the secret folder


> Want to have your config saved and under revision control : Be carefull not to expose your filled secret files !
