# Setting up a Dev Container for Go

## Intro

Hi, in this tutorial you will learn how to set up a project in Go with a VS Code Dev Container and Git.

* **Primary author:** [Jake Deng](https://github.com/jakethellama)
* **Reviewer:** [Michael Pearce-Ros](https://github.com/miketravels)

## Prerequisites

Make sure you have:

1. **A Github account:** Sign up at [GitHub](https://github.com/).
2. **Git installed:** Install [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).
3. **Visual Studio Code:** Download and install [VS Code](https://code.visualstudio.com/).
4. **Docker installed:** Download and install [Docker](https://www.docker.com/products/docker-desktop).

## Part 1: Setting up the Repository

### Step 1. Create a Directory and Initialize Git

a) Open a terminal or command prompt window.

b) Create a new directory for the project. If you didn't change directories this will be created in your home directory by default:

```bash
mkdir hello-423-go
cd hello-423-go
``` 

c) Initialize a new Git repository:

```bash
git init
```

d) Create a README.md file:

```bash
echo "# Hello 423 in Go" > README.md
git add .
git commit -m "Initial commit with README"
```

### Step 2. Create a Repository on GitHub

a) Go to the [Create a New Repository](https://github.com/new) page on GitHub.

b) Fill in these 3 fields:

1. **Repository name:** `hello-423-go`
2. **Description:** Basic Go project with Dev Containers.
3. Select **Public**

c) Click **Create Repository**.

### Step 3. Link your Local Repository to GitHub

a) Add the GitHub repository as a remote:

```bash
git remote add origin https://github.com/<username>/hello-423-go.git
```

Replace `<username>` with your GitHub username.

b) Use `git branch` to see your local branch name. If it is not `main`, use `git branch -M main` to rename it.

c) Push to the GitHub repository:

```
git push --set-upstream origin main
```

## Part 2: Setting up the Dev Container

### Step 1. Add Dev Container Configuration

a) In VS Code, make sure you have the **Dev Containers** extension by Microsoft.

b) Open the `hello-423-go` directory. You can do this with: File > Open Folder.

c) Create a `.devcontainer` directory and create a `devcontainer.json` file within it.

Paste the following into `devcontainer.json`:

```json hl_lines="2 3 6"
{
    "name": "Hello 423 in Go",
    "image": "mcr.microsoft.com/devcontainers/go",
    "customizations": {
        "vscode": {
            "extensions": ["golang.go"]
        }
    }
}
```

The `devcontainer.json` file allows you to specifically configure your development environment. Here, we are specifying the following:

* **`name`:** The name for your dev container.
* **`image`:** The Docker image to use, in our case it is a base image maintained by [Microsoft](https://hub.docker.com/r/microsoft/devcontainers).
* **`customizations`:** Adds customizations to VS Code, in our case the Go extension will be installed.

### Step 2. Reopen the Project in a Dev Container

a) Open the VS Code Command Palette and use `Dev Containers: Reopen in Container`.

b) In the container's terminal, check the version of Go that it is using.

```bash
go version
```

## Part 3: Using Go to Say Hello

### Step 1. Create the Program Files

a) Initialize a Go module, this creates a `go.mod` file which tracks your code's dependencies:

```bash
go mod init tutorial/hello-423-go
```

b) In VS Code, create a `hello.go` file and paste the following:

```go
package main

import "fmt"

func main() {
	fmt.Println("Hello COMP423")
}
```

### Step 2. Compile and Run the Program

a) To quickly compile and run your program:

```bash
go run hello.go
```

b) Or, compile the program into an executable:

```bash
go build
```

And run the resulting executable:

```bash
./hello-423-go
```

!!! note "Comparisons to C"
    Using `go build` is similar to using `gcc hello.c -o hello` as it compiles the program to create an executable that is not immediately ran, unlike `go run`.

Congrats, you now have a basic Go project setup in a Dev Container. Be sure to commit and push your changes to your public repository.

## References

* [RD06 Tutorial](https://comp423-25s.github.io/resources/MkDocs/tutorial/)
* [Go Docs](https://go.dev/doc/tutorial/getting-started)
