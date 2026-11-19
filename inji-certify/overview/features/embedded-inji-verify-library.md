# Embedded Inji Verify Library

#### What it is

Certify now embeds Inji Verify's verify-core (1.0.0-rc.1) to build and verify presentations in the PDI flow. No separate Inji Verify service is called.

#### Benefits

* One less deployable and no network hop on the issuance path.
* Less TLS and configuration surface, and no verifier-unreachable failure mode.

#### How it works

Certify depends on the verify-core artifact and wires its beans into the application context. VerifiablePresentationRequestService builds the OpenID4VP request from the DCQL query, and VerifiablePresentationSubmissionService verifies the wallet's vp\_token.

{% hint style="info" %}
**Migration**:

Remove configuration that points PDI at an external Inji Verify service, and drop the unused Inji Verify database artifacts from your Certify deployment.
{% endhint %}
