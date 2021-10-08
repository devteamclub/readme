# Code style

#### Logging errors
Use `log` instead of `fmt` for logging errors
```go
// ----------- bad
fmt.Print("Error text")

// ----------- good
log.Print("Error text")
```
<br>

#### Environment variables
Inform team members when new environment variables are added
```go
// example
@Egor @Igor @Vitalik @Kirill, new environment variable `API_KEY` was added
```
<br>
