<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a {
    display: inline !important;
}
</style>
<h1>Identity Verification</h1>

**Notification > Notification Hub > Usage Policy and Preset Guide > Identity verification**

<span id="identity-verification"></span>

To use the Notification Hub, you can use it after Identity verification at **Notification Hub** > ** Identity verification ** (compliance with notification related to the Telecommunications Business Act)

* Business members can use the Notification Hub through Identity verification. Individual members are restricted from conducting Identity verification.
  * [ Article 37-7of the Enforcement Decree of the Telecommunications Business Act](https://www.law.go.kr/LSW//lsInfoP.do?lsId=004708&ancYnChk=0#0000)
* Identity verification basically requires a document review of mobile phone self-authentication, business registration certificate, and employment certificate. 
* The name and mobile phone number entered at the time of membership must match the information entered at the time of identity verification to be approved for identity verification.
* NHN Cloud accounts invited to organizations/projects created by business members or IAM accounts invited to organizations created by business members must conduct identity verification to use services.
  * Invited NHN Cloud accounts and IAM accounts are classified as business operators when they approve their Identity verification.
* The certificate of employment is marked with **issuance date and only documents with seal ** are allowed. The 6 digits after the resident registration number in the certificate of employment **must be masked (hidden)**. For example, 000000-0\*\*\*\*\**

## Identity Verification Status

| Status       | Description |
|----------| --- |
| **Approval in progress** | Status where the administrator is reviewing the certification document for the registered Identity verification |
| **Rejected**   | Status where  re-registration of documents is required as identity verification has been rejected.  |
| **Approved**   | Status where identity verification is complete |
