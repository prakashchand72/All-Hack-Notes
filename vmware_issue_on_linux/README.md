# *Cannot open /dev/vmmon: No such file or directory" error*

`1. Run This`
	
	sudo vmware-modconfig --console --install-all

`You'll see that there are issues with monitor and net, thas ok.`

`2. Generate Key`

	openssl req -new -x509 -newkey rsa:2048 -keyout VMWARE15.priv -outform DER -out VMWARE15.der -nodes -days 36500 -subj "/CN=VMWARE/"

`3. Use this key we just generated to sign the two kernel modules.`

	sudo /usr/src/linux-headers-$(uname -r)/scripts/sign-file sha256 ./VMWARE15.priv ./VMWARE15.der $(modinfo -n vmmon)
	sudo /usr/src/linux-headers-$(uname -r)/scripts/sign-file sha256 ./VMWARE15.priv ./VMWARE15.der $(modinfo -n vmnet)

`4. Check that signatures are applied correctly.`

	tail $(modinfo -n vmmon) | grep "Module signature appended"

`5. Now we make this key trusted by importing it to machine owner key (MOK) management system with the command below. Here you can read more about MOK’s job in Linux.`

	
	sudo mokutil --import VMWARE15.der

`6. REBOOT Your System`

	reboot

`7. Enroll the key a bois type of thing will appear`

`8. TO test that setup is done perfectly`

	mokutil --test-key VMWARE15.der

#Enjoy It's done
