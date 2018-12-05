#### Virtual Box虚拟机修复

1. 虚拟机启动列表读取的文件位置: C:\Users\colter\\.VirtualBox\VirtaulBox.xml

2. 编辑文件,MachineRegistry保存的是虚拟机的列表， SystemProperties保存的是位置。

   ```xml
   <MachineRegistry>
         <MachineEntry uuid="{2468b73e-c4c6-42b5-a12e-5a7be1fd6ded}" src="F:\VirtualBox VMs\Arch Linux\Arch Linux.vbox"/>
         <MachineEntry uuid="{226fb1eb-2fb4-409e-91c8-8419fc12591b}" src="F:\VirtualBox VMs\ElementaryOS\ElementaryOS.vbox"/>
         <MachineEntry uuid="{bec06928-47d3-46ea-847e-e614318a943b}" src="F:\VirtualBox VMs\Linux Mint\Linux Mint.vbox"/>
         <MachineEntry uuid="{04458f0c-6e12-4ec2-ab35-2b91a92f7fd5}" src="F:\VirtualBox VMs\Lubuntu\Lubuntu.vbox"/>
         <MachineEntry uuid="{fdfb22f7-f812-43e1-8562-f1e59a2be608}" src="F:\VirtualBox VMs\Manjaro\Manjaro.vbox"/>
         <MachineEntry uuid="{70f9aa55-9b9b-468d-93d3-6c07c787364b}" src="F:\VirtualBox VMs\Mint\Mint.vbox"/>
         <MachineEntry uuid="{1cc1925d-71ed-44fc-b499-0c9388c9af32}" src="F:\VirtualBox VMs\Xubuntu\Xubuntu.vbox"/>
       </MachineRegistry>
       
       
       <SystemProperties defaultMachineFolder="F:\VirtualBox VMs" defaultHardDiskFormat="VDI" VRDEAuthLibrary="VBoxAuth" webServiceAuthLibrary="VBoxAuth" LogHistoryCount="3" exclusiveHwVirt="false"/>	
   ```

3. 上一步的uuid如果不正确，打开Virtual Box。列表中的虚拟机都打不开，选中其中一个，然后你会发现一行错误。(uuid如果格式不正确，需要先改成上边这样，然后就能正常打开虚拟机)

   ```txt
   Machine UUID {1cc1925d-71ed-44fc-b499-0c9388c9af32} in 'F:\VirtualBox VMs\Xubuntu\Xubuntu.vbox' doesn't match its UUID {1cc1925d-71ed-44fc-b499-0c9388c9af12} in the registry file 'C:\Users\colter\.VirtualBox\VirtualBox.xml'.
   ```

4. 看到上边的报错，那么把上边的uuid（1cc1925d-71ed-44fc-b499-0c9388c9af32）复制替换 上边的xml文件的uuid，就可以正常启动了。