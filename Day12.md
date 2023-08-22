![Microservices](https://github.com/thevinitgupta/100-Days-of-Learning/assets/65801700/27fe03f7-da49-4b9b-af38-a4bed3c30b10)
# Connecting to Github with SSH (Windows)

Earlier, GitHub used to allow browser login. Those were the simpler times. 
<img src="https://media.giphy.com/media/rnb3iyd3KSyW4uMrgy/giphy.gif"/>

But now, to push your code to GitHub, you need to generate `SSH Keys`. These SSH Keys are your login credentials - for personal projects and open source contributions. 

While building a project recently, I tried pushing my code to GitHub but I could not. And I got frustrated😭 like everyone of you might have gotten one day. 

And then I discovered this article which was a tough to navigate, but solved my problems : [SSH Keys and Github](https://rharshad.com/github-ssh-windows/)

I immediately thought of sharing this with all of you to make it simpler. 📢📢

## Step 0 : Prerequisites
For using `Git` on your windows, it is very important to have `GitBash` installed in your system. 

> 🚨 If you haven't already installed `GitBash`, follow this [GitBash Guide](https://www.educative.io/answers/how-to-install-git-bash-in-windows) to install it.

Now that you have GitBash installed on your Windows, we can begin.

## Step 1 : Generate a new `SSH` Key
Generating an SSH key is simple, followed by storing and using it.
 - Run Git Bash
 - Generate a new SSH key by pasting the following snippet
```js
// Replace "your_email@example.com" with your GitHub email ID
$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```
 - When you’re prompted with the following message : 

```js
Enter a file in which to save the key
```

press `Enter` to save the key in the default location (`/c/Users/username/.ssh/id_rsa`). Your public key will also get saved here.

 - Now copy the SSH key to your `clipboard` using the following command : 
```js
$ clip < ~/.ssh/id_rsa.pub
```

## Step 2 : Adding the copied SSH Key to your GitHub account
Now that the key is generated, you need to add it to your GitHub account. 
 - Go to `Settings` in your Github account to add the SSH public key.

 - Under SSH keys tab, select `New SSH key`.

 - Give a title and paste the key in the text area.

<img src="https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExZGoxcGFib2pvcTQ5aXl4bnMwcmk2Zmc4c21ha2g1MDR2ZHU5M2xlaSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/mLHXyewrjDoaWaQNqL/giphy.gif"/>


## Step 3 : Add private SSH key to the `ssh-agent`
Git bash tool comes with a `ssh-agent` which needs to be configured to use the SSH key that you create. 

Follow the steps below for an easy configuration.
 - Open `Git Bash`
 - Create a new `~/.profile (or) ~/.bashrc` file using the following command :
```js
$ vi ~/.profile
```
 - Paste below script into your bash file that opens on running the above command: 
```js
env=~/.ssh/agent.env

agent_load_env () { test -f "$env" && . "$env" >| /dev/null ; }

agent_start () {
    (umask 077; ssh-agent >| "$env")
    . "$env" >| /dev/null ; }

agent_load_env

# agent_run_state: 0=agent running w/ key; 1=agent w/o key; 2= agent not running
agent_run_state=$(ssh-add -l >| /dev/null 2>&1; echo $?)

if [ ! "$SSH_AUTH_SOCK" ] || [ $agent_run_state = 2 ]; then
    agent_start
    ssh-add
elif [ "$SSH_AUTH_SOCK" ] && [ $agent_run_state = 1 ]; then
    ssh-add
fi

unset env

```
This will auto launch the ssh-agent whenever you run your git bash shell.

- Exit the editor by typing clicking on `esc` button on keyboard and write : `:wq` and press `Enter`.

The above file will be saved. 

### And there you have it - ready to contribute to open source projects from your `Command Line`.

> 📌But wait, we are the `Good Developers`, so we will test if it works properly.

## Step 4 : Verification
 - Open a new `Git Bash` window.
 - Check if the identity has been added to the ssh agent.
```js
$ ssh-add -l
```
 - Check that the key is being used by trying to connect to git@github.com.
```js
$ ssh -vT git@github.com

OpenSSH_8.0p1, OpenSSL 1.1.1c  18 August 2023
debug1: Reading configuration data
debug1: Offering public key
debug1: Server accepts key
debug1: Authentication succeeded (publickey).
Authenticated to ssh.github.com
```
### Do `share📤` this with your fellow developers and do not forget to leave a `comment 📝` if you enjoyed this guide.
