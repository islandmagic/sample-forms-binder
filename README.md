# Proposal for non-standard winlink form management

## Problem Statement
The Winlink standard form package is quite large (2.2MB zip) and contains numerous forms (~100). The editing and publishing process is centralized. A collection of independently developed forms (so called specialized) has been made available as an ad-hoc download from winlink.org [1]. There are approximately 16 publishers, but no mechanism for users to discover specialized forms through their client applications. Installing these forms is cumbersome and requires unzipping files in the correct location. Additionally, only forms in the standard package can auto-update, with no mechanism for manually added forms to notify users of updates.

## Proposal
Create a protocol for form publishers to register their forms with a central directory, allowing users to browse and subscribe to a collection of forms from specific publishers. Publishers can signal when updated versions are available, and subscribed users will automatically download the updates.

### Terms Definition
Publisher: A party (person or entity) responsible for assembling and publishing forms for a specific purpose. May or may not author the forms themselves. Examples include agencies, cities, local entities or individuals.
Binder: A collection of one or many forms from a publisher.
Hub: A centralized directory of all available binders.

### Envisioned Flow
1. For each binder, form files are hosted on a free, public GitHub git repository. This provides version control and opens the possibility for anyone to submit contributions to the form authors.
2. A simple JSON file (binder) describes the purpose of the forms and other metadata, and is placed in the root of the git repository.
3. Publishers self register their binders with the hub by submitting an HTTPS URL [2] for the binder, which contains all necessary information for the client application to present to the user.
4. The client application connects to the hub and retrieves all available binders. Users can browse a directory of binders and decide which ones to subscribe to. Subscribed forms are retrieved from the binder git repository and stored locally.
5. Periodically, the client app fetches the subscribed binders' files to determine if new versions have been published. If a new version is detected, the client automatically retrieves the updated forms.

A binder can be as simple as one form or contain a more elaborate folder structure with multiple forms.

[1]: https://winlink.org/content/specialized_forms_download_process_instructions
[2]: https://raw.githubusercontent.com/islandmagic/sample-forms-binder/master/binder.json
