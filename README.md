# my-bsl-http-server

A low-level HTTP web server built from scratch using the **Bonezegei Scripting
Language (BSL)** and the **BSL Socket Library**. The server binds directly to a
TCP socket on port `8080`, parses raw incoming HTTP requests, and manually routes
them to the correct response, with no external web framework involved.

## 1. Project Description

This project was built for the "Building an HTTP Server using Socket" laboratory
activity. It demonstrates how an HTTP server works under the hood by handling the
socket lifecycle manually (init, create, bind, listen, accept, read, write,
close) and by constructing raw HTTP responses (status line, headers, and body)
by hand.

The server supports three routes:

| Route | Method | Response |
|---|---|---|
| `/` | GET | `200 OK` with a welcome landing page |
| `/about` | GET | `200 OK` with project and developer information |
| any other path | GET | `404 Not Found` with a custom error page |

## 2. Installation & Setup Guide

### Prerequisites

- [Visual Studio Code](https://code.visualstudio.com/)
- The **Bonezegei Scripting Language Formatter** extension (search "Bonezegei"
  in the VS Code Extensions tab)
- The BSL interpreter, installed using the instructions inside that extension:
  - **Windows / Linux:** follow the native installation instructions in the
    extension guide.
  - **macOS / Android:** use [GitHub Codespaces](https://github.com/features/codespaces)
    and follow the Linux installation steps from inside the Codespace.

The installer provides two executables. `bzg` is the package manager, and
`bonezegei` is the interpreter that runs `.bzg` scripts.

Verify the interpreter is installed:

```bash
bonezegei --version
```

### Steps

1. **Clone this repository**

```bash
   git clone https://github.com/mellow-nick/my-bsl-http-server.git
   cd my-bsl-http-server
```

2. **Install the BSL Socket Library**

```bash
   bzg install socket
```

   This downloads the socket bindings into a local `lib/` folder that
   `src/http.bzg` includes at runtime. Run it from the project root so that
   `include("lib/socket.bzg")` resolves correctly.

3. **Run the server**

```bash
   bonezegei src/http.bzg
```

   On success, the terminal prints:

```
   Socket Ready
   Server running on http://localhost:8080/
```

4. **Stop the server** with `Ctrl+C` when you are done testing.

## 3. Usage Instructions

With the server running, open a browser and visit:

- **Home page:** [http://localhost:8080/](http://localhost:8080/)
  returns the welcome page with a `200 OK` status.
- **About page:** [http://localhost:8080/about](http://localhost:8080/about)
  returns project and developer information with a `200 OK` status.
- **Any unmapped route**, for example
  [http://localhost:8080/anything](http://localhost:8080/anything),
  [http://localhost:8080/home](http://localhost:8080/home), or
  [http://localhost:8080/user](http://localhost:8080/user)
  returns a custom `404 Not Found` page.

You can also test from the terminal with `curl`. The `-i` flag prints the
response headers so the status code is visible:

```bash
curl -i http://localhost:8080/
curl -i http://localhost:8080/about
curl -i http://localhost:8080/does-not-exist
```

## 4. Project Structure

```
my-bsl-http-server/
├── .gitattributes
├── LICENSE
├── README.md
├── src/
│   └── http.bzg
└── documentation/
    ├── home.png
    ├── about.png
    ├── 404.png
    └── terminal.png
```

The `.gitattributes` file contains `*.bzg linguist-language=JavaScript`, which
tells GitHub to apply JavaScript syntax highlighting to `.bzg` source files.

## 5. Screenshots

### `/` Home Route

![Home Route](documentation/home.png)

### `/about` About Route

![About Route](documentation/about.png)

### 404 Unmapped Route

![404 Not Found](documentation/404.png)

### Terminal Output

![Terminal Running Server](documentation/terminal.png)

## License

This project is licensed under the [MIT License](LICENSE).
