# Inventário sanitizado

Este inventário apresenta apenas informações úteis para compreender a arquitetura. Identificadores, endereços, domínios, portas, caminhos internos e configurações operacionais foram removidos.

## Hardware

| Categoria | Especificação |
|---|---|
| Processador | Intel Xeon E5-2650 v4 |
| CPU lógica | 12 núcleos / 24 threads |
| Virtualização | Intel VT-x |
| Memória | 32 GiB |
| Armazenamento rápido | NVMe de 1 TB |
| Armazenamento de capacidade | 2 discos de 4 TB e 1 disco auxiliar de 1 TB |
| Pool atual | mergerfs, aproximadamente 8,2 TiB utilizáveis |
| Rede de borda | MikroTik RB750Gr3 (hEX) com failover LTE |

## Plataforma

| Categoria | Tecnologia |
|---|---|
| Sistema operacional | Debian GNU/Linux |
| Administração de armazenamento | OpenMediaVault |
| Containers | Docker Engine e Docker Compose |
| Virtualização | KVM/QEMU com libvirt |
| VM principal | Home Assistant OS, 4 vCPUs e 8 GiB de memória |
| Proxy e TLS | Traefik |
| VPN | WireGuard |
| DDNS | No-IP atualizado por script RouterOS agendado |

## Workloads

Na fotografia coletada em setembro de 2026, o host executava **48 containers**, organizados em **37 projetos Docker Compose**, além da VM do Home Assistant.

Os workloads são agrupados por função para evitar que a documentação se torne apenas uma lista de aplicações:

| Grupo | Exemplos representativos |
|---|---|
| Observabilidade e séries temporais | Grafana, InfluxDB, Uptime Kuma e Telegraf |
| Operação e automação | Portainer, Semaphore e Watchtower |
| Bancos de dados | PostgreSQL, MariaDB, Redis e TimescaleDB |
| Acesso e publicação | Traefik, Guacamole, RustDesk e WireGuard |
| Mídia e conteúdo | Radarr, Sonarr, Bazarr, Prowlarr, Jellyfin e Plex |
| Automação residencial | Home Assistant OS em VM e serviços de integração |
| Jogos e experimentação | Crafty Controller, Velocity e servidores Purpur |
| Aplicações e dados | WordPress, pipelines próprios e outros serviços self-hosted |

## Observações

- As versões exatas não são tratadas como característica permanente do projeto, pois acompanham a manutenção do ambiente.
- O inventário não representa alta disponibilidade dos serviços; o failover documentado é o da conectividade com a Internet.
- A plataforma Minecraft consta como workload experimental pausado, não como serviço atualmente oferecido a jogadores.
- IPv6 não faz parte do escopo atual do projeto.
