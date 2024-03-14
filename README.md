# Plural Payment Gateway Integration Document

This repository offers integration reference guide for Plural Payment Gateway


## API Reference

1. [Payments API](https://github.com/pluralonline/plural-pg-docs/blob/main/Payment%20API%20v2.1.pdf)
2. [Refund & Inquiry](https://github.com/pluralonline/plural-pg-docs/blob/main/Refund-Inquiry%20API%20v2.1.pdf)
3. [Response Codes List](https://github.com/pluralonline/plural-pg-docs/blob/main/Plural-Edge-Response-Codes.pdf)
4. [Hash Generation Logic](https://github.com/pluralonline/plural-pg-docs/blob/main/HashGeneration.pdf)
5. [Signature Verification](https://github.com/pluralonline/plural-pg-docs/blob/main/Signature%20Verification.pdf)
6. [EMI Calculator](https://github.com/pluralonline/plural-pg-docs/blob/main/EMI%20Calculator%20v2.1.pdf)
7. [EMI Seamless Integration](https://github.com/pluralonline/plural-pg-docs/blob/main/EMI%20Seamless%20v2.1.pdf)
8. [IMEI Validation](https://github.com/pluralonline/plural-pg-docs/blob/main/IMEI%20Validation%20v2.1.pdf)
9. [Cardless EMI Integration](https://github.com/pluralonline/plural-pg-docs/tree/main/Cardless%20EMI)
10. [Tokenised Card Processing](https://github.com/pluralonline/plural-pg-docs/blob/main/Tokenization%20Payment%20Processing%20API.pdf)
11. [Pay By Points Integration](https://github.com/pluralonline/plural-pg-docs/tree/main/PaybyPoints%20V2.1)
12. [Pay By Link](https://github.com/pluralonline/plural-pg-docs/blob/main/Pay%20by%20Link.pdf)

---

## Integration Best practices:

### Signature Verification to avoid data tampering

This is a mandatory step to confirm the authenticity of the details returned to you on the return URL for successful payments.

Require pinelabs sdk and call the `default` method on it. It takes 4 parameters which are as follows:

1. Convert the response received on the return URL into a string (remove secret and secret type params)
2. Sort the string alphabetically
3. Hash the payload with your secret key using SHA256
4. Match the generated signature with the one received in the response from Plural

### Check payment status before providing services

Check if the payment status is in the success state .i.e. : `ppc_Parent_TxnStatus = 4` and `ppc_ParentTxnResponseCode = 1` before providing the services to the customers

1. One Inquiry API call (Fetch payment using `ppc_UniqueMerchantTxnID`) right after the Transaction
2. Run Inquiry API periodically for the payments in initiated state

### Webhook Implementation

Implement webhooks to avoid call-back failures (drop offs due to connectivity/network issues)

1. Payment.captured
2. Payment.failed

### TLS Version

We support `TLS_v_1.2` and above which is strongly recommended. Kindly ensure you are using higher TLS versions to avoid any transaction failures

### Note

1. In UAT, only CC/DC, Net banking (via IDBI), and EMI can be tested.
2. Production credentials will be provided post UAT sign-off to test all flows in the soft production environment before go live.
3. Return URL and Webhook URL to be shared before go-live for configuration and whitelisting at Pine's end.

---

## UAT Credentials

### API Credentials

Kindly reach out to your Business SPOC for UAT API Credentials

### UAT Dasboard

Link: https://uat.pinepgconsole.in:7015/

 


