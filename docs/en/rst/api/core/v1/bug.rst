Bugs
====

The REST API for creating, changing, and getting the details of bugs.

This part of the Bugzilla REST API allows you to file new bugs in Bugzilla and
to get information about existing bugs.

.. _rest_single_bug:

Get Bug
-------

Gets information about particular bugs in the database.

**Request**

To get information about a particular bug using its ID or alias:

.. code-block::  text

   GET /rest/bug/(id_or_alias)

You can also use :ref:`rest_search_bugs` to return more than one bug at a time
by specifying bug IDs as the search terms.

.. code-block:: text

   GET /rest/bug?id=12434,43421

================  =====  ======================================================
name              type   description
================  =====  ======================================================
**id_or_alias**   mixed  An integer bug ID or a bug alias string.
================  =====  ======================================================

**Response**

.. code-block:: js

   {
     "faults": [],
     "bugs": [
       {
         "assigned_to_detail": {
           "id": 2,
           "real_name": "Test User",
           "nick": "user",
           "name": "user@bugzilla.org",
           "email": "user@bugzilla.org"
         },
         "flags": [
           {
             "type_id": 11,
             "modification_date": "2014-09-28T21:03:47Z",
             "name": "blocker",
             "status": "?",
             "id": 2906,
             "setter": "user@bugzilla.org",
             "creation_date": "2014-09-28T21:03:47Z"
           }
         ],
         "resolution": "INVALID",
         "id": 35,
         "type": "defect",
         "qa_contact": "",
         "triage_owner": "",
         "version": "1.0",
         "status": "RESOLVED",
         "creator": "user@bugzilla.org",
         "cf_drop_down": "---",
         "summary": "test bug",
         "last_change_time": "2014-09-23T19:12:17Z",
         "platform": "All",
         "url": "",
         "classification": "Unclassified",
         "cc_detail": [
           {
             "id": 786,
             "real_name": "Foo Bar",
             "nick": "foo",
             "name": "foo@bar.com",
             "email": "foo@bar.com"
           },
         ],
         "priority": "P1",
         "is_confirmed": true,
         "creation_time": "2000-07-25T13:50:04Z",
         "assigned_to": "user@bugzilla.org",
         "flags": [],
         "alias": null,
         "cf_large_text": "",
         "groups": [],
         "op_sys": "All",
         "cf_bug_id": null,
         "depends_on": [],
         "is_cc_accessible": true,
         "is_open": false,
         "cf_qa_list_4": "---",
         "keywords": [],
         "cc": [
           "foo@bar.com",
         ],
         "see_also": [],
         "deadline": null,
         "is_creator_accessible": true,
         "whiteboard": "",
         "dupe_of": null,
         "duplicates": [],
         "target_milestone": "---",
         "cf_mulitple_select": [],
         "component": "SaltSprinkler",
         "severity": "critical",
         "cf_date": null,
         "product": "FoodReplicator",
         "creator_detail": {
           "id": 28,
           "real_name": "hello",
           "nick": "namachi",
           "name": "user@bugzilla.org",
           "email": "namachi@netscape.com"
         },
         "cf_free_text": "",
         "blocks": [],
         "regressed_by": [],
         "regressions": [],
         "comment_count": 12
       }
     ]
   }

``bugs`` (array) Each bug object contains information about the bugs with valid
ids containing the following items:

These fields are returned by default or by specifying ``_default`` in
``include_fields``.

=====================  ========  ================================================
name                   type      description
=====================  ========  ================================================
actual_time            double    The total number of hours that this bug has
                                 taken so far. If you are not in the time-tracking
                                 group, this field will not be included in the
                                 return value.
alias                  string    The unique alias of this bug. A ``null`` value
                                 will be returned if this bug has no alias.
assigned_to            string    The login name of the user to whom the bug is
                                 assigned.
assigned_to_detail     object    An object containing detailed user information
                                 for the assigned_to. To see the keys included
                                 in the user detail object, see below.
blocks                 array     The IDs of bugs that are "blocked" by this bug.
cc                     array     The login names of users on the CC list of this
                                 bug.
cc_detail              array     Array of objects containing detailed user
                                 information for each of the cc list members.
                                 To see the keys included in the user detail
                                 object, see below.
classification         string    The name of the current classification the bug
                                 is in.
component              string    The name of the current component of this bug.
creation_time          datetime  When the bug was created.
creator                string    The login name of the person who filed this bug
                                 (the reporter).
creator_detail         object    An object containing detailed user information
                                 for the creator. To see the keys included in the
                                 user detail object, see below.
deadline               string    The day that this bug is due to be completed, in
                                 the format ``YYYY-MM-DD``.
depends_on             array     The IDs of bugs that this bug "depends on".
dupe_of                int       The bug ID of the bug that this bug is a
                                 duplicate of. If this bug isn't a duplicate of
                                 any bug, this will be null.
duplicates             array     The ids of bugs that are marked as duplicate of
                                 this bug.
estimated_time         double    The number of hours that it was estimated that
                                 this bug would take. If you are not in the
                                 time-tracking group, this field will not be
                                 included in the return value.
flags                  array     An array of objects containing the information
                                 about flags currently set for the bug. Each flag
                                 objects contains the following items
groups                 array     The names of all the groups that this bug is in.
id                     int       The unique numeric ID of this bug.
is_cc_accessible       boolean   If true, this bug can be accessed by members of
                                 the CC list, even if they are not in the groups
                                 the bug is restricted to.
is_confirmed           boolean   ``true`` if the bug has been confirmed. Usually
                                 this means that the bug has at some point been
                                 moved out of the ``UNCONFIRMED`` status and into
                                 another open status.
is_open                boolean   ``true`` if this bug is open, ``false`` if it
                                 is closed.
is_creator_accessible  boolean   If ``true``, this bug can be accessed by the
                                 creator of the bug, even if they are not a
                                 member of the groups the bug is restricted to.
keywords               array     Each keyword that is on this bug.
last_change_time       datetime  When the bug was last changed.
comment_count          int       Number of comments associated with the bug.
op_sys                 string    The name of the operating system that the bug
                                 was filed against.
platform               string    The name of the platform (hardware) that the bug
                                 was filed against.
priority               string    The priority of the bug.
product                string    The name of the product this bug is in.
qa_contact             string    The login name of the current QA Contact on the
                                 bug.
qa_contact_detail      object    An object containing detailed user information
                                 for the qa_contact. To see the keys included in
                                 the user detail object, see below.
regressed_by           array     The IDs of bugs that introduced this bug.
regressions            array     The IDs of bugs that are introduced by this bug.
remaining_time         double    The number of hours of work remaining until work
                                 on this bug is complete. If you are not in the
                                 time-tracking group, this field will not be
                                 included in the return value.
resolution             string    The current resolution of the bug, or an empty
                                 string if the bug is open.
see_also               array     The URLs in the See Also field on the bug.
severity               string    The current severity of the bug.
status                 string    The current status of the bug.
summary                string    The summary of this bug.
target_milestone       string    The milestone that this bug is supposed to be
                                 fixed by, or for closed bugs, the milestone that
                                 it was fixed for.
type                   string    The type of the bug.
update_token           string    The token that you would have to pass to the
                                 ``process_bug.cgi`` page in order to update this
                                 bug. This changes every time the bug is updated.
                                 This field is not returned to logged-out users.
url                    string    A URL that demonstrates the problem described in
                                 the bug, or is somehow related to the bug report.
version                string    The version the bug was reported against.
whiteboard             string    The value of the "status whiteboard" field on
                                 the bug.
=====================  ========  ================================================

Custom fields:

Every custom field in this installation will also be included in the
return value. Most fields are returned as strings. However, some field types have
different return values.

Normally custom fields are returned by default similar to normal bug fields or
you can specify only custom fields by using ``_custom`` in ``include_fields``.

Extra fields:

These fields are returned only by specifying ``_extra`` or the field name in
``include_fields``.

===================  ======  ====================================================
name                 type    description
===================  ======  ====================================================
attachments          array   Each array item is an Attachment object. See
                             :ref:`rest_attachments` for details of the object.
comments             array   Each array item is a Comment object. See
                             :ref:`rest_comments` for details of the object.
counts               object  An object containing the numbers of the items in the
                             following fields: ``attachments``, ``cc``,
                             ``comments``, ``keywords``, ``blocks``,
                             ``depends_on``, ``regressed_by``, ``regressions``
                             and ``duplicates``.
description          string  The description (initial comment) of the bug.
filed_via            string  How the bug was filed, e.g. ``standard_form``.
history              array   Each array item is a History object. See
                             :ref:`rest_history` for details of the object.
tags                 array   Each array item is a tag name. Note that tags are
                             personal to the currently logged in user and are not
                             the same as comment tags.
triage_owner         string  The login name of the Triage Owner of the bug's
                             component.
triage_owner_detail  object  An object containing detailed user information for
                             the ``triage_owner``. To see the keys included in
                             the user detail object, see below.
===================  ======  ====================================================

User object:

=========  ======  ==============================================================
name       type    description
=========  ======  ==============================================================
id         int     The user ID for this user.
real_name  string  The 'real' name for this user, if any.
nick       string  The user's nickname. Currently this is extracted from the
                   real_name, name or email field.
name       string  The user's Bugzilla login.
email      string  The user's email address. Currently this is the same value as
                   the name.
=========  ======  ==============================================================

Flag object:

=================  ========  ====================================================
name               type      description
=================  ========  ====================================================
id                 int       The ID of the flag.
name               string    The name of the flag.
type_id            int       The type ID of the flag.
creation_date      datetime  The timestamp when this flag was originally created.
modification_date  datetime  The timestamp when the flag was last modified.
status             string    The current status of the flag.
setter             string    The login name of the user who created or last
                             modified the flag.
requestee          string    The login name of the user this flag has been
                             requested to be granted or denied. Note, this field
                             is only returned if a requestee is set.
=================  ========  ====================================================

Custom field object:

You can specify to only return custom fields by specifying ``_custom`` or the
field name in ``include_fields``.

* Bug ID Fields: (int)
* Multiple-Selection Fields: (array of strings)
* Date/Time Fields: (datetime)

**Errors**

* 100 (Invalid Bug Alias)
  If you specified an alias and there is no bug with that alias.
* 101 (Invalid Bug ID)
  The bug_id you specified doesn't exist in the database.
* 102 (Access Denied)
  You do not have access to the bug_id you specified.

.. _rest_history:

Bug History
-----------

Gets the history of changes for particular bugs in the database.

**Request**

To get the history for a specific bug ID:

.. code-block:: text

   GET /rest/bug/(id)/history

To get the history for a bug since a specific date:

.. code-block:: text

   GET /rest/bug/(id)/history?new_since=YYYY-MM-DD

=========  ========  ============================================================
name       type      description
=========  ========  ============================================================
**id**     mixed     An integer bug ID or alias.
new_since  datetime  A datetime timestamp to only show history since.
=========  ========  ============================================================

**Response**

.. code-block:: js

   {
     "bugs": [
       {
         "alias": null,
         "history": [
           {
             "when": "2014-09-23T19:12:17Z",
             "who": "user@bugzilla.org",
             "changes": [
               {
                 "added": "P1",
                 "field_name": "priority",
                 "removed": "P2"
               },
               {
                 "removed": "blocker",
                 "field_name": "severity",
                 "added": "critical"
               }
             ]
           },
           {
             "when": "2014-09-28T21:03:47Z",
             "who": "user@bugzilla.org",
             "changes": [
               {
                 "added": "blocker?",
                 "removed": "",
                 "field_name": "flagtypes.name"
               }
             ]
           }
         ],
         "id": 35
       }
     ]
   }

``bugs`` (array) Bug objects each containing the following items:

=======  ======  ================================================================
name     type    description
=======  ======  ================================================================
id       int     The numeric ID of the bug.
alias    string  The unique alias of this bug. A ``null`` value will be returned
                 if this bug has no alias.
history  array   An array of History objects.
=======  ======  ================================================================

History object:

=======  ========  ==============================================================
name     type      description
=======  ========  ==============================================================
when     datetime  The date the bug activity/change happened.
who      string    The login name of the user who performed the bug change.
changes  array     An array of Change objects which contain all the changes that
                   happened to the bug at this time (as specified by ``when``).
=======  ========  ==============================================================

Change object:

=============  ======  ==========================================================
name           type    description
=============  ======  ==========================================================
field_name     string  The name of the bug field that has changed.
removed        string  The previous value of the bug field which has been
                       deleted by the change.
added          string  The new value of the bug field which has been added
                       by the change.
attachment_id  int     The ID of the attachment that was changed.
                       This only appears if the change was to an attachment,
                       otherwise ``attachment_id`` will not be present in this
                       object.
=============  ======  ==========================================================

**Errors**

Same as :ref:`rest_single_bug`.

.. _rest_search_bugs:

Search Bugs
-----------

Allows you to search for bugs based on particular criteria.

**Request**

To search for bugs:

.. code-block:: text

   GET /rest/bug

Unless otherwise specified in the description of a parameter, bugs are
returned if they match *exactly* the criteria you specify in these
parameters. That is, we don't match against substrings--if a bug is in
the "Widgets" product and you ask for bugs in the "Widg" product, you
won't get anything.

Criteria are joined in a logical AND. That is, you will be returned
bugs that match *all* of the criteria, not bugs that match *any* of
the criteria.

Each parameter can be either the type it says, or a list of the types
it says. If you pass an array, it means "Give me bugs with *any* of
these values." For example, if you wanted bugs that were in either
the "Foo" or "Bar" products, you'd pass:

.. code-block:: text

   GET /rest/bug?product=Foo&product=Bar

Some Bugzillas may treat your arguments case-sensitively, depending
on what database system they are using. Most commonly, though, Bugzilla is
not case-sensitive with the arguments passed (because MySQL is the
most-common database to use with Bugzilla, and MySQL is not case sensitive).

In addition to the fields listed below, you may also use criteria that
is similar to what is used in the Advanced Search screen of the Bugzilla
UI. This includes fields specified by ``Search by Change History`` and
``Custom Search``. The easiest way to determine what the field names are and what
format Bugzilla expects is to first construct your query using the
Advanced Search UI, execute it and use the query parameters in they URL
as your query for the REST call.

================  ========  =====================================================
name              type      description
================  ========  =====================================================
alias             string    The unique alias of this bug. A ``null`` value will
                            be returned if this bug has no alias.
assigned_to       string    The login name of a user that a bug is assigned to.
component         string    The name of the Component that the bug is in. Note
                            that if there are multiple Components with the same
                            name, and you search for that name, bugs in *all*
                            those Components will be returned. If you don't want
                            this, be sure to also specify the ``product`` argument.
count_only        boolean   If set to true, an object with a single key called
                            "bug_count" will be returned which is the number of
                            bugs that matched the search.
creation_time     datetime  Searches for bugs that were created at this time or
                            later. May not be an array.
creator           string    The login name of the user who created the bug. You
                            can also pass this argument with the name
                            ``reporter``, for backwards compatibility with
                            older Bugzillas.
description       string    The description (initial comment) of the bug.
filed_via         string    Searches for bugs that were created with this method.
id                int       The numeric ID of the bug.
last_change_time  datetime  Searches for bugs that were modified at this time
                            or later. May not be an array.
limit             int       Limit the number of results returned. If the value is
                            unset, zero or greater than the maximum value set by
                            the administrator, which is 10,000 by default, then
                            the maximum value will be used instead. This is a
                            preventive measure against DoS-like attacks on
                            Bugzilla. Use the ``offset`` argument described below
                            to retrieve more results.
longdescs.count   int       The number of comments a bug has. The bug's description
                            is the first comment. For example, to find bugs which someone
                            has commented on after they have been filed, search on
                            ``longdescs.count`` *greater than* 1.
offset            int       Used in conjunction with the ``limit`` argument,
                            ``offset`` defines the starting position for the
                            search. For example, given a search that would
                            return 100 bugs, setting ``limit`` to 10 and
                            ``offset`` to 10 would return bugs 11 through 20
                            from the set of 100.
op_sys            string    The "Operating System" field of a bug.
platform          string    The Platform (sometimes called "Hardware") field of
                            a bug.
priority          string    The Priority field on a bug.
product           string    The name of the Product that the bug is in.
quicksearch       string    Search for bugs using quicksearch syntax.
resolution        string    The current resolution--only set if a bug is closed.
                            You can find open bugs by searching for bugs with an
                            empty resolution.
severity          string    The Severity field on a bug.
status            string    The current status of a bug (not including its
                            resolution, if it has one, which is a separate field
                            above).
summary           string    Searches for substrings in the single-line Summary
                            field on bugs. If you specify an array, then bugs
                            whose summaries match *any* of the passed substrings
                            will be returned. Note that unlike searching in the
                            Bugzilla UI, substrings are not split on spaces. So
                            searching for ``foo bar`` will match "This is a foo
                            bar" but not "This foo is a bar". ``['foo', 'bar']``,
                            would, however, match the second item.
tags              string    Searches for a bug with the specified tag. If you
                            specify an array, then any bugs that match *any* of
                            the tags will be returned. Note that tags are
                            personal to the currently logged in user.
target_milestone  string    The Target Milestone field of a bug. Note that even
                            if this Bugzilla does not have the Target Milestone
                            field enabled, you can still search for bugs by
                            Target Milestone. However, it is likely that in that
                            case, most bugs will not have a Target Milestone set
                            (it defaults to "---" when the field isn't enabled).
qa_contact        string    The login name of the bug's QA Contact. Note that
                            even if this Bugzilla does not have the QA Contact
                            field enabled, you can still search for bugs by QA
                            Contact (though it is likely that no bug will have a
                            QA Contact set, if the field is disabled).
triage_owner      string    The login name of the Triage Owner of a bug's
                            component.
type              string    The Type field on a bug.
url               string    The "URL" field of a bug.
version           string    The Version field of a bug.
whiteboard        string    Search the "Status Whiteboard" field on bugs for a
                            substring. Works the same as the ``summary`` field
                            described above, but searches the Status Whiteboard
                            field.
================  ========  =====================================================

**Response**

The same as :ref:`rest_single_bug`.

**Errors**

If you specify an invalid value for a particular field, you just won't
get any results for that value.

* 1000 (Parameters Required)
  You may not search without any search terms.

.. _rest_create_bug:

Create Bug
----------

This allows you to create a new bug in Bugzilla. If you specify any
invalid fields, an error will be thrown stating which field is invalid.
If you specify any fields you are not allowed to set, they will just be
set to their defaults or ignored.

You cannot currently set all the items here that you can set on enter_bug.cgi.

The WebService interface may allow you to set things other than those listed
here, but realize that anything undocumented here may likely change in the
future.

**Request**

To create a new bug in Bugzilla.

.. code-block:: text

   POST /rest/bug

.. code-block:: js

   {
     "product" : "TestProduct",
     "component" : "TestComponent",
     "version" : "unspecified",
     "summary" : "'This is a test bug - please disregard",
     "alias" : "SomeAlias",
     "op_sys" : "All",
     "priority" : "P1",
     "platform" : "All",
     "type" : "defect"
   }

Some params must be set, or an error will be thrown. These params are
marked in **bold**.

Some parameters can have defaults set in Bugzilla, by the administrator.
If these parameters have defaults set, you can omit them. These parameters
are marked (defaulted).

Clients that want to be able to interact uniformly with multiple
Bugzillas should always set both the params marked required and those
marked (defaulted), because some Bugzillas may not have defaults set
for (defaulted) parameters, and then this method will throw an error
if you don't specify them.

==================  =======  ====================================================
name                type     description
==================  =======  ====================================================
**product**         string   The name of the product the bug is being filed
                             against.
**component**       string   The name of a component in the product above.
**summary**         string   A brief description of the bug being filed.
**version**         string   A version of the product above; the version the
                             bug was found in.
description         string   (defaulted) The description (initial comment) of the
                             bug. Some Bugzilla installations require this to not
                             be blank.
filed_via           string   (defaulted) How the bug is being filed. It will be
                             ``api`` by default when filing through the API.
op_sys              string   (defaulted) The operating system the bug was
                             discovered on.
platform            string   (defaulted) What type of hardware the bug was
                             experienced on.
priority            string   (defaulted) What order the bug will be fixed in by
                             the developer, compared to the developer's other
                             bugs.
severity            string   (defaulted) How severe the bug is.
**type**            string   The basic category of the bug. Some Bugzilla
                             installations require this to be specified.
alias               string   The alias for the bug that can be used instead of a
                             bug number when accessing this bug. Must be unique
                             in all of this Bugzilla.
assigned_to         string   A user to assign this bug to, if you don't want it
                             to be assigned to the component owner.
cc                  array    An array of usernames to CC on this bug.
comment_is_private  boolean  If set to true, the description is private,
                             otherwise it is assumed to be public.
groups              array    An array of group names to put this bug into. You
                             can see valid group names on the Permissions tab of
                             the Preferences screen, or, if you are an
                             administrator, in the Groups control panel. If you
                             don't specify this argument, then the bug will be
                             added into all the groups that are set as being
                             "Default" for this product. (If you want to avoid
                             that, you should specify ``groups`` as an empty
                             array.)
qa_contact          string   If this installation has QA Contacts enabled, you
                             can set the QA Contact here if you don't want to
                             use the component's default QA Contact.
status              string   The status that this bug should start out as. Note
                             that only certain statuses can be set on bug
                             creation.
resolution          string   If you are filing a closed bug, then you will have
                             to specify a resolution. You cannot currently
                             specify a resolution of ``DUPLICATE``   for new
                             bugs, though. That must be done with
                             :ref:`rest_update_bug`.
target_milestone    string   A valid target milestone for this product.
flags               array    Flags objects to add to the bug. The object format
                             is described in the Flag object below.
keywords            array    One or more valid keywords to add to this bug.
dependson           array    One or more valid bug ids that this bug depends on.
blocked             array    One or more valid bug ids that this bug blocks.
regressed_by        array    One or more valid bug ids that introduced this bug.
==================  =======  ====================================================

Flag object:

To create a flag, at least the ``status`` and the ``type_id`` or ``name`` must
be provided. An optional requestee can be passed if the flag type is requestable
to a specific user.

=========  ======  ==============================================================
name       type    description
=========  ======  ==============================================================
name       string  The name of the flag type.
type_id    int     The internal flag type ID.
status     string  The flags new status (i.e. "?", "+", "-" or "X" to clear flag).
requestee  string  The login of the requestee if the flag type is requestable
                   to a specific user.
=========  ======  ==============================================================

In addition to the above parameters, if your installation has any custom
fields, you can set them just by passing in the name of the field and
its value as a string.

**Response**

.. code-block:: js

   {
     "id" : 12345
   }

====  ====  ======================================
name  type  description
====  ====  ======================================
id    int   This is the ID of the newly-filed bug.
====  ====  ======================================

**Errors**

* 51 (Invalid Object)
  You specified a field value that is invalid. The error message will have
  more details.
* 103 (Invalid Alias)
  The alias you specified is invalid for some reason. See the error message
  for more details.
* 104 (Invalid Field)
  One of the drop-down fields has an invalid value, or a value entered in a
  text field is too long. The error message will have more detail.
* 105 (Invalid Component)
  You didn't specify a component.
* 106 (Invalid Product)
  Either you didn't specify a product, this product doesn't exist, or
  you don't have permission to enter bugs in this product.
* 107 (Invalid Summary)
  You didn't specify a summary for the bug.
* 116 (Dependency Loop)
  You specified values in the "blocks" and "depends_on" fields,
  or the "regressions" and "regressed_by" fields, that would cause a
  circular dependency between bugs.
* 120 (Group Restriction Denied)
  You tried to restrict the bug to a group which does not exist, or which
  you cannot use with this product.
* 129 (Flag Status Invalid)
  The flag status is invalid.
* 130 (Flag Modification Denied)
  You tried to request, grant, or deny a flag but only a user with the required
  permissions may make the change.
* 131 (Flag not Requestable from Specific Person)
  You can't ask a specific person for the flag.
* 133 (Flag Type not Unique)
  The flag type specified matches several flag types. You must specify
  the type id value to update or add a flag.
* 134 (Inactive Flag Type)
  The flag type is inactive and cannot be used to create new flags.
* 135 (Bug Type Required)
  You didn't specify a type for the bug.
* 504 (Invalid User)
  Either the QA Contact, Assignee, or CC lists have some invalid user
  in them. The error message will have more details.

.. _rest_update_bug:

Update Bug
----------

Allows you to update the fields of a bug. Automatically sends emails
out about the changes.

**Request**

To update the fields of a current bug.

.. code-block:: text

   PUT /rest/bug/(id_or_alias)

.. code-block:: js

   {
     "ids" : [35],
     "status" : "IN_PROGRESS",
     "keywords" : {
       "add" : ["funny", "stupid"]
     }
   }

The params to include in the PUT body as well as the returned data format,
are the same as below. You must specify an ID or alias of a bug to update
in the URL path. You can also specify the ``ids`` param and they will be
combined so you can edit more than one bug at a time.

===============  =====  =========================================================
name             type   description
===============  =====  =========================================================
**id_or_alias**  mixed  An integer bug ID or alias.
**ids**          array  The IDs or aliases of the bugs that you want to modify.
===============  =====  =========================================================

All following fields specify the values you want to set on the bugs you are
updating.

=====================  =======  =================================================
name                   type     description
=====================  =======  =================================================
alias                  string   The alias for the bug that can be used instead of
                                a bug number when accessing this bug. Must be
                                unique in all of this Bugzilla.
assigned_to            string   The full login name of the user this bug is
                                assigned to.
blocks                 object   (Same as ``regressed_by`` below)
depends_on             object   (Same as ``regressed_by`` below)
regressions            object   (Same as ``regressed_by`` below)
regressed_by           object   These specify the bugs that this bug blocks,
                                depends on, regresses, or is regressed by,
                                respectively. To set these, you should pass an
                                object as the value. The object may contain the
                                following items:

                                * ``add`` (array) Bug IDs to add to this field.
                                * ``remove`` (array) Bug IDs to remove from this
                                  field. If the bug IDs are not already in the
                                  field, they will be ignored.
                                * ``set`` (array of) An exact set of bug IDs to
                                  set this field to, overriding the current
                                  value. If you specify ``set``, then ``add``
                                  and ``remove`` will be ignored.
cc                     object   The users on the cc list. To modify this field,
                                pass an object, which may have the following
                                items:

                                * ``add`` (array) User names to add to the CC
                                  list. They must be full user names, and an
                                  error will be thrown if you pass in an invalid
                                  user name.
                                * ``remove`` (array) User names to remove from
                                  the CC list. They must be full user names, and
                                  an error will be thrown if you pass in an
                                  invalid user name.
is_cc_accessible       boolean  Whether or not users in the CC list are allowed
                                to access the bug, even if they aren't in a group
                                that can normally access the bug.
comment                object   A comment on the change. The object may contain
                                the following items:

                                * ``body`` (string) The actual text of the
                                  comment. For compatibility with the parameters
                                  to :ref:`rest_add_comment`, you can also call
                                  this field ``comment``, if you want.
                                * ``is_private`` (boolean) Whether the comment is
                                  private or not. If you try to make a comment
                                  private and you don't have the permission to,
                                  an error will be thrown.
comment_is_private     object   This is how you update the privacy of comments
                                that are already on a bug. This is a object,
                                where the keys are the ``int`` ID of comments
                                (not their count on a bug, like #1, #2, #3, but
                                their globally-unique ID, as returned by
                                :ref:`rest_comments` and the value is a
                                ``boolean`` which specifies whether that comment
                                should become private (``true``) or public
                                (``false``).

                                The comment IDs must be valid for the bug being
                                updated. Thus, it is not practical to use this
                                while updating multiple bugs at once, as a single
                                comment ID will never be valid on multiple bugs.
component              string   The Component the bug is in.
deadline               date     The Deadline field is a date specifying when the
                                bug must be completed by, in the format
                                ``YYYY-MM-DD``.
dupe_of                int      The bug that this bug is a duplicate of. If you
                                want to mark a bug as a duplicate, the safest
                                thing to do is to set this value and *not* set
                                the ``status`` or ``resolution`` fields. They will
                                automatically be set by Bugzilla to the
                                appropriate values for duplicate bugs.
estimated_time         double   The total estimate of time required to fix the
                                bug, in hours. This is the *total* estimate, not
                                the amount of time remaining to fix it.
flags                  array    An array of Flag change objects. The items needed
                                are described below.
groups                 object   The groups a bug is in. To modify this field,
                                pass an object, which may have the following
                                items:

                                * ``add`` (array) The names of groups to add.
                                  Passing in an invalid group name or a group
                                  that you cannot add to this bug will cause an
                                  error to be thrown.
                                * ``remove`` (array) The names of groups to
                                  remove. Passing in an invalid group name or a
                                  group that you cannot remove from this bug
                                  will cause an error to be thrown.
keywords               object   Keywords on the bug. To modify this field, pass
                                an object, which may have the following items:

                                * ``add`` (array) The names of keywords to add
                                  to the field on the bug. Passing something that
                                  isn't a valid keyword name will cause an error
                                  to be thrown.
                                * ``remove`` (array) The names of keywords to
                                  remove from the field on the bug. Passing
                                  something that isn't a valid keyword name will
                                  cause an error to be thrown.
                                * ``set`` (array) An exact set of keywords to set
                                  the field to, on the bug. Passing something
                                  that isn't a valid keyword name will cause an
                                  error to be thrown. Specifying ``set``
                                  overrides ``add`` and ``remove``.
op_sys                 string   The Operating System ("OS") field on the bug.
platform               string   The Platform or "Hardware" field on the bug.
priority               string   The Priority field on the bug.
product                string   The name of the product that the bug is in. If
                                you change this, you will probably also want to
                                change ``target_milestone``, ``version``, and
                                ``component``, since those have different legal
                                values in every product.

                                If you cannot change the ``target_milestone``
                                field, it will be reset to the default for the
                                product, when you move a bug to a new product.

                                You may also wish to add or remove groups, as
                                which groups are
                                valid on a bug depends on the product. Groups
                                that are not valid in the new product will be
                                automatically removed, and groups which are
                                mandatory in the new product will be
                                automatically added, but no other automatic group
                                changes will be done.

                                .. note::
                                   Users can only move a bug into a product if
                                   they would normally have permission to file
                                   new bugs in that product.
qa_contact             string   The full login name of the bug's QA Contact.
is_creator_accessible  boolean  Whether or not the bug's reporter is allowed
                                to access the bug, even if they aren't in a group
                                that can normally access the bug.
remaining_time         double   How much work time is remaining to fix the bug,
                                in hours. If you set ``work_time`` but don't
                                explicitly set ``remaining_time``, then the
                                ``work_time`` will be deducted from the bug's
                                ``remaining_time``.
reset_assigned_to      boolean  If true, the ``assigned_to`` field will be
                                reset to the default for the component that the
                                bug is in. (If you have set the component at the
                                same time as using this, then the component used
                                will be the new component, not the old one.)
reset_qa_contact       boolean  If true, the ``qa_contact`` field will be reset
                                to the default for the component that the bug is
                                in. (If you have set the component at the same
                                time as using this, then the component used will
                                be the new component, not the old one.)
resolution             string   The current resolution. May only be set if you
                                are closing a bug or if you are modifying an
                                already-closed bug. Attempting to set the
                                resolution to *any* value (even an empty or null
                                string) on an open bug will cause an error to be
                                thrown.

                                .. note::
                                   If you change the ``status`` field to an open
                                   status, the resolution field will automatically
                                   be cleared, so you don't have to clear it
                                   manually.
see_also               object   The See Also field on a bug, specifying URLs to
                                bugs in other bug trackers. To modify this field,
                                pass an object, which may have the following
                                items:

                                * ``add`` (array) URLs to add to the field. Each
                                  URL must be a valid URL to a bug-tracker, or
                                  an error will be thrown.
                                * ``remove`` (array) URLs to remove from the
                                  field. Invalid URLs will be ignored.
severity               string   The Severity field of a bug.
status                 string   The status you want to change the bug to. Note
                                that if a bug is changing from open to closed,
                                you should also specify a ``resolution``.
summary                string   The Summary field of the bug.
target_milestone       string   The bug's Target Milestone.
type                   string   The Type field on the bug.
url                    string   The "URL" field of a bug.
version                string   The bug's Version field.
whiteboard             string   The Status Whiteboard field of a bug.
work_time              double   The number of hours worked on this bug as part
                                of this change.
                                If you set ``work_time`` but don't explicitly
                                set ``remaining_time``, then the ``work_time``
                                will be deducted from the bug's ``remaining_time``.
=====================  =======  =================================================

You can also set the value of any custom field by passing its name as
a parameter, and the value to set the field to. For multiple-selection
fields, the value should be an array of strings.

Flag change object:

The following values can be specified. At least the ``status`` and one of
``type_id``, ``id``, or ``name`` must be specified. If a ``type_id`` or
``name`` matches a single currently set flag, the flag will be updated unless
``new`` is specified.

==========  =======  ============================================================
name        type     description
==========  =======  ============================================================
name        string   The name of the flag that will be created or updated.
type_id     int      The internal flag type ID that will be created or updated.
                     You will need to specify the ``type_id`` if more than one
                     flag type of the same name exists.
**status**  string   The flags new status (i.e. "?", "+", "-" or "X" to clear a
                     flag).
requestee   string   The login of the requestee if the flag type is requestable
                     to a specific user.
id          int      Use ID to specify the flag to be updated. You will need to
                     specify the ``id`` if more than one flag is set of the same
                     name.
new         boolean  Set to true if you specifically want a new flag to be
                     created.
==========  =======  ============================================================

**Response**

.. code-block:: js

   {
     "bugs" : [
       {
         "alias" : null,
         "changes" : {
           "keywords" : {
             "added" : "funny, stupid",
             "removed" : ""
           },
             "status" : {
               "added" : "IN_PROGRESS",
               "removed" : "CONFIRMED"
           }
         },
         "id" : 35,
         "last_change_time" : "2014-09-29T14:25:35Z"
       }
     ]
   }

``bugs`` (array) This points to an array of objects with the following items:

================  ========  =====================================================
name              type      description
================  ========  =====================================================
id                int       The ID of the bug that was updated.
alias             string    The alias of the bug that was updated, if this bug
                            has any alias.
last_change_time  datetime  The exact time that this update was done at, for
                            this bug. If no update was done (that is, no fields
                            had their values changed and no comment was added)
                            then this will instead be the last time the bug was
                            updated.
changes           object    The changes that were actually done on this bug. The
                            keys are the names of the fields that were changed,
                            and the values are an object with two keys:

                            * ``added`` (string) The values that were added to
                              this field, possibly a comma-and-space-separated
                              list if multiple values were added.
                            * ``removed`` (string) The values that were removed
                              from this field, possibly a
                              comma-and-space-separated list if multiple values
                              were removed.
================  ========  =====================================================

Currently, some fields are not tracked in changes: ``comment``,
``comment_is_private``, and ``work_time``. This means that they will not
show up in the return value even if they were successfully updated.
This may change in a future version of Bugzilla.

**Errors**

This method can throw all the same errors as :ref:`rest_single_bug`, plus:

* 129 (Flag Status Invalid)
  The flag status is invalid.
* 130 (Flag Modification Denied)
  You tried to request, grant, or deny a flag but only a user with the required
  permissions may make the change.
* 131 (Flag not Requestable from Specific Person)
  You can't ask a specific person for the flag.
* 132 (Flag not Unique)
  The flag specified has been set multiple times. You must specify the id
  value to update the flag.
* 133 (Flag Type not Unique)
  The flag type specified matches several flag types. You must specify
  the type id value to update or add a flag.
* 134 (Inactive Flag Type)
  The flag type is inactive and cannot be used to create new flags.
* 140 (Markdown Disabled)
  You tried to set the "is_markdown" flag of the "comment" to true but Markdown feature is
  not enabled.
* 601 (Invalid MIME Type)
  You specified a "content_type" argument that was blank, not a valid
  MIME type, or not a MIME type that Bugzilla accepts for attachments.
* 603 (File Name Not Specified)
  You did not specify a valid for the "file_name" argument.
* 604 (Summary Required)
  You did not specify a value for the "summary" argument.

.. _rest_possible_duplicates:

Possible Duplicates
-------------------

Gets a list of possible duplicate bugs.

**Request**

To search by similar bug.

.. code-block:: text

   GET /rest/bug/possible_duplicates?id=1234567

To search by a similar bug summary directly.

.. code-block:: text

   GET /rest/bug/possible_duplicates?summary=Similar+Bug+Summary

=======  ======  ================================================================
name     type      description
=======  ======  ================================================================
id       int     The id of a bug to find duplicates of.
summary  string  A summary to search for duplicates of, only used if no bug id is
                 given.
product  string  A product group to limit the search in.
limit    int     Limit the number of results returned. If the value is unset,
                 zero or greater than the maximum value set by the administrator,
                 which is 10,000 by default, then the maximum value will be used
                 instead. This is a preventive measure against DoS-like attacks
                 on Bugzilla.
=======  ======  ================================================================

**Response**

.. code-block:: js

   {
     "bugs": [
       {
         "alias": null,
         "history": [
           {
             "when": "2014-09-23T19:12:17Z",
             "who": "user@bugzilla.org",
             "changes": [
               {
                 "added": "P1",
                 "field_name": "priority",
                 "removed": "P2"
               },
               {
                 "removed": "blocker",
                 "field_name": "severity",
                 "added": "critical"
               }
             ]
           },
           {
             "when": "2014-09-28T21:03:47Z",
             "who": "user@bugzilla.org",
             "changes": [
               {
                 "added": "blocker?",
                 "removed": "",
                 "field_name": "flagtypes.name"
               }
             ]
           }
         ],
         "id": 35
       }
     ]
   }

``bugs`` (array) Bug objects each containing the following items. If a bug id was
used to query this endpoint, that bug will not be in the list returned.

=======  ======  ================================================================
name     type    description
=======  ======  ================================================================
id       int     The numeric ID of the bug.
alias    string  The unique alias of this bug. A ``null`` value will be returned
                 if this bug has no alias.
history  array   An array of History objects.
=======  ======  ================================================================

History object:

=======  ========  ==============================================================
name     type      description
=======  ========  ==============================================================
when     datetime  The date the bug activity/change happened.
who      string    The login name of the user who performed the bug change.
changes  array     An array of Change objects which contain all the changes that
                   happened to the bug at this time (as specified by ``when``).
=======  ========  ==============================================================

Change object:

=============  ======  ==========================================================
name           type    description
=============  ======  ==========================================================
field_name     string  The name of the bug field that has changed.
removed        string  The previous value of the bug field which has been
                       deleted by the change.
added          string  The new value of the bug field which has been added
                       by the change.
attachment_id  int     The ID of the attachment that was changed.
                       This only appears if the change was to an attachment,
                       otherwise ``attachment_id`` will not be present in this
                       object.
=============  ======  ==========================================================
