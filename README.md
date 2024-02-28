# optee-template-app


&middot; This repo serves as a template for creating applications to run within the 
Open Portable Trusted Execution Environment. OP-TEE is an open-source Trusted Execution
Environment (TEE) implementation, that provides a secure environment for running
trusted applications. </br>
</br> &middot; Here, you can find application ***"my_example"***, based on 
[optee_examples_hello_world](https://github.com/linaro-swg/optee_examples/tree/master/hello_world). </br>
</br> &middot; If you're looking to build a template application within your own Yocto environment,
consider referring to the [optee-examples-yocto](https://github.com/l-krstic/optee-examples-yocto)
repository. It provides comprehensive instructions tailored specifically for integrating OP-TEE 
applications into Yocto-based Linux distribution. You can use **generate-app-structure.sh**
script from the mentioned repo, that generates optee template application, based on this repo.

# Necessary changes in the optee application done by the [script](https://github.com/l-krstic/optee-examples-yocto/blob/main/generate-app-structure.sh)
## Host section changes

1. **host/Makefile** — Change *BINARY* value(example: *custom_app*)
2. **host/main.c**   — Change the name of the header file included(example *custom_app_ta.h*)
3. **host/main.c**   — Change the value of the *UUID* variable to *CUSTOM_APP_UUID*
4. **host/main.c**   — In the *TEE_InvokeCommand()* function, change the macro responsible for differentiating callbacks from trusted zone to desired(for example *TA_HELLO_WORLD_CMD_INC_VALUE* &rarr; *CUSTOM_APP_CMD1*)

## Trusted section changes

1. **ta/Android.mk** — Replace the value of the *local_module* with UUID generated from [terminal command](https://man7.org/linux/man-pages/man1/uuidgen.1.html) 
2. **ta/user_ta_header_defines.h** — Change the include file to *custom_app_ta.h*
3. **ta/user_ta_header_defines.h** — Change the value of *TA_UUID* macro to *CUSTOM_APP_UUID*
4. **ta/user_ta_header_defines.h** — Change every occurence of *hello_world* to *custom_app* in the *TA_CURRENT_TA_EXT_PROPERTIES* macro
5. **ta/sub.mk** — Replace the file in the *srcs-y* variable to *custom_app_ta.c*
6. **ta/Makefile** — Paste generated *UUID* into the in the value of the *BINARY* variable
7. **ta/custom_app_ta.c** — Rename the file *hello_world_ta.c* to *custom_app_ta.c*; also change the name of the include file to *custom_app_ta.h*
8. **ta/custom_app_ta.c** — In *TA_InvokeCommandEntryPoint()* function, change switch-case macros regarding your own application
9. **ta/include/custom_app_ta.h** — Rename the *hello_world_ta.h* to *custom_app_ta.h* and inside that file, change name and value of *TA_KE_HELLO_WORLD_UUID* macro to *CUSTOM_APP_UUID* and previously generated *UUID*
10. **ta/include/custom_app_ta.h** — Change *HELLO_WORLD_\** macros names and values regarding your own application

## Hgh-level build helper changes

1. **CMakeLists.txt** — Change the name of the CMake project to *custom_app*
2. **Android.mk** — Change the value of the *LOCAL_MODULE* variable to *custom_app*


# IMPORTANT
&middot; **NEVER deploy an optee_os binary with [default](https://github.com/OP-TEE/optee_os/tree/master/keys) key 
in production. Instead, REPLACE key as soon as possible with a public key and keep the private part of 
the key offline, preferably on an HSM.**
