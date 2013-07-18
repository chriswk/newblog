So, I've long harboured a fear of ssh/X on Windows due to a couple of negative experiences in the past, so tonight when I needed to logon to my work computer (the only one of my boxes that were already logged into LastPass to use OTP to recover my master password (a long "secure" password, not always easy to remember, especially with the mnemonic gone from my head)), I had already given it up as a lost case.
However, I found a rather good tutorial. Reposting the main steps:
    - Configure Putty
    - Configure Cygwin, follow install instructions on X/Cygwin project's homepage and you'll get the tools you need.
    - Open Cygwin bash
    - run startxwin
    - Check the X11 port forwarding in putty before you make the ssh connection to the server.
        - Remember to set AllowX11Forwarding to yes in your sshconfig on the remote server</li>
    - Connect to the server using putty
    -  Run necessary command to start the X application you want to use
    -  In this case I found that google-chrome http://www.lastpass.com worked fine
Oh, and credit where credit's due. The URL to the page was: <a href="http://www.erdc.hpc.mil/documentation/Tips_Tricks/cygwinPuTTY">http://www.erdc.hpc.mil/documentation/Tips_Tricks/cygwinPuTTY</a></p>
Personally I did a big no no and did not configure Kerberos which in hindsight I probably should've done, especially since I was working with passwords.</p>
