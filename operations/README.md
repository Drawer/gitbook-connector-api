# Operations

This section describes all operations supported by the API:

* [Configuration](configuration.md) - operations related to configuration of the client, enterprise or API.
  * [Get configuration](configuration.md#get-configuration) - returns configuration of the client and enterprise.
  * [Get all countries](configuration.md#get-all-countries) - returns all countries supported by the API.
  * [Get all currencies](configuration.md#get-all-currencies) - returns all currencies supported by the API.
  * [Get all tax environments](configuration.md#get-all-tax-environments) - returns all tax environments supported by the API.
  * [Get all languages](configuration.md#get-all-languages) - returns all languages supported by the API.
  * [Get language texts](configuration.md#get-language-texts) - returns translations of texts to a specified language.
  * [Get image URLs](configuration.md#get-image-urls) - returns URLs of specified images.
* [Enterprises](enterprises.md) - operations related to the enterprise and its settings.
  * [Get all companies](enterprises.md#get-all-companies) - returns company profiles by filters.
  * [Get all company contracts](enterprises.md#get-all-company-contracts) - returns contracts of the enterprise with companies.
  * [Get all departments](enterprises.md#get-all-departments) - returns all departments of the enterprise.
  * [Get all counters](enterprises.md#get-all-counters) - returns all counters of the enterprise.
  * [Get all outlets](enterprises.md#get-all-outlets) - returns all outlets of the enterprise.
  * [Get all resources](enterprises.md#get-all-resources) - returns all resources of the enterprise.
  * [Update resources](enterprises.md#update-resources) - updates a resource.
  * [Get all resource blocks](enterprises.md#get-all-resource-blocks) - returns resource blocks in an interval.
  * [Add resource blocks](enterprises.md#add-resource-block) - adds a new block to the resource.
  * [Delete resource blocks](enterprises.md#delete-resource-blocks) - deletes resource block.
  * [Add task](enterprises.md#add-task) - adds a task to the enterprise.
  * [Get all tasks](enterprises.md#get-all-tasks) - returns tasks by filters.
  * [Add company](enterprises.md#add-company) - adds a new company to the enterprise.
  * [Update company](enterprises.md#update-company) - updates a company.
* [Services](services.md) - operations related to offered services, availability and prices.
  * [Get all services](services.md#get-all-services) - returns all services offered by the enterprise.
  * [Get all availability blocks](services.md#get-all-availability-blocks) - returns all availability blocks by filters.
  * [Add availability blocks](services.md#add-availability-blocks) - adds new availability blocks.
  * [Update availability blocks](services.md#update-availability-blocks) - updates availability blocks.
  * [Delete availability blocks](services.md#delete-availability-blocks) - delete existing availability blocks.
  * [Get service availability](services.md#get-service-availability) - returns availability of a service in an interval.
  * [Update service availability](services.md#update-service-availability) - updates number of available resources in a service.
  * [Get all products](services.md#get-all-products) - returns all products offered together with services.
  * [Get all rules](services.md#get-all-rules) - returns all automatic rules in services.
  * [Get all business segments](services.md#get-all-business-segments) - returns all business segments of a service.
  * [Get all rates](services.md#get-all-rates) - returns all rates of a service.
  * [Get all companionships](services.md#get-all-companionships) - returns all companionships by filter.
  * [Get all resource access tokens](services.md#get-all-resource-access-tokens) - returns all resource access tokens by filter.
  * [Add resource access tokens](services.md#add-resource-access-tokens) - add new resource access tokens.
  * [Update resource access tokens](services.md#update-resource-access-tokens) - update multiple resource access tokens.
  * [Delete resource access tokens](services.md#delete-resource-access-tokens) - delete existing resource access tokens.
  * [Get rate pricing](services.md#get-rate-pricing) - returns prices of a rate in an interval.
  * [Update rate price](services.md#update-rate-price) - updates prices of a rate.
  * [Get all restrictions](services.md#get-all-restrictions) - returns all restrictions of a service.
  * [Add restrictions](services.md#add-restrictions) - adds new restrictions.
  * [Delete restrictions](services.md#delete-restrictions) - removes restrictions.
  * [Add order](services.md#add-order) - adds a new service order.
  * [Get all vouchers](services.md#get-all-vouchers) - returns all rate vouchers by filters.
* [Reservations](reservations.md) - operations for retrieval and modifications of reservations.
  * [Get all reservations](reservations.md#get-all-reservations) - returns all reservations by filters.
  * [Get all reservation items](reservations.md#get-all-reservation-items) - returns all accounting items of reservations. 
  * [Price reservations](reservations.md#price-reservations) - returns prices of specified reservations.
  * [Add reservations](reservations.md#add-reservations) - adds a new group of reservations.
  * [Update reservations](reservations.md#update-reservations) - updates reservations.
  * [Confirm reservation](reservations.md#confirm-reservation) - confirms a reservation.
  * [Start reservation](reservations.md#start-reservation) - starts \(checks in\) a reservation.
  * [Process reservation](reservations.md#process-reservation) - processes \(checks out\) a reservation.
  * [Cancel reservation](reservations.md#cancel-reservation) - cancels a reservation.
  * [Update reservation customer](reservations.md#update-reservation-customer) - updates customer of a reservation.
  * [Update reservation interval](reservations.md#update-reservation-interval) - updates start \(arrival\) and end \(departure\) of a reservation.
  * [Add reservation companion](reservations.md#add-reservation-companion) - adds a new companion to a reservation.
  * [Delete reservation companion](reservations.md#delete-reservation-companion) - deletes a companion from a reservation.
  * [Add reservation product](reservations.md#add-reservation-product) - adds a new product to the reservation.
* [Customers](customers.md) - operations for retrieval and modifications of customers.
  * [Get all customers](customers.md#get-all-customers) - returns all customers by filters.
  * [Search customers](customers.md#search-customers) - searches among active customers.
  * [Get customers open items](customers.md#get-customers-open-items) - returns open items of customers.
  * [Add customer](customers.md#add-customer) - adds a new customer.
  * [Update customer](customers.md#update-customer) - updates personal/internal information of a customer.
  * [Merge customers](customers.md#merge-customers) - merges two customers into one.
  * [Add customer file](customers.md#add-customer-file) - adds a new file to a customer.
* [Finance](finance.md) - operations related to financial settings, bills and payments.
  * [Get all exchange rates](finance.md#get-all-exchange-rates) - returns all exchange rates of the enterprise.
  * [Get all cashiers](finance.md#get-all-cashiers) - returns all cashiers of the enterprise.
  * [Get all cashier transactions](finance.md#get-all-cashier-transactions) - returns all cashier transactions in an interval.
  * [Get all accounting categories](finance.md#get-all-accounting-categories) - returns all accounting categories of the enterprise.
  * [Get all accounting items](finance.md#get-all-accounting-items) - returns all accounting items in an interval.
  * [Update accounting items](finance.md#update-accounting-items) - updates assignment of accounting items.
  * [Get all bills](finance.md#get-all-bills) - returns all bills by filters.
  * [Add bill](finance.md#add-bill) - adds a new bill for an account.
  * [Delete bill](finance.md#delete-bill) - deletes empty bill.
  * [Close bill](finance.md#close-bill) - closes a bill.
  * [Get bill PDF](finance.md#get-bill-pdf) - returns PDF version of bill.
  * [Get all outlet items](finance.md#get-all-outlet-items) - returns all outlet items in an interval.
  * [Get all credit cards](finance.md#get-all-credit-cards) - returns all credit cards by filters.
  * [Charge credit card](finance.md#charge-credit-card) - charges specified customer credit card.
  * [Get all preauthorizations by customers](finance.md#get-all-preauthorizations-by-customers) - returns all preauthorizations of the specified customers.
  * [Add credit card payment](finance.md#add-credit-card-payment) - adds a new credit card payment.
  * [Add tokenized credit card](finance.md#add-tokenized-credit-card) - adds a new tokenized credit card.
  * [Add external payment](finance.md#add-external-payment) - adds a new external payment.
  * [Add alternative payment](finance.md#add-alternative-payment) - adds a new alternative payment.
  * [Add outlet bills](finance.md#add-outlet-bills) - adds new outlet bills with items.
* [Integrations](integrations.md) - operations related to integrations, devices and commands to them.
  * [Get all devices](integrations.md#get-all-devices) - returns all physical devices defined in the enterprise.
  * [Get all commands](integrations.md#get-all-commands) - returns all active commands issued for the client.
  * [Get all commands by ids](integrations.md#get-all-commands-by-ids) - returns all commands by their identifiers.
  * [Add printer command](integrations.md#add-printer-command) - adds a new command for a printer to print a document.
  * [Add key cutter command](integrations.md#add-key-cutter-command) - adds a new command for key cutter to cut keys.
  * [Update command](integrations.md#update-command) - updates a command for a device.
