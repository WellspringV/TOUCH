# TOUCH
Interface: Tunnel0
Profile: HQ1-HQ2-PROF
Session status: UP-ACTIVE
Peer: 77.34.141.141 port 500
  Session ID: 1
  IKEv2 SA: local 178.207.179.26/500 remote 77.34.141.141/500 Active
  IPSEC FLOW: permit 47 host 178.207.179.26 host 77.34.141.141
        Active SAs: 2, origin: crypto map


crypto ikev2 keyring HQ1-HQ2-KEY
 peer HQ2
  address 77.34.141.141
  pre-shared-key skills
 !
!
!
crypto ikev2 profile HQ1-HQ2-PROF
 match identity remote address 77.34.141.141 255.255.255.255
 authentication remote pre-share
 authentication local pre-share
 keyring local HQ1-HQ2-KEY
!
!
crypto ipsec security-association replay window-size 1024
!
crypto ipsec transform-set HQ1-HQ2-TS esp-aes 256 esp-sha-hmac
 mode transport
!
crypto ipsec profile HQ1-HQ2-IPSPR
 set transform-set HQ1-HQ2-TS
 set ikev2-profile HQ1-HQ2-PROF




interface Tunnel2
tunnel protection ipsec profile R1-R2-IPSPR
