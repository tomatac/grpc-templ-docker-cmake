message(STATUS "*")
message(STATUS "*** src/CMakeList.txt ***")

find_package(Protobuf REQUIRED)
find_package(gRPC REQUIRED)

set(hw_proto_srcs "${CMAKE_CURRENT_BINARY_DIR}/../protos/helloworld.pb.cc")
set(hw_grpc_srcs "${CMAKE_CURRENT_BINARY_DIR}/../protos/helloworld.grpc.pb.cc")

set(_PROTOBUF_LIBPROTOBUF protobuf::libprotobuf)
set(_REFLECTION gRPC::grpc++_reflection)
set(_GRPC_GRPCPP gRPC::grpc++)

# Include generated *.pb.h files
include_directories("${CMAKE_CURRENT_BINARY_DIR}/../protos")

set_source_files_properties(${hw_proto_srcs} PROPERTIES GENERATED TRUE)
set_source_files_properties(${hw_grpc_srcs} PROPERTIES GENERATED TRUE)

add_executable (greeter_client greeter_client.cc ${hw_proto_srcs} ${hw_grpc_srcs})
target_link_libraries (greeter_client PUBLIC ${_REFLECTION} ${_GRPC_GRPCPP} ${_PROTOBUF_LIBPROTOBUF})


add_executable (greeter_server greeter_server.cc ${hw_proto_srcs} ${hw_grpc_srcs})
target_link_libraries (greeter_server PUBLIC ${_REFLECTION} ${_GRPC_GRPCPP} ${_PROTOBUF_LIBPROTOBUF})

add_dependencies(greeter_server my_custom_target)

