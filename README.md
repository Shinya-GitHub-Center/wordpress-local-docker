# [Wiki Site : Step by Step Lecture as for WP data migration between local docker and cloud servers](https://github.com/Shinya-GitHub-Center/wordpress-local-docker/wiki)

## First WordPress for you!
No time and no motivation to search for any WordPress servers, but want to play with WordPress just for basic things instantly.  
Then, this is the right place to start with.
- If you want to try to build multiple WordPress environment at the same time, please consider to use my another [repos](https://github.com/Shinya-GitHub-Center/wordpress-simulocal-docker)!

## Preparation
* Ubuntu User : docker installation beforehand
* Windows User : WSL2 and docker desktop installation beforehand

## How to setup docker containers
1. Download the source code of this docker project, unzip, and rename the root directory to your favorite project name: e.g. `my-first-wp_CTNR`
2. Rename `.env.sample` to `.env`
3. Delete the file `./wordpress/html/delete-this-file.txt` (not necessary though)
4. You can go ahead this wordpress project without modifying anything in the `.env` file, but if you want to change any values including the database's table prefix, please modify `.env` file in the first place
5. Up all containers - execute command from your project's root directory (where `docker-compose.yml` exists)
```
docker compose up -d
```
6. Open your browser in order to connect to the wordpress and do initialize
```
http://localhost
```
7. Please follow the installation procedure: e.g.
    * Language : English (USA)
    * Site Title : my-first-wp
    * Username : wp-user
    * Password : wp-user
    * Confirm Password : Check
    * Your Email : hoge-at-example.com
    * Search engine visibility : Check
    * Login as 'wp-user' for password 'wp-user'
8. Next time you login, you will be directed to the wordpress regular top page. If you need to go to the admin console panel, use this url instead
```
http://localhost/wp-admin
```

## How to connect to mysql database via phpMyAdmin
* Make sure all containers are being up, then access to the following url from your browser
```
http://localhost:8080
```

## How to uninstall this wordpress project from your local machine
* If you want to uninstall this docker project, please do not forget to remove the data volume, along with removing containers (`docker compose down`) and images (`docker rmi <repository names>`)
```
docker volume ls
docker volume rm <project-name_mysql>
```

## Others
* Wordpress container's user ID is currently set to 1000, this is for an easy access from your host machine. You may change this value to other numbers such as 2000 depending on your host machine's user ID. (But I am not sure if the IDs other than 1000 would work correctly....)
* If you want to change the default max file upload size, please add the following php parameters before `# BEGIN WordPress` sentence in the `.htaccess` file located at the wordpress's html root folder (close wordpress browser prior to doing this action)
```
php_value upload_max_filesize 512M
php_value post_max_size 512M
php_value memory_limit 512M
php_value max_execution_time 300
php_value max_input_time 300

# BEGIN WordPress
# The directives (lines) between "BEGIN WordPress" and "END WordPress" are
# dynamically generated, and should only be modified via WordPress filters.
# Any changes to the directives between these markers will be overwritten.

# END WordPress
```
