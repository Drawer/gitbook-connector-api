## Using tokenized credit cards

If your solution interacts with customers and the user interface involves the collection and storage of credit card details in a secure manner against the customer's profile in Mews, use [Add tokenized credit card](../operations/finance#add-tokenized-credit-card), and then [Charge credit card](../operations/finance#charge-credit-card) operations to take a payment. 

The former mimics the result of a user manually [adding a credit card](https://help.mews.com/en/articles/4245466-add-a-new-payment-card) in Mews. The latter mimics the result of a user [taking a card payment via the payment gateway](https://intercom.help/mews-systems/en/articles/4245460-take-a-payment) built into Mews.

Read more about [PCI Compliance at Mews](https://help.mews.com/en/articles/4245459-pci-compliance).

### Adding a tokenized credit card

#### 1. Retrieve PublicKey

As an integration partner, you will not need to set up your own PCI Proxy account. Rather, when automating payments via the Connector API, you should work with Mews' own account. To do so, call [Get configuration](../operations/configuration#get-configuration) to obtain the `PublicKey` value, found within the [payment card storage](../operations/configuration#payment-card-storage) object. This value will be used as the `merchantId` with PCI Proxy.

#### 2. Set up Secure Fields (iframes) to collect cards

Refer to the PCI Proxy documentation on [collecting and storing cards](https://docs.pci-proxy.com/collect-and-store-cards/capture-iframes#3-retrieve-a-transaction-id) and implement steps 1 through 3. See [Examples](https://docs.pci-proxy.com/collect-and-store-cards/capture-iframes#examples) in the documentation for more help.
1. [Set up Secure Fields](https://docs.pci-proxy.com/collect-and-store-cards/capture-iframes#1-setup-secure-fields).
2. [Create payment form](https://docs.pci-proxy.com/collect-and-store-cards/capture-iframes#1-setup-secure-fields) to collect card number and CVV.
3. [Retrieve a Transaction ID](https://docs.pci-proxy.com/collect-and-store-cards/capture-iframes#3-retrieve-a-transaction-id) using the `merchantId`. Take note of the `transactionId` in the response, which looks like a series of numbers (e.g. `201028230732590232`).

[Step 4 - Obtain tokens](https://docs.pci-proxy.com/collect-and-store-cards/capture-iframes#4-obtain-tokens) is done by Mews’ backend. No action is required by the integration partner in this step.

**Note:** 

Though not required by PCI Proxy, credit card expiration date is listed as a mandatory parameter on the [Add tokenized credit card](../operations/finance#add-tokenized-credit-card) so that it can be displayed within the customer profile in Mews. This can be also used and an additional validation method for the property to know if there is an expired card on file.

To handle this, we recommend that the payment form includes a field for guests to input their credit card expiration date, which needs not be sent to PCI Proxy, and only needs to be included in the [Add tokenized credit card](../operations/finance#add-tokenized-credit-card) API request. 

#### 3. Add the tokenized credit card to a customer profile in Mews

Add the tokenized credit card to a customer profile in Mews by calling [Add tokenized credit card](../operations/finance#add-tokenized-credit-card). Enter the `transactionId` and obfuscated credit card details in the [credit card data](../operations/finance#credit-card-data) object. Take note of the `CreditCardId` in the API response.

The credit card will now be visible in the customer profile in Mews, under the *Payments tab* > *Credit cards* section. 

**Note:** While customer profiles are shared across all properties in a chain, credit card details are not. 

### Charging the tokenized credit card

Now that you have the `CreditCardid`, you can use the [Charge credit card](../operations/finance#charge-credit-card) endpoint to charge the customer. 

**Note:** The [Charge credit card](../operations/finance#charge-credit-card) operation actually charges the customer's credit card, whereas the [Add credit card payment](../operations/finance#add-credit-card-payment) operation does NOT. The latter simply records a credit card payment in Mews and does not trigger any additional action beyond Mews - suitable for when the customer's credit card has already been charged from your solution.



