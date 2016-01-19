# NGINX Snippets

A collection of various useful NGINX and NGINX Plus configuration
code snippets, related files and examples of how they can be used.

<sub>Important: These are not production tested and should be implemented at your
own risk,</sub>

### GeoIP based routing

<hr>

#### Route traffic based on subnet

Route traffic based on the requesters specific IP address.

```
geo $to_specific_web {
    2.3.4.5 1;
    default 0;
}

upstream specific_web {
    server 1.2.3.4;
}

server {
    ...
    if ( $to_specific_web ) { return 307; }
    error_page 307 = @specific;

    location @specific  {
        proxy_pass http://specific_web;
    }
}
```
