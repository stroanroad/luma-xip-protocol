# XIP Protocol — ISO 20022 Mapping
**Version:** v1.0.0  
**Document:** 03-XIP-ISO20022-Mapping  
**Status:** Released  

---

## 1. Overview

This document explains how XIP receipts map to **ISO 20022** message structures for regulated financial environments.  
The mapping enables:

- CBDC and stablecoin audit integration  
- Transaction network compliance  
- Regulator-ready exports  
- XRPL settlement reporting  
- Government financial oversight  

ISO 20022 is the global standard for financial messaging.  
XIP integrates cleanly due to its deterministic structure and zero-knowledge design.

---

## 2. Why ISO 20022?

ISO 20022 is used by:

- SWIFT  
- SEPA  
- central banks  
- payment service providers  
- regulatory bodies  
- settlement networks  
- cross-border messaging systems  

XIP supports ISO 20022 export so governments and financial institutions can:

- Interoperate with existing rails  
- Audit offline events after reconnection  
- Integrate XIP into national payment and reporting systems  

---

## 3. High-Level Mapping

XIP does **not** replace ISO 20022.  
Instead, each XIP receipt is wrapped inside ISO-compliant envelopes (`MX` messages).

Example mapping categories:

- Payments  
- Remittances  
- CBDC movements  
- Merchant transactions  
- Invoice lifecycle events  
- Regulatory reporting  

---

## 4. Field Mapping Table

### 4.1 Core Fields

| XIP Field     | ISO 20022 Equivalent               | Notes |
|--------------|------------------------------------|-------|
| `timestamp`  | `GrpHdr/CreDtTm`                    | UTC timestamp |
| `hub_id`     | `AppHdr/MsgDefIdr`                 | Identifies application domain |
| `device_id`  | `InitgPty/Id/OrgId/Othr/Id`         | Non-personal device identifier |
| `event`      | `Document/*`                        | Depends on message type |
| `prev_hash`  | `SplmtryData/Envlp/XIPPrevHash`     | Audit hash |
| `signature`  | `SplmtryData/Envlp/XIPSignature`    | Signature block |
| `ledger_ref` | `SplmtryData/Envlp/XIPLedgerRef`    | Optional CBDC/XRPL reference |
| `version`    | `AppHdr/Fr` or `SplmtryData`        | XIP version |

---

## 5. Message Examples

### 5.1 Payment Event (pacs.008)

A XIP payment event can be encoded inside a `pacs.008` message:

```xml
<FIToFICstmrCdtTrf>
  <GrpHdr>
    <CreDtTm>2025-12-03T14:12:11Z</CreDtTm>
  </GrpHdr>

  <CdtTrfTxInf>
    <PmtId>
      <EndToEndId>...</EndToEndId>
    </PmtId>

    <SplmtryData>
      <Envlp>
        <XIPPrevHash>...</XIPPrevHash>
        <XIPSignature>...</XIPSignature>
        <XIPLedgerRef>...</XIPLedgerRef>
      </Envlp>
    </SplmtryData>
  </CdtTrfTxInf>
</FIToFICstmrCdtTrf>
Key point:
All XIP metadata lives inside SplmtryData, keeping the financial payload untouched.

6. Verification Flow
Steps to verify a XIP → ISO 20022 export:

Extract SplmtryData

Reconstruct the XIP hash chain

Verify signatures

Validate ordering and continuity

Apply regulatory/financial logic

Auditors can verify:

Offline payment history

Multi-device chain merges

Subsidy or welfare payments

CBDC transaction evidence

Merchant event trails

7. Benefits of ISO Integration
Compatible with all global financial rails

Requires no changes to banking infrastructure

Works instantly with CBDC & stablecoin platforms

Preserves tamper-proof XIP chain integrity

Enables cross-border regulatory reporting

Bridges offline audited actions to online settlement systems

8. Conclusion
XIP integrates seamlessly with ISO 20022 using the SplmtryData extension block.
This enables tamper-proof, offline-first receipts to be exported directly into global payment and regulatory systems.

This mapping is foundational for:

CBDC and stablecoin issuers

Government disbursement platforms

National payment systems

Financial regulators

Cross-border auditing infrastructure

yaml
Copy code

---

# 🎉 When you’ve pasted, saved, committed, and pushed it:

Just say:

### **“ISO file complete”**

And we move on to the **XRPL mapping doc**, which is the Ripple-facing one.






