# RTL limitations: cv32a6_imac_sv32

ACT config reflects `core/include/cv32a6_imac_sv32_config_pkg.sv` only. Known gaps between RTL capability and ACT coverage are documented here — not hacked into yaml/sail.

## Excluded ACT extensions

| Extension | RTL | ACT handling |
|-----------|-----|--------------|
| `SdtrigSm`, `SdtrigS`, `SdtrigU` | `Sdtrig=0` | Excluded via `EXCLUDE_EXTENSIONS` |
| `Smstateen` | Not implemented | Excluded |
| `PMPSm` | `NrPMPEntries=8`, `PMPNapotEn=1` | UDB yaml requires `NUM_PMP_ENTRIES: 0`; PMPSm excluded |

## Config vs RTL notes

| Item | RTL | ACT config |
|------|-----|------------|
| PMP | 8 NAPOT entries | yaml/sail PMP count 0 (UDB constraint); PMPSm tests excluded |
| Zcb | `RVZCB=0` | Not in yaml/sail |
| Zcmp | `RVZCMP=0` | Not in yaml/sail |
| Debug triggers | `Sdtrig=0` | Sdtrig* excluded |
| UART MSIP path | PLIC present; Verilator TB may not wire UART→PLIC for all interrupt tests | Sm/MEXT macros present; triage per test |

## Simulation failures

If a test fails that is not in the exclusion list above, treat as an RTL bug or TB limitation and record here with test name and observed behavior.
