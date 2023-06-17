# msvrt_libs

These are the msvrt libs created using this ![gist](https://gist.github.com/SolomonSklash/fc02b48a7a70ecb1508977a8e41d43e5)
```
# On Windows, within a VS developer prompt

# Dump the exports of msvcrt.dll 
dumpbin.exe /exports C:\Windows\System32\msvcrt.dll > msvcrt.txt

# Copy msvcrt.txt to a Linux box

# Convert the file to Unix line endings
dos2unix msvcrt.txt

# Remove the header from dumpbin
sed -i '1,19d' msvcrt.txt

# Create msvcrt.def file and add the required "EXPORTS" line to the beginning
echo "EXPORTS" > msvcrt.def

# Get the list of functions and remove everything else, redirecting it to the .def file
awk '{print $4}' msvcrt.txt | sed '/^[[:space:]]*$/d' >> msvcrt.def

# Copy back to Windows in a developer prompt

# Create a .lib file from the .def file
lib.exe /def:msvcrt.def /out:msvcrt.lib /machine:x64
```

and dll's from https://www.dll-files.com/msvcrt.dll.html


Uses can be refrenced at
 1. https://www.solomonsklash.io/smaller-c-payloads-on-windows.html
 2. https://0xpat.github.io/Malware_development_part_4/