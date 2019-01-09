---
date: 2018-09-10
title: Authorization
categories:
  - Documentation
type: Document
showSidebar: false
published: false
nav_ordering: 10
pageTitle: "Authorization"
---

## Overview
Every record is made up of `fields`. Fields have metadata, including who is the `owner` of the field and if necessary, a `proxy owner` of the field. By default, a proxy owner can be added to a field only for those fields created during new `record` creation. To access a field, the system checks if the accessor has a `consent artifact` AND if you are the owner of the field for which consent has been given.

Consent artifact looks like:
```
id: ,         # id of the consent
user_id: ,    # which user is given consent OR
role_id: ,    # which role is given consent
action: [],   # any one of create/read/update/delete      
fields: [],   # field list, * wildcard supported
filter: [],   # any criteria     
proxy: ,      # true if a proxy is using the consent 
created_by: , # which user created the consent
created_at: , # when was it created
awarded_by:   # which user awarded the consent    
awarded_at:   # when was it awarded
expires_at: , # when will it expire
nonce: ,      # with a nonce the consent can only be used once
```

Nothing is accessible without Consent. So, if by chance, all consent artifacts are deleted, instead of opening up, the Registry will be closed for access. Also, one cannot delete a Consent but can only end date it.

Roles can be simply understood as a way to connect a group of users to consent. Role would already be setup externally in the Authentication mechanism. OpenSABER would expect the User and Role imformation to be present in the JWT as per the OpenID Connect Flow.

## Ownership assignment
Following diagram explains how field ownership mappings are dynamically managed. Since, OpenSABER vocabulary is extendable, it would be hard to setup ownership everytime a new field is introduced. Rather than that, a combination of consent and simple workflow, would assign ownership of record level fields.

[![Ownership assignment](/images/ownership-assignment.png)](/images/ownership-assignment.png){:target="_blank"}


A Proxy entity is being elevated, since there maybe many cases where registry initiation may happen via a Proxy source than organic. However, once the Proxy has inserted data, control needs to go back to the record owner to prevent misuse by the Proxy.

## Scenarios
Let's look at the following scenario's to understand possible authorization flows:

### Scenario #1 - Proxy scenario
An entity creating a record where record is not of the entity. Examples:
- A head master creating teacher records
- A bulk importing mechanism 

Record creation consents will be awarded to the Proxy (e.g. headmaster who is registering teachers) via a consent artifact such as
```
# custom consent: creator_f1_f2_f3_f4
action: [create],      # ACTION SCOPE - creating properties
fields: [f1,f2,f3,f4], # PROPERTIES SCOPE - f1,f2,f3,f4
filter: [id==null]     # SUBJECTS SCOPE - new subject
proxy: true            # Indicates that the user with this consent is a proxy so the default rule of field writer becoming the owner is overriden by field writer becoming the proxy. The owner will remain the record owner.
```
The above means that the proxy, can create 4 fields - f1, f2, f3, f4 ONLY when the subject does not exists. It cannot read, update or delete the data.

Suppose, the proxy requires to read the fields it proxied, then the following consent is required:
```
# canned consent: read_as_proxy
action: [read],               # ACTION SCOPE - reading properties
fields: [f1,f2,f3,f4],        # PROPERTIES SCOPE - f1,f2,f3,f4
filter: [proxy.id==$(userid)] # SUBJECTS SCOPE - proxied subject
```
Consequently, for any entity to access it's own records, the following consent artifact is necessary:
```
# canned consent: rw_as_owner
action: [read, update],       # ACTION SCOPE - r/w
fields: [*],                  # PROPERTIES SCOPE - f1,f2,f3,f4
filter: [owner.id==$(userid)] # SUBJECTS SCOPE - self
```
The above means that you can read/write all fields for which you are the owner. Of course, if you want to explicitly list fields, it is possible too.

### Scenario #2 - Self registration
A user creating the record of itself
Example:
- self registration

Consent is a union of
```
# canned consent: godlike_creator
action: [create],   # ACTION SCOPE - creating properties
fields: [*],        # PROPERTIES SCOPE - any property
filter: [id==null]  # SUBJECTS SCOPE - new subject
```
and
```
# canned consent: rw_as_owner
```
Note that multiple consents stack up and have a default union effect, than most_restrictive, intersection, etc.

### Scenario #3 - Publisher
A user adding a new field to an existing record of some other entity
Example:
- Any publishing entity, for instance, badge awarded to a teacher

Consent needed:
```
# canned consent: publish_f5
action: [create,update],  # ACTION SCOPE - add or update
fields: [f5],             # PROPERTIES SCOPE - f5
filter: []                # SUBJECTS SCOPE - any
```
If f5 represented the field into which badge is updated, the above consent grants creation or updation of the badge to the entity which has the consent.

Of course, one may restrict a publisher so that it may only target a set of subjects via `filter`.

### Scenario #4 - Reader
If a user wishes to grant read access to otherwise private info, she can give consent as:
```
# dynamic consent: consent_hgyi6t3tgjasd98hdgasd
action: [read],               # ACTION SCOPE - read
fields: [f1],                 # PROPERTIES SCOPE - f1
awarded_by: [shashank@diksha]
```
In this case, `shashank@diksha` is an indicative identifier. And `shashank@diksha` is essentially granting consent to read their data in f1. It is not necessary, that `shashank@diksha` is the `owner of the field`, as it may be written into only by a specific publicher. [Publisher scenario]

## Authorization Negotiation

[![Venn Diagram](/images/venn-diagram-consent.png)](/images/venn-diagram-consent.png){:target="_blank"}

The above Venn diagram should indicate the various sets of fields possible in a Registry.

For instance, in the diagram above, 
- the registry has fields: `a, b, c, d, e, f, g, h`
- the requester requested for: `b, c, d, e, f, g, h`
- the requester had bearer consent only for `c`, so `b` was an unauthorised access
- the requester needed consent from Owner 1 for `f and g`
- the requester needed consent from Owner 2 for `d and e`
- Owner 1 gave consent for both `f and g` requested
- Owner 2 gave consent only for `d` and rejected consent for `e`
- Field `a` and `h` did not need consent since they were not requested. So, they should also not be returned to the user.

## Roles
Roles need to be mapped internally within the Registry.

## Open Items
- How to revoke a Consent artifact? Look at Open Badge spec.
- How to provide grant to another entity so that they may generate a Consent artifact?
- Does the ID Token contain Role identifier?

## Dependency

### Authentication
This wiki assumes that Authentication step is over and the Current User and the Role information is available.

[Authentication wiki](/authentication.html)
