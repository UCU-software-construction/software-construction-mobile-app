# software-construction-mobile-app

Part C: Change and Maintainability


Which parts of the app would need changes?
Introducing mobile payments in Uganda would require changes across multiple layers of the Uber system rather than in a single isolated component. At the user interface level, the payment screens would need to be updated to allow users to select local mobile money options such as MTN Mobile Money or Airtel Money. This includes modifying payment setup screens, checkout flows, and receipts to clearly show mobile money as a supported method.

At the business logic level, significant changes would be required to handle new payment rules. The system would need logic to initiate mobile money payment requests, handle asynchronous payment confirmations, manage retries for failed transactions, and support partial or delayed payments. Unlike card payments, mobile money transactions often depend on user approval via USSD or SMS, which adds complexity to transaction state management.

At the network and API layer, Uber would need to integrate with local mobile money provider APIs or third-party payment aggregators operating in Uganda. This would involve building new secure API connections, handling different response formats, and managing callbacks from payment providers to confirm transaction success or failure.

At the data storage level, the database schema would need updates to store mobile money transaction references, provider identifiers, payment statuses, and reconciliation data. Existing payment tables designed primarily for card-based systems would likely need extensions or redesigns to support the different lifecycle of mobile money transactions.


What existing features could break?
Several existing features could be affected or temporarily broken by the introduction of mobile payments. The payments and billing feature is the most directly impacted, as assumptions made for instant card authorization may no longer hold true for mobile money, which can be delayed or fail due to network or user interaction issues. This could lead to incorrect fare settlements if not handled carefully.

Ride completion workflows could also be affected, since Uber currently assumes that payment confirmation happens quickly after a trip ends. With mobile money, there may be delays in confirmation, which could cause issues such as rides being marked as unpaid or drivers not receiving timely earnings updates.

Promotions and discounts could break if they are tightly coupled to specific payment methods. For example, promo codes designed for card payments may not apply correctly to mobile money unless explicitly adapted.
Driver payouts may also be impacted, as Uber would need to ensure that funds collected via mobile money are correctly reconciled and transferred to drivers, possibly through different payout mechanisms than those used for card-based transactions.


Why would this change be difficult to implement?
This change would be difficult to implement because it cuts across many core assumptions in Uber’s existing architecture. From a technical perspective, mobile money systems are fundamentally different from traditional card payment systems. They are often asynchronous, depend on external telecom infrastructure, and can be less reliable in terms of network availability, which requires robust error handling and state management.

From a maintainability standpoint, adding Uganda-specific payment logic risks introducing country-specific code paths that increase system complexity. If not carefully abstracted, this can lead to tightly coupled code that is harder to maintain and extend to other regions with similar payment needs.

Scalability is another challenge, as mobile money providers may have rate limits or performance constraints that differ from global card processors. Uber would need to design the system to handle spikes in payment requests without overwhelming local providers or degrading user experience.

Finally, regulatory and compliance requirements add further complexity. Financial regulations, data protection laws, and telecom policies in Uganda may require additional validation, auditing, and reporting mechanisms, increasing development time and ongoing maintenance costs.

