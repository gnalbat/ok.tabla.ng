---
title: Git, [for] Windows, and SSH
date: 2025-06-12
tags:
  - tech
---
To my astonishment, I spent almost 2 hours solving this. I have Git for Windows from scoop and moved to using ssh for Git since CredentialHelper selector keeps popping up whenever I interact with the remote and won't remember the "Always use this from now on" setting (why put it if it doesn't work?)

So the key gets loaded in ssh-agent but git won't fetch it. Then I find out that Git for Windows **bundles it's own ssh binary**! For context, Windows has included OpenSSH since Windows 10 1803.<sup>[1]</sup> What a waste of time. Thanks, Stack Overflow.

So run this:

```powershell
 git config --global core.sshCommand C:/Windows/System32/OpenSSH/ssh.exe
```

Update (12 June 2025):

It started working somehow. 

Ran
```powershell
git credential-manager configure
git credential-manager diagnose
```

And `credential.helper` suddenly pointed to the absolute path of git-credential-manager.

```powershell
git config --global credential.helper manager
# warning: credential.helper has multiple values
# error: cannot overwrite multiple values with a single value
#       Use a regexp, --add or --replace-all to change credential.helper.
git config --global credential.helper
# C:/ProgramData/scoop/apps/git/2.47.1.2/mingw64/bin/git-credential-manager.exe
```

I changed it to point to scoop git's current symlink.

.gitconfig
```ini
[credential]
    helper =  C:/ProgramData/scoop/apps/git/current/mingw64/bin/git-credential-manager.exe
```

Update 2 (8 August 2025):

Apparently running `git credential-manager configure` changes the credential section to
```
[credential]
    helper = manager
    helper =
    helper = C:/ProgramData/scoop/apps/git/2.49.0/mingw64/bin/git-credential-manager.exe
```

And it will not work otherwise.

I still don't understand how this works.

1. Durr, Yosef (7 March 2018). ["What's new for the Command Line in Windows 10 version 1803"](https://devblogs.microsoft.com/commandline/windows10v1803/). _Windows Command Line Tools For Developers_.
2. ["How to run ssh-add on Windows?"](https://stackoverflow.com/questions/18683092/how-to-run-ssh-add-on-windows/68386656#comment133124115_68386656) _Stack Overflow_. 
3. ["Git does not use SSH key (Windows)."](https://stackoverflow.com/questions/71556140/git-does-not-use-ssh-key-windows) _Stack Overflow_. 
