# Services

> A service is typically a PHP class or a collection of PHP classes that you would call from within your
> application. Below, we will create a class that outputs a message, for simplicity. We are going to 
> assume that there is an `App` namespace that has been registered within the PSR-4 section of the 
> `composer.json` file in the root of the project.

```php
namespace App\Services\Message;

class Message
{
    /**
     * Displays a message to the end-user
     * 
     * @param string $message the message to display
     *                       
     * @return string
     */
    public function display(string $message): string
    {
        return $message;
    }
}
```

> As you can see, there is nothing special about this PHP class. Its sole job is to display a message. Services can
> be as simple or as complex as the developer would like; sometimes combining many classes together to form a
> comprehensive library that can later be injected into the application. For this example, we kept it basic for
> the sake of not being too verbose.

___
- **See Also: [Service Providers](https://github.com/FrameworkFactoryPHP/docs/blob/main/PROVIDERS.md)**
- **See Also: [Accessors](https://github.com/FrameworkFactoryPHP/docs/blob/main/ACCESSORS.md)**