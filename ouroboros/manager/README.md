# WSUDOR_Manager (aka 'Ouroboros')

Though technically part of the greater "Ouroboros" ecosystem, because "WSUDOR Manager" is the primary GUI for the stack as a whole, it's often referred to as "Ouroboros" itself.  WSUDOR_Manager is where things are "done" in a practical sense.

WSUDOR Manager is a flask app that provides a GUI for performing just about any repository work that is not performed on the command line.  WSUDOR Manager uses LDAP for login (via the digital collections login form), is availble to multiple people (limited by hand-created user accounts by admins), performs long, complex background jobs, and much more.

WSUDOR_Manager is critical to managing the digital collections, and as such, is fairly complex.  The following documentation is broken up by major areas of Ouroboros.

## Users
Users are defined by the `User` model in the [models.py](https://github.com/WSULib/ouroboros/blob/master/WSUDOR_Manager/models.py).  Users in Ouroboros can be considered a combination of university LDAP accounts + an Ouroboros user account on top.  Said another way, while users will login with their Access ID and password via LDAP, there must be a corresponding user account in Ouroboros for the login process to complete. 

A handful of default Ouroboros admin accounts are created when the server is built, and from there, admins are responsibile for making further user accounts. 

Users are important in Ouroboros because routes, views, pages, and celery tasks are limited based on a User's associated **roles**.  These roles currently include `admin`, `metadata`, and `view`.  Users may belong to multiple roles.  

Roles are enforced using the decorator `@roles.auth(LIST_OF_AUTHORIZED_ROLES)` from `roles.py`.  This decorator is expecting a single parameter, a list of roles that approved to continue with that route, page, or celery task.

For example you might have user `foobar` with roles `['metadata','view']`.

Because `metadata` is in the following decorator stack,
```
@batch_edit.route('/batch_edit/export')
@utilities.objects_needed
@login_required
----> @roles.auth(['metadata'])
def batch_edit():
    ...
```
`foobar` would be authorized to view.

Any users belong to role `admin` are authorized for all routes, pages, and tasks.

### Viewing and Creating Users

View current users: `/ouroboros/users/view`<br>
Create new user: `/ouroboros/users/create`


