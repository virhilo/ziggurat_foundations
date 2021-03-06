Overview
========

ziggurat_foundations supplies a set of *sqlalchemy mixins* that can be used to extend
models in your application. The aim of this project is to supply set of generic 
models that cover the most common needs in application development when it comes 
to authorization - using flat and tree like data structures.

So far following basics are supplied:

- User - base for user accounts
- Group - container for many users 
- Resource - Arbitrary database entity that can represent various object hierarchies - blogs, forums, cms documents, pages etc.

Currently following information and data manipulation is supported:

- assigning arbitrary permissions directly to users (ie. access admin panel) 
- assigning users to groups
- assigning arbitrary permissions to groups 
- assigning arbitrary resource permissions to users (ie. only user X can access  private forum)
- assigning arbitrary resource permissions to groups 


All permutations between those patterns allow for complex and flexible permission 
systems that are easly understandable for non-technical users.
 
The sqlalchemy mixins make all the interactions easy to use in your application 
and save development time.

.. warning::
   Be cautious about creating your database models directly with sqlalchemy - **be sure
   to at least stamp the database with latest alembic timestamp. It is recommended 
   to use alembic for table creation**.

Quick usage examples
--------------------

assigning custom "read" permission for user "foo" for a given resource::

    permission = UserResourcePermission()
    permission.perm_name = "read"
    permission.user_name = "foo"
    resource.user_permissions.append(permission)   

fetching all resources with permissions "edit", "vote"::

    user.resources_with_perms(["edit","vote"])

fetching all non-resource based permissions for user::

    user.permissions

given a resource fetching all permissions for user, both direct and  
inherited from groups user belongs to::

    resource.perms_for_user(user_instance)

and a lot more...
