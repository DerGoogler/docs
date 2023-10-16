# Build cURL on Android

It is posible to build cURL on Android? Yes but limited.. 

## Requirements

- Any method to get the tar file
- [Systemless Mkshrc](https://github.com/Magisk-Modules-Alt-Repo/mkshrc)
- [GCC Toolchain](https://github.com/Googlers-Repo/gcc)

## Building

```shell
xh -d https://curl.se/download/curl-7.87.0.tar.gz
```

Then you'll need to run `configure`

```shell
./configure --host aarch64-linux-android --with-pic --disable-shared --without-ssl --prefix=$PREFIX
```

Adjustments to the features and protocols

```
  Host setup:       aarch64-unknown-linux-android
  Install prefix:   /data/chuser/<USER>/usr
  Compiler:         aarch64-linux-android-gcc
   CFLAGS:          -pie -Werror-implicit-function-declaration -O2 -Wno-system-headers
   CPPFLAGS:
   LDFLAGS:
   LIBS:            -lz

  curl version:     7.87.0
  SSL:              no      (--with-{openssl,gnutls,nss,mbedtls,wolfssl,schannel,secure-transport,amissl,bearssl,rustls} )
  SSH:              no      (--with-{libssh,libssh2})
  zlib:             enabled
  brotli:           no      (--with-brotli)
  zstd:             no      (--with-zstd)
  GSS-API:          no      (--with-gssapi)
  GSASL:            no      (libgsasl not found)
  TLS-SRP:          no      (--enable-tls-srp)
  resolver:         POSIX threaded
  IPv6:             enabled
  Unix sockets:     enabled
  IDN:              no      (--with-{libidn2,winidn})
  Build libcurl:    Shared=no, Static=yes
  Built-in manual:  no      (--enable-manual)
  --libcurl option: enabled (--disable-libcurl-option)
  Verbose errors:   enabled (--disable-verbose)
  Code coverage:    disabled
  SSPI:             no      (--enable-sspi)
  ca cert bundle:   no
  ca cert path:
  ca fallback:
  LDAP:             no      (--enable-ldap / --with-ldap-lib / --with-lber-lib)
  LDAPS:            no      (--enable-ldaps)
  RTSP:             enabled
  RTMP:             no      (--with-librtmp)
  PSL:              no      (libpsl not found)
  Alt-svc:          enabled (--disable-alt-svc)
  Headers API:      enabled (--disable-headers-api)
  HSTS:             no      (--enable-hsts)
  HTTP1:            enabled (internal)
  HTTP2:            no      (--with-nghttp2, --with-hyper)
  HTTP3:            no      (--with-ngtcp2, --with-quiche --with-msh3)
  ECH:              no      (--enable-ech)
  WebSockets:       no      (--enable-websockets)
  Protocols:        DICT FILE FTP GOPHER HTTP IMAP MQTT POP3 RTSP SMTP TELNET TFTP
  Features:         AsynchDNS IPv6 Largefile UnixSockets alt-svc libz threadsafe
```

Check if it's working

```shell
$PREFIX/local/bin/curl --version
```