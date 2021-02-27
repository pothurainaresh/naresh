---
     hosts: webservers
     become:  true
     become_user : root
  tasks:
      - name: install tomcat
       yum : name= tomcat state= present
     - name: start tomcat
       service: name=tomcat  state= started
     - name: deploy war file
      get_url:  url=https://tomcat.apache.org/tomcat-7.0-doc/appdev/sample/sample.war dest=/usr/share/tomcat/webapps
       notify: restart tomcat
    handlers:
      - name: restart tomact
      service: name=tomcat state=restarted
