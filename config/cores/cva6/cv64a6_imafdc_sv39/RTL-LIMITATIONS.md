# RTL limitations: cv64a6_imafdc_sv39

ACT config reflects `core/include/cv64a6_imafdc_sv39_config_pkg.sv` only. Known gaps between RTL capability and ACT coverage are documented here — not hacked into yaml/sail.

## Excluded ACT extensions

| Extension | RTL | ACT handling |
|-----------|-----|--------------|
| `SdtrigSm`, `SdtrigS`, `SdtrigU` | `Sdtrig=0` | Excluded via `EXCLUDE_EXTENSIONS` |
| `Smstateen` | Not implemented | Excluded |
| `PMPSm` | `NrPMPEntries=8`, `PMPNapotEn=1` | UDB yaml requires `NUM_PMP_ENTRIES: 0`; PMPSm excluded |

## Config vs RTL notes

| Item | RTL | ACT config |
|------|-----|------------|
| ISA | RV64IMAFDC + Zba/Zbb/Zbc/Zbs/Zcb/Zicond + Zkn | yaml/sail extensions |
| MMU | Sv39, `SvnapotEn=1` | Sv39 + Svnapot in yaml/sail |
| PMP | 8 NAPOT entries | yaml/sail PMP count 0 (UDB constraint); PMPSm excluded |
| Cvxif | `CvxifEn=1` | Not in ACT (coprocessor interface untested) |
| Zcmp | `RVZCMP=0` | Not in yaml/sail |
| Debug triggers | `Sdtrig=0` | Sdtrig* excluded |
| H / V | `RVH=0`, `RVV=0` | Not in yaml/sail |

## Simulation failures

If a test fails that is not in the exclusion list above, treat as an RTL bug or TB limitation and record here with test name and observed behavior.
