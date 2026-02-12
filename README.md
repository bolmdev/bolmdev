# ⚡ Terminal::bolmdev.sh

<p align="center">
  <img src="https://github-readme-stats.vercel.app/api?username=YOUR_USERNAME_HERE&show_icons=true&theme=tokyonight&hide_border=true&include_all_commits=true" alt="bolmdev stats" />
</p>

### 🛰️ Network Kernel & DNS Optimization
"Efficiency is not an option, it's a lifestyle." I specialize in squeezing every bit of performance out of the network stack.

- **Primary Resolver:** `1.1.1.1` (Cloudflare Warp Speed) 🚀
- **Secondary Resolver:** `8.8.8.8` (Google Public DNS) 🌐
- **Protocol:** DoH (DNS over HTTPS) for maximum privacy.
- **Current Latency Target:** `< 31ms` ⚡

---

### 💻 System & Creative Stack
| **Core Technology** | **Design & UI/UX** |
| :--- | :--- |
| ![Windows](https://img.shields.io/badge/Windows-0078D6?style=for-the-badge&logo=windows&logoColor=white) | ![Photoshop](https://img.shields.io/badge/Photoshop-31A8FF?style=for-the-badge&logo=adobe-photoshop&logoColor=white) |
| ![CMD](https://img.shields.io/badge/CMD-4D4D4D?style=for-the-badge&logo=windows-terminal&logoColor=white) | ![Figma](https://img.shields.io/badge/Figma-F24E1E?style=for-the-badge&logo=figma&logoColor=white) |
| ![PowerShell](https://img.shields.io/badge/PowerShell-5391FE?style=for-the-badge&logo=powershell&logoColor=white) | ![Canva](https://img.shields.io/badge/Canva-00C4CC?style=for-the-badge&logo=canva&logoColor=white) |

---

### ⌨️ Professional Scripting (CMD/PowerShell)
*Advanced scripts I use to maintain system peak performance:*

```powershell
# Turbocharge Network Stack
netsh int tcp set global autotuninglevel=experimental;
ipconfig /flushdns; 
netsh winsock reset;

# DNS Integrity Check
nslookup google.com 1.1.1.1
