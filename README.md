# Anvil Connect JWT / camfou fork
**[Anvil Connect](https://github.com/christiansmith/anvil-connect)** aims to be a scalable, full-featured, ready-to-run [**OpenID Connect**](http://openid.net/connect/) + [**OAuth 2.0**](http://tools.ietf.org/html/rfc6749) **Provider**. This package contains the JWT modeling library used by [Anvil Connect](https://github.com/camfou/connect).


![Build Status](https://img.shields.io/travis/camfou/connect-jwt/master.svg) ![License](https://img.shields.io/github/license/camfou/connect-jwt.svg) ![npm](https://img.shields.io/david/camfou/connect-jwt.svg?style=flat) ![Coverage Status](https://coveralls.io/repos/github/camfou/connect-jwt/badge.svg?branch=master)


## Install

    $ npm install camfou-connect-jwt --save

## Usage

All JWTs must conform to the JWT/JWS/JWE/JW\* specifications, but applications may impose additional requirements. For example, an OpenID Connect ID Token must require certain claims and headers, restrict the use of others, set default values, etc. Anvil Connect JWT is an abstract class that can be used to define JWTs conforming to application specfic requirements.

    // require the package
    var JWT = require('camfou-connect-jwt');


    // define a subclass
    var IDToken = JWT.define({

      // default header
      header: {
        alg: 'RS256'
      },

      // permitted headers
      headers: [
        'alg'
      ],

      // modify header schema
      registeredHeaders: {
        alg:   { format: 'StringOrURI', required: true, enum: ['RS256'] }
      },

      // permitted claims
      claims: ['iss', 'sub', 'aud', 'exp', 'iat', 'nonce', 'acr', 'at_hash'],

      // modify payload schema
      registeredClaims: {
        iss:      { format: 'StringOrURI', required: true },
        sub:      { format: 'StringOrURI', required: true },
        aud:      { format: 'StringOrURI', required: true },
        exp:      { format: 'IntDate',     required: true, default: expires('day')  },
        iat:      { format: 'IntDate',     required: true, default: Date.now },
        nonce:    { format: 'String' },
        acr:      { format: 'String' },
        at_hash:  { format: 'String' }
      }

    });


## The MIT License (MIT)

Copyright (c) 2015 Anvil Research, Inc.


