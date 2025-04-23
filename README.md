1. Amplitude Shift Keying (ASK) using Python
Tool: Scilab
```sci
clc;
bits = [1 0 1 1];
f = 5; fs = 1000;
t = linspace(0, 1, fs);
ask = [];

for i = 1:length(bits)
    if bits(i) == 1 then
        signal = cos(2*%pi*f*t);
    else
        signal = zeros(1, length(t));
    end
    ask = [ask, signal];
end

plot(ask); xtitle("ASK Modulated Signal");
```
output:
![image](https://github.com/user-attachments/assets/1af81a2a-27e1-4b83-aeeb-382bf4b7d4f6)

or python
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

2. Crimping a Straight Cable (Universal Color Code)

Standard Color Order (EIA-568B – Both Ends):

1. White-Orange  
2. Orange  
3. White-Green  
4. Blue  
5. White-Blue  
6. Green  
7. White-Brown  
8. Brown

Tools: RJ-45 Connectors, Crimping Tool, Cable Tester
Steps:
Strip cable → Arrange wires in order → Insert into RJ-45 → Crimp → Test.



---

3. Time Division Multiplexing (TDM) – Python Simulation

Tool: MATLAB / Scilab
Concept: Combine multiple signals by allocating time slots.
```sci
clc;
t = linspace(0, 1, 500);
s1 = sin(2*%pi*5*t);
s2 = cos(2*%pi*5*t);

tdm = zeros(1, length(t));
for i = 1:length(t)
    if modulo(i, 2) == 0 then
        tdm(i) = s1(i);
    else
        tdm(i) = s2(i);
    end
end

plot(t, tdm); xtitle("Time Division Multiplexed Signal");

```
output:
![image](https://github.com/user-attachments/assets/d5da80ac-6b5e-454e-884e-2f80a224e957)

or python
```python
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

4. Create a Hybrid Network using Bluetooth

Hybrid Setup Example:
Laptop connected to WiFi (Internet)
Bluetooth-connected speaker/mouse
Devices form a Hybrid (WiFi + Bluetooth) Network

No code needed. Configure in Settings → Network & Bluetooth.


---

5. Wireshark – Capture IP, TELNET, FTP Packets

Steps:
Open Wireshark → Start capture

Use filters:
IP: ip
TELNET: tcp.port == 23
FTP: tcp.port == 21

Use FTP/TELNET client to generate packets



---

6. Capture TCP and UDP Packets with Wireshark

Filters:
TCP: tcp
UDP: udp

Steps:

Start Wireshark
Run browser, ping, etc.
Use filters to isolate packet types


---

7. Install Operating System (Linux/Windows)

Steps:

Download ISO (Ubuntu, Windows)

Create bootable USB (Rufus/Etcher)

Boot from USB → Follow installation wizard

Setup hostname, partitions, and users


---

8. Visit Computer Lab

a) Topology: Star

b) Devices: Switch (D-Link), Router (TP-Link)

c) Cables: Cat5e/Cat6 – RJ-45

d) Applications: Chrome, VS Code, Packet Tracer

e) Layout: Sketch a star layout with Switch in center, PCs around



---

9. Implement Wireless Network

Steps:
Use WiFi Router → Enable DHCP
Connect laptop/phones
Check via ipconfig / ifconfig

Optional Testing:
Ping router IP
Access shared files via SMB


---

10. CRC Error Detection – C Code
```c
#include <stdio.h>
#include <string.h>
void xor(char *a, char *b, int n) {
  for (int i = 1; i < n; i++) a[i] = (a[i] == b[i]) ? '0' : '1';
}
void crc(char *data, char *key, char *rem) {
  char temp[50]; int k = strlen(key);
  strcpy(temp, data); strcat(temp, "000");
  strncpy(rem, temp, k);
  for (int i = 0; i < strlen(data); i++) {
    if (rem[0] == '1') xor(rem, key, k);
    memmove(rem, rem+1, k-1); rem[k-1] = temp[i+k];
  }
}
int main() {
  char data[50], key[20], rem[20];
  printf("Data: "); scanf("%s", data);
  printf("Key: "); scanf("%s", key);
  crc(data, key, rem); printf("CRC: %s\n", rem);
}
```

---

11. Hamming Code – C Code
```c
#include <stdio.h>
int main() {
  int d[8], h[12]={0};
  printf("Enter 8 bits: ");
  for (int i=0; i<8; i++) scanf("%d", &d[i]);

  h[2]=d[0]; h[4]=d[1]; h[5]=d[2]; h[6]=d[3];
  h[8]=d[4]; h[9]=d[5]; h[10]=d[6]; h[11]=d[7];

  h[0]=h[2]^h[4]^h[6]^h[8]^h[10];
  h[1]=h[2]^h[5]^h[6]^h[9]^h[10];
  h[3]=h[4]^h[5]^h[6]^h[11];
  h[7]=h[8]^h[9]^h[10]^h[11];

  printf("Hamming: ");
  for (int i=0; i<12; i++) printf("%d", h[i]);
}
```
