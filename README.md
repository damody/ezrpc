# EZRPC - macro-based, easy use rpc library

This is a easy use rpc library for rust
The library is designed to be easily adapatable and places no restrictions on
transport protocol or serialization format.

```toml
[dependencies]
ezrpc = "0.1.0"
```

# Features

- Define functions one place, call them from the server and execute them on the
  client.

# Example

Start by defining a rpc service:

Define rpc functions with the following:

```rust
// macro EzrpcA for Async function
#[derive(EzrpcA)]
async fn add(a: i32, b: i32) -> Result<i32, ()> {
    Ok(a + b)
}

// macro EzrpcB for Blocking function
#[derive(EzrpcB)]
fn sub(a: i32, b: i32) -> i32 {
    a - b
}
```

And call them on the server with:

```rust
// init rpc on mqtt server
ezrpc_server_mqtt("mqtt://127.0.0.1:1883")
// or
// init rpc on server
ezrpc_server_tcp("tcp://0.0.0.0:3333")

// call async rpc for random client
rpc_add(5, 6).await;
// assign task by clientid
rpc_id_add("clientid",5, 6).await;

// call block function
rpc_sub(5, 6);
// assign task by clientid
rpc_id_sub("clientid",5, 6);

```

init on client
```rust
// init on client
ezrpc_client_init_mqtt("mqtt://127.0.0.1:1883", "clientid");

// init on client
ezrpc_client_init_tcp("mqtt://127.0.0.1:3333", "clientid");

```
# Check list
- [ ] rpc macro base
- [ ] async rpc
- [ ] blocking rpc
- [ ] rpc on mqtt
- [ ] rpc on tcp
