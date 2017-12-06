Roles Permissions Laravel (RPL)

A stater kit with Roles and Permissions implementation on Laravel 5.4

Install

To use it just clone the repo and composer install.
Set the database connection
To test the app run php artisan db:seed, our interactive seeder will take care of everything.
Add a new Resource

Create desired resource by running
## Create Comment model with migration and resource controller
php artisan make:model Comment -m -c --resource
Register route for it.
Route::group( ['middleware' => ['auth']], function() {
    ...
    Route::resource('comments', 'CommentController');
});
Now implement your controllers methods and use the Authorizable trait
use App\Authorizable;

class CommentController extends Controller
{
    use Authorizable;
    ...
Now add the permissions for this new Comment model.
php artisan auth:permission Comment
That's it, you have added new resource controller which have full access control by laravel permissions.

auth:permission command

This command can be user to add or remove permission for a given model

## add permission
php artisan auth:permission Comment

## remove permissions
php artisan auth:permission Comment --remove
Inspired From

QCode.in

License

MIT license.
