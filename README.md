# Deep Learning on Jetson TX2
Setting Environment for Deep Learning on Jetson TX2
- Flash JetPack 3.3 on Jetson TX2
    Follow the official [guide](https://developer.download.nvidia.com/embedded/L4T/r27_Release_v1.0/Docs/Jetson_X2_Developer_Kit_User_Guide.pdf?dSygcMtyZ5vJ-LM2eRMOA5hFx8ytqFgN5aU9ZqLHhI35fEbgNmH0Vz8Z2FUguk3lkSWbjlKf2VQGmFyc5_kOmha4fKYBzX7l4uHK3uvyxm32nWngSdnpz8uU1eJhaePquaRjh3t66hmfeQWz2dvtvoMbY4v0cuJNcjnjALnRkjJhcCY5UAZ1dQ) or instructions on [YouTube](https://www.youtube.com/watch?v=D7lkth34rgM).
- After installing the JetPack you are ready to go. The Jetpack 3.3, has support for Docker out of the box. 
    Verify the installation with:
    ```console
    $ sudo docker run hello-world
    ```
    You should get a confirmation message:
    ![docker hello-world](http://pix.toile-libre.org/upload/original/1544262477.png)
