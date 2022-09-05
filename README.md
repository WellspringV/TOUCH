# TOUCH
Check
crypto ikev2 keyring R1-R2-KEY
 peer HQ2
  address 0.0.0.0 0.0.0.0
  pre-shared-key Cisco123

crypto ikev2 profile R1-R2-PROF
 match identity remote address 0.0.0.0 
 authentication remote pre-share
 authentication local pre-share
 keyring local HQ1-HQ2-KEY


crypto ipsec security-association replay window-size 1024
     
crypto ipsec transform-set HQ1-HQ2-TS esp-aes 256 esp-sha-hmac 
 mode transport

crypto ipsec profile R1-R2-IPSPR
 set transform-set R1-R2-TS 
 set ikev2-profile R1-R2-PROF



interface Tunnel2
tunnel protection ipsec profile R1-R2-IPSPR
