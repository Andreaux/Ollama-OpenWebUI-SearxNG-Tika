Stack version 1.0

# Self-hosted AI LLM Stack with Ollama, OpenWebUI, SearxNG and Tika

This is my Self-hosted AI LLM Stack's Docker-Compose template.

The stack features separate containers for:
- Ollama (ollama/ollama:latest)
- OpenWebUI (ghcr.io/open-webui/open-webui:latest)
- SearxNG (searxng/searxng:latest)
- Tika (apache/tika:latest-full)

The stack also includes dependencies to make sure the services start in the desired order.

My Home Lab runs Ubuntu Virtual Machines to host my Docker Projects where I run Nginx Proxy Manager as a reverse proxy. You will need to set up a proper domain and/or reverse proxy for OpenWebUI to be served over HTTPS. In my Homelab, I use Nginx Proxy Manager as reverse proxy and to issue Let's Encrypt SSL certificates through Cloudflare so I don't have to keep a port open for certbot to call in (a free Cloudflare account totally works which will enable free wildcard certificates for all your local hosts as well).

## GPUs

This deployment assumes you have 1 or more configured (or passed-through) NVIDIA GPUs with installed DRIVERS and the NVIDIA CONTAINER TOOLKIT!
My Home Lab runs 2 NVIDIA GPUs dedicated to this stack, that are passed through to the VM by Proxmox. Your setup will vary, but you need at least one available GPU as the configuration assumes the presence of one.

## Environment variables

Docker Compose needs environment variables to set up the containers correctly (notably for example a DB password). I have included an EXAMPLE.env file to make what is expected there easier to understand. Make a copy, edit your secrets and anything you might add and rename the file to .env

If you use Portainer, you will have to set these within Portainer (Advanced mode is easier as you just need to copy-paste the contents of the .env file) when creating the AI stack after you've pasted the docker-compose.yml file into Portainer. If you use "docker-compose" to bring up the stack, the .env file should be picked up automatically so fill in your information in there if you need it.

## Traefik / Nginx Proxy Manager

A reverse proxy is needed to be able to provide all internal services with an SSL certificate and be able to use all services without needing to write port numbers in URLs. I found the easiest for me was to use Cloudflare and get SSL certificates through Cloudflare. A free Cloudflare account is more than enough to achieve this. While you can deploy this Stack without Traefik or Nginx Proxy Manager, you would have to set up SSL certificates for each service individually. Traefik and Nginx Proxy Manager make this otherwise tedious process effortless.

This stack assumes you will be running your own Reverse Proxy (not part of this stack)

## Support this project

If you find this useful, a coffee through Ko-Fi is all it takes to make me happy <3 (I love coffee :D) Click the Sponsor button on the top of this page or visit https://ko-fi.com/andreaux to buy me a coffee.

## Disclaimer

This template is provided as-is with no pretention as for its usefulness or accuracy. I provide no support, but am open to comments, suggestions or corrections (please do!). Bear in mind that I'm still learning docker and docker-compose so there's no guarantee I haven't made errors in there although this installation works fine since a few months now.
