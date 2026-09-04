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

### Hardlinks no pipeline de mídia

As importações de mídia utilizam hardlinks quando origem e destino estão no mesmo filesystem. Isso permite que a aplicação de download e os servidores de mídia referenciem o mesmo conteúdo sem duplicar os dados. Em um pool mergerfs, a posição física do arquivo continua relevante: hardlinks não atravessam filesystems, mesmo quando os caminhos aparecem sob o mesmo namespace agregado.

### Backups em camadas para workloads de jogos

Os perfis do Crafty foram distribuídos entre armazenamento rápido e o pool de capacidade. Para os servidores principais, o fluxo foi configurado com avisos aos usuários, parada controlada, arquivo compactado e reinicialização. A inspeção encontrou aproximadamente **19 GiB de backups históricos** nos dois destinos, evidenciando a execução real dessas rotinas.

Os agendamentos estão desativados no estado atual porque a plataforma experimental foi pausada. A documentação diferencia a automação configurada no passado do que está em execução hoje.

### Pausa orientada por capacidade

Durante o teste da plataforma Minecraft, o proxy, o lobby e dois backends ativos ocuparam cerca de **10,5 GiB dos 32 GiB** disponíveis no host. Como o Cerberus também sustenta serviços de dados, automação residencial, observabilidade e mídia, manter essa carga permanentemente reduziria a margem operacional do restante do ambiente.

A plataforma foi pausada antes da abertura para usuários reais. A decisão priorizou previsibilidade e capacidade do homelab, mantendo configurações e backups como base para uma retomada futura com limites de memória e escopo revistos.

## Roadmap

- adicionar um terceiro disco de 4 TB e planejar a migração das cargas adequadas para ZFS RAIDZ1;
- modernizar a base do sistema operacional e a camada de administração de armazenamento;
- ampliar a reprodutibilidade das stacks com documentação e infraestrutura como código sanitizada;
- evoluir métricas e alertas orientados a capacidade, disponibilidade e falhas recorrentes.

O roadmap descreve intenções e não deve ser interpretado como funcionalidade já implantada.
