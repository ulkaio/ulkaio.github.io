# Retry

```csharp
    static void Main(string[] args)
    {
        // Retry 3 times
        var simpleRetry = Policy.Handle<Exception>().Retry(3);
        simpleRetry.Execute(Compute);

        // Retry with exponential backoff
        var exponentialBackoff = Policy.Handle<Exception>()
            .WaitAndRetry(3, retryAttempt => TimeSpan.FromSeconds(Math.Pow(2, retryAttempt)));
        exponentialBackoff.Execute(Compute);
    }

    private static void Compute()
    {
        throw new NotImplementedException();
    }
```