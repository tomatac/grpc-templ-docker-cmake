grpc-templ-docker-cmake
=======================

## A gRPC C++ Template Project using VS Code, Building in a Docker Container Development Environment with modern CMake
----------------------------------------------------------

This project can be used as a template to build gRPC applications within a Docker container using VS Code

It is using modern CMake to build the 2 sample applications: greeter_server and greeter_client. 

There is nothing special about the C++ gRPC application. It is a copy of an example provided by Google. 

The interesting aspects of the project are:
- **Docker container development environment for gRPC**:
    - creates an easy reproducible environment to share a project the code with other developers or move to a new machine
    - keep the main operating system clean
    - easy to test with different library versions or operating systems
    - See the [Dockerfile](https://github.com/tomatac/grpc-templ-docker-cmake/blob/main/.devcontainer/Dockerfile) in the current repository
- **VS Code integration with Docker** 
    - It speeds up the development within the Docker containers
    - See the [devcontainer.json](https://github.com/tomatac/grpc-templ-docker-cmake/blob/main/.devcontainer/devcontainer.json) in the current repository
    - For more informations see [Working with containers guide and extension](https://code.visualstudio.com/docs/containers/overview) on Microsoft website
- **Using modern CMake** to build the project and automatically generate the proto files. 
    - The CMakeLists.txt files are spread within each subfolder of the project making it easy to follow and work with large projects.

To find more about gRPC and for a complete set of instructions about the gRPC application see Hello World app in the [C++ Quick Start](https://grpc.io/docs/languages/cpp/quickstart).

 

