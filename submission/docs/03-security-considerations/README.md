# Security and Privacy Review

*Section 4 of the WeatherSafe interaction flow and wireframes document. The full document is in [docs/04-prototype](../04-prototype).*

**Reviewer:** David Moses-Ailemen Ibukunoluwa


### Purpose

This review examines WeatherSafe’s proposed interaction flows and wireframes to identify security and privacy risks before implementation. It covers trusted-contact pairing, access to incident information, location sharing, data retention and cancellation.

The proposed flow already includes safeguards such as contact verification, a cancellation window and location sharing during active incidents only. The requirements below clarify how these controls should behave.


### Risk and Required Controls
| Risk | Required Control | Suggested Wireframe Update |
| --- | --- | --- |
| Incorrect or unapproved trusted contact receives sensitive alerts. | Pairing must require contact verification and the user’s approval | Show Pending, Verified, and Removed contact states. Include confirmation before approving or replacing a contact. |
| Unauthorized access exposes a user’s location or incident history. | The system must check that the person requesting incident information is authorized for that specific incident. | Include a contact authentication or secure verification step and an Access denied or expired screen. |
| Accidental activation sends an unwanted alert. | Ordinary taps must not activate an incident. Cancelling within the cancellation window must prevent alert sending and discard queued work for that activation. | Show a discreet cancellation control and return to the weather screen when cancelled. |
| Location sharing continues after an incident ends. | Ending an incident must stop location collection and sharing on the device immediately, including when offline. | Explain that ending stops sharing. Show Sharing stopped separately from End update pending when the contact cannot yet be notified |
| Sensitive information is stored indefinitely | Define retention periods for location points, incident records and delivery logs. Automatically delete expired data and provide a way to request deletion. | Add a privacy explanation describing what is stored, why, for how long, and how users can request deletion. |
| Offline retries send an obsolete alert after cancellation on ending | Before retrying, check that the incident is still valid and the contact remains approved. Cancelled activations must never be retried, ended incidents must not restart live sharing. | Distinguish Alert not sent, Delivery unconfirmed, and Incident ended. Explain what remains queued. |
| Misleading status information gives users false confidence. | Distinguish sending, delivery and explicit human acknowledgement. Label location timestamps and accuracy; never present an old position as live. | Display separate delivery and acknowledgement states. Show Last updated, location accuracy and Location unavailable where appropriate. |


### Requirements for the Architecture

The implementation must enforce permissions on the server rather than relying only on hidden buttons on screens. Sensitive data must use encrypted connections, and location details or access tokens must not appear in ordinary application logs.

Incident-handling must also prevent duplicate alerts and conflicting action. If cancellation occurs while an activation is being prepared, the cancelled activation must not subsequently send an alert. Once an alert has already been sent, ending the incident cannot retract information the contact has already received.


### Outcome

The proposed flow provides a useful starting point, but contact access, retention periods and cancellation behavior need clearer requirements before implementation.

The above controls should be incorporated into the relevant mock-ups and linked to development tasks. **This review identifies design requirements; completion still requires evidence that the team has applied them to the mock-ups.**
