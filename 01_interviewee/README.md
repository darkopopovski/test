## Summary

- Given this PR, I assume that this is a CalendarScheduler application that uses Google Calendar API. Nice to know that this feature is implemented but there are several things we might need to look into before merging.

## Summary

- Given this PR, I assume that this is a CalendarScheduler application that uses Google Calendar API. Nice to know that this feature is implemented but there are several things we might need to look into before merging.

## Review
### Must-Fix
- God Class - Bad approach in basic OOP Principles. Single class handles all the functions of the scheduler which is bad approach. Separating it into smaller classes will improve the overall structure.
- Hardcoded Values - URLS, ApiKeys or similar should be replaced with Environment Variable, it will increase our security and make it more production ready.
- No Logs - Cannot track errors when making requests with third party systems in production level.
- No Exceptions - Not handling exceptions may crash the application.
- Sync Calls - Try using async calls to avoid thread blocking and improve the overall performance of the application.
- No Request Handling - When making a POST request its always nice to validate the request first before making any requests further, also handles exceptions in case some fields are missing.
- No Dependency Injection - Having a global client of HttpClient can cause bad output of tests and be used by other functions / requests (bad practice), same goes for Api.cs be aware of making a scheduler without Dependency injection
may cause the same thing as the HttpClient

### Inline-Comments
```
CalendarScheduler.cs:13 -> Dependency injection needed
this way we may have problems with testing and overall behaviour of the client

CalendarScheduler.cs:14 -> Hardcoded Secret should be moved in Environment variable.
its bad to have it this way, for security reasons and for production.

CalendarScheduler.cs:10 -> Should be separted in smaller classes
this way we have bad approach of overall OOP structure.

CalendarScheduler.cs:46 -> Handle and log status after request is made
this way we may encounter application crash no track of errors in production

CalendarScheduler.cs:55 -> Async calls should be used to ignore thread blocking
this way we have thread blocking

CalendarScheduler.cs:57 -> Check for status code after request is made
this way we handle nothing may get application crash

CalendarScheduler.cs:64 -> Return response body from the actual request
this way we dont handle exceptions nor return response body

Api.cs:12 -> Make validations before making request to ensure everything is handled
this way we errors when creating request.
```

### Tests
- Suggested tests should be added:
- Google Api Integration Test -> This will handle integration after request is made.
- Logs / Exceptions Test -> This will make sure that our application doesnt crash.
- Input validation Test - > This will handle that object is validated before making a schedule.
