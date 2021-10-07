# Deeper CLI Usage

### Download
- Windows
- Linux x64
- Linux ARM (Raspberry Pi's etc.)

### Notes
- If you are not intending to use the CLI with New Relic, then download the appropriate version from above and unpack in whichever directory you'd like.
- If you are using it with New Relic, then I would suggest unpacking it into the appropriate New Relic directory unless you want to maintain two copies of the CLI. Follow the New Relic guide for your operating system instead.

### Steps
- The CLI requires no installation or depedencies, it is a single compiled binary that can be run from anywhere.
- Download the CLI package and unpack it where you like, you can then use the help flag to view all the available options.
- Use the `-v` flag for verbose logging if you are experiencing issues or want to see what is being executed.

### Help Options
```
# Navigate to the directory where your CLI is, then run with the -h flag.

# Linux
./deeper-cli -h

# Windows (in powershell)
.\deeper-cli.exe -h
```
![Help options](/images/deeper-cli-help-options.png)


### Authenticating the CLI
- To use most of the CLI commands you will need to authenticate and create a credential file.
- The credential file is an encrypted copy of your password so you do not need to expose your plain text password any longer. This is the exact same encryption and method the Atmos Web UI uses.
- You can use the `-e` flag to encrypt your password inline (as below) or use `-encrypt-password-prompt` for prompt based method.

```
# Linux
./deeper-cli -e yourAtmosPassword -v

# Windows (in powershell)
.\deeper-cli.exe -e yourAtmosPassword -v
```
- If you do not receive any error, your password should be successfully encrypted.
- You can view the encrypted credential in the following directory `.deeper-cli.cache`
![Credential location](/images/deeper-cli-credential-location.png)

---

## Fetching data
- With the credential file created you can then use any of the following flags listed in the help section to collect information about your device.

Example getting only hardware info (note you do not require sudo, but the directory I am using the CLI in is owned by root so I require it in this case)

```
# Linux
./deeper-cli --get-hardware-info

# Windows (in powershell)
.\deeper-cli.exe --get-hardware-info
```

![Credential location](/images/deeper-cli-hardware-output.png)


Example getting all data (note you do not require sudo, but the directory I am using the CLI in is owned by root so I require it in this case)

```
# Linux
./deeper-cli --get-all

# Windows (in powershell)
.\deeper-cli.exe --get-all
```

![All output](/images/deeper-cli-all-output.png)

---

## Dumping sharing logs
Prefix the below commands with either ./deeper-cli or .\deeper-cli.exe depending on your operating system.

```
# Get past 1 day of sharing logs
--get-sharing-logs 1

# Get past 1 day of sharing logs, but on subsequent runs only get the new logs
--get-sharing-logs 1 -n

# Get past 7 days of logs and write to logs.json file
 --get-sharing-logs 7 -o logs.json

# Write 1 day of logs out in raw format, useful for log parsing engines, this will write each log line as a single json item
 --get-sharing-logs 1 -o logs.out -r

 # Write 1 day of logs out in raw format, and subsequently only new logs after, useful for log parsing engines, this will write each log line as a single json item
 --get-sharing-logs 1 -o logs.out -r -n
```