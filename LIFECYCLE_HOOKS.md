# Lifecycle Hooks
> A lifecycle hook for a service provider is a method that is automatically called by an application at a specific stage 
> of its life cycle, allowing the provider to perform work at the appropriate time. Lifecycle hooks help ensure that 
> initialization logic occurs in the correct order, preventing situations where code attempts to use services before they
> are available and allowing applications to maintain a predictable and organized startup sequence.
>
> There are two separate lifecycle hooks that are available on the container instance:
> - `beforeResolving()` - executes _before_ a dependency has been resolved
> - `afterResolving()` - executes _after_ a dependency has been resolved

> When using lifecycle hooks in a service provider we will call them using the available container instance, from within 
> the service providers' `boot()` method.
```php
use App\Services\Message as MessageService;

public register function(): void
{
    $this->bind(MessageService::class, fn() => new MessageService());
}

public function boot(): void
{
    $this->beforeResolving(MessageService::class, fn() => 'Do Something ...')
    
    $this->afterResolving(MessageService::class, fn() => 'Do Something Else ...')
}
```

___
- **See Also: [Service Providers](https://github.com/FrameworkFactoryPHP/docs/blob/main/PROVIDERS.md)**
- **See Also: [Context API](https://github.com/FrameworkFactoryPHP/docs/blob/main/CONTEXT_API.md)**