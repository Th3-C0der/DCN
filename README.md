DCN PRACTICAL EXAM – QUICK SOLUTIONS


---

1. ASK Modulation using Python
```python
import numpy as np
import matplotlib.pyplot as plt

bit_stream = [1, 0, 1, 1, 0, 0, 1]
T = 1  # bit duration
fs = 1000
t = np.linspace(0, T, fs)
f = 5  # carrier frequency

ask_signal = []
for bit in bit_stream:
    if bit == 1:
        ask_signal.extend(np.cos(2 * np.pi * f * t))
    else:
        ask_signal.extend(np.zeros_like(t))

plt.plot(np.linspace(0, len(bit_stream), len(ask_signal)), ask_signal)
plt.title("ASK Modulation")
plt.xlabel("Time")
plt.ylabel("Amplitude")
plt.grid()
plt.show()
```

---

2. Crimping Straight Cable (EIA-568B Order)

Wire color order (both ends):

1. White-Orange  
2. Orange  
3. White-Green  
4. Blue  
5. White-Blue  
6. Green  
7. White-Brown  
8. Brown

Use: Crimping tool + RJ-45 + Cable tester.


---

3. TDM Signal Simulation (Python)
```python
import numpy as np, matplotlib.pyplot as plt
import numpy as np
import matplotlib.pyplot as plt

t = np.linspace(0, 1, 500)
signal1 = np.sin(2 * np.pi * 5 * t)
signal2 = np.cos(2 * np.pi * 5 * t)
tdm = []

for i in range(len(t)):
    if i % 2 == 0:
        tdm.append(signal1[i])
    else:
        tdm.append(signal2[i])

plt.plot(t, tdm)
plt.title("TDM Signal")
plt.show()
```

---

4. Hybrid Network (Bluetooth + WiFi)

Connect phone/laptop to Wi-Fi.

Connect Bluetooth devices (printer/headset).

Hybrid network = WLAN + PAN.



---

5. Wireshark: Capture IP, TELNET, FTP

Filters:

IP: ip

TELNET: tcp.port == 23

FTP: tcp.port == 21


Generate traffic via browser/TELNET/FTP client.



---

6. Capture TCP & UDP Packets in Wireshark

Use Filters:

TCP: tcp

UDP: udp




---

7. OS Installation

Download ISO (Ubuntu/Windows Server)

Make bootable USB (e.g., Rufus)

Boot & install, setup user/network



---

8. Computer Lab Survey

a) Topology: Likely Star

b) Devices: Switch, Router (TP-Link, etc.)

c) Cables: Cat5e/Cat6, RJ-45

d) Applications: Browsers, IDEs, Simulators

e) Sketch layout showing PC, switch, router



---

9. Implement Wireless Network

Setup router → Enable SSID/password

Connect devices → Check with ipconfig/ifconfig



---

10. CRC Error Detection (C)
```c
#include<stdio.h>
void xor(char *a, char *b, int len){ for(int i=1;i<len;i++) a[i]=a[i]==b[i]?'0':'1'; }
void crc(char *ip, char *key, char *rem){
  char temp[50]; int k=strlen(key);
  strcpy(temp, ip); strcat(temp, "000");
  strncpy(rem, temp, k);
  for(int i=0; i<strlen(ip); i++) {
    if(rem[0]=='1') xor(rem,key,k);
    for(int j=0;j<k-1;j++) rem[j]=rem[j+1];
    rem[k-1]=temp[i+k];
  }
}
int main(){
  char ip[50], key[20], rem[20];
  printf("Enter data: "); scanf("%s", ip);
  printf("Enter key: "); scanf("%s", key);
  crc(ip, key, rem);
  printf("CRC: %s\n", rem);
}
```


---

11. Hamming Code (C)
```c
#include<stdio.h>
int main(){
  int d[8], h[12]={0};
  printf("Enter 8 bits: "); for(int i=0;i<8;i++) scanf("%d", &d[i]);

  h[2]=d[0]; h[4]=d[1]; h[5]=d[2]; h[6]=d[3];
  h[8]=d[4]; h[9]=d[5]; h[10]=d[6]; h[11]=d[7];

  h[0]=h[2]^h[4]^h[6]^h[8]^h[10];
  h[1]=h[2]^h[5]^h[6]^h[9]^h[10];
  h[3]=h[4]^h[5]^h[6]^h[11];
  h[7]=h[8]^h[9]^h[10]^h[11];

  printf("Hamming Code: ");
  for(int i=0;i<12;i++) printf("%d", h[i]);
}
```
