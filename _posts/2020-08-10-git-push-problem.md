---
layout: post
title:  "Git push problem: \"The authenticity of host 'github.com (140.82.118.4)' can't be established\" and \"git@github.com: Permission denied (publickey).\""
categories: posts
tags: git
---

## The problem

When you try to push the commits from your local git repository to github, you may see the following"

{% highlight bash %}
user@suers-computer:~/Desktop/my_project$ git push origin master
The authenticity of host 'github.com (140.82.118.4)' can't be established.
RSA key fingerprint is SHA256:nThbgtiX5jufSl7E1IG45tFYmTdrtew536w6E5SY8.
Are you sure you want to continue connecting (yes/no/[fingerprint])? y
Please type 'yes', 'no' or the fingerprint: yes
Warning: Permanently added 'github.com,140.82.118.4' (RSA) to the list of known hosts.
git@github.com: Permission denied (publickey).
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
{% endhighlight %}

When you test connection to GitHub with ``ssh -T git@github.com`` you see the following:

{% highlight bash %}
user@users-computer:~/Desktop/my_project$ ssh -T git@github.com
Warning: Permanently added the RSA host key for IP address '140.82.118.4' to the list of known hosts.
git@github.com: Permission denied (publickey).
{% endhighlight %}

## Solution

1. Check if you have any existing SSH keys: open ``GitBash`` and type

{% highlight bash %}ls -al ~/.ssh{% endhighlight %}

Public keys are files with ``.pub`` extension. If there are no SSH keys, go to step 2. If there are, go to this [step](#Copy).

{:start="2"}
2. Start the ssh-agent in the background: 

{% highlight bash %}
ssh-agent -s
{% endhighlight %}

{:start="3"}
3. Generate new SSH key with ``ssh-keygen -t rsa -b 4096 -C "your-email@gmail.com"``: 

{% highlight bash %}
user@users-computer:~/Desktop/my_project$ ssh-keygen -t rsa -b 4096 -C "user@gmail.com"
Generating public/private rsa key pair.
Enter file in which to save the key (/home/USER/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/USER/.ssh/id_rsa
Your public key has been saved in /home/USER/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:6+WLdmP45oW0HMx33doUtiRuxfMDKCVbKZmsd09Xars user@gmail.com
The key's randomart image is:
+---[RSA 4096]----+
|                 |
|                 |
|         o       |
|        . =      |
|       +S  = +   |
|    o    *oOo*.. |
|   . = O+**o     |
| ..   ..=*@      |
|  ...E*+ B*=     |
+----[SHA256]-----+
{% endhighlight %}

{:start="4"}
4. Add your key to the ssh-agent: 

{% highlight bash %}
user@user-computer:~/Desktop/my_project$ ssh-add ~/.ssh/id_rsa
Identity added: /home/USER/.ssh/id_rsa (user@gmail.com)
{% endhighlight %}

{:start="5"} 
5. <a name="Copy">Copy</a> the SSH key to the clipbord.

Too look for the key, use ``ls -al ~/.ssh`` command. 

On Windows, the key may be copied using ``clip < ~/.ssh/id_rsa.pub`` command in ``GitBash``.

{:start="6"}
6. Add the key in GitHub account settings.

Go to ``Settings``, ``SSH and GPG keys``, click ``New SSH key``. Provide a name for your key (e.g. ``computer-os-user_name``) and paste the copied key.

Your SSH connection test should be established: 

{% highlight bash %}
user@users-computer:~/Desktop/my_project$ ssh -T git@github.com
Hi user! You've successfully authenticated, but GitHub does not provide shell access.
{% endhighlight %}

## Sources

- [Testing your SSH connection](https://help.github.com/en/articles/testing-your-ssh-connection)
- [Adding your SSH key to the SSH agent](https://help.github.com/en/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent#adding-your-ssh-key-to-the-ssh-agent)

