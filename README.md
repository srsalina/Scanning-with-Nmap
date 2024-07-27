# Vulnerability Scanning with Nmap

## Project Description

In this project, I used Nmap to scan a network and identify potential vulnerabilities as a security analyst for a hypothetical company. I verified the installation and version of Nmap, ran scans to discover information on a target, and saved the scan results to a file for further assessment. My tasks included discovering information about active hosts, ports, services, and operating systems within a virtual desktop hosted by Rhyme Cloud. I began by checking the Nmap version and using the help features for command references. I performed basic and comprehensive scans on targets like scanme.nmap.org, identifying open ports and services. Additionally, I executed detailed scans with specific options to gather as much information as possible and saved the outputs to text files for documentation and future analysis.

### Skills Learned

- Gained hands-on experience with Nmap to identify active hosts, open ports, and potential vulnerabilities in a network
- Developed skills in saving scan results to files for  documentation, analysis, and future reporting
- Enhanced my ability to use various Nmap options and commands for performing both basic and comprehensive network scans

### Tools Used

- Rhyme Virtual Desktop
- Nmap


## Process

### Nmap Basics

#### Nmap Version Check
I began my project by entering <b>nmap --version</b> in the terminal. Running this command displayed the version of Nmap my virtual machine had installed, as seen below. This way, I ensured that the version of Nmap I had installed would be compatible with any of the commands I had planned to use and to avoid any issues regarding the version. Knowing which version is also important for troubleshooting.
<br><br/>
![image](https://github.com/user-attachments/assets/ddbbfac3-710c-425b-a223-d4aa4787ba2a)


#### Accessing the Help Feature and Man Page for Nmap

I used the Nmap help feature and the Nmap Reference Guide whenever I needed to double-check commands during the project. The commands for accessing these resources are demonstrated below. 

Command to reach the Nmap help feature: <b>nmap --help</b> or <b>nmap</b>.

![image](https://github.com/user-attachments/assets/35da47ad-4db4-445c-8787-312eb583ae95)

![image](https://github.com/user-attachments/assets/79022188-8993-4266-ba21-840d64ba6ab0)

Command to reach the Nmap Reference Guide: <b>man nmap</b>. Its output is displayed below. 

![image](https://github.com/user-attachments/assets/0220d097-9470-4162-93ac-d9fc1ace1375)

### Performing Basic Nmap Scans

Once I had reviewed the help and man pages for Nmap, I wanted to perform a basic ping scan on one of the sample targets provided by the help page. I targeted <b>scanme.nmap.org</b>. Below is the basic layout for a Nmap command that I found by entering <b>nmap</b> in the terminal. 

![image](https://github.com/user-attachments/assets/743dc233-2f16-4e5e-bd15-983b7b7477b7)

A basic ping scan detects if a target is active and which ports it has open. It also checks to see what services the target has running on its open ports. To view this information on my target site, I entered the following command: <b>nmap scanme.nmap.org</b>. Its output is displayed below.

![image](https://github.com/user-attachments/assets/8e2106c6-91b1-42cc-8c21-59290614f976)


After running the scan, I found that a few ports were open on the host, including HTTP port 80. This information led me to believe in the presence of a web server, which could be used to leverage any vulnerabilities.

### Running a Scan on the Host Network

As previously mentioned, the entirety of this project took place within a virtual desktop hosted by  Rhyme Cloud. For my next task, I wanted to see what ports and services were running on my host network. I ran the command <b>ifconfig</b> to verify that I could scan it. As demonstrated below, I found that I could use the IP address provided by the <b>ens5</b> interface for this task.  

![image](https://github.com/user-attachments/assets/3e750066-5f26-404a-8755-3acf59ee0231)

I then used the command <b>nmap 10.199.10.236</b> to scan this target. 

![image](https://github.com/user-attachments/assets/08562b87-ce17-4acb-88a7-53a6bcf237a9)

I found that TCP port 22 was open on the host network, and it was running SSH. Port 5800 was also open and was running VNC-HTTP.

### Performing a Comprehensive Scan Using Options

Next, I wanted to run a more aggressive scan on the previously used example target (<b>scanme.nmap.org</b>/). More specifically, I wanted to find the operating system running on it. To do this, I ran the sample command provided by the help page, as seen below.

![image](https://github.com/user-attachments/assets/c0fd6955-2dea-414e-bacb-ef4c1c71d89c)

Here is a breakdown of the options added to the Nmap command:

- <b>-A</b>: Stands for aggressive and enables OS detection, version detection, script scanning, and traceroute. It is useful when attempting to find vulnerabilities, as it gathers as much information as possible. However, I was cautious about using it, as using -A can consume more resources and generate excessive network traffic, causing a host to crash.
- <b>-T</b>: Sets the timing of the scan. The higher the number, the quicker, more aggressive, and less accurate the scan.


I found that the target was running Linux as its operating system. I made note of the service versions present on the open ports found on the target (such as Apache httpd 2.4.7 running on port 80). A malicious actor could research these services and find any vulnerabilities particular to those service versions. 

### Outputting a Nmap Scan to a File

This section demonstrates how I saved the output of an Nmap scan to a file. Saving the output to a file is essential for maintaining good documentation, which can assist with future analysis and reporting. For this task, my hypothetical organization asked me to save a detailed port 80 scan to a text file for a future review with the IT team. To complete this task, I ran the command displayed in the following screenshot. Its output is also displayed.

![image](https://github.com/user-attachments/assets/1ebbcfb0-a555-409d-a057-5587e0dda4e1)

The following list breaks down the options I entered for the command:
- <b>-p</b>: Specifies the port to be scanned, which in this case was HTTP port 80
- <b>-A</b>: Enables OS detection and script scanning. I chose this option to view as much information as possible
- <b>-oN scan.txt</b>: Saves the output to a normal text file, which I named scan.txt in this case

Next, I entered <b>ls</b> in the terminal to verify that the file was created. The file appeared in my working directory, as seen below.

![image](https://github.com/user-attachments/assets/0161a986-a60d-4214-a8a2-e01e39daf745)


I checked to see that the output was saved properly and could be read by running the command <b>cat scan.txt</b. I noticed that the file had the same information initially displayed in the output of the Nmap command, confirming that the scan was successfully saved as a text file.

![image](https://github.com/user-attachments/assets/e322e425-8036-45cd-b4a9-51d1d8089aea)

### Remediating Vulnerabilities

My final task required me to run a detailed Nmap scan on a range of ports. As before, the scan output must be saved to a text file for future analysis.

These were my task conditions:
- Perform a Nmap scan on the host <b>scanme.nmap.org</b>
- Scan only ports 22-80
- Enable OS and version detection, script scanning, and traceroute
- Set a timing execution of T3
- Output the results to a .txt file named <b>output.txt</b>
- Verify that the file was saved properly by reading the contents

I knew that the port attribute could take in a custom range of ports, so I added <b>-p 22-80</b> to the command. Secondly, I added <b>-A</b> to view a detailed scan of the ports as required by the conditions. Lastly, I set a timing execution of T3 and used <b>-oN output.txt</b> to save the output to a text file. Pictured below is the complete command and its output.

![image](https://github.com/user-attachments/assets/5e99a389-b039-4178-888f-2300e95e6e07)

I verified that the text file was created in my present directory by entering the command <b>ls</b>, the same as before. 

![image](https://github.com/user-attachments/assets/3a8a4e0e-6088-4508-a569-a7ec8e112f56)

Finally, I scanned the contents of the <b>output.txt</b> file to verify that everything was saved correctly. 

![image](https://github.com/user-attachments/assets/e415f08a-1823-47e3-b10e-00b0c0e660bf)




## Summary
In this project, I demonstrated using Nmap to scan and analyze network vulnerabilities from a virtual desktop environment. I started by confirming the Nmap version and using its help features. I performed basic scans to identify active hosts and open ports and executed more detailed scans to detect operating systems and service versions. By saving the scan results to text files, I ensured thorough documentation and facilitated future analysis and reporting, thereby enhancing my practical skills in network security and vulnerability assessment.
