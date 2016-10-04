INTRODUCTION
------------

This module was created as a technical test for Adyax team.
As far as no information about Drupal core version was provided, I decided to
create Drupal7 module. Moreover, Drupal8 has built-in Rest support so there
is no reason to create it in Drupal8.

Test description:
Without using any contributed modules, create custom module that implements
simple REST Service. Web service URL should be: /adyax_ws

It should support next methods:
* GET - returns JSON with data from node. NID provided in URL request, for
example:
/adyax_ws?nid=123 ;
* POST - retrieve JSON data with title, type and body and create new node
based on provided data;
* PUT - retrieve JSON data and update node by NID provided in URL or JSON (up
to you);
* DELETE - deletes node by provided NID

REQUIREMENTS
------------

No special requirements.

INSTALLATION
------------

Install as you would normally install a contributed Drupal module. See:
https://drupal.org/documentation/install/modules-themes/modules-7
for further information.

CONFIGURATION
-------------

The module has no menu or modifiable settings. There is no configuration. As
far as nothing about user authorization was mentioned in the task description,
when enabled, the module will add Adyax WS web service URL accessible by any
user of any role.

REQUEST EXAMPLES
----------------

* GET request example (returns code 200 and Node data in Json if exists, 404
  otherwise):

    GET /adyax_ws?nid=1 HTTP/1.1
    Host: <your hostname>
    Accept: application/json
    Cache-Control: no-cache

* POST request example (returns code 201 on success, 403 otherwise):

    POST /adyax_ws HTTP/1.1
    Host: <your hostname>
    Accept: application/json
    Content-Type: application/json
    Cache-Control: no-cache

    {
    "type":"article",
    "title":"Article test #1",
    "body":"Article test body #1"
    }

* PUT request example (returns 200 on success, 404 if node not found,
  403 otherwise):

    PUT /adyax_ws?nid=1 HTTP/1.1
    Host: <your hostname>
    Accept: application/json
    Content-Type: application/json
    Cache-Control: no-cache

    {
    "title":"Article test #2",
    "body":"Article body2"
    }

* DELETE request example (returns 200 on success, 404 if not not found):

    DELETE /adyax_ws/adyax_ws?nid=3 HTTP/1.1
    Host: localhost
    Accept: application/json
    Cache-Control: no-cache

All other request types are not allowed and will return 405 error.
If application doesn't accept application/json 406 error will be returned.

MAINTAINERS
-----------

Current maintainers:
 * Dmitry Evdokimov (devdokimov) - https://www.drupal.org/u/devdokimov
