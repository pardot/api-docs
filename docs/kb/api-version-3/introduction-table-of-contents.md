# API (version 3) - Introduction & Table of Contents


## [](#introduction-a-name-intro-id-intro-a-)Introduction

This reference provides an in-depth explanation of Pardot's
API's functionality. Each section of this reference describes an
individual feature of the API in detail. To most effectively
navigate this guide, begin by studying the [Overview](overview), [Authentication](authentication), and [Using the Pardot API](using-the-pardot-api) sections. After
doing so, refer to the sections listed after [Using the Pardot API](using-the-pardot-api) in the [Table of Contents](#contents) to leverage the desired features.
Each of these sections is designed to be consulted independently
and in any order. References for [Object Fields](object-field-references) and [Error Codes &amp; Messages](error-codes-and-messages) are also
provided.

## [](#table-of-contents-)Table of Contents

*   **[Introduction](#14746-intro)**
*   **[Overview](overview)**
*   **[Authentication](authentication)**
*   **[Using the Pardot API](using-the-pardot-api)**
* Emails
    *   **[Reading Emails](reading-emails)**
    *   **[Sending One To One Emails](#api-version-3-sending-one-to-one-emails)**
    *   **[Sending List Emails](#api-version-3-sending-list-emails)**
* Lists
    *   **[Querying Lists](querying-lists)**
        *   [Supported Operations](querying-lists#supported-operations)
        *   [Supported Search Criteria](querying-lists#supported-search-criteria)
        *   [Manipulating the Result Set](querying-lists#manipulating-the-result-set)
        *   [Supported Sorting Operations](querying-lists#supported-sorting-options)
        *   [XML Response Format](querying-lists#xml-response-format)
    *   **[Using Lists](using-lists)**
         *   [Supported Operations](using-lists#supported-operations)
         *   [XML Response Formats](using-lists#xml-response-formats)
         *   [Updating Field Values](using-lists#updating-field-values)
*   Opportunities
    *   **[Querying Opportunities](querying-opportunities)**
        *   [Supported Operations](querying-opportunities#supported-operations)
        *   [Supported Search Criteria](querying-opportunities#supported-search-criteria)
        *   [Manipulating the Result Set](querying-opportunities#manipulating-the-result-set)
        *   [Supported Sorting Operations](querying-opportunities#supported-sorting-options)
        *   [XML Response Format](querying-opportunities#xml-response-format)
    *   **[Using Opportunities](using-opportunities)**
        *   [Supported Operations](using-opportunities#supported-operations)
        *   [XML Response Formats](using-opportunities#xml-response-formats)
        *   [Updating Field Values](using-opportunities#updating-field-values)
*   Prospects
    *   **[Querying Prospects](querying-prospects)**
        *   [Supported Operations](querying-prospects#supported-operations)
        *   [Supported Search Criteria](querying-prospects#supported-search-criteria)
        *   [Manipulating the Result Set](querying-prospects#manipulating-the-result-set)
        *   [Supported Sorting Options](querying-prospects#supported-sorting-options)
        *   [XML Response Format](querying-prospects#xml-response-format)

        *   **[Using Prospects](using-prospects)**
            *   [Supported Operations](using-prospects#supported-operations)
            *   [XML Response Formats](using-prospects#xml-response-formats)
            *   [Assigning and Reassigning Prospects](using-prospects#assigning-and-reassigning-prospects)
            *   [Creating Prospects](using-prospects#creating-prospects)
            *   [Updating Field Values](using-prospects#updating-field-values)
            *   [Updating Fields with Predefined Values](using-prospects#updating-fields-with-predefined-values)
            *   [Updating Fields with Multiple Values](using-prospects#updating-fields-with-multiple-values)
            *   [Updating List Subscriptions](using-prospects#updating-list-memberships)
            *   [Updating Profile Criteria Matching Statuses](using-prospects#updating-profile-criteria-matching-statuses)
*   Prospect Accounts
    *   **[Querying Prospect Accounts](querying-prospect-accounts)**
    *   [Supported Operations](querying-prospect-accounts#supported-operations)
    *   [Supported Search Criteria](querying-prospect-accounts#supported-search-criteria)
        *   [Manipulating the Result Set](querying-prospect-accounts#manipulating-the-result-set)
        *   [Supported Sorting Options](querying-prospect-accounts#supported-sorting-options)
        *   [XML Response Format](querying-prospect-accounts#xml-response-format)

            *   **[Using Prospect Accounts](using-prospect-accounts)**

                *   [Supported Operations](using-prospect-accounts#supported-operations)
                *   [XML Response Formats](using-prospect-accounts#xml-response-formats)
                *   [Creating Prospect Accounts](using-prospect-accounts#creating-prospect-accounts)
*   Users
     *   **[Querying Users](querying-users)**
        *   [Supported Operations](querying-users#supported-operations)
        *   [Supported Search Criteria](querying-users#supported-search-criteria)
        *   [Manipulating the Result Set](querying-users#manipulating-the-result-set)
        *   [Supported Sorting Options](querying-users#supported-sorting-options)
        *   [XML Response Format](querying-users#xml-response-format)
            *   **[Using Users](using-users)**
                *   [Supported Operations](using-users#supported-operations)
                *   [XML Response Format](using-users#xml-response-format)
*   Vists
    *   **[Querying Visits](querying-visits)**
        *   [Supported Operations](querying-visits#sort-order)
        *   [Supported Search Criteria](querying-visits#supported-search-criteria)
        *   [Manipulating the Result Set](querying-visits#manipulating-the-result-set)
        *   [Sort Order](querying-visits#sort-order)
        *   [XML Response Format](querying-visits#xml-response-format)
    *   **[Using Visits](using-visits)**
        *   [Supported Operations](using-visits#supported-operations)
        *   [XML Response Formats](using-visits#xml-response-formats)
    *   **[Querying Visitors](querying-visitors)**
        *   [Supported Operations](querying-visitors#supported-operations)
        *   [Supported Search Criteria](querying-visitors#supported-search-criteria)
        *   [Manipulating the Result Set](querying-visitors#manipulating-the-result-set)
        *   [Supported Sorting Options](querying-visitors#supported-sorting-options)
        *   [XML Response Format](querying-visitors#xml-response-format)
    *   **[Using Visitors](using-visitors)**
        *   [Supported Operations](using-visitors#supported-operations)
        *   [XML Response Formats](using-visitors#xml-response-formats)
        *   [Assigning and Reassigning Visitors](using-visitors#assigning-and-reassigning-visitors)
    *   **[Object Field References](object-field-references)**
        *   [Identified Company](object-field-references#identified-company)
        *   [List](object-field-references#list)
        *   [List Membership](object-field-references#list-membership)
        *   [Opportunity](object-field-references#opportunity)
        *   [Profile](object-field-references#profile)
        *   [Profile Criteria](object-field-references#profile-criteria)
        *   [Prospect](object-field-references#prospect)
        *   [Prospect Account](object-field-references#prospectAccount)
        *   [User](object-field-references#user)
        *   [Visit](object-field-references#visit)
        *   [Visitor](object-field-references#visitor)
        *   [Visitor Activity](object-field-references#visitor-activity)
        *   [Visitor Referrer](object-field-references#visitor-referrer)

*   **[Error Codes &amp; Messages](error-codes-and-messages)**
