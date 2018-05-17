* setup maven repo in nexus
* add java project
* create gogs repo (no auth for now)
* load jenkins gogs plugin
* setup webhook for jenkins
* configure sonar (each time)
    * install sonar java plugin (admin/admin)
    * download via administration/marketplace SonarJava
    * restart sonar!!

* test sonar setup
    * get deploy key (e.g. springbootdemo: b57f766a18413dfc58efaf4586e189ba601ea7ce)

        ```sh
        mvn sonar:sonar \
          -Dsonar.host.url=http://sonarqube-cicd.192.168.42.249.nip.io \
          -Dsonar.login=b57f766a18413dfc58efaf4586e189ba601ea7ce
        ```
* TODO: autoload java plugin for sonarqube

* nexus configure allow redeploy for maven repositories

* verify healthcheck URLs in deployconfig & make sure the java app serves those endpoints


* issues

    * oc import-image jenkins:v3.7 --from="registry.access.redhat.com/openshift3/jenkins-2-rhel7" --confirm -n openshift
      Error from server (Forbidden): User "developer" cannot update imagestreams.image.openshift.io in the namespace "openshift": User "developer" cannot update imagestreams.image.openshift.io in project "openshift" (put imagestreams.image.openshift.io jenkins)
    *  workaround: <br>
         * import jenkins image locally

oc import-image redhat-openjdk18-openshift --from="registry.access.redhat.com/redhat-openjdk-18/openjdk18-openshift" --confirm

then use simply image name=redhat-openjdk18-openshift
check with 
oc get is
