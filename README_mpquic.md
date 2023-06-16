
To integrate mpquic module in ns-3,

```
cd src
git clone git@github.com:ssjShirley/ns3-mpquic-module.git quic
cp -r quic/quic-applications/helper/. applications/helper/.
cp -r quic/quic-applications/model/. applications/model/.
```

In src/applications/wscrpt, add the following to module.source
```
    'model/mpquic-bulk-send-application.cc',
    'model/quic-client.cc',
    'model/quic-server.cc',
    'model/quic-echo-client.cc',
    'model/quic-echo-server.cc',
    'helper/mpquic-bulk-send-helper.cc',
    'helper/quic-client-server-helper.cc',
    'helper/quic-echo-helper.cc',
```

add the following to headers.source
```
    'model/mpquic-bulk-send-application.h',
    'model/quic-client.h',
    'model/quic-server.h',
    'model/quic-echo-client.h',
    'model/quic-echo-server.h',
    'helper/mpquic-bulk-send-helper.h',
    'helper/quic-client-server-helper.h',
    'helper/quic-echo-helper.h',
```

Configure the mpquic module
```
./waf configure --enable-example
./waf
```

Run examples
