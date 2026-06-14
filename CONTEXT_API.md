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

> In order to add contextual rules inside a Service Provider, we simply have to call the
> Context API from that Provider from within the `register()` method. The Context System
> provides a Fluent API with descriptive methods that are to be chained together, in order
> to create the required contextual rules.

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
        
        // now we can utilize the Context API
        $this->when(ReportService::class)
             ->needs(LoggerInterface::class)
             ->give(ReportLogger::class)
    }
}
```

___
- **See Also: [Service Providers](https://github.com/FrameworkFactoryPHP/docs/blob/main/PROVIDERS.md)**
- **See Also: [Lifecycle Hooks](https://github.com/FrameworkFactoryPHP/docs/blob/main/LIFECYCLE_HOOKS.md)**
- **See Also: [Accessors](https://github.com/FrameworkFactoryPHP/docs/blob/main/ACCESSORS.md)**