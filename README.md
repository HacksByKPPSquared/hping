# 🚀 Reconnaissance with hping: Mastering Packet Crafting ⚙️

Welcome to the exciting world of **hping**, where packets fly, ports reveal their secrets, and networks tremble in fear! In this lab, we explore how to use **hping** as a network reconnaissance tool, employing it for everything from ICMP pings to sneaky port scans. So buckle up, because things are about to get packet-crafty! 😎

---

## 1️⃣ Using hping as an ICMP Utility 🛰️

We kick things off with the good ol’ **ICMP protocol**. Who needs basic pings when you can craft your own with **hping**?

1. **Launch the Kali VM** and log in as the superuser, aka root.  
   _Pro-tip: Don’t forget the iconic password—**toor**. It’s like "root" but backwards, because we’re clever like that._ 🧠

2. Open the terminal and let the packet-crafting magic begin. 🎩✨  
   Type the following command to send ICMP packets (essentially, custom pings) to our target at `192.168.68.12`:
   ```bash
   hping3 -1 192.168.68.12
   ```
   After about 6 packets, we hit CTRL+C to stop before we get carried away. ⚡

3. Now for something more exotic—**ICMP Type 13** (timestamp request). This is a bit fancier than your usual ping, so we added the verbose flag to show off the details:
   ```bash
   hping3 -1 --icmp-ts -c 3 192.168.68.12 -V
   ```
   Because who doesn't love timestamp pings? ⏱️

4. Feeling adventurous, we ran a **traceroute** using ICMP. It’s like a journey for packets, hopping through the network and waving hello at each stop!  
   ```bash
   hping3 --traceroute -1 192.168.68.12
   ```

---

## 2️⃣ Using hping for Port Scanning 🔍🔓

Why stop at ICMP when you can also scan for open ports? With **hping**, we can even control the flags in our TCP packets. Let’s knock on some doors and see which ports answer! 🚪

1. Fired up **tcpdump** to capture packets on the network. We need to watch those packets fly by! 👀  
   ```bash
   tcpdump -i eth0
   ```

2. Then, we sent a **SYN** packet to port 80 of our target (because, you know, web servers love port 80). This time we used port **5151** as our source because it’s more fun to pick random numbers:
   ```bash
   hping3 -S 192.168.68.12 -p 80 -s 5151
   ```
   Over in the tcpdump terminal, we noticed the **SYN** packet was sent, and a **Reset** flag came back—port 80 is up but not accepting our request. 😅

3. Now we got even more sneaky by targeting the **firewall** instead, sending another SYN packet. What would the firewall say to us? Reset, of course. Firewalls don’t like uninvited guests! 🚷  
   ```bash
   hping3 -S 192.168.68.12 -p 80
   ```

4. We tried our luck on **SSH port 22** next, just to see how the firewall would react. Spoiler: SSH is not amused. 🔐  
   ```bash
   hping3 -S 192.168.68.12 -p 22
   ```

5. Finally, we initiated a **port scan** over a range of ports—because why settle for one when you can scan them all? Let’s see what other treasures the network holds! 🗝️  
   ```bash
   hping3 -S 192.168.68.12 -p 1-100
   ```

---

## 🛠️ Tools of the Trade:

- **hping**: The Swiss Army knife of network tools, allowing us to craft and send custom packets. 🛠️  
- **tcpdump**: The eyes and ears on the network, capturing every packet we send. 👁️  
- **Kali Linux**: The ultimate platform for penetration testing and making us feel like network ninjas. 🐉

---

## 🌟 Why This Lab Matters:

Understanding how to use **hping** to craft custom packets and perform reconnaissance is crucial for any aspiring network security professional. It’s like having superpowers—you can explore, analyze, and gather intel on networks in ways that simple pings and scans can’t. Plus, it’s just plain fun! 😄

---

💡 **Pro-Tip**: Always, always make sure you have permission before performing any network scans or packet crafting. You don’t want to accidentally end up on the wrong side of a firewall... or worse, the law. 😬⚖️

---

Ready to explore the world of networks, one packet at a time? Let’s keep scanning, pinging, and learning! 🖥️🚀
## 👉🏾[Lab Walkthrough](https://github.com/Kpierre03/hping/blob/main/Reconnaissance.md)
