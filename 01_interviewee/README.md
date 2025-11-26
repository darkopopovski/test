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


2. Review the PR. Call out must-fix blockers vs follow-ups, propose a safe rollout, and list tests you'd add.
3. Create a path that would address the issues you've discovered.
