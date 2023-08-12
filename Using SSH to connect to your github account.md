
### Generate key pair

So, the flow is pretty simple. We need to use some utility to create a key pair. We will use one of these keys, the private key, to encrypt the data. When this data is received by someone, they can use the the other key, the public key to decrypt the data. 

So, we will use ssh-keygen to create the key pair, we can specify the filename either as command line input, or we can enter it once the command runs and asks for it. We can choose which algorithm to use to create the key pair, by default ssh-keygen uses rsa.

				ssh-keygen -t rsa

Once the command runs, it will create 2 files, `[fileName]` and `[fileName].pub`.  The files will be created in the user's home directly. So, you can navigate to `~/.ssh` folder and see the files. Now, we will keep both of these on our system. But, we will have to share the public key in `[fileName].pub` with the intended receiver, in this case github.

So, we will login to the github account. Go to ssh keys sections and add the public key by giving it an identifier. 

### Create config

Now, when we try to connect to github.com, our system needs to use the private key stored in `[fileName]` to connect to github. So, the ssh command needs to know which private key to pick. It uses `id.[algo]` by default. So, if rsa was used, it would look for id_rsa, unless you specify it which key to use. It is always good to be explicit and create a config to specify which private key to use for the host you intend to connect with. So we will create a config file in the `~/.ssh` folder and add config for every host we want to connect with ssh in it.

				cd ~/.ssh
				touch config
				vi config

Once done, we will then add config for github.com in it

				Host github.com
				HostName github.com
				IdentityFile ~/.ssh/[fileName]

Now, when you try to ssh to github.com, this config file would be looked up and the content will be encrypted by the private key, the location of which is specified by the IdentityFile.