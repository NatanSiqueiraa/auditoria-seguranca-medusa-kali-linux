# 06 - Enumeração de Usuários e Password Spraying SMB

## 1. Objetivo

Realizar uma auditoria controlada do serviço SMB utilizando enumeração de usuários e Password Spraying com as ferramentas enum4linux e Medusa.

## 2. Ambiente utilizado

- Sistema operacional: Kali Linux
- Máquina vulnerável: Metasploitable 2
- IP do alvo: 192.168.56.101
- Serviço: Samba/SMB
- Ferramentas: Nmap, enum4linux e Medusa

## 3. Reconhecimento do serviço

Foi executado:

```bash
nmap -p 139,445 -sV 192.168.56.101
```

Resultado:

- Porta 139/tcp: aberta.
- Porta 445/tcp: aberta.
- Serviço identificado: Samba.

## 4. Enumeração de usuários

Ferramenta utilizada: enum4linux.

Comando:

```bash
enum4linux -U 192.168.56.101
```

A ferramenta identificou 34 contas no sistema, incluindo:

- root
- msfadmin
- user
- service
- postgres
- ftp
- www-data

Também foi identificado que o servidor permite sessões anônimas utilizando usuário e senha vazios.

Esse comportamento possibilitou consultar informações de contas sem autenticação.

## 5. Preparação das wordlists

Arquivo `usuarios-smb.txt`:

```text
msfadmin
user
service
root
```

Senha utilizada no teste:

```text
msfadmin
```

## 6. Execução do Password Spraying

Ferramenta utilizada: Medusa.

Comando:

```bash
medusa -h 192.168.56.101 -U usuarios-smb.txt -p msfadmin -M smbnt -m GROUP:LOCAL -t 1 -T 1
```

O teste utilizou uma única senha contra quatro contas diferentes.

## 7. Resultado obtido

O Medusa identificou uma credencial válida:

- Usuário: msfadmin
- Senha: msfadmin
- Serviço: SMB
- Resultado: SUCCESS
- Acesso ao ADMIN$: permitido.

Os demais usuários testados não apresentaram credenciais válidas durante essa execução.

## 8. Análise de segurança

A auditoria identificou duas fragilidades principais:

1. Enumeração de usuários sem autenticação.
2. Utilização de uma senha fraca em uma conta com privilégios administrativos no SMB.

A combinação dessas condições aumenta o risco de comprometimento do serviço.

## 9. Recomendações de mitigação

- Desabilitar a enumeração anônima de usuários.
- Utilizar senhas fortes e exclusivas.
- Restringir o acesso às portas 139 e 445.
- Aplicar o princípio do menor privilégio.
- Monitorar tentativas repetidas de autenticação.
- Desabilitar contas desnecessárias.
- Manter o Samba atualizado.
- Restringir o acesso administrativo aos compartilhamentos.

## 10. Conclusão

A atividade demonstrou como informações obtidas por enumeração podem auxiliar uma auditoria de autenticação SMB.

O Password Spraying identificou uma credencial válida com privilégios administrativos, evidenciando o impacto de senhas fracas em serviços de rede.