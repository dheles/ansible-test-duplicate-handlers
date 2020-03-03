# Ansible Test Project: Duplicate Handlers

This project is designed to test how Ansible deals with duplicate handlers in
included roles. By manipulating the vars in the test playbooks, the handlers can
be triggered by name or as listeners.

## Results:
### Primary tests (`main.yml`):
When called by name only:

    vars:
      by_name: true
      as_listener: false

The handler in the first role (test1) runs one time.

When called as listeners (regardless of the value of the `by_name` var):

    vars:
      by_name: true
      as_listener: true
OR

    vars:
      by_name: false
      as_listener: true

The handlers in the both of the roles (test1 & test2) each run one time.  
(NOTE: the test3 role is used to trigger handlers, but does not itself contain
a third copy of the handler)

### Alt syntax
One additional test is in `test_alt_syntax.yml`, wherein the older syntax is
used to include (import?) the roles. In this test the playbook's vars are not
passed to the roles, so by default none of the handlers fire. If the vars in the
roles are set directly, the results match those of the main playbook.

### Importing roles
Another additional test is in `test_import.yml`, wherein the roles are imported,
rather than included. None of the handlers fire in that test, regardless of the
state of the playbook's vars.
