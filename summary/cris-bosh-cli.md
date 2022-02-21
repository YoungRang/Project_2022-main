#  Bosh CLI

### 1. BOSH CLI 기본 사용법

  ```shell
  $ bosh [<options>] <command> [<args>]
  ```

### 2. bosh environment

* 기본 문법
 ```shell
$ bosh environments (Alias: envs)
 ```

* 사용 예시
```shell
$ bosh env

Using environment '10.0.1.6' as client 'admin'
CPI                aws_cpi  
Features           compiled_package_cache: disabled  
                   config_server: enabled  
                   local_dns: enabled  
User               admin  

Succeeded
```

### 3. bosh delete-env

* 기본 문법
 ```shell
 $ bosh delete-env [deploymentFile] [--state path] [-v ...] [-o ...] [--vars-store path]
 ```

* 사용 예시
 ```shell
 $ bosh delete-env ~/workspace/bosh-deployment/bosh.yml \
 ```

### 4. bosh log-in

* 기본 문법
 ```shell
 $ bosh -e [my-env] l
 ```

* 사용 예시
```shell
$ bosh -e micro-bosh l

Successfully authenticated with UAA

Succeeded
```

### 5. bosh log-out

* 기본 문법
 ```shell
$ bosh -e [my-env] log-out 
 ```

* 사용 예시
```shell
$ bosh log-out 

Logged out from '192.168.10.241'

Succeeded
```

### 6. bosh stemcells

* 기본 문법
 ```shell
$ bosh -e [my-env] stemcells (Alias: ss) 
 ```

* 사용 예시
```shell
$ bosh -e micro-bosh ss
OR
$ bosh ss

Name                                     Version  OS             CPI  CID  
bosh-aws-xen-hvm-ubuntu-bionic-go_agent  1.34*    ubuntu-bionic  -    ami-0cde8d8d2d5179f43  

(*) Currently deployed

1 stemcells

Succeeded
```

### 7. bosh releases

* 기본 문법
 ```shell
$ bosh -e [my-env] releases (Alias: rs)
 ```

* 사용 예시
```shell
$ bosh -e micro-bosh rs
Or
$ bosh rs

Name                   Version              Commit Hash  
binary-buildpack       1.0.37*              d26e6dd  
bosh-dns               1.29.0*              f1433e0  
bosh-dns-aliases       0.0.3*               eca9c5a  
bpm                    1.1.9*               fd65e36  
capi                   1.109.0-PaaS-TA-v2*  37968404+  
.
.
.

(*) Currently deployed
(+) Uncommitted changes

36 releases
```

### 8. bosh cloud-config

* 기본 문법
 ```shell
$ bosh -e [my-env] cloud-config (Alias: cc)
 ```

* 사용 예시
```shell
$ bosh -e micro-bosh cc
Or
$ bosh cc

Using environment '10.0.1.6' as client 'admin'

azs:
- cloud_properties:
    availability_zone: ap-northeast-2c
  name: z1
- cloud_properties:
    availability_zone: ap-northeast-2c
 .
 .
 - cloud_properties:
    ephemeral_dist:
      size: 30000
      type: gp2
    instance_type: m4.xlarge
  name: caas_small_highmem

Succeeded
```

### 9. bosh runtime-config

* 기본 문법
 ```shell
$ bosh -e my-env runtime-config (Alias: rc)
 ```

* 사용 예시
```shell
$ bosh -e micro-bosh rc
OR
$ bosh rc

Using environment '10.0.1.6' as client 'admin'

addons:
- include:
    deployments:
    - paasta
    - pinpoint
    - pinpoint-monitoring
.
.
.
- name: "/dns_api_client_tls"
  options:
    alternative_names:
    - api.bosh-dns
    ca: "/dns_api_tls_ca"
    common_name: api.bosh-dns
    extended_key_usage:
    - client_auth
  type: certificate

Succeeded
```

### 10. bosh vms

* 기본 문법
 ```shell
bosh -e [my-env] -d [my-dep] vms [--vitals]
 ```

* 사용 예시
```shell
$ bosh vms

Task 42. Done

Deployment 'paasta'

Instance                                                  Process State  AZ  IPs           VM CID               VM Type             Active  Stemcell  
api/245bd808-3c98-45ae-a9a4-d130c9b8fbce                  stopped        z1  10.0.1.126    i-0ae497586a635242e  small               true    bosh-aws-xen-hvm-ubuntu-bionic-go_agent/1.34  
cc-worker/e0952fc5-607d-40f3-b12a-76add9f9095e            running        z1  10.0.1.127    i-039fe7762c7d26d9a  minimal             true    bosh-aws-xen-hvm-ubuntu-bionic-go_agent/1.34  
.
.
```