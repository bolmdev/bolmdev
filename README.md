<p align="center">
  <img src="https://images2.imgbox.com/96/a8/THkokCjt_o.png" alt="DNS Logo" width="220" />
  <br/>
  <img src="https://images2.imgbox.com/3b/7d/QEI3091q_o.png" alt="Profile Avatar" width="120" />
</p>

# BOLMDEV — Personal Tech Lab

**Technology enthusiast lab: practical notes on DNS, basic Windows network tuning, and safe experimentation.**  
This repository is a personal learning project (experimental). Not intended as production infrastructure.

---

## Table of Contents

- [About](#about)
- [Project Goals](#project-goals)
- [DNS Resolver Reference](#dns-resolver-reference)
- [PowerShell Test Script](#powershell-test-script)
- [How to Test](#how-to-test)
- [Rollback & Safety](#rollback--safety)
- [Contributing](#contributing)
- [License & Contact](#license--contact)

---

## About

This README contains compact, actionable guidance to experiment with DNS configuration and minimal Windows network adjustments. The content is intentionally concise, easy to audit, and reversible.

**Audience:** learners, hobbyists, and engineers who want a safe place to experiment.  
**Status:** Experimental / Learning

---

## Project Goals

- Document practical DNS choices and use cases.
- Provide a small, auditable PowerShell snippet to test tweaks locally.
- Emphasize safety, rollback, and reproducibility.
- Keep the documentation minimal and developer-friendly.

---

## DNS Resolver Reference

Choose a primary + secondary resolver pair depending on your objective:

| Provider     | Primary IP       | Secondary IP      | Use Case                                 |
|--------------|------------------|-------------------|-------------------------------------------|
| Cloudflare   | `1.1.1.1`        | `1.0.0.1`         | Low latency, privacy-focused              |
| Google DNS   | `8.8.8.8`        | `8.8.4.4`         | Wide availability and reliability         |
| AdGuard DNS  | `94.140.14.14`   | `94.140.15.15`    | Blocking ads & trackers at DNS level      |
| OpenDNS      | `208.67.222.222` | `208.67.220.220`  | Policy/filtering for managed environments |

**Recommendation:** Test a pair on one machine first. Keep notes of previous settings.

---

## PowerShell Test Script

> **Run only on a personal/test machine.** Open PowerShell **as Administrator**. Review the code before executing.

```powershell
<#
  BOLMDEV: Set-TurboMode
  Purpose: Minimal, reversible network adjustments (TCP autotuning + DNS)
  Usage: Paste into an elevated PowerShell session and run Set-TurboMode
#>

function Set-TurboMode {
    [CmdletBinding()]
    param(
        [string[]] $DnsServers = @('1.1.1.1','8.8.8.8')
    )

    Write-Host "[*] BOLMDEV: Starting network adjustments..." -ForegroundColor Green

    try {
        # 1) TCP autotuning (non-destructive; reversible)
        netsh int tcp set global autotuninglevel=experimental | Out-Null

        # 2) Enable RSS if available (non-destructive)
        netsh int tcp set global rss=enabled | Out-Null

        # 3) Set DNS servers for all active physical adapters
        $adapters = Get-NetAdapter -Physical | Where-Object {$_.Status -eq 'Up'}
        foreach ($a in $adapters) {
            try {
                Set-DnsClientServerAddress -InterfaceIndex $a.ifIndex -ServerAddresses $DnsServers -ErrorAction Stop
                Write-Host "  [+] Adapter '$($a.Name)' -> $($DnsServers -join ', ')" -ForegroundColor Yellow
            } catch {
                Write-Warning "  [!] Could not update adapter '$($a.Name)': $_"
            }
        }

        # 4) Flush caches to apply changes immediately
        ipconfig /flushdns | Out-Null
        netsh winsock reset | Out-Null

        Write-Host "[✓] BOLMDEV: Adjustments applied. Reboot recommended for full effect." -ForegroundColor Green
    } catch {
        Write-Error "[!] BOLMDEV: Error during adjustments: $_"
    }
}
Example usage

# Run in elevated PowerShell
Set-TurboMode -DnsServers @('1.1.1.1','8.8.8.8')

How to Test

DNS resolution

Resolve-DnsName example.com


Latency check

ping -n 6 1.1.1.1


Application & browser checks

Open several sites and verify they load normally.

Confirm no captive portal or ISP DNS interception issues.

Rollback & Safety

Rollback DNS to automatic (DHCP):

Get-NetAdapter -Physical | Where-Object {$_.Status -eq 'Up'} | ForEach-Object {
  Set-DnsClientServerAddress -InterfaceIndex $_.ifIndex -ResetServerAddresses
}


Notes

Do not run untrusted scripts.

Keep a short runbook: note current DNS settings before changes.

Test on one machine or a small test group before wider rollout.

Some driver-level features (e.g., RSS) require NIC and driver support.

Contributing

Small, well-documented changes are welcome. Suggested workflow:

Fork the repository.

Create a feature branch: git checkout -b feature/your-change.

Submit a concise PR with testing notes.

License & Contact

License: MIT (or replace with your preferred license).

Maintainer: BOLMDEV — open an issue for questions or improvements.

This README is intentionally minimal and follows common open-source conventions for clarity and easy adoption.


