### General informations

Since Flatcar Linux official ISO cannot be booted on an UEFI board, you have to find a workaround to install it on bare-metal.

The idea here is to include the official Flatcar install script into the ISO using SystemRescue SRM feature with a small Ignition wrapper file to retrieve the final Ignition remotely at installation time.

More informations about SystemRescue SRM modules: https://www.system-rescue.org/Modules/

### How-to

* Unpack SystemRescue ISO:
  ```shell
  ./bin/sysrescue-customize --unpack --source systemrescue-12.01-amd64.iso --dest systemrescue/
  ```
* Edit the `srm/` folder according to your needs (e.g add other tools, scripts, files...)
* Rebuild the ISO to include the SRM:
  ```shell
  ./bin/sysrescue-customize --rebuild --srm-dir srm/ --source systemrescue/ --dest systemrescue-custom.iso --overwrite
  ```
* Boot into the custom SystemRescue ISO and then install Flatcar:
  ```shell
  flatcar-install -d <device> -C <channel> -i /usr/share/flatcar/ignition.json
  ```
* And voilà !

> [!NOTE]
> More informations about scripts used here:
> - https://www.system-rescue.org/scripts/sysrescue-customize/
> - https://www.flatcar.org/docs/latest/installing/bare-metal/installing-to-disk/

### References

- Flatcar Linux: https://www.flatcar.org/
- SystemRescue: https://www.system-rescue.org/