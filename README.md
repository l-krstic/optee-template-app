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





# IMPORTANT
&middot; **NEVER deploy an optee_os binary with [default](https://github.com/OP-TEE/optee_os/tree/master/keys) key 
in production. Instead, REPLACE key as soon as possible with a public key and keep the private part of 
the key offline, preferably on an HSM.**
