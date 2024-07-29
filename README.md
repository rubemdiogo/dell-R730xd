# dell-R730xd
Configure dell R730xd fam control


This tutorial works for Dell 10th, 12th, 13th and 14th Gen PowerEdge servers running iDRAC prior to v3.34.34.34, and most HPE ProLiant servers.

❌❌❌ DISCLAIMER ❌❌❌ By using these commands you consent to sole ownership of the results of usage of any of the listed commands or values. Understand what you're about to do before you do it. Point, read, type, read back what you typed.

❶ Download IPMI Tool from Dell's website...

Dell IPMI Tool Download: 
https://dl.dell.com/FOLDER06447028M/1...

❷ Install IPMI Tool to C:\ipmitool
❸ Log into iDRAC web interface and under Network enable IPMI.
❹ In Win search bar type "cmd" and right click Command Prompt and 'Run as Administrator'.
❺ Type: cd\
❻ Type: cd ipmitool
❼ You're now ready to start giving commands...

(I recommend opening up Notepad to type out the commands for simple copy/paste into IPMI Command Prompt. Go ahead and copy all of the commands here so you can just copy from a list.)

Replace 'ipaddress' with the IP address of your Dell iDRAC or HPE iLO. Replace 'username' and 'password' with your iDRAC or iLO login credentials. It's convenient to have the iDRAC or iLO web interface displaying the fan speeds to verify its actions as you submit the commands. The low refresh rate makes the reported speeds have a slight delay.

Executed from Command Prompt=

✅ Enable Manual Fan Control=   
ipmitool -I lanplus -H ipaddress -U username -P password raw 0x30 0x30 0x01 0x00

✅ Disable Manual Fan Control=    
ipmitool ... raw 0x30 0x30 0x01 0x01

✅ 3rd Party PCIe Response State (Fast  fan speed when no therm sensors on PCIe card)=    
ipmitool ... raw 0x30 0xce 0x01 0x16 0x05 0x00 0x00 0x00 
                    Result1= ... 00 00 00 (Enabled)
                    Result2= ... 01 00 00 (Disabled)

✅ Enable 3rd Party PCIe Response=   
ipmitool ... raw 0x30 0xce 0x00 0x16 0x05 0x00 0x00 0x00 0x05 0x00 0x00 0x00 0x00  

✅ Disable 3rd Party PCIe Response=    
ipmitool ... raw 0x30 0xce 0x00 0x16 0x05 0x00 0x00 0x00 0x05 0x00 0x01 0x00 0x00

✅ Set All Fans (0xff) to % (??) Speed (in Hexadecimal)=   
ipmitool ... raw 0x30 0x30 0x02 0xff 0x??

✅ Set All Fans (0xff) to 50% (0x32)=
ipmitool ... raw 0x30 0x30 0x02 0xff 0x32

🚩System fan #'s vary per chassis. Fan1 starts on the left side behind the Dell logo and can go up to 7 fans to the right side behind the Intel badge. The IPMI fan numbers are NOT the same as the Fan# labels on the chassis. Fan1=0x00, Fan2=0x01, Fan3=0x02, Fan4=0x03, Fan5=0x04, ect.🚩

✅ Set Fan1 (0x00) to 30%  (0x1E)=                   
ipmitool ... raw 0x30 0x30 0x02 0x00 0x1E

✅ Set Fan2 (0x01) to 30% (0x1E)=
ipmitool ... raw 0x30 0x30 0x02 0x01 0x1E

✅ Set Fan3 (0x02) to 30% (0x1E)
ipmitool ... raw 0x30 0x30 0x02 0x02 0x1E

☑ Percentages to Hexadecimal & Fan Speed (R720 example)
10% = 0xA
11% = 0xB
12% = 0xC
13% = 0xD
14% = 0xE
15% = 0xF
16% = 0x10 (~3,300 RPM)
17% = 0x11
18% = 0x12
19% = 0x13
20% = 0x14 (~3,900 RPM)
21% = 0x15 (~4,000 RPM)
22% = 0x16 (~4,200 RPM)
23% = 0x17 (~4,300 RPM)
24% = 0x18 (~4,400 RPM)
25% = 0x19 (~4,500 RPM)
26% = 0x1A (~4,700 RPM)
27% = 0x1B (~4,800 RPM)
28% = 0x1C (~5,000 RPM)
29% = 0x1D (~5,100 RPM) 
30% = 0x1E (~5,200 RPM)
31% = 0x1F (~5,400 RPM)
32% = 0x20 (~5,500 RPM)
33% = 0x21 (~5,700 RPM)
34% = 0x22 (~5,800 RPM) 
35% = 0x23 (~6,000 RPM)
36% = 0x24 (~6,100 RPM)
37% = 0x25 (~6,200 RPM)
38% = 0x26 (~6,300 RPM)
39% = 0x27 (~6,500 RPM)
40% = 0x28
41% = 0x29
42% = 0x2A
43% = 0x2B
44% = 0x2C
45% = 0x2D (~7,300 RPM)
46% = 0x2E
47% = 0x2F
48% = 0x30
49% = 0x31
50% = 0x32 (~8,000 RPM)
51% = 0x33
52% = 0x34
53% = 0x35
54% = 0x36
55% = 0x37
56% = 0x38
57% = 0x39
58% = 0x3A
59% = 0x3B
60% = 0x3C (~9,400 RPM)
61% = 0x3D
62% = 0x3E
63% = 0x3F
64% = 0x40
65% = 0x41
66% = 0x42
67% = 0x43
68% = 0x44
69% = 0x45
70% = 0x46 (~10,800 RPM)
71% = 0x47
72% = 0x48
73% = 0x49
74% = 0x4A
75% = 0x4B
76% = 0x4C
77% = 0x4D
78% = 0x4E
79% = 0x4F
80% = 0x50 (~12,100 RPM)
81% = 0x51
82% = 0x52
83% = 0x53
84% = 0x54
85% = 0x55
86% = 0x56
87% = 0x57
88% = 0x58
89% = 0x59
90% = 0x5A (~13,300 RPM)
91% = 0x5B
92% = 0x5C
93% = 0x5D
94% = 0x5E
95% = 0x5F
96% = 0x60
97% = 0x61
98% = 0x62
99% = 0x63
100% = 0x64 (15,000 RPM)

✅ Report Temperatures
ipmitool ... sdr type temperature

✅ Report Only Temp, Volt & Fan Sensors=    
ipmitool ... sdr elist full

✅ Report Power Supply Output
ipmitool ... sdr type ‘Power Supply’

✅ Displays Energy Consumption
ipmitool ... delloem powermonitor
