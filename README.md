grpc-templ-docker-cmake
=======================

## A gRPC C++ Template Project using VS Code, Building in a Docker Container Development Environment with modern CMake
----------------------------------------------------------

This project can be used as a template to build gRPC applications within a Docker container using VS Code

It is using modern CMake to build 2 sample applications: *greeter_server* and *greeter_client*. 

There is nothing special about the C++ gRPC application. It is a copy of a very simple example provided by Google.

The interesting aspects of the project are:
- **Docker container development environment for gRPC**
    - Creates an easy reproducible environment.
    - Makes it easy to share a project with other developers or move the development environment to a new machine
    - Keeps the main operating system clean making it easy to work with multiple projects
    - Makes it easy to test different library versions or operating systems. Just change the Dockerfile and you can run your application in a completely new environment in minutes.
    - See the [Dockerfile](https://github.com/tomatac/grpc-templ-docker-cmake/blob/main/.devcontainer/Dockerfile) in the current repository
- **VS Code integration with Docker containers** 
    - It speeds up the development working with the Docker containers
    - The application is compiled and ran inside the container with full step by step debugging capabilities
    - For more information see [Working with Containers Guide and Extension](https://code.visualstudio.com/docs/containers/overview) on Microsoft website
    - See the [devcontainer.json](https://github.com/tomatac/grpc-templ-docker-cmake/blob/main/.devcontainer/devcontainer.json) in the current repository
- **Using modern CMake** to build the project and automatically generate the proto files
    - The CMakeLists.txt files are spread out within each source subfolder of the project making it easy to follow them and work with large projects.
    - The [CMakeLists.txt](https://github.com/tomatac/grpc-templ-docker-cmake/blob/main/protos/CMakeLists.txt) within the proto folder is responsible of generating the proto source and header files. To use CMake to generate a custom command that executes when we run *make*, we use *add_custom_command*, but we also need to add custom targets and link them to the source files that are defined in the source files typically located in another folder. This could be quite challenging and I did not see this done in other gRPC examples. 

To find more about gRPC and for a complete set of instructions about the gRPC application see he Hello World app in the [C++ gRPC Quick Start](https://grpc.io/docs/languages/cpp/quickstart) page on [grpc.io](https://grpc.io/) website.

I found this CMake article interesting describing [CMake: dependencies between targets and files and custom commands](https://samthursfield.wordpress.com/2015/11/21/cmake-dependencies-between-targets-and-files-and-custom-commands/)

### Steps to build and test the project
- install [Docker](https://docs.docker.com/get-docker/)
- install [VS Code](https://code.visualstudio.com/download)
- install [Remote Development VS Code extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack)
- git clone https://github.com/tomatac/grpc-templ-docker-cmake.git
- open the project folder in VS Code
- watch the VS Code messages on the lower right hand side of the screen. Because this project include a "*.devcontainer*" folder VS code recognize it as a container based development environment. A message should pop up asking to “*Reopen folder to develop in a container*”. Select “**Reopen in Container**”
- VS Code will reopen and start to build the container based on the *Dockerfile* from *.devcontainer* folder.
- Another message should pop up on lower right hand side of the screen giving the opportunity to **Show Log** as the container is getting built
- in a terminal in VS Code
    - cd build
	- cmake ..
	- make
- open a new terminal in VS Code
	- cd build/src/
	- ./greeter_server
- open a new terminal in VS Code
	- cd build/src/
	- ./greeter_client

I welcome comments and improvements ideas to this project.
 

