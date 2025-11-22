# Testing Weaviate REST and gRPC Connectivity

This guide explains how to verify whether your **Weaviate REST and gRPC servers** are accessible and responding correctly.

---

## Prerequisites

Before testing, you must have the following:

### 1. grpcurl

`grpcurl` is a command-line tool used to interact with gRPC servers.

Install grpcurl:

**Linux / macOS:**

```bash
brew install grpcurl
```

**Ubuntu / Debian:**

```bash
sudo apt install grpcurl
```

**Windows:**
Download from:
[https://github.com/fullstorydev/grpcurl/releases](https://github.com/fullstorydev/grpcurl/releases)

---

### 2. Weaviate Proto Files

You need Weaviate gRPC proto definitions to test the gRPC server.

Download them from GitHub:

```bash
git clone https://github.com/weaviate/weaviate.git
```

Proto file location:

```
weaviate/grpc/proto/
```

Ensure the proto path exists on your system. Example path used below:

```
/opt/backend/weaviate/weaviate/grpc/proto
```

---

## ✅ Test REST API (HTTP)

Use the following curl command to confirm the REST API is working:

```bash
curl -v -H "Authorization: Bearer YOUR_TOKEN_HERE" \
https://weaviate.example.com/v1/schema
```

Replace:

* `YOUR_TOKEN_HERE` with your actual Bearer token
* `weaviate.example.com` with your domain

A valid JSON response confirms REST API is accessible.

---

## ✅ Test gRPC Server

Use `grpcurl` to list available gRPC services and confirm connectivity:

```bash
grpcurl -plaintext \
  -import-path /opt/backend/weaviate/weaviate/grpc/proto \
  -proto v1/weaviate.proto \
  grpc.example.com:50051 \
  list weaviate.v1.Weaviate
```

Replace:

* `/opt/backend/weaviate/weaviate/grpc/proto` with your actual proto directory path
* `grpc.example.com:50051` with your gRPC host and port

### ✅ Expected Result

If the gRPC server is running correctly, it will return a list of available RPC methods under:

```
weaviate.v1.Weaviate
```

---

## Troubleshooting

| Issue              | Solution                                                   |
| ------------------ | ---------------------------------------------------------- |
| Connection refused | Ensure gRPC server is running and firewall allows the port |
| Proto not found    | Validate the proto directory path                          |
| Unauthorized       | Check Authorization header or token                        |

---

## Summary

This README helps you:

* Verify Weaviate REST endpoint health
* Confirm gRPC server availability using grpcurl
* Ensure proto files are correctly referenced

Use this as a quick validation step during deployments or debugging.

---

✅ You can now reliably test both REST and gRPC connectivity for Weaviate
