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
    - Makes it easy to test different library versions or operating systems. Just change the Dockerfile and you can your application in a completely new environment.
    - See the [Dockerfile](https://github.com/tomatac/grpc-templ-docker-cmake/blob/main/.devcontainer/Dockerfile) in the current repository
- **VS Code integration with Docker** 
    - It speeds up the development working with the Docker containers
    - The application is compiled and ran inside the container with full step by step debugging capabilities
    - For more information see [Working with containers guide and extension](https://code.visualstudio.com/docs/containers/overview) on Microsoft website
    - See the [devcontainer.json](https://github.com/tomatac/grpc-templ-docker-cmake/blob/main/.devcontainer/devcontainer.json) in the current repository
- **Using modern CMake** to build the project and automatically generate the proto files
    - The CMakeLists.txt files are spread within each source subfolder of the project making it easy to follow them and work with large projects.
    - The [CMakeLists.txt](https://github.com/tomatac/grpc-templ-docker-cmake/blob/main/protos/CMakeLists.txt) within the proto folder is responsible of generating the proto source and header files. To use CMake to generate a custom command that executes when we run make, we use add_custom_command, but we also need to add custom targets and link them to the source files that are defined in the source files typically located in another folder.This could be quite challenging and I did not see this done in other gRPC examples. 

To find more about gRPC and for a complete set of instructions about the gRPC application see he Hello World app in the [C++ gRPC Quick Start](https://grpc.io/docs/languages/cpp/quickstart) page on [grpc.io](https://grpc.io/) website.

I found this CMake article interesting describing [CMake: dependencies between targets and files and custom commands](https://samthursfield.wordpress.com/2015/11/21/cmake-dependencies-between-targets-and-files-and-custom-commands/)

I welcome comments and improvements ideas to this project.
 

