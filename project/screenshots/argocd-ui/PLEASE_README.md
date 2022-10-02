Because I am running a Mac M1 I cannot use VirtualBox.
Unfortunately, it was not mentioned that the training currently does not provide support for Mac M1.
Instead of using Vagrant I ran everything directly on my Mac using Minikube.
I added the screenshots of Minikube Dashboard to show that it is correctly running.
Exposing the port as per instructions doesn't work with Minikube.
To expose the service I need to run minikube service argocd-server -n argocd.
Below is the output of running that command. This shows that Minikube binds to different ports than specified.
That is also the reason why you'll see ArguCD accessed in the browser using different ports than specified.


minikube service argocd-server -n argocd
|-----------|---------------|-------------|--------------|
| NAMESPACE |     NAME      | TARGET PORT |     URL      |
|-----------|---------------|-------------|--------------|
| argocd    | argocd-server |             | No node port |
|-----------|---------------|-------------|--------------|
😿  service argocd/argocd-server has no node port
🏃  Starting tunnel for service argocd-server.
|-----------|---------------|-------------|------------------------|
| NAMESPACE |     NAME      | TARGET PORT |          URL           |
|-----------|---------------|-------------|------------------------|
| argocd    | argocd-server |             | http://127.0.0.1:53070 |
|           |               |             | http://127.0.0.1:53071 |
|-----------|---------------|-------------|------------------------|
[argocd argocd-server  http://127.0.0.1:53070
http://127.0.0.1:53071]
❗  Because you are using a Docker driver on darwin, the terminal needs to be open to run it.

I also tried using K3S, but I ran into issues with ARM64 vs AMD architecture and wasn't able to figure out how to fix this.
I also tried using Parallels Desktop and Vagrant, but ran into the issue that there are hardly any properly working ARM64 images.
I tried to use almalinux/9.aarch64 (parallels, 9.0.20220905) box, but also here I ran into the issue that the image created with GitHub is AMD64. I am not entirely sure why this isn't a problem with Minikube.

I hope you can accept my submission because I spend a ton of time trying to get other setups working.
But my knowledge is at this point still too limited to fix some of the issues in a reasonable amount of time.
