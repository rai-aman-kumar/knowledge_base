
For the details on how to configure ssh for your github account, see [[Using SSH to connect to your github account]]

### Set global git config

If you have a single github account, let's say your personal account to use on your system, you should consider adding global git config. There is no point specifying it in every repo as the global one would be used by default. You can override it for a git repo. 

				git config --global user.name "[user name]"
				git config --global user.email "[user email]"

So, for every commit you make on any repo in your system, the above author details would be picked up. 

#### Generate another key pair

But, there is just one key pair we have on our system, we need to create one more, let's say we want to use our company github account from our system. Follow the same process again.

				ssh-keygen -t rsa

Specify the file name to something else this time, else it will override the previously generated key pair files. So, let's assume this to be the `ls` output  in `~/.ssh` folder, once the 2nd key pair is generated.

				personal_id_rsa
				personal_id_rsa.pub
				company_id_rsa
				company_id_rsa.pub
				config


Now, you should add the public key generate to your company github account.

### Update config file

Now, we need to add another set of config in the `config` file. Now, the hostname is still github. So, you would be connecting to github only, but the ssh command needs to know which key to use for data encryption. That is where the host comes in.

So, we will update our config, and it would look something like this


				# Personal account
				Host github.com
				HostName github.com
				IdentityFile ~/.ssh/personal_id_rsa
			 
			 
				 # Company account
				 Host github.com-[company]
				 HostName github.com
				 IdentityFile ~/.ssh/company_id_rsa

Now, when you git clone a company repo, replace the `github.com` portion with `gitbub.com-[company]`. So, basically the host you set in the config.

Now, when ever you would try to connect, the ssh clone url stored in the git repo in `.git/config` file would have this `github.com-[company]` url entry. So, the corresponding key would be picked for encrypting data.


### Managing git user

You can set author details in git at global level and per repo level. We set our personal details at global level so that we don't have to add it to any repo we create for personal projects. But, we don't want to use the personal author details. So, in any company repo you want to work on, set the author details like this

				git config user.name "[company user name]"
				git config user.email "[company mail id]"