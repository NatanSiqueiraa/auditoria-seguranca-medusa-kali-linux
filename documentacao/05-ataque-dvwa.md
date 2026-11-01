# 05 - Auditoria de Autenticação Web com Hydra e DVWA

## 1. Objetivo

Realizar uma auditoria controlada de autenticação web utilizando o Hydra contra a aplicação DVWA (Damn Vulnerable Web Application), identificando possíveis fragilidades no mecanismo de autenticação.

## 2. Ambiente utilizado

- Sistema operacional: Kali Linux
- Máquina vulnerável: Metasploitable 2
- Aplicação: DVWA
- Ferramenta: Hydra 9.7
- IP do alvo: 192.168.56.101
- Nível de segurança do DVWA: Low

## 3. Análise da requisição HTTP

Durante a análise da página Brute Force, utilizando as ferramentas de desenvolvedor do Firefox, foram identificadas as seguintes características:

- Método HTTP: GET
- Endpoint: `/dvwa/vulnerabilities/brute/`
- Parâmetros:
  - `username`
  - `password`
  - `Login`

Mensagem retornada para autenticação inválida:

`Username and/or password incorrect`

Mensagem retornada para autenticação válida:

`Welcome to the password protected area admin`

Também foi identificado que a aplicação utiliza um cookie de sessão PHPSESSID.

## 4. Wordlist utilizada

Arquivo: `senhas-dvwa.txt`

Conteúdo:

```text
123456
admin123
senha123
password
```

## 5. Execução do Hydra

Foi utilizada a ferramenta Hydra com o módulo `http-get-form`.

Comando utilizado (com o cookie de sessão armazenado em variável):

```bash
hydra -l admin -P senhas-dvwa.txt -t 1 -f -V 192.168.56.101 http-get-form "/dvwa/vulnerabilities/brute/:username=^USER^&password=^PASS^&Login=Login:H=Cookie\: PHPSESSID=${PHPSESSID}; security=low:F=Username and/or password incorrect"
```

### Parâmetros utilizados

- `-l admin`: usuário que será testado.
- `-P`: arquivo contendo as senhas.
- `-t 1`: realiza uma tentativa por vez.
- `-f`: interrompe o teste após encontrar uma credencial válida.
- `-V`: exibe as tentativas realizadas.
- `http-get-form`: módulo utilizado para testar formulários HTTP GET.
- `H=`: adiciona o cookie de sessão na requisição.
- `F=`: identifica a mensagem de autenticação inválida.

**Observação:** o cookie de sessão foi utilizado localmente e não deve ser publicado na documentação ou no repositório.

## 6. Resultado obtido

O Hydra realizou quatro tentativas de autenticação.

Resultado:

| Usuário | Senha | Resultado |
|---|---|---|
| admin | 123456 | Inválida |
| admin | admin123 | Inválida |
| admin | senha123 | Inválida |
| admin | password | Válida |

Credencial identificada:

- Usuário: `admin`
- Senha: `password`

A credencial encontrada também foi testada manualmente na aplicação DVWA, confirmando o resultado.

## 7. Análise de segurança

O teste demonstrou que a aplicação permite múltiplas tentativas de autenticação sem mecanismos suficientes de proteção contra ataques automatizados.

O uso de uma senha fraca e previsível, associado à ausência de controles adequados, facilita a descoberta de credenciais.

## 8. Recomendações de mitigação

- Utilizar senhas fortes e exclusivas.
- Implementar limitação de tentativas de autenticação.
- Adotar mecanismos de bloqueio temporário após várias falhas.
- Implementar CAPTCHA quando apropriado.
- Monitorar tentativas repetidas de login.
- Utilizar HTTPS para proteger a comunicação.
- Configurar cookies com atributos de segurança adequados.

## 9. Conclusão

A atividade demonstrou, em ambiente controlado, como o Hydra pode ser utilizado para auditar mecanismos de autenticação web.

O exercício permitiu compreender a importância da análise de requisições HTTP, do gerenciamento de sessões e da implementação de mecanismos de proteção contra tentativas automatizadas de autenticação.

