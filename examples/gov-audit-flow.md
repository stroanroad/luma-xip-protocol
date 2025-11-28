# Example: Government Cannabis Prescription Flow (NI)

This document shows a simplified sequence of XIP receipts in a
Government + Health/Cannabis context.

1. **Case created**  
   - `event_type`: `gov.case.opened`  
   - Subject: patient case ID  
   - Emitted by: government case management hub  

2. **Consultation recorded**  
   - `event_type`: `health.consultation.recorded`  
   - Subject: patient case ID  
   - Emitted by: clinic telehealth hub  

3. **Prescription issued**  
   - `event_type`: `health.prescription.issued`  
   - Subject: prescription ID  
   - Emitted by: clinic / prescriber  

4. **Pharmacy dispense**  
   - `event_type`: `cannabis.order.fulfilled`  
   - Subject: prescription ID  
   - Emitted by: pharmacy hub  

5. **CBDC payment + tax**  
   - `event_type`: `finance.invoice.paid`  
   - Subject: invoice ID  
   - Routing: CBDC + XRPL mirror  
   - Emitted by: finance hub  

Each step emits an XIP-compliant receipt (`xip-receipt-v1.json`) and adds
it to the local hash-chain for the relevant hub.

Hash-chain anchors and CBDC/XRPL proofs can be used by national audit
authorities to verify that:

- Every prescription is linked to a consultation  
- Every dispense is linked to a valid prescription  
- Every payment and tax event is recorded and auditable  
