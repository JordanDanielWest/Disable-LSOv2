## 🛠️ Issue: Severely Reduced Upload Speed on Windows (0.6 Mbps)

**Problem:**  
A Windows PC was experiencing extremely low upload speeds (~0.6 Mbps) despite a 1 Gbps connection and using the same Ethernet cable and switch as another PC that had normal performance (~40 Mbps upload). The issue persisted across restarts, driver updates, and cable swaps.

**Root Cause:**  
The culprit was **Large Send Offload v2 (LSO v2)** — a network adapter feature that offloads packet segmentation to the NIC. Some adapters or drivers handle this poorly, especially during uploads, leading to throttled performance.

---

## ✅ Solution: Disable LSO v2 (IPv4 and IPv6)

Disabling **LSO v2** for both **IPv4** and **IPv6** on the affected Ethernet adapter restored normal upload speeds instantly.

LSO can wreck upload speeds for some systems.

    Open Device Manager → Network Adapters → Right-click your Ethernet adapter → Properties

    Go to the Advanced tab

    Find and disable the following if present:

        Large Send Offload v2 (IPv4)

        Large Send Offload v2 (IPv6)

Click OK, reboot, and retest.

> 📌 You can use the included `Disable-LSOv2.ps1` PowerShell script to apply this fix automatically across all Ethernet adapters.
