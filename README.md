# Deep Learning on Jetson TX2
Setting Environment for Deep Learning on Jetson TX2
- Flash JetPack 3.3 on Jetson TX2
    Follow the official [guide](https://developer.download.nvidia.com/embedded/L4T/r27_Release_v1.0/Docs/Jetson_X2_Developer_Kit_User_Guide.pdf?dSygcMtyZ5vJ-LM2eRMOA5hFx8ytqFgN5aU9ZqLHhI35fEbgNmH0Vz8Z2FUguk3lkSWbjlKf2VQGmFyc5_kOmha4fKYBzX7l4uHK3uvyxm32nWngSdnpz8uU1eJhaePquaRjh3t66hmfeQWz2dvtvoMbY4v0cuJNcjnjALnRkjJhcCY5UAZ1dQ) or instructions on [YouTube](https://www.youtube.com/watch?v=D7lkth34rgM).
- The Jetpack 3.3, has support for Docker out of the box. 
    Verify the installation with:
    ```console
    $ sudo docker run hello-world
    ```
    You should get a confirmation message:
    ![docker hello-world](http://pix.toile-libre.org/upload/original/1544262477.png)
- Copy a short Bash script to enable use of the GPU within a docker container running on an NVIDIA Jetson TX2 (taken from [here](https://gist.github.com/JasonAtNvidia/e03e6675849d1d4049b85ea41efb2171)). Place it inside /usr/local/bin/, chmod +x txdocker, ensure it is in your system PATH, and use just as you would the docker command.
```console
#!/bin/bash
#Jason T. 2-6-2018

# Check specifically for the run command
if [[ $# -ge 2 && $1 == "run" ]]; then
    # Tell docker to share the following folders with the base system
    # This allows the docker containers to find CUDA, cuDNN, TensorRT
    LIB_MAPS="/usr/lib/aarch64-linux-gnu \
              /usr/local/cuda \
              /usr/local/cuda/lib64"
		 
    # GPU device sharing is for a docker container to have access to
    # system devices as found in the /dev directory
    DEVICES="/dev/nvhost-ctrl \
             /dev/nvhost-ctrl-gpu \
             /dev/nvhost-prof-gpu \
             /dev/nvmap \
             /dev/nvhost-gpu \
             /dev/nvhost-as-gpu"
	
	# There is a need to map the libraries inside the container
	# in the exact way programs would expect to find them as
	# though the TX2 were operating without containers
	LIBS=""
	for lib in $LIB_MAPS; do
		LIBS="$LIBS -v $lib:$lib"
	done
	
	DEVS=""
	for dev in $DEVICES; do
		DEVS="$DEVS --device=$dev"
	done
	
	#echo "docker run $LIBS $DEVS ${@:2}"
	docker run $LIBS $DEVS ${@:2}
else
    # Run command not found, run everything straight through docker
    #echo "docker $@"
	docker $@
fi
```
TO BE CONTINUED...
