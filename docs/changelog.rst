.. _change_logs:

Change Logs
===========

0.10.0(Development)
------------------

* # 39_ - **Improvement** -  Django has dropped support for pypy-3. So, It should be dropped from django itself too.
* **Remove** -  ``pypy`` support has been dropped
* **Remove** -  ``Python3.3`` support has been dropped
* **Improvement** - ``Django2.0`` support with ``Python3.5`` and ``Python3.6`` is provided

.. _39: https://github.com/javrasya/django-river/issues/39

0.9.0(Stable)
-------------

* # 30_ - **Bug** -  Missing migration file which is ``0007`` because of ``Python2.7`` can not detect it.
* # 31_ - **Improvement** - unicode issue for Python3.
* # 33_ - **Bug** - Automatically injecting workflow manager was causing the models not have default ``objects`` one. So, automatic injection support has been dropped. If anyone want to use it, it can be used explicitly.
* # 35_ - **Bug** - This is huge change in django-river. Multiple state field each model support is dropped completely and so many APIs have been changed. Check documentations and apply changes.

.. _30: https://github.com/javrasya/django-river/pull/30  
.. _31: https://github.com/javrasya/django-river/pull/30
.. _33: https://github.com/javrasya/django-river/pull/33
.. _35: https://github.com/javrasya/django-river/pull/35

0.8.2
-----

* **Bug** - Features providing multiple state field in a model was causing a problem. When there are multiple state field, injected attributes in model class are owerriten. This feature is also unpractical. So, it is dropped to fix the bug.
* **Improvement** - Initial video tutorial which is Simple jira example is added into the documentations. Also repository link of fakejira project which is created in the video tutorial is added into the docs.
* **Improvement** - No proceeding meta parent input is required by user. It is set automatically by django-river now. The field is removed from ProceedingMeta admin interface too.


0.8.1
-----

* **Bug** - ProceedingMeta form was causing a problem on migrations. Accessing content type before migrations was the problem. This is fixed by defining choices in init function instead of in field

0.8.0
-----

* **Deprecation** - ProceedingTrack is removed. ProceedingTracks were being used to keep any transaction track to handle even circular one. This was a workaround. So, it can be handled with Proceeding now by cloning them if there is circle. ProceedingTracks was just causing confusion. To fix this, ProceedingTrack model and its functions are removed from django-river.
* **Improvement** - Circular scenario test is added.
* **Improvement** - Admins of the workflow components such as State, Transition and ProceedingMeta are registered automatically now. Issue #14 is fixed.

0.7.0
-----

* **Improvement** - Python version 3.5 support is added. (not for Django1.7)
* **Improvement** - Django version 1.9 support is added. (not for Python3.3 and PyPy3) 

0.6.2
-----

* **Bug** - Migration ``0002`` and ``0003`` were not working properly for postgresql (maybe oracle). For these databases, data can not be fixed. Because, django migrates each in a transactional block and schema migration and data migration can not be done in a transactional block. To fix this, data fixing and schema fixing are seperated.
* **Improvement** - Timeline section is added into documentation.
* **Improvement** - State slug field is set as slug version of its label if it is not given on saving.


0.6.1
-----

* **Bug** - After ``content_type`` and ``field`` are moved into ``ProceedingMeta`` model from ``Transition`` model in version ``0.6.0``, finding initial and final states was failing. This is fixed.
* **Bug** - ``0002`` migrations was trying to set default slug field of State model. There was a unique problem. It is fixed. ``0002`` can be migrated now.
* **Improvement** - The way of finding initial and final states is changed. ProceedingMeta now has parent-child tree structure to present state machine. This tree structure is used to define the way. This requires to migrate ``0003``. This migration will build the tree of your existed ProceedingMeta data.

0.6.0
-----

* **Improvement** - ``content_type`` and ``field`` are moved into ``ProceedingMeta`` model from ``Transition`` model. This requires to migrate ``0002``. This migrations will move value of the fields from ``Transition`` to ``ProceedingMeta``.
* **Improvement** - Slug field is added in ``State``. It is unique field to describe state. This requires to migrate ``0002``. This migration will set the field as slug version of ``label`` field value. (Re Opened -> re-opened)
* **Improvement** - ``State`` model now has ``natural_key`` as ``slug`` field.
* **Improvement** - ``Transition`` model now has ``natural_key`` as (``source_state_slug`` , ``destination_state_slug``) fields
* **Improvement** - ``ProceedingMeta`` model now has ``natural_key`` as (``content_type``, ``field``, ``transition``, ``order``) fields
* **Improvement** - Changelog is added into documentation.
  

0.5.3
-----

* **Bug** - Authorization was not working properly when the user has irrelevant permissions and groups. This is fixed.
* **Improvement** - User permissions are now retreived from registered authentication backends instead of ``user.user_permissions``
  

0.5.2
-----

* **Improvement** - Removed unnecessary models.
* **Improvement** - Migrations are added
* **Bug** - ``content_type__0002`` migrations cause failing for ``django1.7``. Dependency is removed
* **Bug** - ``DatabaseHandlerBacked`` was trying to access database on django setup. This cause ``no table in db`` error for some django commands. This was happening; because there is no db created before some commands are executed; like ``makemigrations``, ``migrate``.


0.5.1
-----

* **Improvement** - Example scenario diagrams are added into documentation.
* **Bug** - Migrations was failing because of injected ``ProceedingTrack`` relation. Relation is not injected anymore. But property ``proceeing_track`` remains. It still returns current one.
