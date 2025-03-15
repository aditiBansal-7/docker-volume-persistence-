# 📌 Steps & Observations  

## 1️⃣ Run a Container with a Bind Mount  
Run the following command:  
```sh
docker run -dit --name alpine_with_bind_mount -v C:\Users\aditi\docker_data:/data alpine:latest sh
```
🔍 What Happened?

Since alpine:latest was not found locally, Docker pulled it from the official repository.
A new container named alpine_with_bind_mount was created.
The -v flag mounted the local directory C:\Users\aditi\docker_data to /data inside the container.
The container started a shell (sh) in detached mode.

2️⃣ Create a File Inside the Bind Mount
Inside the container, create a file:

```sh
docker exec -it alpine_with_bind_mount sh -c "echo 'Hello, Aditi!' > /data/testfile.txt"
```
🔍 What Happened?

The command executed a shell inside the running container.
It created a file testfile.txt inside /data and wrote "Hello, Aditi!" into it.
Since /data is a bind-mounted directory, the file was actually stored in C:\Users\aditi\docker_data on the host system.
3️⃣ Verify the File Exists
To check the contents of the file inside the container:

```sh

docker exec -it alpine_with_bind_mount sh -c "cat /data/testfile.txt"
```
📌 Output:

```sh
Hello, Aditi!
```
🎉 This confirms that the file was successfully created and is accessible inside the container.

4️⃣ Remove the First Container
Remove the container:

```sh
docker rm -f alpine_with_bind_mount
```
🔍 What Happened?

The container was forcefully stopped and removed.
However, since testfile.txt was inside the bind-mounted directory, it remained on the host system. 🏠
5️⃣ Create a New Container with the Same Bind Mount
Start a new container:

```sh
docker run -dit --name new_alpine -v C:\Users\aditi\docker_data:/data alpine sh
```
🔍 What Happened?

A new container named new_alpine was created.
The same bind-mounted directory (C:\Users\aditi\docker_data) was mounted to /data.
6️⃣ Verify File Persistence
Inside the new container, check if testfile.txt still exists:

```sh
docker exec -it new_alpine sh -c "cat /data/testfile.txt"
```
📌 Output:

```sh
Hello, Aditi!
```
🔥 This confirms that bind mounts persist data even after a container is removed!

🎯 Conclusion
✅ Bind mounts allow data persistence across multiple container instances.
✅ Deleting a container does not remove data stored in the bind-mounted directory.
✅ Any new container with the same mount can access data from previous containers.
✅ Useful for containerized applications that need persistent storage.

