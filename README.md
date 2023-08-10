# Gallagher Command Centre REST API

In 2020 this Github repository became the authoritative source of the reference documentation for
Command Centre's REST API.

The `ref` folder of this repository contains the documentation in HTML form.  You can browse it
online at [github.io].

We use [Spectacle](https://github.com/sourcey/spectacle) to generate that HTML from OpenAPI/Swagger
2.0 files in the `swagger` folder.  Generating good-looking HTML is the sole purpose of those
Swagger files:  we do not use them for code generation or API testing.  Therefore they do not follow
OpenAPI guidelines where doing so would compromise the readability of the documentation.

To download the HTML and YAML in a zip file use the Code button on
[Github.com](https://github.com/GallagherSecurity/cc-rest-docs).  However, to benefit from our
regular improvements to that documentation we suggest you browse [the HTML][github.io] whenever
possible.

[github.io]: https://gallaghersecurity.github.io/cc-rest-docs/ref

```mermaid
flowchart TD;
        start --> op1;
        op1 --> cond;
        cond -->|no|clientquit;
        cond --> |yes| o_reqclientcert;
        o_reqclientcert  -->  o_clientsendscert;
        o_clientsendscert  -->  o_clientreq;
        o_clientreq --> c_apikeycheck;

        c_apikeycheck --> |no| o_noapikey;
        c_apikeycheck --> |yes| c_versioncheck;

        c_versioncheck  -->  |">= 8.50"| c_clientcertcheck1;
        c_versioncheck  -->  |"< 8.50" | c_clientcertcheck840;

        c_clientcertcheck1 --> |no| c_clientcertcheck2;

        c_clientcertcheck840 --> |yes| c_sourceip1;
        c_clientcertcheck840 --> |no| c_correctcert;

        c_clientcertcheck2 --> |no| o_badprint;
        c_clientcertcheck2 --> |yes| c_sourceip1;

        c_clientcertcheck1 --> |yes| c_correctcert;
        c_correctcert --> |no| o_badprint;

        c_correctcert --> |yes| c_sourceip1;
        c_sourceip1 --> |no| c_licence;
        c_sourceip1 --> |yes| c_sourceip2;
        
        c_sourceip2 --> |yes| c_licence;
        c_sourceip2 --> |no| o_badip;

        c_licence --> |no| o_nolicence;
        c_licence --> |yes| c_privcheck;
        c_privcheck --> |no| o_nopriv;
        c_privcheck --> |yes| o_argcheck;

```
