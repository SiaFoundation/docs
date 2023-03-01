# How to automatically restart and unlock Sia

When your Sia wallet is locked, it isn't able to perform common and important tasks. For renters, this might mean new contract formation or renewing your allowance. For hosts, it would mean downtime that affects your host scoring and the collateral you've put into contracts.

You can have your Sia wallet automatically unlock by setting up a few simple steps.

## Set the environment variable

An environment variable is just a piece of information that is specific to your computer. In this case, it's your Sia wallet password, so you'll set an environment variable named `SIA_WALLET_PASSWORD`.

[How do I set an environment variable?](how-to-set-an-environment-variable.md)

Environment variables are accessible by any program on your computer. If you still use your Sia seed to unlock your wallet instead of a custom password, you should change this before entering your Sia seed into the environment variable. Someone with access to your seed can easily steal your Siacoins and access your files. Learn how to set a custom password.

## Set your computer to automatically reboot after a power failure

Everything we do here won't matter much if you physically need to reboot your machine after it loses power. At that point, you could just launch Sia again on your own. This setting will allow your computer to reboot automatically anytime its power is interrupted.

* [Windows and Linux](https://www.technewsworld.com/story/78930.html) (done through your BIOS, complete with instructions for connecting to an APC for smooth power-downs and startups)
* [Mac](https://www.wikihow.com/Make-Your-Mac-Restart-Automatically-After-a-Power-Failure) (only applicable to certain models)

## Set your user to automatically login on startup

Your computer needs to automatically log in to your user after it reboots. Follow these steps depending on your OS.

* [Windows](https://www.groovypost.com/howto/automatically-sign-in-windows-10/)
* [Mac](https://support.apple.com/en-us/HT201476)
* [Linux - Ubuntu](https://help.ubuntu.com/stable/ubuntu-help/user-autologin.html.en)
* [Linux - other distros](http://www.linfo.org/automatic\_login.html)

## Set Sia as a startup item

Now that your computer will automatically login after startup, you need to make sure that Sia will launch on its own after that happens. Follow one of these options:

* Visit one of the following links to learn how to setup Sia as a startup item. Once all these steps are set, reboot your computer and verify that your account logs in, Sia starts, and your wallet unlocks automatically.
  * &#x20;[Windows](https://support.microsoft.com/en-us/help/4026268/windows-10-change-startup-apps)
  * [Mac](https://support.apple.com/kb/PH25590?locale=en\_US)
  * [Linux - Ubuntu](https://www.howtoforge.com/tutorial/how-to-use-startup-applications-on-ubuntu/)
  * [Linux - other distros](https://www.simplified.guide/linux/automatically-run-program-on-startup)
* If you are using Linux Ubuntu and are comfortable with the command line, you can follow the systemd service setup guide featured in the next section.

### Creating a systemd service on Ubuntu

By creating a systemd file we can start Sia whenever the computer is booted instead of starting it manually. Run the following command to create a new systemd unit file:

```sh
$ sudo nano /etc/systemd/system/siad.service
```

Then, modify the following snippet to fit your host and then paste it into the file. You will want to change `asecurewalletpassword` to a more secure wallet password.

```
[Unit]
Description=siad
After=network.target

[Service]
Type=simple
ExecStart=/usr/local/bin/siad -M gctwh -d /home/ubuntu/siad
ExecStop=/usr/local/bin/siac stop
Restart=always
RestartSec=15
User=ubuntu 
Environment="SIA_WALLET_PASSWORD=asecurewalletpassword"
LimitNOFILE=900000

[Install]
WantedBy=multi-user.target
Alias=siad.service
```

```sh
$ sudo systemctl start siad
$ sudo systemctl enable siad
```

Your Sia node should now be running and accessible. You can try out a few commands to test it:

```sh
$ siac consensus
Synced: No
Height: 0
Progress (estimated): 0.0%
```

```sh
$ siac gateway
Address: localhost:9981
Active peers: 0
Max download speed: 0
Max upload speed: 0
```
