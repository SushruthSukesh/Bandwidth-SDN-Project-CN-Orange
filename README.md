# 📊 Bandwidth Measurement and Analysis using SDN (Mininet + POX)

## 👤 Author

Sushruth Sukesh

---

# 🚀 Project Overview

This project analyzes how network topology and constraints affect bandwidth using Software Defined Networking (SDN).

The system is implemented using:

* **Mininet** (network emulator)
* **POX controller** (SDN control plane)
* **iperf** (bandwidth measurement)
* **Wireshark** (packet-level analysis)

---

# 🎯 Objectives

* Measure bandwidth across different network topologies
* Compare performance under normal and constrained conditions
* Demonstrate SDN-based network control
* Analyze packet-level behavior using Wireshark

---

# 🧩 Technologies Used

* Python (POX controller)
* Mininet
* OpenFlow Protocol
* iperf
* Wireshark

---

# ⚙️ Setup Instructions

## 1. Install Mininet

```bash
sudo apt update
sudo apt install mininet -y
```

## 2. Install POX Controller

```bash
git clone https://github.com/noxrepo/pox
cd pox
./pox.py
```

## 3. Install iperf

```bash
sudo apt install iperf -y
```

## 4. Install Wireshark

```bash
sudo add-apt-repository universe
sudo apt update
sudo apt install wireshark -y
```

---

# ▶️ Running the Project

## Step 1: Start POX Controller

```bash
cd ~/pox
./pox.py forwarding.l2_learning
```

## Step 2: Run Mininet Topologies

### Case 1: Single Topology (Normal)

```bash
sudo mn --controller=remote,ip=127.0.0.1,port=6633 --topo=single,2
```

### Case 2: Linear Topology (Normal)

```bash
sudo mn --controller=remote --topo=linear,3
```

### Case 3: Tree Topology (Normal)

```bash
sudo mn --controller=remote --topo=tree,depth=2,fanout=2
```

### Case 4: Single Topology (Limited)

```bash
sudo mn --controller=remote --topo=single,2 --link tc,bw=10,delay=5ms
```

### Case 5: Linear Topology (Limited)

```bash
sudo mn --controller=remote --topo=linear,3 --link tc,bw=10,delay=10ms
```

### Case 6: Tree Topology (Limited)

```bash
sudo mn --controller=remote --topo=tree,depth=2,fanout=2 --link tc,bw=10,delay=15ms
```

---

# 📡 Bandwidth Testing (iperf)

Inside Mininet CLI:

```bash
h1 iperf -s &
h2 iperf -c h1
```

For other topologies:

```bash
h3 iperf -c h1
h4 iperf -c h1
```

---

# 📊 Results

| Case | Topology | Condition | Bandwidth |
| ---- | -------- | --------- | --------- |
| 1    | Single   | Normal    | 22.2 Gbps |
| 2    | Linear   | Normal    | 21.8 Gbps |
| 3    | Tree     | Normal    | 21.0 Gbps |
| 4    | Single   | Limited   | 6.96 Mbps |
| 5    | Linear   | Limited   | 6.44 Mbps |
| 6    | Tree     | Limited   | 5.62 Mbps |

---

# 📉 Analysis

Bandwidth decreases as network complexity increases due to additional hops and switching delays. Under constrained conditions, bandwidth limitations and delay significantly reduce throughput, simulating real-world network performance.

Key Observations:

* Single topology gives highest bandwidth
* Linear topology introduces slight delay
* Tree topology shows lowest performance
* Constrained networks simulate real-world conditions

---

# 🔍 Wireshark Analysis

Wireshark was used to capture and analyze network traffic generated during iperf testing.

### Observations:

* TCP traffic observed between hosts (10.0.0.2 → 10.0.0.1)
* Continuous packet flow confirms active data transmission
* TCP retransmissions and duplicate acknowledgements observed
* Indicates network delay and congestion in simulated environment

### Filter Used:

```
ip.addr == 10.0.0.1 || ip.addr == 10.0.0.2
```

---

# 🧠 SDN Explanation

The POX controller manages network traffic using OpenFlow protocol. It dynamically installs flow rules based on incoming packets, enabling centralized control and efficient routing of traffic.

---

# 🎯 Conclusion

Bandwidth decreases with increasing network complexity and constraints, demonstrating the impact of topology and link conditions in SDN-based networks. SDN provides flexibility to control and optimize network performance dynamically.

---

# 📂 Repository Structure

```
Bandwidth-SDN-Project/
│── README.md
│── controller/
│   └── bandwidth_logger.py
│── results/
│   ├── screenshots/
│   └── outputs.txt
```

---

# ⭐ Future Work

* Implement QoS using SDN
* Use advanced controllers like Ryu
* Perform real-time traffic monitoring

---

# 📌 Notes

* Mininet shows high bandwidth due to virtualization
* Constrained experiments simulate realistic networks

---

🔥 Project Completed Successfully
