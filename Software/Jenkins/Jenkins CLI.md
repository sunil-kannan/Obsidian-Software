---
date: 2024-09-06
tags: 
link:
---

# Jenkins CLI

> Jenkins CLI Setup and Usage. My Jenkins is running on port 8989.

### Step 1: Download Jenkins CLI Jar

1. Go to [http://localhost:8989/manage/cli/](http://localhost:8989/manage/cli/) and download the `jenkins-cli.jar` file.
   
### Step 2: Create a New API Token

1. Visit [http://localhost:8989/user/sunil/configure](http://localhost:8989/user/sunil/configure).
2. Create a new API token.
3. Copy the API token for later use.

### Step 3: Run Jenkins CLI Command

1. Navigate to the folder where you downloaded `jenkins-cli.jar`.
2. Use the following command to authenticate and check the available commands:

```bash

java -jar jenkins-cli.jar -noCertificateCheck -s http://192.168.11.192:8989/ -auth sunil:116eb332774e1255cb2814fac416879683
```
### Step 4: Create batch file

You can create an alias for the Jenkins CLI command in Windows to shorten the typing process. Since Windows doesn’t support native command aliases like Linux, you can achieve this using batch files.
- **Create a Batch File**:
    
    - Open **Notepad** or any text editor.
        
    - Add the following content:
        `@echo off java -jar C:\path\to\jenkins-cli.jar -noCertificateCheck -s http://192.168.11.192:8989/ -auth sunil:116eb332774e1255cb2814fac416879683 %*`
        
    - Replace `C:\path\to\jenkins-cli.jar` with the actual path where your `jenkins-cli.jar` file is located.
        
- **Save the Batch File**:
    
    - Save the file as `jenkins.bat`.
    - Save it in a directory that's included in your **PATH** environment variable (e.g., `C:\Windows\` or any other directory added to the PATH).
    - Make sure that you have added the path in the **PATH** environment variable and it should be in the 'C' folder.
    
- Run the command to check
	```bash
	jenkins who-am-i
	# Authenticated as: sunil
	# Authorities:
	# authenticated
```

### 📃 Real time use case

- Automation: Automating routine tasks  
- Bulk updates: Performing bulk updates  
- Troubleshooting: Diagnosing issues  
- Managing projects: Managing operations center jobs or projects  
- Agent and administration activities: Managing agent- and administration-related activities