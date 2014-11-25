# Welcome to Pardot Docs

For full documentation visit [developer.pardot.com](/kb/api-version-3/http://developer.pardot.com).

## Commands

* `mkdocs new [dir-name]` - Create a new project.
* `mkdocs serve` - Start the live-reloading docs server.
* `mkdocs build` - Build the documentation site.
* `mkdocs help` - Print this help message.

## Project layout

    mkdocs.yml    # The configuration file.
    docs/
        index.md  # The documentation homepage.
        ...       # Other markdown pages, images and other files.


Pages are created within mkdocs.yml, and are structured like this:

	pages:
	- ['index.md', 'Home']
	- ['kb/overview.md', 'Knowledge Base', 'Overview']
	- ['kb/subpage.md', 'Knowledge Base', 'Sub Page']
	- ['kb/querying-prospects.md', 'Querying Prospects']

"KB" itself is not a page, but a directory hierarchy. Within the docs folder, add a hierarchy to fit and create markdown files for each.

H1s and H2s will automatically enter the sidebar format and use scrollspy to highlight the section of the document.

More information on project structure and deployment can be found at [MakeDocs.org](/kb/api-version-3/http://www.mkdocs.org/)


## [](/kb/api-version-3/#introduction-a-name-intro-id-intro-a-)Introduction

This reference provides an in-depth explanation of Pardot's
API's functionality. Each section of this reference describes an
individual feature of the API in detail. To most effectively
navigate this guide, begin by studying the [Overview](/kb/api-version-3/overview), [Authentication](/kb/api-version-3/authentication), and [Using the Pardot API](/kb/api-version-3/using-the-pardot-api) sections. After
doing so, refer to the sections listed after [Using the Pardot API](/kb/api-version-3/using-the-pardot-api) in the [Table of Contents](/kb/api-version-3/#contents) to leverage the desired features.
Each of these sections is designed to be consulted independently
and in any order. References for [Object Fields](/kb/api-version-3/object-field-references) and [Error Codes &amp; Messages](/kb/api-version-3/error-codes-and-messages) are also
provided.

## [](/kb/api-version-3/#table-of-contents-)Table of Contents

*   **[Overview](/kb/api-version-3/overview)**
*   **[Authentication](/kb/api-version-3/authentication)**
*   **[Using the Pardot API](/kb/api-version-3/using-the-pardot-api)**
* Emails
    *   **[Reading Emails](/kb/api-version-3/reading-emails)**
    *   **[Sending One To One Emails](/kb/api-version-3/sending-one-to-one-emails)**
    *   **[Sending List Emails](/kb/api-version-3/sending-list-emails)**
* Lists
    *   **[Querying Lists](/kb/api-version-3/querying-lists)**
        *   [Supported Operations](/kb/api-version-3/querying-lists#supported-operations)
        *   [Supported Search Criteria](/kb/api-version-3/querying-lists#supported-search-criteria)
        *   [Manipulating the Result Set](/kb/api-version-3/querying-lists#manipulating-the-result-set)
        *   [Supported Sorting Operations](/kb/api-version-3/querying-lists#supported-sorting-options)
        *   [XML Response Format](/kb/api-version-3/querying-lists#xml-response-format)
    *   **[Using Lists](/kb/api-version-3/using-lists)**
         *   [Supported Operations](/kb/api-version-3/using-lists#supported-operations)
         *   [XML Response Formats](/kb/api-version-3/using-lists#xml-response-formats)
         *   [Updating Field Values](/kb/api-version-3/using-lists#updating-field-values)
*   Opportunities
    *   **[Querying Opportunities](/kb/api-version-3/querying-opportunities)**
        *   [Supported Operations](/kb/api-version-3/querying-opportunities#supported-operations)
        *   [Supported Search Criteria](/kb/api-version-3/querying-opportunities#supported-search-criteria)
        *   [Manipulating the Result Set](/kb/api-version-3/querying-opportunities#manipulating-the-result-set)
        *   [Supported Sorting Operations](/kb/api-version-3/querying-opportunities#supported-sorting-options)
        *   [XML Response Format](/kb/api-version-3/querying-opportunities#xml-response-format)
    *   **[Using Opportunities](/kb/api-version-3/using-opportunities)**
        *   [Supported Operations](/kb/api-version-3/using-opportunities#supported-operations)
        *   [XML Response Formats](/kb/api-version-3/using-opportunities#xml-response-formats)
        *   [Updating Field Values](/kb/api-version-3/using-opportunities#updating-field-values)
*   Prospects
    *   **[Querying Prospects](/kb/api-version-3/querying-prospects)**
        *   [Supported Operations](/kb/api-version-3/querying-prospects#supported-operations)
        *   [Supported Search Criteria](/kb/api-version-3/querying-prospects#supported-search-criteria)
        *   [Manipulating the Result Set](/kb/api-version-3/querying-prospects#manipulating-the-result-set)
        *   [Supported Sorting Options](/kb/api-version-3/querying-prospects#supported-sorting-options)
        *   [XML Response Format](/kb/api-version-3/querying-prospects#xml-response-format)

        *   **[Using Prospects](/kb/api-version-3/using-prospects)**
            *   [Supported Operations](/kb/api-version-3/using-prospects#supported-operations)
            *   [XML Response Formats](/kb/api-version-3/using-prospects#xml-response-formats)
            *   [Assigning and Reassigning Prospects](/kb/api-version-3/using-prospects#assigning-and-reassigning-prospects)
            *   [Creating Prospects](/kb/api-version-3/using-prospects#creating-prospects)
            *   [Updating Field Values](/kb/api-version-3/using-prospects#updating-field-values)
            *   [Updating Fields with Predefined Values](/kb/api-version-3/using-prospects#updating-fields-with-predefined-values)
            *   [Updating Fields with Multiple Values](/kb/api-version-3/using-prospects#updating-fields-with-multiple-values)
            *   [Updating List Subscriptions](/kb/api-version-3/using-prospects#updating-list-memberships)
            *   [Updating Profile Criteria Matching Statuses](/kb/api-version-3/using-prospects#updating-profile-criteria-matching-statuses)
*   Prospect Accounts
    *   **[Querying Prospect Accounts](/kb/api-version-3/querying-prospect-accounts)**
    *   [Supported Operations](/kb/api-version-3/querying-prospect-accounts#supported-operations)
    *   [Supported Search Criteria](/kb/api-version-3/querying-prospect-accounts#supported-search-criteria)
        *   [Manipulating the Result Set](/kb/api-version-3/querying-prospect-accounts#manipulating-the-result-set)
        *   [Supported Sorting Options](/kb/api-version-3/querying-prospect-accounts#supported-sorting-options)
        *   [XML Response Format](/kb/api-version-3/querying-prospect-accounts#xml-response-format)

            *   **[Using Prospect Accounts](/kb/api-version-3/using-prospect-accounts)**

                *   [Supported Operations](/kb/api-version-3/using-prospect-accounts#supported-operations)
                *   [XML Response Formats](/kb/api-version-3/using-prospect-accounts#xml-response-formats)
                *   [Creating Prospect Accounts](/kb/api-version-3/using-prospect-accounts#creating-prospect-accounts)
*   Users
     *   **[Querying Users](/kb/api-version-3/querying-users)**
        *   [Supported Operations](/kb/api-version-3/querying-users#supported-operations)
        *   [Supported Search Criteria](/kb/api-version-3/querying-users#supported-search-criteria)
        *   [Manipulating the Result Set](/kb/api-version-3/querying-users#manipulating-the-result-set)
        *   [Supported Sorting Options](/kb/api-version-3/querying-users#supported-sorting-options)
        *   [XML Response Format](/kb/api-version-3/querying-users#xml-response-format)
            *   **[Using Users](/kb/api-version-3/using-users)**
                *   [Supported Operations](/kb/api-version-3/using-users#supported-operations)
                *   [XML Response Format](/kb/api-version-3/using-users#xml-response-format)
*   Vists
    *   **[Querying Visits](/kb/api-version-3/querying-visits)**
        *   [Supported Operations](/kb/api-version-3/querying-visits#sort-order)
        *   [Supported Search Criteria](/kb/api-version-3/querying-visits#supported-search-criteria)
        *   [Manipulating the Result Set](/kb/api-version-3/querying-visits#manipulating-the-result-set)
        *   [Sort Order](/kb/api-version-3/querying-visits#sort-order)
        *   [XML Response Format](/kb/api-version-3/querying-visits#xml-response-format)
    *   **[Using Visits](/kb/api-version-3/using-visits)**
        *   [Supported Operations](/kb/api-version-3/using-visits#supported-operations)
        *   [XML Response Formats](/kb/api-version-3/using-visits#xml-response-formats)
    *   **[Querying Visitors](/kb/api-version-3/querying-visitors)**
        *   [Supported Operations](/kb/api-version-3/querying-visitors#supported-operations)
        *   [Supported Search Criteria](/kb/api-version-3/querying-visitors#supported-search-criteria)
        *   [Manipulating the Result Set](/kb/api-version-3/querying-visitors#manipulating-the-result-set)
        *   [Supported Sorting Options](/kb/api-version-3/querying-visitors#supported-sorting-options)
        *   [XML Response Format](/kb/api-version-3/querying-visitors#xml-response-format)
    *   **[Using Visitors](/kb/api-version-3/using-visitors)**
        *   [Supported Operations](/kb/api-version-3/using-visitors#supported-operations)
        *   [XML Response Formats](/kb/api-version-3/using-visitors#xml-response-formats)
        *   [Assigning and Reassigning Visitors](/kb/api-version-3/using-visitors#assigning-and-reassigning-visitors)
    *   **[Object Field References](/kb/api-version-3/object-field-references)**
        *   [Identified Company](/kb/api-version-3/object-field-references#identified-company)
        *   [List](/kb/api-version-3/object-field-references#list)
        *   [List Membership](/kb/api-version-3/object-field-references#list-membership)
        *   [Opportunity](/kb/api-version-3/object-field-references#opportunity)
        *   [Profile](/kb/api-version-3/object-field-references#profile)
        *   [Profile Criteria](/kb/api-version-3/object-field-references#profile-criteria)
        *   [Prospect](/kb/api-version-3/object-field-references#prospect)
        *   [Prospect Account](/kb/api-version-3/object-field-references#prospectAccount)
        *   [User](/kb/api-version-3/object-field-references#user)
        *   [Visit](/kb/api-version-3/object-field-references#visit)
        *   [Visitor](/kb/api-version-3/object-field-references#visitor)
        *   [Visitor Activity](/kb/api-version-3/object-field-references#visitor-activity)
        *   [Visitor Referrer](/kb/api-version-3/object-field-references#visitor-referrer)

*   **[Error Codes &amp; Messages](/kb/api-version-3/error-codes-and-messages)**
