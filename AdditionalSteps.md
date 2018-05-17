* first Install
    * git clone https://github.com/uvwild/appagile-cicd-demo.git
    * run provisioning.sh deploy as a system user 
        provisioning.sh deploy --user developer
    * or as another user with sufficient permissions
        provisioning.sh deploy

* nexus
    * login admin/admin123
    * nexus configure allow redeploy for maven-releases in demo 

* sonar (each time)
    * login admin/admin
    * go to quality profiles and verify the JAVA profile
        * ELSE
        * go to administration/marketplace 
        * install SonarJava plugin
        * restart sonar!!
    * test sonar setup
        * get deploy key (e.g. springbootdemo: b57f766a18413dfc58efaf4586e189ba601ea7ce)
        ```sh
        mvn sonar:sonar \
          -Dsonar.host.url=http://sonarqube-cicd.192.168.42.249.nip.io \
          -Dsonar.login=b57f766a18413dfc58efaf4586e189ba601ea7ce
        ```
    * TODO: autoload java plugin for sonarqube

* gogs
    * login gogs/gogs
    * gogs repo created (gogs/openshift-springbootdemo)
    * (add other userss as collaborator to gogs repo!!)
    * git clone https://github.com/uvwild/springbootdemo.git
        * verify healthcheck URLs in deployconfig & make sure the java app serves those endpoints
    * cd springbootdemo
    * git remote add openshift http://gogs-cicd-springbootdemo.192.168.42.249.nip.io/gogs/openshift-springbootdemo.git    
    * git push openshift


* jenkins
    * load jenkins gogs plugin
    * setup webhook for jenkins



* issues

    * oc import-image jenkins:v3.6 --from="registry.access.redhat.com/openshift3/jenkins-2-rhel7" --confirm -n openshift
      Error from server (Forbidden): User "developer" cannot update imagestreams.image.openshift.io in the namespace "openshift": User "developer" cannot update imagestreams.image.openshift.io in project "openshift" (put imagestreams.image.openshift.io jenkins)
    *  workaround: <br>
         * import jenkins image locally
            oc import-image redhat-openjdk18-openshift --from="registry.access.redhat.com/redhat-openjdk-18/openjdk18-openshift" --confirm


* continue
    * oc project cicd-springbootdemo
    * oc start-build springbootdemo-pipeline
