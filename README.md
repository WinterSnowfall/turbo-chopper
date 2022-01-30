# turbo-chopper
Sample SysVInit service scripts that disable turbo boost on all Intel CPUs using intel\_pstate (Sandy Bridge and later). Will, for obvious reasons, only work on Linux. A sample script is also provided on how to further limit the max frequency of an Intel cpu below that of its base clock, using intel\_pstate frequency limits.

## How to use the scripts?

The scripts are written with Ubuntu in mind, but should work on any Linux distro as long as something in the likes of **systemd-sysv-generator** is used either manually or automagically to convert them to systemd services. Copying the scripts in the */etc/init.d* directory and running:
```
update-rc.d turbo-chopper defaults
service turbo-chopper start
```

will enable the services to run on boot. The above steps are sufficient on the latest Ubuntu LTS.

## What does turbo-chopper-freq do?

Same thing as turbo-chopper with additional enforcing of max frequency limits on all CPU cores. You'll need to replace the frequency levels (in Hz) provided in the script with your desired target max frequency & your CPU’s maximum boost frequency, which will be restored once the service is stopped. Note that the desired max frequency needs to be below the base clock in this case, though it is possible to use the script as a simple frequency limiter as well (beyond base frequency), by commenting out the turbo boost limitation.

## How are these scripts useful?

They provide a quick way to keep an Intel CPU within a lower thermal envelope and ensure it draws power around its specced wattage.

## Disclaimer
I've only tested these scripts on the following Intel CPUs: i7-7700, i7-8559U, i7-8705G, i5-1135G7. That being said all Intel CPUs later than Sandy Bridge should work, as long as intel_pstate is used by the Linux kernel. The scripts will **NOT** work on AMD CPUs, or any other vendors except Intel.

