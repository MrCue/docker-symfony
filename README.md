### How to use
Open a terminal window

##### First run
`cp .env.dist .env`

Change any settings

`docker-compose up -d --build`

##### Subsequent runs
`docker-compose start`

##### HTTPS
To use HTTPS you need to generate the certificates with certbot, you will need a publicly accessible IP\
Find and replace `${DOMAIN_NAME}` and `${EMAIL_ADDRESS}` with your actual values.\

If this is the first run, use:\
`docker-compose exec certbot certbot certonly --webroot --webroot-path=/var/www/symfony/public --email ${EMAIL_ADDRESS} --agree-tos --no-eff-email -d ${DOMAIN_NAME}`

Subsequent runs can use:\
`docker-compose exec certbot certbot renew`


### How to use
Remove any files and folders from the symfony directory before installing a new symfony version.