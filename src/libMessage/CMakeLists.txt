protobuf_generate_cpp(PROTO_SRC PROTO_HEADER ZilliqaMessage.proto)

add_library (Message ${PROTO_HEADER} ${PROTO_SRC} Messenger.cpp MessengerAccountStoreBase.cpp MessengerAccountStoreTrie.cpp)
#target_compile_options(Message PRIVATE "-Wno-unused-variable")
#target_compile_options(Message PRIVATE "-Wno-unused-parameter")
get_target_property(MESSAGE_COMPILE_FLAGS Message COMPILE_OPTIONS )
message(STATUS "Message compile flags old = ${MESSAGE_COMPILE_FLAGS}")
list(REMOVE_ITEM MESSAGE_COMPILE_FLAGS -Wextra -Werror)
message(STATUS "Message compile flags new = ${MESSAGE_COMPILE_FLAGS}")
set_target_properties(Message PROPERTIES COMPILE_OPTIONS "${MESSAGE_COMPILE_FLAGS}")
target_include_directories (Message PUBLIC ${PROJECT_SOURCE_DIR}/src ${CMAKE_BINARY_DIR}/src)
target_link_libraries (Message PUBLIC protobuf AccountData Block BlockHeader MiningData Utils CoinbaseData)

add_library (MessageSWInfo ${PROTO_HEADER} ${PROTO_SRC} MessengerSWInfo.cpp)
#target_compile_options(MessageSWInfo PRIVATE "-Wno-unused-variable")
#target_compile_options(MessageSWInfo PRIVATE "-Wno-unused-parameter")
get_target_property(MESSAGESWINFO_COMPILE_FLAGS MessageSWInfo COMPILE_OPTIONS )
message(STATUS "MessageSWInfo compile flags old = ${MESSAGESWINFO_COMPILE_FLAGS}")
list(REMOVE_ITEM MESSAGESWINFO_COMPILE_FLAGS -Wextra -Werror)
message(STATUS "MessageSWInfo compile flags new = ${MESSAGESWINFO_COMPILE_FLAGS}")
set_target_properties(MessageSWInfo PROPERTIES COMPILE_OPTIONS "${MESSAGESWINFO_COMPILE_FLAGS}")
target_include_directories (MessageSWInfo PUBLIC ${PROJECT_SOURCE_DIR}/src ${CMAKE_BINARY_DIR}/src)
target_link_libraries (MessageSWInfo PUBLIC protobuf Utils)
