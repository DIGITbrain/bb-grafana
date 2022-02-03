=======
Grafana
=======

About
=====
**Grafana** [1]_ is an open-source platform for monitoring and observability that allows to query, visualize, alert on and understand metrics,
create, explore, and share dashboards.

Version
-------
Grafana version **8.3.4** deployed based on the Docker Hub image: [2]_ released by verified publisher Grafana Labs. 

License
-------
**AGPL-3.0-only** and **Apache-2.0** [3]_

Pre-requisites
==============
* *docker* installed
* access to DIGITbrain private docker repo (username, password) to pull the image:
  
  - ``docker login dbs-container-repo.emgora.eu``
  - ``docker pull dbs-container-repo.emgora.eu/grafana:8.3.4``

Usage
=====
.. code-block:: bash

  docker run -d --rm \
      --name grafana \
      -e GF_SECURITY_ADMIN_USER=myusername \
      -e GF_SECURITY_ADMIN_PASSWORD=mypassword \
      -p 3000:3000 \
      grafana:8.3.4 

where GF_SECURITY_ADMIN_USER and GF_SECURITY_ADMIN_PASSWORD values are set to access the web UI of Grafana accessible on host port 3000.

The open a browser with URL: https://<<container-host>>:3000/ (in Chrome type in: 'thisisunsafe' to proceed).

Security
========
The web UI requires username-password authentication and network trafic is encrypted over HTTPS with a server certificate signed by DIGITbrain CA. 

You can override the default settings (certificates, ports).

Configuration
=============

Environment variables
---------------------
.. list-table:: 
   :header-rows: 1

   * - Name
     - Example
     - Comment
   * - *GF_SECURITY_ADMIN_USER*
     - ``-e GF_SECURITY_ADMIN_USER=myusername``
     - The usename to access the web UI
   * - *GF_SECURITY_ADMIN_PASSWORD*
     - ``-e GF_SECURITY_ADMIN_PASSWORD=mypassword``
     - The password to access the web UI

Ports
-----
.. list-table:: 
  :header-rows: 1

  * - Container port
    - Host port bind example
    - Comment
  * - *HTTPS (web UI)*
    - ``-p 13000:3000``
    - The default web UI port 3000 is opened on host port 13000

Volumes
-------
.. list-table:: 
  :header-rows: 1

  * - Name
    - Volume mount example
    - Comment
  * - *Data*    
    - ``-v $PWD/data:/var/lib/grafana``
    - Grafana data will be persisted on host directory: ``./data``.
  * - *Configuration*    
    - ``-v $PWD/grafana.ini:/etc/grafana/grafana.ini``
    - Custom Grafana configuration file. See [4]_ for details.
  * - *Server certificate*    
    - ``-v $PWD/certificates/server-cert.pem:/etc/grafana/certs/server-cert.pem``  
    - The server certificate (for HTTPS connection)
  * - *Server key*    
    - ``-v $PWD/certificates/server-key.pem:/etc/grafana/certs/server-key.pem``  
    - The server key (for HTTPS connection)

References
==========
.. [1] https://grafana.com/

.. [2] https://hub.docker.com/r/grafana/grafana

.. [3] https://github.com/grafana/grafana/blob/HEAD/LICENSING.md

.. [4] https://grafana.com/docs/grafana/latest/administration/configuration/


