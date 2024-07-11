#### Setup new project

```bash
# docker clear cache: https://depot.dev/blog/docker-clear-cache

docker compose build
docker compose run --rm setup bash
rails new XXX
```

#### Setup SSL

```bash
# Install OpenSSL if it isn't already installed (Assuming you use Apt)
sudo apt install openssl

# Generate the SSL Certificates
openssl req -x509 -sha256 -nodes -newkey rsa:2048 -keyout localhost.key -out localhost.crt -subj "/CN=localhost" -days 365

# Make the SSL directory
mkdir config/ssl

# Move the files to config/ssl
mv localhost.key localhost.crt config/ssl/

# Running the server the long way by specifying both files

# OR
rails s -b "ssl://0.0.0.0:3000?key=config/ssl/localhost.key&cert=config/ssl/localhost.crt"

# OR
# config/puma.rb

#...rest of file...

# At the bottom, we add these lines
ssl_bind '0.0.0.0', '3000', {
  key: ENV.fetch("SSL_KEY_PATH") { 'config/ssl/localhost.key' },
  cert: ENV.fetch("SSL_CERT_PATH") { 'config/ssl/localhost.crt' }
}
```
