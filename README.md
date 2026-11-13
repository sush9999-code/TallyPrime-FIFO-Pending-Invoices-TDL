# TallyPrime FIFO Pending Invoices Report (`SPD_Pending.tdl`)

A lightweight, **100% read-only** TallyPrime TDL add-on that adds a **Pending Invoices** report directly inside **Ledger Vouchers** (`Ctrl + Alt + D`).

Unlike Tally's default *Bills Receivable / Outstandings* report, this TDL calculates pending invoices using **strict FIFO (First-In, First-Out)** purely from ledger voucher entries—meaning **it works identically whether "Maintain balances bill-by-bill" is enabled or disabled**, and works even when receipts are entered *On Account* or without bill references.

---

## Key Features

- **Bill-by-Bill Independent (Pure FIFO):** Settles oldest invoices first against net receipts (`Receipts + Credit Notes - Cheque Bounces`), without touching or requiring bill allocations.
- **Cheque Bounce Safe:** Bounced cheque entries (e.g., `Payment` or `Journal` debiting the party) automatically reduce net receipts and reopen the corresponding unpaid invoices instead of appearing as fake invoices.
- **Smart Default Compact View (`Ctrl + Alt + D`):** Automatically scans from the beginning of the Financial Year (`1-Apr`) regardless of any short period selected in Ledger Vouchers, displaying **at most the last 3 fully-paid invoices** for quick context, followed by **all partially-paid and unpaid invoices**.
- **Unpaid Opening Balance Alert:** Automatically stays hidden when the Opening Balance is cleared, and displays an **`OLD BILLS! — Opening (Unpaid)`** alert row only if the opening balance itself remains unpaid.
- **Built-in Tie-Out Check:** The bottom **`Total Pending`** line always equals the ledger's exact **Closing Balance (`Dr/Cr`)**.
- **Party-Friendly Screenshot Mode + Secret `F8` Toggle:**
  - By default, the **`Knocked Off in Days`** column is hidden (and its shortcut is hidden from the right button bar) so you can cleanly share screenshots with customers showing only their pending days.
  - Press **`F8`** inside the report to toggle the **`Knocked Off in Days`** column (showing how many days each fully paid invoice took to get cleared).
- **Quick Navigation:**
  - **`Alt + F2` (Period):** View all paid and unpaid invoices for any custom date range.
  - **`F4` (Ledger):** Switch to another party ledger directly inside the report.
- **100% Read-Only & Safe:** Uses zero UDFs, zero data storage, and does not alter any vouchers, masters, P&L, or Balance Sheet. All definitions are prefixed with `SPD` to avoid conflicts with other TDLs.

---

## Sample Output (Dummy Data)

### 1. Default View (`Ctrl + Alt + D`) — Ready for Customer Screenshot
*Party: **Shri Hardware & Plywood** | As on: **13-Nov-2026***

| Date | Vch No | Vch Type | Inv Amt | Received | Pending | Days |
| :--- | :--- | :--- | ---: | ---: | ---: | ---: |
| 12-Jun-26 | 341 | Sales | 11,021.00 | 11,021.00 | **0.00** | - |
| 26-Jun-26 | 398 | Sales | 4,936.00 | 4,936.00 | **0.00** | - |
| 24-Jul-26 | 504 | Sales | 15,710.00 | 15,710.00 | **0.00** | - |
| 17-Aug-26 | 578 | Sales | 4,084.00 | 0.00 | **4,084.00** | 88 |
| 04-Sep-26 | S0390 | Sales | 1,048.00 | 0.00 | **1,048.00** | 70 |
| 30-Sep-26 | 761 | Sales | 18,389.00 | 0.00 | **18,389.00** | 44 |
| 12-Oct-26 | 787 | Sales | 2,929.00 | 0.00 | **2,929.00** | 32 |
| 30-Oct-26 | 841 | Sales | 4,287.00 | 0.00 | **4,287.00** | 14 |
| | | **Total Pending** | | | **30,737.00 Dr** | |

### 2. Internal Audit View (After Pressing `F8`)
*Reveals the **`Knocked Off in Days`** column (`Clearance Receipt Date - Invoice Date`):*

| Date | Vch No | Vch Type | Inv Amt | Received | Pending | Days | Knocked Off in Days |
| :--- | :--- | :--- | ---: | ---: | ---: | ---: | ---: |
| 12-Jun-26 | 341 | Sales | 11,021.00 | 11,021.00 | **0.00** | - | **66** |
| 26-Jun-26 | 398 | Sales | 4,936.00 | 4,936.00 | **0.00** | - | **64** |
| 24-Jul-26 | 504 | Sales | 15,710.00 | 15,710.00 | **0.00** | - | **75** |
| 17-Aug-26 | 578 | Sales | 4,084.00 | 0.00 | **4,084.00** | 88 | - |
| ... | ... | ... | ... | ... | ... | ... | ... |

---

## Shortcut Keys Reference

| Key | Where to Press | Action |
| :--- | :--- | :--- |
| **`Ctrl + Alt + D`** | Ledger Vouchers screen | Open **Pending Invoices** report (Last 3 paid + all unpaid) |
| **`F8`** | Inside Pending Invoices report | Toggle **`Knocked Off in Days`** column ON/OFF |
| **`Alt + F2`** | Inside Pending Invoices report | Change Period (shows all paid & unpaid bills in chosen period) |
| **`F4`** | Inside Pending Invoices report | Select another Party Ledger |

---

## How to Install in TallyPrime

1. Download `SPD_Pending.tdl` from this repository and save it in a permanent folder (e.g., `D:\TallyTDLs\SPD_Pending.tdl`).
2. Open **TallyPrime** -> Press **`F1` (Help)** -> Select **TDLs & Add-Ons**.
3. Press **`F4` (Manage Local TDLs)**.
4. Set **Load selected TDL files on startup** to **Yes**.
5. Enter the full file path (`D:\TallyTDLs\SPD_Pending.tdl`) and press **`Ctrl + A`** to save.
6. Open any party's **Ledger Vouchers** (`Gateway of Tally -> Display More Reports -> Account Books -> Ledger`) and press **`Ctrl + Alt + D`**.

---

## Compatibility & License

- **Tested on:** TallyPrime Silver (Release 4.x / 5.x+)
- **License:** MIT License (Free to use, modify, and share)
<img width="1535" height="816" alt="Screenshot 2026-11-13 222240" src="https://github.com/user-attachments/assets/79b476d5-f325-41b7-9ac9-7378994e99e9" />
<img width="1527" height="820" alt="image" src="https://github.com/user-attachments/assets/4e67f900-bb02-49ad-bf1d-bb7de91ee04f" />
<img width="1529" height="250" alt="image" src="https://github.com/user-attachments/assets/c750d63b-d594-44a4-9667-c5898b0d1526" />
