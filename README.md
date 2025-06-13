---
   - name: Deploy a web application
     hosts: cloud_server
     tasks:
       - name: Install Dependencies
         apt: name='{{ item }}' state=present
         with_items:
          - python
          - python-setuptools
          - python-dev
          - build-essentials
          - python-pip
          - python-mysqldb
            
    - name: install Mysql database
      apt: name='{{ item }}' state=present
      with_items:
       - mysql-server
       - mysql-client

    - name: start the mysql services
      service: 
        name: mysql
        state: started
        enabled: yes

    - name: create application database
      mysql_db:
        name: oradb
        state: present
        
     
