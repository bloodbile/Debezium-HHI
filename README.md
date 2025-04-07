# 🎀 Debezium HHI 🎀
## Overview
All versions of the Debezium Web UI have been discovered to be vulnerable to arbitrary Host Header Injection. This vulnerability arises due to the applications reliance on user supplied host headers without adequate validation or sanitization.
## Details
The vulnerability was descovered by sending 2 GET requests to the /locales/en-US/public.json endpoint. The first request was a standard GET request without the Host header supplied, and the server responded with:<br>
'RESTEASY003210: Could not find resource for full path: http://103.93.133.24:8081/locales/en-US/public.json?cachebust=v4uepg'</br>
The second request was the same request, but with the Host header set to '8.8.8.8', and this time the server responded with:<br>
'RESTEASY003210: Could not find resource for full path: http://8.8.8.8/locales/en-US/public.json?cachebust=v4uepg'</br>
As you can see, the server responded with the domain of the path set to the injected host header, indicating that the Host Header Injection was successful.
## Impact
This vulnerability can allow attackers to manipulate the Host header to misdirect requests, impersonate other domains, or bypass security mechanisms in place. Depending on additional application logic, this can facilitate further attacks, such as unauthorized data access or execution of undesired commands.
