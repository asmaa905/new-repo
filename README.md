<p align="center"><a href="https://laravel.com" target="_blank"><img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="400"></a></p>

<p align="center"><a href="https://vuejs.org" rel="nofollow"><img width="100" src="https://camo.githubusercontent.com/0b17e5a01574a2c1251b51c910c422f6ca6cb968a52686a770b668a634792c09/68747470733a2f2f7675656a732e6f72672f696d616765732f6c6f676f2e706e67" alt="Vue logo" data-canonical-src="https://vuejs.org/images/logo.png" style="max-width:100%;"></a></p>

<br/>

## Get Started

### Local Server (Xampp/Wampp/..)
- run `cd <YOUR LOCAL SERVER ROOT DIRECTORY>`
    - xampp : `C:\xampp\htdocs`
    - wamp  : `C:\wamp64\www`
    - .. and so on
- run `git clone https://github.com/Mina4lfy/RGB rgbksa/RGB`
- run `cd rgbksa/RGB`
- Create an empty database for our application
- download your starting db from <a href="https://drive.google.com/file/d/1veFtOWudelQ8J3VmB8jOPDuXVUBJgzPF/view?usp=sharing">here</a> and import it using <a href="http://localhost/phpmyadmin">phpmyadmin</a>
- run `composer install` (for production, use `--no-dev`) `preferred to run using bash`
    - This command creates your `/vendor` directory
- run `npm install` (for production, use `--prod`)
    - This command creates your `/node_modules` directory
- run `xcopy .env.example .env`
- <span id="configure-dotenv">Configure `.env` file with your new settings</span>
    - Modify your database connection creds:
        ```
        DB_CONNECTION=mysql
        DB_HOST=127.0.0.1
        DB_PORT=3306
        DB_DATABASE=afaqstore
        DB_USERNAME=root
        DB_PASSWORD=
        ```
    - Modify mail credentials with yours in:
        ```
        MAIL_MAILER=smtp
        MAIL_HOST=smtp.mailtrap.io
        MAIL_PORT=2525
        MAIL_USERNAME=null
        MAIL_PASSWORD=null
        MAIL_ENCRYPTION=null
        ```
    - Login to your <a href="https://dashboard.pusher.com/accounts/sign_in">Pusher account</a>, then create a project & add your credentails here :
        ```
        BROADCAST_DRIVER=log
        ...
        PUSHER_APP_ID=
        PUSHER_APP_KEY=
        PUSHER_APP_SECRET=
        PUSHER_APP_CLUSTER=tls
        ```
- run `php artisan key:generate`
- run `php artisan jwt:secret`
- run `php artisan storage:link`
- run `php artisan build`
    - to start with already filled in data, you can append `afaqstore` to this command
    - in case of missing images, download <a href="https://drive.google.com/file/d/1jJjibXhJf8YvPgeOJEkddfFuK4n1uztc/view?usp=sharing">this file</a> and extract it to your `c:/xampp/htdocs/rgbksa/RGB/storage/app/public`


### Docker
- Similarly to local servers, <a href="#configure-dotenv">configure your dotenv.</a> You may also need to change your ports:
    ```
    DOCKER_APPSERVER_PORT="80"
    DOCKER_DATABASE_PORT="3306"
    DOCKER_DBADMIN_PORT="88"
    DOCKER_REDIS_PORT="6379"
    ```
- Simply run: `./scripts/docker-restart.sh`. It accepts one of the following options:
    - `--volumes` ~ removes the persistent volumes. Watch out! You will be about to lose all your database and cached data.
    - `--hard` ~ removes all existing docker images of the app, volumes, networks, and do a fresh installation.
- You will be inside the `app` container. When first used, you need to install the app using: `./scripts/install.sh`. It can accept the following options:
    - `--prod` ~ runs the app as in production. (`composer install --no-dev` | `npm run prod`)

<br/>
<br/>

## Git Workflow

### <a href="https://github.com/Mina4lfy/RGB/branches">Branches</a>

<b>Flow:</b> merge `YOUR-BRANCH` into `dev`, then `dev` into `testing`, then `testing` into `master`.
<br/><b>Kindly note that DIRECTLY PUSHING TO MASTER BRANCH IS NOT ALLOWED UNDER ANY CIRCUMSTANCES</b>.

- By merging your branch into `dev`, developers working on the same feature/fix should review the changes or add their own contributions.
- By merging `dev` into `testing` branch, testing team should review the added feature / applied fix and confirm that all added stuff works exactly the same as required. Otherwise, bugs are reported and send again to the dev team for repairs. This step is repeated until everything just meets the requirements.
- By merging into `master`, this means that tested features/fixes are all fine and ready for a new release.

### <a href="https://github.com/Mina4lfy/RGB/branches">How to start your fix/feature</a>

- First, create a new branch from `master`. It 's preferable to have it under a directory that categorizes it. (as in `features/login-form-ui`)
- Continue working on your separate branch until your feature/fix is ready-to-go.
- When done, merge your branch into `dev` to be reviewed by other developers.
- When reviewed, check the availability of the testing team to test newly added features/fixes to check if there is any technical or logical issue. This may prevent conflicts that may occur when committing too many features/fixes at a time to the testers, making it difficult to know which feature caused a problem.
- When available, merge `dev` into `testing` and wait for the testing team to make sure that everything works fine.
- In case that issues exist, the dev cycle is repeated again until all issues are fixed.
- Voila! go ahead and merge `testing` into `master` and generate a new release.
