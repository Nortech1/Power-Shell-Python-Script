import subprocess
import os
import os.path
import sys
import re

if os.path.isfile('result.txt'):
    print("File Exist")
    f = open(r'result.txt')
    os.system("start notepad result.txt")
    f.close()
else:
    print("No such file found, File is created now:")

    with open('result.txt','a') as f:
        f.write('Running processes')
        runningProcesses = subprocess.check_output(
            'powershell -ExecutionPolicy ByPass -Comman'
            'd Get-WmiObject win32_process | select ProcessName,'
            'ProcessId, CommandLine')
        f.write(runningProcesses.decode())
        f.write('Local User')
        runningProcesses = subprocess.check_output(
            'powershell -ExecutionPolicy ByPass -Command Get-LocalUser')
        f.write(runningProcesses.decode())
        f.write("User information:")
        runningProcesses = subprocess.check_output(
            'powershell -ExecutionPolicy ByPass -Command Get-LocalUser | Select *')
        f.write(runningProcesses.decode())
        f.write('Downloaded files:')
        runningProcesses = subprocess.check_output(
            'powershell -ExecutionPolicy ByPass -Command Get-ChildItem -LiteralPath C:\\Users\\$_\\')
        f.write(runningProcesses.decode())
        f.write("Last objects used:")
        runningProcesses = subprocess.check_output(
            'powershell -ExecutionPolicy ByPass -Command Get-ChildItem -Path $dir | Sort-Object LastAccessTime -Descending'
            '| Select-Object -First 10')
        f.write(runningProcesses.decode())
        f.write("Connected USB Devices")
        runningProcesses = subprocess.check_output(
            'powershell -ExecutionPolicy ByPass -Command Get-ItemProperty -ea 0 '
            'hklm:\\system\\currentcontrolset\\enum\\usbstor\\*\\* | select '
            'FriendlyName,PSChildName')
        f.write(runningProcesses.decode())

    #sys.stdout.close()






