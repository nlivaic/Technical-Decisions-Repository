## Repositories

* Use as part of commands.
* Use `DbContext`directly from queries.
* Do integration testing with either InMemory or SqlLite providers, as these are fast, but a different behaviour is possible from the database your solution is running against. Another, more involved option is a [dedicated Dockerized instance](https://github.com/pdevito3/OncoLimsLite/blob/6cebcda69cc4e5df8d7cbbc29882d63b88232c00/Ordering/tests/Ordering.IntegrationTests/TestFixture.cs) of your database.
