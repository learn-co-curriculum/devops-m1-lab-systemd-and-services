# Users & Permissions Lab

## Task

In this lab, we will be creating, enabling, and managing a `systemd` service.

## Instructions

### Creating the service

In your terminal, navigate to `/etc/systemd/system`:

```bash
$ cd /etc/systemd/system
```

This directory typically contains most of the `systemd` services. Since it's under `/etc`, we need to use `sudo` if we wish to create or modify any of the files here. Let's go ahead and make a new service:

```bash
$ sudo nano lab_service.service
```

Let's go ahead and create a service that creates a file:

```bash
[Unit]
Description=Lab service that creates a file when ran

[Service]
User=<your username>
ExecStart=/bin/sh -c 'touch /tmp/file.txt'
Type=oneshot

[Install]
WantedBy=multi-user.target
```

For context, the `WantedBy` directive specifies which target should be started when activated. A target is simply a way to group services that you want to start together at the same time. In this case, we use `multi-user` because that is an already-existing target commonly used in a lot of *Linux* distributions.

Save and exit the file. Then, as mentioned earlier, you need to restart the `systemd` daemon in order to detect the new service:

```bash
$ sudo systemctl daemon-reload
```

### Enabling the service

Now that we have our service created and the daemon restarted, we can finally enable it so it starts at boot time:

```bash
$ sudo systemctl enable lab_service.service
```

Let's make sure it runs properly by starting it:

```bash
$ sudo systemctl start lab_service.service
```

Check the status of the service:

```bash
$ sudo systemctl status lab_service.service
```

If the service ran successfully, we should have a file now created in the `/tmp` folder:

```bash
$ ls /tmp
file.txt
```

Lastly, let's restart our system to make sure it runs automatically as we intended:

```bash
$ reboot
# once rebooted
$ ls /tmp
file.txt
```

That's it!

## Submission

Take a screenshot of the terminal after running the `sudo systemctl status lab_service.service` command, as well as `ls /tmp`.

Upload the screenshot as the submission for this assignment.