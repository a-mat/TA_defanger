# TA_defanger


Sometimes URLs and IPs can be malicious. It prevent accidental clicks or searches, you'll want to "defang" them so they become less harmful. In other cases, you'll want to "refang" them. This Splunk commands makes it easy to defang and refang any URL or IP addresses to suite your process.

# What is it?

A custom search command for defanging and refanging URLs and IP Addresses .This TA contains a custom command `defang` that allows users to do both, depending on the arguments passed.

# Pre-requisites.

* An instance of Splunk where you can install the command.
* Splunk 8.0+ as this is only python3 compatible 

# Setup

* Copy this application to a new folder in your `$SPLUNK_HOME$\etc\apps\` folder.
* Restart your splunk instance so the the app is loaded.
* Global Permission so that the custom command and script is accessible

# ppsdecode Command 101

This command is straightforward. At minimum, you just need to specify the field that contains the field you want to defang/refang


Defang the dest_url field and place the defanged value in a new field. This will output the result into a field called "defanged_value"
```
index=... | ...| defang input_field="dest_url"  mode="append"
```

Defang the dest_url field and replace the value with a defanged version
```
index=... | ...| defang input_field="dest_url"  mode="replace". In this case, the defanged dest_url will replace the original value 
```

Refang the dest_url field and place the fanged value in a new field. This will output the result into a field called "fanged_value"
```
index=... | ...| defang input_field="dest_url"  mode="append" action="fanger"
```

Refang the dest_url field and replace the value with a fanged version. In this case, the defanged dest_url will replace the original value
```
index=... | ...| defang input_field="dest_url"  mode="replace" action="fanger"  
```




# Parameters

The following is the list of parameters. Any values that contain spaces, must be within double quotes.

*  "input_field"  - [required]  Specify the field that contains the field of interest
*  "mode"       -   [optional]  Specify if the field value should overwrite the original or if a new one should be created  (default: append)
*  "action"     -   [optional]  Specify if you want the field to decoded field to be defanged (default: defanger)
