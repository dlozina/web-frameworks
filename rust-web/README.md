# Rust web framework

First steps with Rust web framework

1. Create new project
```shell
cargo new rust-web
```

2. Add dependencies to Cargo.toml
```toml
[dependencies]
actix-web = "4"
```

3. Add code to main.rs
```rust
use actix_web::{get, post, web, App, HttpResponse, HttpServer, Responder};

#[get("/")]
async fn hello() -> impl Responder {
    HttpResponse::Ok().body("Hello world!")
}

#[post("/echo")]
async fn echo(req_body: String) -> impl Responder {
    HttpResponse::Ok().body(req_body)
}

async fn manual_hello() -> impl Responder {
    HttpResponse::Ok().body("Hey there!")
}

#[actix_web::main]
async fn main() -> std::io::Result<()> {
    HttpServer::new(|| {
        App::new()
            .service(hello)
            .service(echo)
            .route("/hey", web::get().to(manual_hello))
    })
        .bind(("127.0.0.1", 8080))?
        .run()
        .await
}
```

4. Run the server

Start on the path of the project
```shell
cargo run
```

Start with apsolute path
```shell
cargo run --manifest-path <path_to_project>/Cargo.toml
```

Paths to test
```shell
http://localhost:8080
http://localhost:8080/echo
http://localhost:8080/hey
```