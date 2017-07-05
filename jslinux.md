# Notes on building Node.js on jor1k Javascript Linux emulator

Emulator used: [jor1k](https://s-macke.github.io/jor1k/demos/main.html)

## Downloading Node source
Version 0.10.0 was arbitrarily chosen from older Node releases. More current Node releases are too large for compilationon the host.

```
wget https://nodejs.org/download/release/v0.10.0/node-v0.10.0.tar.gz
tar -zxf node-v0.10.0.tar.gz
```

### Build issues and solutions
* Running `./configure` in the Node source root should work. However, attempting to `make` results in gcc complaining about an unknown flag `-m32`
  * **Solution**: edit `common.gypi` and remove `-m32` from the compiler flags array.
* gcc error when building `libssl`.
  * **Solution**: exclude it from the build. Also exclude `npm`, while we're at it. We just want the runtime.

  ```
  ./configure --without-npm --without-ssl
  ```

* gcc error when building `libuv`: `uv_statbuf_t` has no member named `st_ctimensec`
  * **Solution**: add the compiler flag `-D__USE_MISC` to the compiler flags in `common.gypi`.

* Python error: no module named `bz2`
  * This is caused by the `libbz2` library missing on the distribution. This is fairly straightforward to build and install:

    ```
    wget http://www.bzip.org/1.0.6/bzip2-1.0.6.tar.gz
    tar -zxf bzip2-1.0.6.tar.gz
    make
    make install (as root)
    ```

  * Unfortunately, installing the Python `bz2` module seems like it requires recompiling Python.

### Compiling Python
We use the Python 2.7.7 source, the same version as shipped in the distribution:

  ```
  wget https://www.python.org/ftp/python/2.7.7/Python-2.7.7.tgz
  tar -zxf Python.2.7.7.tgz
  ```

#### Problems and solutions
* `./configure` fails with "unable to detect system"
  * *Possible solution*: specify a build triplet for `configure`. Since `config.guess` does not work however, what is the correct build triplet? For now, try using `openrisc-linux-gnu` as a guess.

    ```
    ./configure -build=openrisc-linux-gnu
    ```
