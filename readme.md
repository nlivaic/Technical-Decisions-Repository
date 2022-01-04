## Repositories

* Use as part of commands.
* Use `DbContext`directly from queries.
* Do integration testing with either InMemory or SqlLite providers, as these are fast, but a different behaviour is possible from the database your solution is running against. Another, more involved option is a [dedicated Dockerized instance](https://github.com/pdevito3/OncoLimsLite/blob/6cebcda69cc4e5df8d7cbbc29882d63b88232c00/Ordering/tests/Ordering.IntegrationTests/TestFixture.cs) of your database.

## Testing

### Domain

* Unit test domain classes thoroughly. This is the core of the system and must be covered completely.

### Controllers

* Testing thin controllers brings very little value, as all the relevant code is either in the framework itself (routing, validation, model binding, security) or in the domain services and domain models. Therefore, integration tests bring much more value.

### Command and query handlers
  
* Write unit tests only if they bring value. I am guessing the bulk of command and query handlers will be adequately covered by appropriate integration tests.

### Repositories
  
* Rely on integration tests to make sure all the complex data relationships are covered.

### How to integration test

* The in-memory `TestServer` available in the `Microsoft.AspNetCore.TestHost` package lets you create small, focused, "integration" tests for [testing custom middleware](https://docs.microsoft.com/en-us/aspnet/core/test/middleware?view=aspnetcore-3.1). These are "integration" in the sense that they're executed in the context of a "dummy" ASP.NET Core application, but are still small, fast, and focused.
* At the other end, the `WebApplicationFactory<T>` in the `Microsoft.AspNetCore.Mvc.Testing` package lets you test things in the context of your real application. You can still add [stub services for the database](https://docs.microsoft.com/en-us/ef/core/miscellaneous/testing/in-memory) (for example) if you want to keep everything completely in-memory.

#### What about external dependencies?

* When doing an integration test which involves sending a message to the Azure Service Bus then that dependency should be mocked out. Another option worth looking into might be  MassTransit and the In memory transport.
  
### End to end tests

* If additional confidence is needed then integration tests mentioned above, utilizing `WebApplicationFactory<T>`, can be supplemented by a Dockerized database instance of the same kind as used in production. This gives complete confidence the system works as it should.
