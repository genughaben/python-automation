# Python Automation

## Manage Downloads Folder

### Prepare Downloads folder:

Create the following folders in your Downloads and create folders:

['pdf' 'else' 'data' 'image' 'video' 'document' 'programming']

using:

```shell
> cd ~/Downloads
> array=( 'pdf' 'else' 'data' 'image' 'video' 'document' 'programming' )
for i in "${array[@]}"
do
  mkdir $i
done
```


### Setup manage-downloads service

```shell
> cd automation/manage-downloads
> cp manage-downloads.service.template manage-downloads.service
```

Modifiy manage-downloads.service entries:
* ExecStart=/usr/bin/python /your/path/to/automation/manage-downloads/manage_downloads.py (Line 8) and
* User=your-user-name-get-by-typing-whoami-in-console (Line 13)

NB:
* Get username by entering whoami into console.
* Get /your/path/to/manage_downloads.py by entering:

```shell
> realpath manage_downloads.py
```

```shell
> cd automation/manage-downloads
> sudo mv manage-downloads.service /lib/systemd/system
> sudo systemctl daemon-reload
> sudo systemctl enable manage-downloads.service
> sudo systemctl start manage-downloads.service
> sudo systemctl status manage-downloads.service
```

The last commands should result in:

```shell
➜  system sudo systemctl status manage-downloads.service
● manage-downloads.service - Manage_Download Service
     Loaded: loaded (/lib/systemd/system/manage-downloads.service; enabled; vendor preset: enabled)
     Active: active (running) since Sat 2020-05-23 18:09:30 CEST; 5min ago
   Main PID: 26219 (python3.8)
      Tasks: 4 (limit: 57730)
     Memory: 6.6M
     CGroup: /system.slice/manage-downloads.service
             └─26219 /usr/bin/python3.8 /your/folder/automation/manage-downloads/manage_downloads.py

Mai 23 18:09:30 DeepL systemd[1]: Started Manage_Download Service.
```

In terms you get an error, use:

```shell
> sudo journalctl -xe
```

to view service logs.
