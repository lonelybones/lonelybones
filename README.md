# lonelybones

Independent vulnerability researcher. Native code, kernel subsystems, protocol implementations, smart contracts.

## Focus

Linux kernel (kTLS, net/crypto, vsock, SCTP, TIPC), OPC UA and industrial protocols, ML inference runtimes, browser media pipelines, DeFi and cross-chain bridges. Prefer translation-layer targets and boundary-dwelling bugs in boring code. All findings sanitizer-verified before submission.

## Selected Findings

**Protocol / Native**

- **libiec61850** — Heap OOB read in `mmsServer_handleGetNameListRequest` objectClass parsing (missing BER length validation in MMS server). Fixed upstream in [fb9418d](https://github.com/mz-automation/libiec61850/commit/fb9418d9d6dbf1b835d824ebaaf8de03990b0320). CVE requested.
- **OpenThread** — Missing IPv4 IHL validation in NAT64 translator causing packet corruption. Reported via Google VRP, fixed in [26a882d](https://github.com/openthread/openthread/commit/26a882dab). Nexus regression test included. CVE requested.

**ML Inference Runtimes**

- **ONNX Runtime (Microsoft)** — Heap OOB write in TreeEnsemble MIN/MAX aggregators via crafted model. MSRC 110413, CVSS 8.3. MSRC acknowledged as heap write primitive with code execution potential; fix in progress at [PR #27677](https://github.com/microsoft/onnxruntime/pull/27677).
- **ONNX Runtime (Microsoft)** — Heap OOB read in STFT operator via double-counted complex stride enabling cross-tenant data leakage in multi-tenant inference. MSRC 110224, CVSS 6.5.

**Smart Contracts**

- **GTE Spot CLOB and Router** *(Code4rena, High)* — DOS via order amendment bypassing `maxLimitsPerTx` protection. 4th / 997 wardens.
- **GTE Perps and Launchpad** *(Code4rena, High)* — `CREATE2` address of Uniswap pair used by `LaunchPad` does not match address deployed by `GTELaunchpadV2PairFactory`, breaking pair resolution.

## Profiles

- Code4rena — [@lonelybones](https://code4rena.com/@lonelybones)
- HackerOne — [lonelybones](https://hackerone.com/lonelybones)
- Google Bug Hunters — [profile](https://bughunters.google.com/profile/e61c8f54-4b86-471f-a7da-c60b8ef5e8b7)
- ZDI — lonelybones0001
