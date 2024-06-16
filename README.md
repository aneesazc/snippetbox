# SnippetBox

SnippetBox is a simple web application that allows users to create, view, and manage code snippets. It is similar to GitHub Gists but focuses on simplicity and ease of use.

## Features

- User authentication (sign up, login, logout)
- Create, view, and manage code snippets
- Secure session management
- HTTPS support with TLS configuration
- CSRF protection
- Simple and clean UI

## Getting Started

### Prerequisites

- Go 1.22 or later
- MySQL database
- Git

### Installation

1. **Clone the repository:**

   ```sh
   git clone https://github.com/aneesazc/snippetbox.git
   cd snippetbox
   ```

2. **Set up the database:**

- Ensure you have MySQL installed and running.
- Create a new database named snippetbox.
- Create a new MySQL user and grant it access to the snippetbox database.
- Update the DSN (Data Source Name or DB URL) in the main.go file with your MySQL credentials if necessary.

3. **Build and run the application:**

   ```sh
   go build -o snippetbox cmd/web/*.go
   ./snippetbox
   ```

4. **Access the application:**

- Open your web browser and navigate to https://localhost:4000.

### Configuration

You can configure the application using command-line flags:

- `addr`: The network address to listen on (default `:4000`).
- `dsn`: The MySQL data source name (default `web:wpass@/snippetbox?parseTime=true`).

Example:

```sh
./snippetbox -addr ":8080" -dsn "user:password@/snippetbox?parseTime=true"
```

## Project Structure

- `cmd/web/`: Contains the main application code.
- `internal/models/`: Contains the database models for Snippets and Users.
- `ui/`: Contains the UI assets and templates.
- `tls/`: Contains the TLS certificates (`cert.pem` and `key.pem`).

## Routes

### Public Routes

- `GET /`: Home page displaying the latest snippets.
- `GET /snippet/view/{id}`: View a specific snippet.
- `GET /user/signup`: User sign-up page.
- `POST /user/signup`: Handle user sign-up.
- `GET /user/login`: User login page.
- `POST /user/login`: Handle user login.
- `GET /ping`: Health check endpoint.

### Protected Routes (Authentication Required)

- `GET /snippet/create`: Create snippet page.
- `POST /snippet/create`: Handle snippet creation.
- `POST /user/logout`: Handle user logout.

### Static Files

- `GET /static/`: Serve static files.

## Middleware

- `sessionManager.LoadAndSave`: Load and save session data.
- `noSurf`: CSRF protection middleware.
- `app.authenticate`: Authentication middleware.
- `app.requireAuthentication`: Require authentication for protected routes.
- `app.recoverPanic`: Recover from panics and display an error page.
- `app.logRequest`: Log incoming HTTP requests.
- `commonHeaders`: Set common security headers.

## Database Models

### SnippetModel

Handles operations related to code snippets.

### UserModel

Handles operations related to users.

## Templates

The application uses HTML templates for rendering the UI. The templates are cached for performance.

## Session Management

Sessions are managed using `github.com/alexedwards/scs` with MySQL as the session store.

## CSRF Protection

CSRF protection is implemented using the `noSurf` middleware.

## Logging

The application uses structured logging with `slog`.

## Security

- HTTPS is enforced with TLS configuration.
- Secure cookies are used for session management.
