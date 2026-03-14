# Task A – 502 Bad Gateway

## Goal
Identify the root cause of the 502 error, apply a fix, and explain how to prevent it in production.

``` docker-compose.yml
# docker-compose.yml
version: '3'
services:
 web:
 build:.
 ports:
 - "3000:3000"
 nginx:
 image: nginx:alpine
 volumes:
 - ./nginx.conf:/etc/nginx/conf.d/default.conf
 ports:
 - "80:80"
 depends_on:
 - web
# nginx.conf
server {
 listen 80;
 location / {
 proxy_pass http://web:8080;
 ...
 }
}
// server.js
const express = require('express');
const app = express();
const PORT = 3000;

```

## Notes
This task will contain:
- root cause analysis,
- fixed configuration,
- prevention recommendations,
- optional screenshots or logs.

## Problem

The root cause is an incorrect backend port in nginx.conf.
Node.js app listens on: 3000
Docker exposes: 3000:3000
Nginx proxies to: 8080 ❌

This mismatch causes the reverse proxy to fail.
The problem is a port mismatch.

In `nginx.conf`, Nginx sends traffic to:

```nginx
proxy_pass http://web:8080;
```
But in server.js, the Node.js app runs on:
```const PORT = 3000;```
## Process
So Nginx is trying to reach port 8080, but the app is actually listening on port 3000.
Because of that, Nginx cannot connect to the backend and returns 502 Bad Gateway

## Fix
Why this works
The Node.js app listens on port 3000.
So Nginx also has to forward traffic to port 3000.
After changing:
```server {
  listen 80;

  location / {
    proxy_pass http://web:3000;
  }
}
```


