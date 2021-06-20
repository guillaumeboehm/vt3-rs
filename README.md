# VirusTotal Api v3 (Public & Enterprise)
![Crates.io](https://img.shields.io/crates/v/vt3)
[![Documentation](https://docs.rs/vt3/badge.svg)](https://docs.rs/vt3)
![docs.rs](https://img.shields.io/docsrs/vt3/latest)
[![Build Status](https://travis-ci.com/marirs/vt3-rs.svg?branch=main)](https://travis-ci.com/marirs/vt3-rs)
[![GitHub license](https://img.shields.io/github/license/marirs/vt3-rs)](https://github.com/marirs/vt3-rs/blob/main/LICENSE)

VT3 provides an easy api interface to use VirusTotal v3 REST endpoints, 
including those exclusive to VirusTotal Enterprise such as 
- Live Hunt
- Retro Hunt 
- Zip Files 

## Usage
- Cargo.toml
```toml
[dependencies]
vt3 = "0.6.0"
```

- to enable enterprise features
```toml
[dependencies]
vt3 = { version = "0.6.0", features = ["enterprise"] }
```

- and then: to get `ip information`
```rust
use vt3::VtClient;

fn main() {
    let api_key = match std::env::args()
        .skip(1)
        .next()
        .ok_or_else(|| "Please provide the api key!")
    {
        Ok(api_key) => api_key,
        Err(e) => {
            println!("{:?}", e);
            std::process::exit(1)
        }
    };
    let ip_address = "5.2.69.42";

    let res = VtClient::new(&api_key).ip_info(ip_address);
    match res {
        Ok(report) => println!("{:#?}", report),
        Err(e) => println!("Error: {}", e.to_string()),
    }
}
```
- Providing a `user agent` for the client

```rust
use vt3::VtClient;

fn main() {
    let api_key = match std::env::args()
        .skip(1)
        .next()
        .ok_or_else(|| "Please provide the api key!")
    {
        Ok(api_key) => api_key,
        Err(e) => {
            println!("{:?}", e);
            std::process::exit(1)
        }
    };
    let ip_address = "5.2.69.42";

    let res = VtClient::new(&api_key)
        .user_agent("Chrome for Windows")
        .ip_info(ip_address);
    match res {
        Ok(report) => println!("{:#?}", report),
        Err(e) => println!("Error: {}", e.to_string()),
    }
}
```

## Examples
To run the examples - `Universal API Endpoints`:
- Domain info: `cargo run --example domain_info <your_api_key>`
- IP info: `cargo run --example ip_info <your_api_key>`
- URL info: `cargo run --example url_info <your_api_key>`
- URL info by id: `cargo run --example url_info_by_id <your_api_key>`
- URL rescan: `cargo run --example url_rescan <your_api_key>`
- File info: `cargo run --example file_info <your_api_key>`
- File scan: `cargo run --example file_scan <your_api_key>`
- File rescan: `cargo run --example file_rescan <your_api_key>`
- Get latest comments: `cargo run --example get_latest_comments <your_api_key>`
- Get comment by comment id: `cargo run --example get_comment <your_api_key>`

To run the examples - `Enterprise API Endpoints`:
- Get user information: `cargo run --example user_info --features="enterprise" <your_api_key> <user_id>`
- Delete a user: `cargo run --example delete_user --features="enterprise" <your_api_key> <user_id>`
- Get Api usage info: `cargo run --example api_usage --features="enterprise" <your_api_key> <user_id>`
- Get overall quotas for user: `cargo run --example overall_quotas --features="enterprise" <your_api_key> <user_id>`
- Get group information: `cargo run --example group_info --features="enterprise" <your_api_key> <group_id>`
- Get group api usage: `cargo run --example group_api_usage --features="enterprise" <your_api_key> <group_id>`
- Get group members: `cargo run --example group_members --features="enterprise" <your_api_key> <group_id>`
- Get Livehunt rulesets: `cargo run --example livehunt_get_rulesets --features="enterprise" <your_api_key>`
- Get Retrohunt jobs: `cargo run --example retrohunt_jobs --features="enterprise" <your_api_key>`

## VT Developer reference

- https://developers.virustotal.com/v3.0/reference

---
License: MIT

