# 🔐 Auditoria de Segurança com Medusa, Kali Linux e Metasploitable 2

Laboratório prático de auditoria de segurança com foco na identificação de vulnerabilidades em serviços de rede e mecanismos de autenticação.

O projeto explora técnicas de reconhecimento, enumeração de usuários, força bruta e Password Spraying, utilizando ferramentas como Nmap, Medusa, Hydra e enum4linux.

Todas as atividades foram realizadas em um ambiente virtual isolado, com finalidade exclusivamente educacional.

## 🎯 Objetivos

- Configurar um laboratório de cibersegurança utilizando máquinas virtuais.
- Realizar reconhecimento de serviços e portas com Nmap.
- Identificar serviços vulneráveis em uma máquina Metasploitable 2.
- Executar auditorias de autenticação FTP utilizando Medusa.
- Automatizar tentativas de autenticação HTTP utilizando Hydra.
- Realizar enumeração de usuários em serviços SMB.
- Executar testes controlados de Password Spraying.
- Identificar riscos e propor medidas de mitigação.

## 🛠️ Ferramentas utilizadas

| Ferramenta | Finalidade |
|---|---|
| Kali Linux | Sistema operacional utilizado nos testes |
| Metasploitable 2 | Máquina virtual vulnerável utilizada como alvo |
| VirtualBox | Virtualização do laboratório |
| Nmap | Reconhecimento de portas e serviços |
| Medusa | Auditoria de autenticação FTP e SMB |
| Hydra | Auditoria automatizada de autenticação HTTP |
| enum4linux | Enumeração de usuários e informações SMB |
| DVWA | Aplicação web vulnerável para testes de autenticação |

## 🌐 Ambiente de laboratório

O ambiente foi configurado utilizando uma rede Host-only no VirtualBox, permitindo a comunicação entre as máquinas virtuais sem expor os serviços vulneráveis diretamente à rede externa.

| Máquina | Endereço IP |
|---|---|
| Kali Linux | 192.168.56.102 |
| Metasploitable 2 | 192.168.56.101 |

## 🧪 Atividades realizadas

### 1. Preparação do ambiente
Instalação e configuração das máquinas virtuais Kali Linux e Metasploitable 2.

### 2. Configuração de rede
Criação de uma rede isolada Host-only e validação da comunicação entre as máquinas.

### 3. Reconhecimento com Nmap
Identificação de portas abertas, serviços e versões utilizando técnicas de varredura.

### 4. Auditoria FTP com Medusa
Criação de wordlists personalizadas e execução de testes controlados de autenticação FTP.

Resultado: identificação da credencial de laboratório `msfadmin:msfadmin`.

### 5. Auditoria Web com Hydra e DVWA
Análise de requisições HTTP, identificação de parâmetros de autenticação e automação de tentativas de login.

Resultado: identificação e validação da credencial de laboratório `admin:password`.

### 6. Enumeração e Password Spraying SMB
Utilização do enum4linux para identificar usuários e informações do serviço Samba.

Posteriormente, foi utilizado o Medusa para testar uma senha contra múltiplas contas.

Resultado: identificação da conta `msfadmin` com acesso administrativo ao compartilhamento ADMIN$.

### 7. Recomendações de segurança
Elaboração de medidas de mitigação para reduzir os riscos identificados durante as auditorias.

## 📁 Estrutura do projeto

```text
auditoria-seguranca-medusa-kali-linux/
│
├── README.md
│
└── documentacao/
    ├── 01-preparacao-ambiente.md
    ├── 02-configuracao-rede.md
    ├── 03-reconhecimento-nmap.md
    ├── 04-ataque-ftp.md
    ├── 05-ataque-dvwa.md
    ├── 06-password-spraying-smb.md
    └── 07-mitigacoes.md
```

## 📚 Documentação

Cada atividade possui um documento específico com explicações, ferramentas utilizadas, comandos executados e resultados obtidos.

A documentação está disponível no diretório `documentacao/`.

## 🛡️ Medidas de mitigação

Durante as atividades foram identificados riscos relacionados a:

- Senhas fracas e previsíveis.
- Exposição de informações de usuários.
- Ausência de mecanismos adequados contra tentativas automatizadas de autenticação.
- Privilégios administrativos excessivos.

Foram propostas medidas como políticas de senhas fortes, limitação de tentativas de login, restrição de acesso aos serviços, monitoramento de autenticação e aplicação do princípio do menor privilégio.

## ⚠️ Aviso legal

Este projeto possui finalidade exclusivamente educacional.

Todos os testes foram realizados em um ambiente virtual próprio e isolado, utilizando máquinas intencionalmente vulneráveis.

Não utilize as técnicas apresentadas contra sistemas, redes ou serviços sem autorização expressa.

As credenciais apresentadas pertencem exclusivamente ao laboratório e não devem ser reutilizadas em ambientes reais.

## 👨‍💻 Autor

Projeto desenvolvido como atividade prática de estudos em Cibersegurança, com foco em reconhecimento de redes, auditoria de autenticação e análise de vulnerabilidades.