# This is an example of running WASM server in kubernetes

The `src/main.rs` contains a simple echo server written in Rust. When a POST request is received the responds with the received request body. The application is compiled to `WASM` and then a container image that containes the compiled `WASM` binary and a `WASM` runtime is generated. The runtime used in this example is `WasmEdge`. Then this image is used to create a Pod in a K8s local K8s cluster. Docker descktop is used to run the local cluster.

## Steps
________
01. First we need to compile the rust code into WASM. In order to do this we need the WASI enabled Rust toolchain. Run the command below to install it.
```
rustup target add wasm32-wasi
```
Then we can compile the code to WASM using the following command.
```
cargo build --target wasm32-wasi
```
This will create the `.wasm` file in the `target/wasm32-wasi/release` directory.

02. Next we have to build the cotainer image and push it to docker hub.

03. Create a Pod using the `pod.yaml` file.
```
kubectl create -f pod.yaml
```
Please replace the image field by [your-user-name]/[your-repo]

04. Test the server. Use command below to creat a port forwarding.
```
kubectl port-forward rust-server 3000:1234
```
Run below command to send a request.
```
curl -X POST http://localhost:3000 -d "hello_world"
```
This should return "hello_world". If every thing is OK.