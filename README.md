ansible-haproxy-endpoints
=========

An ansible role that installs listening handlers to manage haproxy endpoints.

[![Build Status](https://travis-ci.org/Logan2211/ansible-haproxy-endpoints.svg?branch=master)](https://travis-ci.org/Logan2211/ansible-haproxy-endpoints)

Requirements
------------

Populated HAProxy ansible group

Example Playbook
----------------

```yaml
- hosts: endpoints
  roles:
     - role: ansible-haproxy-endpoints
       haproxy_state: disabled
     - your_role
     - role: ansible-haproxy-endpoints
       haproxy_state: enabled
```

In `your_role`, notify a handler named `Manage LB` when notifying service
restart handlers or other handlers that require LB orchestration. The LB
endpoint will be disabled before your handler runs, and then re-enabled after
`your_role` handlers are finished.

You may wish to add a "stub" handler listening to `Manage LB` in your role
in case the playbook does not implement this role.

To do that, add a handler like:
```yaml
- meta: noop
  listen: Manage LB
  when: false
```

The handler will prevent an error from being thrown if no LB orchestration
exists, but will do nothing otherwise.

License
-------

Apache2

Author Information
------------------

Logan V.
