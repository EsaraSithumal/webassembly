FROM wasmedge/slim-runtime:0.10.1

ADD target/wasm32-wasi/release/rust_server.wasm /

CMD ["wasmedge", "--dir", ".:/", "/rust_server.wasm"]