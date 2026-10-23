# WorldFIPForge Pro (v1.0.0)

**WorldFIP (EN 50170-3 / IEC 61158-6 / NFC 46-602) Protocol Studio, Bus Arbitrator (BA) Macrocycle Scheduler, 150-Ohm Physical Sizer, & 10-Point Critical Safety Auditor**

---

## ⚡ Overview

**WorldFIPForge Pro** is a mission-critical fieldbus protocol engineering suite specifically targeted at **WorldFIP (EN 50170-3 / IEC 61158-6 / NFC 46-602)** real-time industrial networks (Alstom TGV high-speed rail, EDF nuclear reactor instrumentation, CERN Large Hadron Collider). It delivers zero-dependency, browser-based, and command-line automation for:

1. **Producer-Consumer-Distributor (PCD) Physical Frame Engine**: Models Manchester Biphase-L signaling, 0x1E Start Delimiter, 0xE1 End Delimiter, CCITT-False CRC-16 Frame Check Sequences (\$x^{16} \+ x^{12} \+ x^5 \+ 1\$), ID\_DAT question broadcasts, and RP\_DAT producer response frames with PDU status decoding.  
2. **Bus Arbitrator (BA) Macrocycle Scheduler**: Automatically sequences Elementary Cycles (EC) to guarantee jitter-free cyclic variable delivery while preserving balanced aperiodic Pass Token windows (\$\\ge 20%\$) for diagnostic traffic.  
3. **150-Ohm Physical Sizer & Line Budget Engine**: Models cable propagation delay (5.0 ns/m), trunk lengths, drop branch constraints (\$10\\text{m}\$ max at 1.0 Mbps, \$5\\text{m}\$ max at 2.5 Mbps), and attenuation across 31.25k, 1.0M, 2.5M, and 5.0M profiles.  
4. **10-Point Critical Safety Auditor**: Pre-flight verification checking 16-bit VarID collisions, single-producer PCD compliance, dual 150-ohm line terminators, elementary cycle periodic overruns, 32-station transceiver limits, and Redundant BA readiness.  
5. **Multi-Target Exporter**: Outputs Alstom Agate Train Control Variable CSV tables, MicroFIP / FullFIP C header definitions (`.h`), and Python 3 Bus Arbitrator simulation scripts.

---

## 📁 Repository Structure

product\_198/

├── source-code/

│   ├── worldfip-engine.js           \# PCD framing, delimiters, CRC-16, ID\_DAT/RP\_DAT

│   ├── worldfip-scheduler.js        \# Bus Arbitrator Elementary Cycle & Macrocycle math

│   ├── worldfip-physical-sizer.js   \# 150-ohm cable attenuation & line delay engine

│   ├── worldfip-auditor.js          \# 10-Point safety auditor engine

│   ├── worldfip-forge.css           \# French TGV rail blue/red dark UI theme

│   ├── app.js                       \# Interactive web controller

│   └── index.html                   \# Responsive 5-tab web studio

├── build/

│   ├── worldfip-cli.py              \# Standalone Python CLI executable (chmod \+x)

│   └── worldfipforge-pro-v1.0.0.zip \# Production release archive

├── documentation/

│   ├── ARCHITECTURE.md              \# Engineering specification & protocol mathematics

│   ├── USER\_GUIDE.md                \# Operator manual & CLI instructions

│   ├── MONETIZATION\_AND\_MARKETING\_PLAYBOOK.md \# Commercial strategy & pricing tiers

│   └── PROGRESS\_REPORT.md           \# Cycle \#198 milestone report

├── screenshots/

│   └── worldfip-studio-preview.svg  \# High-resolution SVG preview diagram

└── README.md                        \# Master product documentation

---

## 🚀 Quick Start

### 1\. Launch Interactive Web Studio

Open `product_198/source-code/index.html` in any web browser. Zero server, node packages, or build steps required.

### 2\. Standalone Python CLI Usage

\# Make CLI executable

chmod \+x product\_198/build/worldfip-cli.py

\# Build an ID\_DAT Bus Arbitrator Question Frame for Variable 0x1001

./product\_198/build/worldfip-cli.py id-dat \--var 0x1001

\# Build an RP\_DAT Producer Data Frame for Variable 0x1001

./product\_198/build/worldfip-cli.py rp-dat \--var 0x1001 \--status 0x00

\# Dissect a raw WorldFIP hex frame

./product\_198/build/worldfip-cli.py dissect "55 55 1E 03 10 01 79 61 E1"

\# Calculate Bus Arbitrator Macrocycle schedule

./product\_198/build/worldfip-cli.py schedule \--vars '\[{"id":4097,"bytes":4},{"id":4098,"bytes":4}\]' \--ec 10 \--baud 1000

\# Run 10-Point Safety Auditor

./product\_198/build/worldfip-cli.py audit \--vars '\[{"id":4097,"bytes":4},{"id":4098,"bytes":4}\]' \--stations '\[{"name":"Cab A","drop":2.5,"ba":true},{"name":"Traction 1","drop":4.0}\]' \--trunk 600 \--speed 1000

---

## 🧪 Verification & Automated Testing

The engine has been tested against 10 comprehensive unit tests:

python3 test\_worldfipforge.py

\# Output: Ran 10 tests in 0.638s \- OK

---

## 💼 Commercial & Pricing Model

- **Community Edition**: Free / Open Source (ID\_DAT / RP\_DAT Frame Builder, Basic Scheduler, Web UI).  
- **Professional License**: \$299 one-time per engineer seat (Elementary Cycle Macrocycle Sizer, 10-Point Safety Auditor, Python CLI, Alstom CSV & C Header Exporters).  
- **Enterprise / Fleet License**: \$2,890 / facility / year (Site-wide license, automated CI/CD schedule verification hooks, MicroFIP/FullFIP profile customization, priority support).