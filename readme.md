File	Who has it?	Purpose
kafka.crt	Kafka server	Public server certificate
kafka.key	Kafka server only	Private key
ca.crt	Kafka and applications	Certificate authority used to establish trust

generate private CA

# Private CA key
openssl genrsa -out ca.key 4096

# CA public certificate
openssl req -x509 -new -nodes \
  -key ca.key \
  -sha256 \
  -days 3650 \
  -out ca.crt \
  -subj "/CN=My Kafka CA"

# kafa private key
  openssl genrsa -out kafka.key 2048
# Create a certificate signing request:
  openssl req -new \
  -key kafka.key \
  -out kafka.csr \
  -subj "/CN=kafka.example.com"

  # Create a SAN configuration file:
  subjectAltName=DNS:kafka,DNS:kafka.example.com

  # Sign the server certificate using your CA:
  openssl x509 -req \
  -in kafka.csr \
  -CA ca.crt \
  -CAkey ca.key \
  -CAcreateserial \
  -out kafka.crt \
  -days 365 \
  -sha256 \
  -extfile san.cnf

  <img width="845" height="355" alt="image" src="https://github.com/user-attachments/assets/ebd99fd0-d3d0-40a6-9825-1b040f5edc07" />

  
