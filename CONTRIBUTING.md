# Contributing

## Building from source

To build `spin-test` from source, you'll need to [download the `WASI_SDK`](https://github.com/WebAssembly/wasi-sdk/releases/) (needed for the C compiler used to compile some C dependencies).

Once you have the SDK on your machine somewhere, point to it via the `WASI_SDK_PATH` environment variable.

Then set the following environment variables:

```bash
export LIBSQLITE3_FLAGS="\
    -DSQLITE_OS_OTHER \
    -USQLITE_TEMP_STORE \
    -DSQLITE_TEMP_STORE=3 \
    -USQLITE_THREADSAFE \
    -DSQLITE_THREADSAFE=0 \
    -DSQLITE_OMIT_LOCALTIME \
    -DSQLITE_OMIT_LOAD_EXTENSION \
    -DLONGDOUBLE_TYPE=double"
export CC_wasm32_wasi=$WASI_SDK_PATH/bin/clang
export WASI_SYS_ROOT=$WASI_SDK_PATH/share/wasi-sysroot
export CC="$WASI_SDK_PATH/bin/clang --sysroot=$WASI_SYS_ROOT"
```

You can then run `cargo build --release` to build `spin-test`.