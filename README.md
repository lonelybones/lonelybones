# Andrew Letourneau

Independent vulnerability researcher. Native code, kernel subsystems, protocol implementations, cryptography, smart contracts. GitHub: [`@lonelybones`](https://github.com/lonelybones).

## Focus

Linux kernel (kTLS, net/crypto, vsock, SCTP, TIPC), OPC UA and industrial protocols, ML inference runtimes, browser media pipelines, DeFi and cross-chain bridges. I prefer translation-layer targets and boundary-dwelling bugs in boring code. Everything is sanitizer-verified before submission and disclosed through coordinated channels.

## Selected Findings

**Protocol / Native**
- **libiec61850**: Heap OOB read in `mmsServer_handleGetNameListRequest` objectClass parsing (missing BER length validation in the MMS server). Fixed upstream in [fb9418d](https://github.com/mz-automation/libiec61850/commit/fb9418d9d6dbf1b835d824ebaaf8de03990b0320). CVE requested.
- **open62541 (OPC UA)**: Wild-pointer dereference in the server discovery path (`securityPolicyUriPostfix`), where an empty URI underflows a raw pointer into unmapped memory. Patch authored and merged upstream in [PR #7963](https://github.com/open62541/open62541/pull/7963). Additional findings disclosed privately to the maintainer.
- **OpenThread (Google)**: Missing IPv4 IHL validation in the NAT64 translator causing packet corruption and an RFC 7915 source-route bypass. Reported via Google VRP, fixed in [26a882d](https://github.com/openthread/openthread/commit/26a882dab) with a Nexus regression test. [CVE-2026-8369](https://www.cve.org/CVERecord?id=CVE-2026-8369).
- **OpenThread (Google)**: Unauthenticated backbone-router address-cache poisoning via `HandleExtendedBackboneAnswer`, which acted on backbone `BB.ans` with no validation. Accepted through the OSS VRP and fixed in [PR #13136](https://github.com/openthread/openthread/pull/13136).
- **protobuf (Google)**: Unbounded stack recursion (DoS) in the `BinaryToJson` group-decode path, missing the recursion-depth guard present on the message path. Same class as CVE-2024-7254, previously unaddressed in the C++ path. Fixed in [PR #27597](https://github.com/protocolbuffers/protobuf/pull/27597).

**ML Inference Runtimes**
- **ONNX Runtime (Microsoft)**: Heap OOB write in TreeEnsemble MIN/MAX aggregators via a crafted model. MSRC 110413, CVSS 8.3, acknowledged as a heap-write primitive with code-execution potential; fix at [PR #27677](https://github.com/microsoft/onnxruntime/pull/27677).
- **ONNX Runtime (Microsoft)**: Heap OOB read in the STFT operator via a double-counted complex stride, enabling cross-tenant data leakage in multi-tenant inference. MSRC 110224, CVSS 6.5.

**Smart Contracts**
- **GTE Spot CLOB and Router** *(Code4rena, High)*: DoS via order amendment bypassing `maxLimitsPerTx` protection. 4th of 997 wardens.
- **GTE Perps and Launchpad** *(Code4rena, High)*: `CREATE2` address of the Uniswap pair used by `LaunchPad` does not match the address deployed by `GTELaunchpadV2PairFactory`, breaking pair resolution.

**Cryptography / MPC**
- **cb-mpc (Coinbase)**: Paillier encryption randomness-handling flaw: assertion cascade on `r=0` with release-build `NDEBUG` implications for ciphertext integrity in MPC protocol paths. Accepted and fixed by Coinbase.

## Profiles
- LinkedIn: [Andrew Letourneau](https://www.linkedin.com/in/andrew-letourneau-sec)
- Code4rena: [@lonelybones](https://code4rena.com/@lonelybones)
- HackerOne: [lonelybones](https://hackerone.com/lonelybones)
- Google Bug Hunters: [profile](https://bughunters.google.com/profile/e61c8f54-4b86-471f-a7da-c60b8ef5e8b7)
- X: [@lonelybonesec](https://x.com/lonelybonesec)
