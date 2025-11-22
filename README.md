curl -v -H "Authorization: Bearer 1194c288d74a5a7904bdae2029622d2c" \
https://weaviate.example.com/v1/schema

grpcurl -plaintext   -import-path /opt/dev-deployments/anveshn-SaaS/backend/weaviate/weaviate/grpc/proto   -proto v1/weaviate.proto   grpc-weaviate.example.com:50051   list weaviate.v1.Weaviate