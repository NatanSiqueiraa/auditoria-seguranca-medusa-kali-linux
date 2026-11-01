# 04 — Auditoria de credenciais FTP com Medusa

## 1. Objetivo

Realizar uma auditoria controlada de credenciais no serviço FTP da máquina Metasploitable 2, utilizando a ferramenta Medusa e wordlists personalizadas.

O objetivo foi compreender como ataques de força bruta podem identificar credenciais fracas e demonstrar a importância de políticas de senhas seguras.

## 2. Ambiente utilizado

| Máquina | Endereço IP |
|---|---|
| Kali Linux (atacante) | 192.168.56.102 |
| Metasploitable 2 (alvo) | 192.168.56.101 |

Serviço analisado: FTP (porta 21).

Ferramenta: Medusa 2.3.

## 3. Preparação das wordlists

Foram criados dois arquivos para realizar os testes:

**usuarios.txt**
```text
admin
usuario
teste
msfadmin
```

**senhas.txt**
```text
123456
admin123
senha123
msfadmin
```

As wordlists foram armazenadas no diretório:

```bash
~/laboratorio-medusa/wordlists/
```

## 4. Validação inicial

Antes de utilizar as wordlists, foi realizado um teste individual com uma credencial conhecida:

```bash
medusa -h 192.168.56.101 -u msfadmin -p msfadmin -M ftp
```

Resultado:

```text
ACCOUNT FOUND: [ftp] Host: 192.168.56.101 User: msfadmin Password: msfadmin [SUCCESS]
```

A autenticação foi realizada com sucesso.

## 5. Auditoria utilizando wordlists

Após a validação inicial, foi executado o teste com as listas de usuários e senhas:

```bash
medusa -h 192.168.56.101 -U usuarios.txt -P senhas.txt -M ftp
```

O Medusa testou as combinações disponíveis nas duas wordlists.

Quantidade de combinações:

- 4 usuários.
- 4 senhas.
- 16 combinações testadas.

## 6. Resultado

Durante a execução, foi identificada uma credencial válida:

```text
ACCOUNT FOUND: [ftp] Host: 192.168.56.101 User: msfadmin Password: msfadmin [SUCCESS]
```

A combinação encontrada foi:

| Usuário | Senha | Resultado |
|---|---|---|
| msfadmin | msfadmin | Sucesso |

As demais combinações não apresentaram autenticação bem-sucedida.

## 7. Análise de segurança

O teste demonstrou que a utilização de credenciais padrão e senhas fracas representa um risco para a segurança dos serviços.

Um invasor com acesso à rede poderia tentar diferentes combinações até encontrar uma credencial válida.

## 8. Recomendações de mitigação

Para reduzir esse tipo de risco, recomenda-se:

- Substituir credenciais padrão.
- Utilizar senhas fortes e exclusivas.
- Implementar limitação de tentativas de autenticação.
- Monitorar logs de acesso.
- Restringir o acesso ao serviço FTP.
- Preferir SFTP ou outros protocolos seguros, quando aplicável.

## 9. Conclusão

A atividade permitiu compreender o funcionamento do Medusa, a utilização de wordlists e o processo de auditoria de credenciais em serviços FTP.

O laboratório demonstrou, na prática, como credenciais padrão podem comprometer a segurança de um serviço.