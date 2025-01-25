# Setting up a dev container for Go

* Primary author: [Rishyendra Medamanuri](https://github.com/rishyendra333)
* Reviewer: [Rachit Bajpai](https://github.com/rbajpai-unc)

## Introduction to Go
Go (often referred to as Golang) is a programming language developed by Google engineers Robert Griesemer, Rob Pike, and Ken Thompson. It was born out of frustration with existing languages being used at Google in 2007, and was officially announced in 2009. The language was designed to address the challenges of large-scale software development at Google.

Key Features of Go:

- It's concurrency allows you to run multiple tasks simultaneously, making it 
- Simple, efficient, and easy to learn
- Automatic garbage collection manages the memory for you

-[Geeks for Geeks](https://www.geeksforgeeks.org/go-programming-language-introduction/)

!!! Legend
    "Legend has it that Go was made while the three founders were waiting for their code to compile."
    -[Reddit](https://www.reddit.com/r/golang/comments/176b5pn/what_problem_did_go_actually_solve_for_google/)

## Prerequisites

- Visual Studio Code installed
- Docker Desktop installed and running
- Git installed and configured
- GitHub account setup

## Creating a New Go Project

### Step 1: Create and Initialize Project Directory

You want to first make a directory (folder) to encompass all your code for this tutorial.
```bash
# Create a new directory for your project
mkdir go-tutorial-comp423
cd go-tutorial-comp423
```

To allow Git actions on your repository, you want to initialize a new Git repository in this folder.
```bash
# Initialize git repository
git init
```

Now, you want to make a README file.
```bash
# Create a simple README
echo "# Hello COMP423 Go Project" > README.md
git add README.md
git commit -m "initializing README"
```

!!! note "Why README?"
    The README.md file is included in almost all GitHub projects to introduce the contents of the repository to the visitors. Obviously, communicating through raw code would be difficult, so the README.md file allows the author(s) of the repo to communicate with their audience.

### Step 2: Set Up Dev Container Configuration

!!! warning "Docker Check"
    Ensure Docker Desktop is running before continuing on. If Docker isn't running, you'll receive an error when trying to open the dev container.

Create a new `.devcontainer` directory and to add the configuration file:
```bash
mkdir .devcontainer
```

Now, open your `go-comp423` file in Visual Studio Code. Then, create a new file called `devcontainer.json` inside of the `.devcontainer` folder.

Add the following configurations to the `devcontainer.json` file.
```json
{
    "name": "Go Hello COMP 423 Tutorial",
    "image": "mcr.microsoft.com/devcontainers/go:latest",
    "customizations": {
      "vscode": {
        "settings": {},
        "extensions": ["golang.go"]
      }
    }
  }
```

### Step 3: Verify Go Installation

Now, let's verify whether we have Go installed in our dev container. To do this, reopen the repository in the dev container  by doing the following:  
Open the Command Palette with `Ctrl + Shift + P` if on Windows or `Cmd + Shift + P` on windows  
Then, type "Dev Containers: Reopen in Container"  

!!! note
    This may take a while to run the first time while your device is making necessary downloads.

Navigate to your terminal and type:
```bash
go version
```

!!! tip "Version Check"
    You should see a recent version of Go installed. This confirms your dev container is set up correctly.

### Step 4: Initialize Go Module

Initialize your Go module, which is required for modern Go projects:

```bash
# Initialize a new module
go mod init go-tutorial-comp423
```

!!! note "Module Name"
    The module name should match your project name.

### Step 5: Create Your First Go Program

Create a new file called `main.go` in your `go-tutorial-comp423` directory. Next, add the following Go program:

```go
package main

import "fmt"

func main() {
    fmt.Println("Hello COMP423")
}
```

### Step 6: Build and Run

!!! tip "Build vs Run"
    Let's explore both ways to run your Go program.

```bash
# Method 1: Quick run without creating an executable
go run main.go
```

The `go run` command compiles and executes your program immediately, similar to if you used both `gcc` and `./a.out` in one step. This is convenient during development when you're making frequent changes and want to test them quickly.

```bash
# Method 2: Build an executable called 'go-tutorial-comp423'
go build

# This line runs the executable
./go-tutorial-comp423
```

The `go build` command is more similar to `gcc`. Let's break down the comparison:

- With GCC:
    1. `gcc hello.c` would create an executable (default name: a.out)
    2. `./a.out` would run that executable

- Go Build:
    1. `go build` creates an executable (named after your module)
    2. `./go-tutorial-comp423` runs that executable

!!! info "Understanding the Difference"
    - `go run` is best for development and testing
    - `go build` is what you'll use when preparing your program for distribution

!!! note "Executable Name"
    The executable's name comes from your module name (what you specified in `go mod init`). If you used a different name, your executable will have that name instead of "go-tutorial-comp423".

### Step 7: Push to GitHub

1. Create a new repository on GitHub:
   - Go to github.com and click "New repository"
   - Name it `go-tutorial-comp423`
   - Leave it public and don't initialize it with the READMe.me file
   - Click "Create repository"

2. Link your local repository to GitHub (replace `<your-username>` with your GitHub username):

```bash
git remote add origin https://github.com/<your-username>/go-tutorial-comp423.git
git add .
git commit -m "Add Hello COMP423 program"
git push -u origin main
```