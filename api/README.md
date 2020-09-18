# API

## JSON format

JSON fields should be snake_case.

## Documentation

General guidelines, though not applicable in every case should be:

- Request/Response model naming should follow: _[Subject][SubjectAction][Request|Response]_; I.E. **SessionListRequest, SessionListResponse, PasswordChangeRequest, PasswordResetResponse**...  
Ideally this should add consistency to names, a benefit of grouping common Subjects and their Actions thus providing discoverability and readability boost. 
