# Decisões técnicas e roadmap

## Decisões atuais

### Docker Compose por stack

Cada domínio funcional é mantido como uma stack independente. Isso facilita atualizações, diagnóstico e isolamento de falhas sem exigir um único arquivo de orquestração para todo o homelab.

### Home Assistant OS em KVM/libvirt

O Home Assistant utiliza uma VM dedicada, persistente e com inicialização automática. A separação preserva o modelo de appliance do HAOS e reduz o acoplamento com os serviços em containers.

### MikroTik na borda

O RouterOS concentra roteamento, firewall/NAT IPv4, WireGuard e failover para LTE. Um script agendado atualiza o No-IP quando o endereço público muda. Essa automação elimina uma etapa manual e mantém o acesso remoto independente de um IP fixo.

### Traefik como ponto de entrada

A publicação de aplicações web é centralizada no Traefik para evitar configurações TLS e de roteamento duplicadas em cada serviço. O acesso administrativo remoto é priorizado pela VPN.

### InfluxDB e Grafana para séries temporais

O InfluxDB recebe métricas produzidas por serviços e coletores; o Grafana fornece exploração e visualização. Os pipelines de velocidade da Internet e energia nasceram de necessidades do próprio ambiente e foram separados em projetos públicos reutilizáveis.

### mergerfs para capacidade heterogênea

O mergerfs atende ao desenho atual porque agrega discos de capacidades e filesystems distintos com baixa barreira de migração. O trade-off é não oferecer, sozinho, a redundância e a integridade ponta a ponta esperadas de um pool ZFS.

## Roadmap

- adicionar um terceiro disco de 4 TB e planejar a migração das cargas adequadas para ZFS RAIDZ1;
- modernizar a base do sistema operacional e a camada de administração de armazenamento;
- ampliar a reprodutibilidade das stacks com documentação e infraestrutura como código sanitizada;
- evoluir métricas e alertas orientados a capacidade, disponibilidade e falhas recorrentes.

O roadmap descreve intenções e não deve ser interpretado como funcionalidade já implantada.
