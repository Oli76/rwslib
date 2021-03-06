.. _rws_requests:
.. index:: rws_requests

rws_requests
************

The rws_requests module contains the core RWSRequest class and a set of Request classes that are standard in all
versions of Rave Web Services for Rave.

Also part of this module:

* :ref:`architect`
* :ref:`glv`
* :ref:`working_clinical_data`
* :ref:`post_clinical_data`

rws_requests also provides additional requests in sub-modules for additional features:

* :ref:`biostats_gateway`
* :ref:`odm_adapter`


.. _version_request:
.. index:: VersionRequest

VersionRequest()
----------------

Returns the text result of calling::

    https://{ host }/RaveWebServices/version

Example::

    >>> from rwslib import RWSConnection
    >>> from rwslib.rws_requests import VersionRequest
    >>> r = RWSConnection('innovate', 'username', 'password')  #Authorization optional
    >>> r.send_request(VersionRequest())
    1.8.0


.. _buildversion_request:
.. index:: BuildVersionRequest

BuildVersionRequest()
---------------------

Returns the text result of calling::

    https://{ host }/RaveWebServices/version/build

Returns a 200 response code and the internal build number.

Example::

    >>> from rwslib import RWSConnection
    >>> from rwslib.rws_requests import BuildVersionRequest
    >>> r = RWSConnection('innovate', 'username', 'password')  #Authorization optional
    >>> r.send_request(BuildVersionRequest())
    5.6.5.12



.. _diagnostics_request:
.. index:: DiagnosticsRequest

DiagnosticsRequest()
--------------------

Returns the text result of calling::

    https://{ host }/RaveWebServices/version/build

Returns a 200 response code and the text *OK* if RWS self-checks pass.

Example::

    >>> from rwslib import RWSConnection
    >>> from rwslib.rws_requests import DiagnosticsRequest
    >>> r = RWSConnection('innovate', 'username', 'password')  #Authorization optional
    >>> r.send_request(DiagnosticsRequest())
    OK



.. _cacheflush_request:
.. index:: CacheFlushRequest

CacheFlushRequest()
-------------------

Authorization is required for this method call.

Returns the text result of calling::

    https://{ host }/RaveWebServices/webservice.aspx?CacheFlush


.. warning::

    Calling CacheFlush unnecessarily causes RWS to re-load objects, causing additional resource utilization that
    could have a detrimental affect on Rave performance.


Flushes the RWS cache. Generally Rave and RWS manage their own caching. You should not need to use this method
in normal operation. Returns a  :class:`rwsobjects.RWSResponse` object with a istransactionsuccessful attribute:

Example::

    >>> from rwslib import RWSConnection
    >>> from rwslib.rws_requests import CacheFlushRequest
    >>> r = RWSConnection('innovate', 'username', 'password')  #Authorization REQUIRED
    >>> response = r.send_request(CacheFlushRequest())
    >>> response.istransactionsucessful
    True

