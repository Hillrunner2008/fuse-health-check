## JBoss Fuse 6.3 health check
This project contains health check code extracted from https://github.com/fabric8io/fabric8 for the purpose of having similar functionality in JBoss Fuse 6.3. It was not possible to simply use the code without modification as a result of some internal scr state not meeting the expectations of the health check out of the box.  This modified health check ignores the unsatisfied scr services from io.fabric8 bundles. 

### Health Check Endpoint
```bash
  curl -X GET -i http://localhost:8181/health-check
```
#### Health Result Example
```bash
HTTP/1.1 200 OK
Date: Mon, 15 May 2017 23:11:25 GMT
Content-Length: 8
Server: Jetty(9.2.19.v20160908)

HEALTHY
```

#### Failure Example
```bash
HTTP/1.1 503 Service Unavailable
Date: Mon, 15 May 2017 23:13:22 GMT
Content-Length: 52
Server: Jetty(9.2.19.v20160908)

NOT HEALTHY
bundle-state: Bundle 284 is not started
```

#### Install

From Fuse Shell
```bash
features:addurl mvn:com.rhc/fuse-health-check-feature/1.0.0/xml/features
features:install fuse-health-check-feature 
```

#### featuresBoot Install

1. Add health check bundle and feature file to system directory
2. Add fuse-health-check-feature to featuresBoot in  etc/org.apache.karaf.features.cfg
