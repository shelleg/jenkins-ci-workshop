Jenkins CI Workshop
===================

Workshop to cover the process of setting-up maintaining and running Jenkins pipelines.

QuickStart
----------

git clone <this repo>
cd <this repo>
vagrant up


Access nexus via:
http://172.16.1.5:8081

Access jenkins via:
http://172.16.1.6:8080


Beyond the basics:
------------------

You can choose to use the squid proxy server as a good fallback during development / presentation
The Ultimate solution would be if you have one already present on LAN and you can customize [ jenkins only ATM ] it by adding the following to the playbook:

    vars:
    cj_set_proxy: true
    proxy_server: "172.16.1.99"
    noproxy_hosts:
      - '127.0.0.1'
      - '172.16.1.*'
      
So the Jenkins.yml playbook hould look something like:

    - hosts: jenkins
      become: true
      vars:
        cj_set_proxy: true
        proxy_server: "172.16.1.99"
        noproxy_hosts:
          - '127.0.0.1'
          - '172.16.1.*'
      roles:
        - role: epel
        - role: git
        - role: squid
          squid_server_mode: false
        - role: oracle-java
        - role: ansible-role-custom-jenkins

