# SSH-SERVER-ON-SWITCH
!---
SW(config)#crypto key generate rsa
SW(config)#ip ssh pubkey-chain
SW(conf-ssh-pubkey)#username <user name>
SW(conf-ssh-pubkey-user)#key-string
SW(conf-ssh-pubkey-data)#key-hash ssh-rsa <key ID>
SW(conf-ssh-pubkey-data)#end

SW(config)#ip ssh port 2001 rotary 1
line 1 16
   no exec
   rotary 1
   transport input ssh
   exec-timeout 0 0
   modem InOut
   stopbits 1

!---Restrict SSH on a subnet.

SW(config)#access-list 23 permit 10.10.10.0 0.0.0.255
SW(config)#line vty 5 15
SW(config-line)#transport input ssh
SW(config-line)#access-class 23 in
SW(config-line)#exit

SW(config)#ip ssh version 2

SW#show ssh
