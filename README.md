# yii2-dev-env
An easy mod for Yii2 basic application to switch between development and production environments 
when using Composer to install the project.

Add this extension to the `require-dev` section of your project's composer.json file.

Edit the project's `index.php` file as follows:

Remove these lines
    // comment out the following two lines when deployed to production
    defined('YII_DEBUG') or define('YII_DEBUG', true);
    defined('YII_ENV') or define('YII_ENV', 'dev');

Add these lines in their place
    // If the package is installed via composer with --no-dev then yii2-dev-env will not be included
    // If the development packages are included then including dev-env.php will set the YII_DEBUG and
    // YII_ENV constants to their development/debug values, otherwise they default to production values
    $dev_env = __DIR__ . '/../vendor/garya/yii2-dev-env/dev-env.php';
    if(file_exists($dev_env))
    {
        include $dev_env;
    }

Now, when you use Composer to install the project with the `--no-dev` option the `dev-env.php` file 
will not be installed and the environment will be set as production. When the development 
dependencies are included the environment will be set to development with debug enabled.