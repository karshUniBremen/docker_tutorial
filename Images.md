# Images

### What's in an image (and what Isn't)

What's in

- App binaries and dependencies

- Metadata about the image data and how to run the image

  

  Binaries can be small (even one file) or even large binaries like ubuntu with apt

What's not

- Not a complete OS
- No kernel
- No kernel modules (ex: drivers)

Images comes in two variant in  https://hub.docker.com 

- official (always written "official" under the image repo icon)
- not-official

Official image is only one for the give repo and the name of the image is just one single word without any slash in their names. Typically **<repo_name>:< tag-name>**

Not-official images are many for a repo and the name of the image contains atleast two word with a slash. Typically it will be **< username>/<repo_name>:< tag-name>** or  **< organization_name>/<repo_name>: < tag-name>** 

Images is actually a tag. There can be multiple images or tags in a repo with different version of software.

:octopus: To view attributes pertaining to all image in host 

```bash
docker image ls
```

:octopus: To pull an image with specific version

```bash
docker pull <image-name>:<version>
```

:octopus: To pull latest image or default pull

```bash
docker pull <image-name>
```

- :bell: Note latest is just to indicate its latest tag. 



### Image layers & caching

Images are broken in multiple layers. In host we only store only one copy of each layer. This saves a lot of space in the host system. These layers are combined as described by docker-compose file to run instantiate a container. If any changes are made then more layers are created (only pertaining to the changes made). Only one copy of each layer is saved in host disk.

:octopus: To know the history of the image

```bash
docker history <image-name>
```

:bell: Note: in the command output, it mentions <missing> it does not mean something is missing or wrong. It just indicates these are the layers within the image and so they wont get SHA or image ID .

:octopus: Inspect the image, this give metadata about the image such as port opened, environment variables, processor architecture and many more important stuffs

```bash
docker image inspect <image-name>
```

How to recognize the image

Images are of the format

- official image:   <repo-name>:<tag-name>
- not official image: <user-name>/<repo-name>:<tag-name>

Tag are just a label in human readable format to a corresponding image ID. Image ID is SHA ID. Thus an image ID can be corresponded with one or more tag name.

The docker is checks the image ID and downloads it only if image is'nt there.  So it does not actually take account of tag name while downloading. While during image inspect it might show 2 images with multiple tag name , on close look at image ID they have same Image ID and are downloaded only once. This saves lot of disk space in host computer. 

:octopus: Tagging a image

```bash
docker image tag <image-name-old> <image-name-new>
```

- :bell: **Latest** tag does not mean latest, it just means default tag name.

:octopus: Pushing image

```bash
docker image push <image-name>
```



