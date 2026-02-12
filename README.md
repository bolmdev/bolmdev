<div align="center">

<div style="position: relative; width: 160px; height: 160px;">
  <div style="position: absolute; width: 100%; height: 100%; border-radius: 50%; border: 4px solid #20C20E; box-shadow: 0 0 15px #20C20E, inset 0 0 15px #20C20E; animation: pulse 2s infinite alternate;"></div>
  <img src="https://images2.imgbox.com/3b/7d/QEI3091q_o.png" width="150" style="border-radius: 50%; padding: 5px; z-index: 10; position: relative;" alt="bolmdev" />
</div>

<style>
@keyframes pulse {
  0% { box-shadow: 0 0 10px #20C20E, inset 0 0 10px #20C20E; transform: rotate(0deg); }
  100% { box-shadow: 0 0 30px #20C20E, inset 0 0 20px #20C20E; transform: rotate(360deg); }
}
</style>

# 🟢 BOLMDEV: DNS ARCHITECT & PERFORMANCE ENGINEER
> **"السرعة ليست خياراً، بل هي حق مشروع لكل مستخدم"**

---

### 🌐 دليل الـ DNS الشامل (للمحترفين والمبتدئين)
الـ DNS هو "مترجم" الويب. بلاصت ما تحفظ أرقام IP معقدة، هو كيرد ليك `google.com` لـ عنوان رقمي. هادو هما "العمالقة" لي كنخدمو بيهم:

| Provider | DNS Primary | DNS Secondary | Speciality |
| :--- | :--- | :--- | :--- |
| **Cloudflare** | `1.1.1.1` | `1.0.0.1` | الأسرع عالمياً + الخصوصية ⚡ |
| **Google** | `8.8.8.8` | `8.8.4.4` | الأكثر استقراراً 🌍 |
| **OpenDNS** | `208.67.222.222` | `208.67.220.220` | الحماية من المواقع الضارة 🛡️ |
| **AdGuard** | `94.140.14.14` | `94.140.15.15` | قطع الإعلانات من الجدر 🚫 |

---

### 🛠️ سكريبت "النيترو" الخارق (PowerShell Optimization)
هاد السكريبت كيدير 3 ديال الحوايج فدقة وحدة: كيمسح الكاش، كيبدل الـ DNS لـ Cloudflare، وكيفعل تقنيات تسريع TCP فـ قلب الويندوز.

```powershell
# 🚀 Run as Administrator for God-Mode Speed
Write-Host "--- Initializing System Warp Speed ---" -ForegroundColor Cyan
# 1. تخصيص الـ DNS لجميع كروت الشبكة
Get-NetAdapter | Where-Object {$_.Status -eq "Up"} | Set-DnsClientServerAddress -ServerAddresses ("1.1.1.1", "8.8.8.8")
# 2. تفعيل بروتوكول التسريع Experimental
netsh int tcp set global autotuninglevel=experimental
# 3. تنظيف شامل للعوائق
ipconfig /flushdns; nbtstat -R; nbtstat -RR; netsh int ip reset; netsh winsock reset
Write-Host "--- System Optimized by BolmDev ---" -ForegroundColor Green
