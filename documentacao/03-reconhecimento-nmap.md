# 3. Reconhecimento com Nmap

## 3.1. Objetivo

Nesta etapa, foi realizado um reconhecimento da máquina Metasploitable 2 utilizando a ferramenta Nmap.

O objetivo foi identificar portas TCP abertas, serviços disponíveis e suas respectivas versões, permitindo compreender a superfície de exposição da máquina vulnerável.

## 3.2. Ferramenta utilizada

**Nmap:** ferramenta de código aberto utilizada para descoberta de dispositivos, identificação de portas abertas e reconhecimento de serviços em redes.

## 3.3. Comando utilizado

```bash
nmap -sV 192.168.56.101
```

O parâmetro `-sV` permite identificar os serviços e tentar descobrir suas versões.

## 3.4. Resultados encontrados

Durante o reconhecimento, foram identificadas 23 portas TCP abertas.

Entre os serviços encontrados, destacam-se:

| Porta | Serviço | Versão |
|---|---|---|
| 21 | FTP | vsftpd 2.3.4 |
| 22 | SSH | OpenSSH 4.7p1 |
| 23 | Telnet | Linux telnetd |
| 80 | HTTP | Apache 2.2.8 |
| 139 | SMB | Samba |
| 445 | SMB | Samba |
| 2121 | FTP | ProFTPD 1.3.1 |
| 3306 | MySQL | 5.0.51a |
| 5432 | PostgreSQL | 8.3 |

Além dessas, foram identificadas outras portas abertas, incluindo serviços DNS, RPC, NFS, VNC e IRC.

## 3.5. Análise dos resultados

Os resultados demonstraram que a máquina possui diversos serviços de rede ativos.

Para as próximas etapas do projeto, foram selecionados três serviços principais:

- **FTP (porta 21):** será utilizado para estudar tentativas automatizadas de autenticação com Medusa.
- **HTTP (porta 80):** será utilizado para trabalhar com a aplicação DVWA.
- **SMB (portas 139 e 445):** será utilizado para estudar enumeração de usuários e segurança de autenticação.

A identificação de versões antigas de serviços também demonstra a importância de manter softwares atualizados e aplicar correções de segurança.

## 3.6. Conclusão

O reconhecimento foi realizado com sucesso, permitindo identificar os serviços disponíveis na máquina Metasploitable 2.

Essas informações serão utilizadas como base para os testes de segurança das próximas etapas.

**Ferramenta:** Nmap  
**Resultado:** 23 portas TCP abertas identificadas.