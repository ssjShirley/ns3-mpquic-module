To integrate mpquic module in ns-3,

```
cd src
git clone https://github.com/ssjShirley/ns3-mpquic-module.git quic
cp -r quic/quic-applications/helper/. applications/helper/.
cp -r quic/quic-applications/model/. applications/model/.
cp -r quic/examples ../examples/quic
```

## `CMake`
After `ns-3.36`, `ns-3` adopted `cmake` as the new build system.

```
git apply < quic/ns3.patch
```

To enable Python bindings, additionally install `cppyy` and add `--enable-python-bindings` to the `./ns3 configure` command line.

```
./ns3 configure --enable-examples --enable-python-bindings -- -DNS3_BINDINGS_INSTALL_DIR="$HOME/.local/lib/python3.10/site-packages"
```

Otherwise, configure `ns3` without Python bindings

```
./ns3 configure --enable-examples
```

Build and install

```
./ns3 build -j$(nproc)
./ns3 install
sudo ldconfig
```

Run mpquic examples

```
./ns3 run wns3-mpquic-two-path
```

## `Waf`

In src/applications/wscript, add the following to module.source
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
```
./waf --run wns3-mpquic-two-path
```
