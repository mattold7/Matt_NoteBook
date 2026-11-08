# 2027 Bronco: Trailer Module Activation with FORScan

Purpose: the steps to enable trailer lighting after installing the trailer module and the HK hitch. Compiled 2026-11-06 from the Bronco6G thread "FORScan changes to activate '25 trailer module". The settings were posted for **2025** Broncos (Big Bend and Heritage reports). Nobody in the thread reported a 2026 or 2027, so check every value against your own truck before writing anything.

Related: [[2027 Ford Bronco Badlands 4-Door Build]]

---

## Before starting

- [ ] Confirm the trailer module part number for a 2027 with Granger's parts counter. The thread cites **S2DT-19H378-BA** for MY2025 and later (one member said later suffixes such as BB or BC supersede it). That differs from the S2DZ-19H332-A in the build tracker, so make sure you're buying the trailer module, not a different part.
- [ ] Install the hitch and the trailer module first.
- [ ] Have FORScan on a Windows laptop with a compatible OBD adapter. As-built editing needs FORScan's extended license. *(General FORScan practice, not from the thread.)*
- [ ] Keep a battery maintainer on the truck while writing modules. *(General practice, not from the thread.)*
- [ ] **Back up every module's as-built data before changing anything**, and save the files somewhere safe. The posters say to use the changes at your own risk.
- [ ] Alternative: a dealer can activate the module instead. One member's dealer had already done it.

## Rules from the thread

- The `x` positions are VIN-specific (trim, packages, options). Only change the digit shown. Leave every `x` as it is on your truck.
- Only write the lines whose values differ from your current settings.
- Don't write the whole IPC. It holds odometer data, so write only the changed lines.

---

## Changes (2025 values as posted)

| Module | As-built line | Setting | Values | Set to |
|---|---|---|---|---|
| IPC | `720-03-02xx4xxx` | Trailer sway | 0 = Disabled, 4 = Enabled | 4 |
| IPC | `720-03-02xxxxx1` | Trailer lighting (2025 addition, same line) | 1 | 1 |
| IPC | `720-07-01xxxxxCxxxx` | Trailer brake controller | 4 = Disabled, C = Enabled | **4 unless a hardwired brake controller is installed** |
| BCM | `726-01-02xxx1xxxxxx` | Trailer connect config | 0 = Disabled, 1 = Enabled | 1 |
| BCM | `726-40-01xxxxx1xxxx` | Trailer outage config | 0 = Disabled, 1 = Enabled | 1 |
| BCM | `726-69-02xxxxxxxxx1` | TRM installed / config | 0 = Disabled, 1 = Enabled | 1 |
| PAM | `736-01-01xx8xxxxxxx` | PAM config | 0 = No trailer module, 8 = Trailer module | 8 |
| BLIS left | `7C4-01-01Bxxx` | Blind spot, trailer mode | 3 = Auto/No trailer, B = Auto/Trailer, 7 = Manual/No trailer, F = Manual/Trailer | B (see notes) |
| BLIS right | `7C6-01-01Bxxx` | Blind spot, trailer mode | Same as left | B (see notes) |
| APIM | `7D0-01-03xxxxxxx4xx` | Trailer setup configuration | 0 = Disabled, 4 = Enabled | 4 (see notes) |
| APIM | `7D0-01-04xxx6xxxxxx` | 4-pin / 7-pin connector | 2 = No connector, 6 = Connector | 6 |
| APIM | `7D0-09-02Cxxxxxxxxx` | Trailer sway | 4 = Disabled, C = Enabled | C |
| TRM | `791-01-01` through `791-07-09` | Trailer module configuration (about 40 lines) | Copy exactly from the original post | See below |

### TRM lines

The 2025+ trailer module is a different, larger firmware module than earlier years. The thread lists about 40 `791-xx-xx` lines to enter exactly as posted. **Copy them from the original post, not from a summary.** I couldn't capture them reliably. Paste them here once you have them:

```
791-01-01 
...
791-07-09 
```

---

## Notes and known problems

- **Brake controller:** leave the IPC TBC setting at 4 (Disabled) unless you install a hardwired brake controller. One owner got DTC U0137 ("Lost Communication With Trailer Brake Control Module") with it enabled and no controller, and disabling it cleared the code. With a Bluetooth brake controller, leave it disabled too.
- **Manual transmission:** a 2025 Big Bend manual owner got a cross-traffic fault after the mod and fixed it with different blind spot settings for the manual. Expect to adjust the BLIS lines on your manual.
- **BLIS and bike racks:** with the module installed, blind spot monitoring turns off when a trailer is detected. One owner lost it with a lighted bike rack attached.
- **IPC security error:** two 2025 owners got "Gain security access failed - security key is wrong" writing the IPC on FORScan v2.3.70. A FORScan beta build was said to address it, but one owner still had the error. One of them gave up and went to a dealer.
- **TRM trouble codes:** one owner had TRM codes that wouldn't clear, and a "Write All" on the TRM fixed them.
- **APIM chart may be off by one:** one owner found the trailer setup 4 in the 7th position, not the 8th as the chart shows. Check your own line before writing.
- **Light testers:** cheap single-LED testers may not register as a trailer. A NeaLia 7-pin tester worked on a 2025 Big Bend. Another owner's tester didn't trigger the trailer light check, but the turn signals still worked.
- **Dealer visits:** a Ford recall visit reloaded one owner's as-built data and removed the trailer menu. Tell the service writer the module is installed and configured, and keep your saved settings to restore.
- **Used modules:** the TRM holds no VIN information, so a used or salvage module should work.

---

## After writing

- [ ] Clear codes, cycle the ignition, and check for new DTCs.
- [ ] Check the trailer menu on the screen.
- [ ] Test running lights, brake lights and both turn signals with a 7-pin tester or a real trailer.
- [ ] Save a new as-built backup with the working settings.

---

## Sources

- [FORScan changes to activate '25 trailer module (Bronco6G)](https://www.bronco6g.com/forum/threads/forscan-changes-to-activate-25-trailer-module.122794/latest)
- [Post with the 2025 settings (Bronco6G)](https://www.bronco6g.com/forum/goto/post?id=2735988)
- [Posts on the IPC security error and the manual-transmission fix (Bronco6G)](https://bronco6g.com/forum/goto/post?id=2777966)
- [Posts on TRM codes, Write All and the APIM chart (Bronco6G)](https://bronco6g.com/forum/goto/post?id=2795778)
- [Posts on the part number and dealer reloads (Bronco6G)](https://bronco6g.com/forum/goto/post?id=2733305)
- [Posts on the 2025 Big Bend results (Bronco6G)](https://bronco6g.com/forum/goto/post?id=2788853)
