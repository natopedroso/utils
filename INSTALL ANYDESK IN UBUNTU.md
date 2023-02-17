Open the terminal on your Ubuntu machine.
Run the following command to add the AnyDesk repository to your system:
```
echo "deb http://deb.anydesk.com/ all main" | sudo tee /etc/apt/sources.list.d/anydesk-stable.list
```
Import the AnyDesk GPG key using the following command:
```
wget -qO - https://keys.anydesk.com/repos/DEB-GPG-KEY | sudo apt-key add -
```
Update the package list using the following command:
```
sudo apt update
```
Finally, install AnyDesk using the following command:
```
sudo apt install anydesk
```
After completing these steps, AnyDesk should be installed on your Ubuntu machine and ready to use. You can launch it using the command "anydesk" in the terminal or by searching for it in the applications menu.

To set password
```
anydesk --set-password <password>
```

You can get the AnyDesk ID of the current machine using the terminal by running the following command:
```
anydesk --get-id
```
This will display the AnyDesk ID of the current machine in the terminal output. Note that AnyDesk must be installed and running on the machine in order for this command to work.
