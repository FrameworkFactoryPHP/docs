# Context API

> What is the Context API? In simplest terms, the Context API 
> allows us to replace on dependency with another, based on a  contextual circumstance. Basically, it allows a program to 
> say _When using "A", and "A" needs "B", give "C"_.
> 
> **How this translates:**
>  - If we’re resolving a dependency
>  - And we know _who_ asked for it
>  - And there’s a contextual rule for that pair
>  - Use the override instead
>
> We can see it in action by thinking of it programmtically using a context tree below:
>
> ```
> when → ReportService
>   └─ needs → LoggerInterface
>   └─ give → ReportLogger
> ```

> We can access the Context API by two methods. Either within the service Provider, or using an Accessor class. We will look
> at each example below.

## Within a Service Provider
> How do we access the Context API using a service provider? The process is quite simple. Using the example above, we 
> can add the following to a service providers `boot()` method. This ensures that the  service has been bound to the 
> container and that the container is fully built.

```php
use FrameworkFactory\Contracts\Providers\ServiceProvider;
use App\Services\ReportService;
use App\Loggers\ReportLogger;
use Psr\Log\LoggerInterface;

class ReportServiceProvider extends ServiceProvider
{
    public function register()
    {
        // first we want to bind the service to the container
        $this->bind(ReportService::class, fn() => new ReportService());
    }
    
    public function boot(): void
    {    
        // now we can utilize the Context API
        $this->when(ReportService::class)
             ->needs(LoggerInterface::class)
             ->give(ReportLogger::class)
    }
}
```

## Within an Accessor
**IN PROGRESS**

___
- **See Also: [Service Providers](https://github.com/FrameworkFactoryPHP/docs/blob/main/PROVIDERS.md)**
- **See Also: [Accessors](https://github.com/FrameworkFactoryPHP/docs/blob/main/ACCESSORS.md)**