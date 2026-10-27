# Network Troubleshooting Lab

**Documentação técnica com procedimentos de diagnóstico de rede para Windows.**

---

## 📋 Visão Geral / Overview

Laboratório de documentação com procedimentos de diagnóstico de rede usando comandos nativos do Windows: ipconfig, ping, tracert, nslookup. Inclui checklists por sintoma, fluxos de diagnóstico e comandos seguros.

Technical documentation with network troubleshooting procedures using native Windows commands: ipconfig, ping, tracert, nslookup. Includes symptom-based checklists, diagnostic flows, and safe commands.

---

## ⚠️ Aviso / Disclaimer

> **Projeto Pessoal / Laboratório / Personal Project / Laboratory Project**
>
> Este projeto é destinado apenas para fins educacionais e de laboratório. Uso educacional apenas.
>
> This project is for educational and laboratory purposes only.

---

## 📁 Estrutura do Projeto / Project Structure

```
network-troubleshooting-lab/
├── README.md
├── diagnistic_flows/
│   ├── fluxo_geral.md
│   ├── fluxo_internet.md
│   └── fluxo_local.md
├── checklists/
│   ├── checklist_lentidao.md
│   ├── checklist_sem_internet.md
│   └── checklist_dns.md
└── comandos_referencia/
    ├── ipconfig.md
    ├── ping.md
    ├── tracert.md
    └── nslookup.md
```

---

## 🚀 Uso / Usage

Este repositório serve como referência para técnicos de suporte de TI. Cada arquivo pode ser consultado individualmente.

This repository serves as a reference for IT support technicians. Each file can be consulted individually.

---

## 📖 Comandos de Referência / Reference Commands

### `ipconfig`

Exibe configuração de rede atual.

```cmd
ipconfig              # Exibe configuração básica
ipconfig /all         # Exibe configuração completa
ipconfig /release     # Libera o endereço IP (DHCP)
ipconfig /renew       # Renova o endereço IP (DHCP)
ipconfig /flushdns    # Limpa o cache DNS
ipconfig /displaydns  # Exibe o cache DNS
ipconfig /registerdns  # Registra registros DNS
```

---

### `ping`

Testa conectividade com hosts.

```cmd
ping 8.8.8.8          # Ping para Google DNS
ping google.com       # Ping para domínio
ping -t 8.8.8.8       # Ping contínuo (Ctrl+C para parar)
ping -n 4 8.8.8.8     # 4 pacotes (padrão do Windows)
ping -l 1500 8.8.8.8  # Pacote com tamanho 1500 bytes
ping -w 3000 8.8.8.8  # Timeout de 3000ms
```

---

### `tracert`

Rastreia a rota até um host.

```cmd
tracert google.com    # Rastreamento para domínio
tracert -d 8.8.8.8    # Sem resolução DNS (mais rápido)
tracert -h 30 8.8.8.8 # Máximo de 30 saltos
```

---

### `nslookup`

Consulta registros DNS.

```cmd
nslookup google.com         # Consulta A (IPv4)
nslookup -type=mx gmail.com # Consulta MX (Mail Exchange)
nslookup -type=txt example.com # Consulta TXT
nslookup                    # Modo interativo
  > set type=AAAA
  > google.com
```

---

## 📋 Checklists por Sintoma / Symptom Checklists

### Sem Internet / No Internet

1. Verificar se o adaptador está habilitado
2. Executar `ipconfig` para verificar IP
3. Executar `ping 127.0.0.1` (loopback)
4. Executar `ping` do gateway (ver `ipconfig`)
5. Executar `ping 8.8.8.8` (DNS externo)
6. Executar `nslookup google.com` (resolução DNS)
7. Se DNS falhar → `ipconfig /flushdns`
8. Executar `tracert 8.8.8.8` para identificar onde falha

### Internet Lenta / Slow Internet

1. Verificar velocidade com `ping` para gateway
2. Executar `tracert` para identificar gargalos
3. Verificar se há muitos pacotes perdidos no ping
4. Verificar uso de banda em `Resource Monitor`
5. Verificar se há DHCP funcionando corretamente

### Problemas DNS / DNS Issues

1. Executar `nslookup google.com`
2. Verificar IP do DNS em `ipconfig /all`
3. Testar com DNS público (`8.8.8.8`, `1.1.1.1`)
4. Executar `ipconfig /flushdns`
5. Verificar configuração de proxy

---

## 🔄 Fluxos de Diagnóstico / Diagnostic Flows

### Fluxo Geral de Diagnóstico

```
Problema relatado
    ↓
Verificar conectividade física (cabo/Wi-Fi)
    ↓
ipconfig → Verificar IP, gateway, DNS
    ↓
ping 127.0.0.1 → Loopback OK?
    ↓
ping gateway → Gateway OK?
    ↓
ping 8.8.8.8 → Internet OK?
    ↓
nslookup google.com → DNS OK?
    ↓
tracert 8.8.8.8 → Identificar onde falha
```

---

## 🚫 Comandos a Evitar / Commands to Avoid

**NUNCA execute comandos destrutivos sem autorização:**

- `netsh interface ip delete` — Deleta configuração de interface
- `netsh wlan set hostednetwork` — Pode afetar rede sem fio
- `ipconfig /release` — Libera IP sem autorização pode causar perda de conectividade

---

## 📝 Licença / License

Projeto pessoal / laboratório. Uso educacional.
