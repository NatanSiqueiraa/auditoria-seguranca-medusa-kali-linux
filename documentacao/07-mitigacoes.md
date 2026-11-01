# 07 - Recomendações de Segurança e Mitigações

## 1. Introdução

Durante as atividades práticas deste projeto, foram realizadas auditorias controladas nos serviços FTP, HTTP e SMB da máquina Metasploitable 2.

Os testes permitiram identificar fragilidades relacionadas ao uso de senhas fracas, exposição de informações e ausência de mecanismos adequados de proteção contra tentativas automatizadas de autenticação.

Este documento apresenta recomendações para reduzir os riscos identificados.

## 2. Mitigações para o serviço FTP

### Problemas identificados

Durante a auditoria FTP, foi identificada uma credencial válida utilizando uma senha fraca:

- Usuário: msfadmin
- Senha: msfadmin

### Recomendações

- Utilizar senhas fortes e exclusivas.
- Desabilitar contas desnecessárias.
- Evitar autenticação anônima quando não for necessária.
- Restringir o acesso ao serviço por meio de firewall.
- Preferir SFTP ou FTPS em vez de FTP sem criptografia.
- Manter o serviço FTP atualizado.

## 3. Mitigações para autenticação Web (DVWA)

### Problemas identificados

Durante os testes com Hydra, foi possível realizar tentativas automatizadas de autenticação e identificar a senha da conta administrativa.

A aplicação estava configurada com nível de segurança Low.

### Recomendações

- Implementar limitação de tentativas de login.
- Aplicar bloqueio temporário após sucessivas falhas.
- Utilizar senhas fortes.
- Implementar CAPTCHA quando apropriado.
- Monitorar tentativas suspeitas de autenticação.
- Utilizar HTTPS.
- Configurar corretamente os cookies de sessão.
- Implementar proteções contra ataques de força bruta.

## 4. Mitigações para o serviço SMB

### Problemas identificados

A enumeração realizada com enum4linux demonstrou que o servidor permitia sessões anônimas e exposição de informações sobre usuários.

Além disso, o Password Spraying com Medusa identificou uma conta com credenciais fracas e acesso administrativo ao compartilhamento ADMIN$.

### Recomendações

- Desabilitar sessões anônimas quando não forem necessárias.
- Restringir a enumeração de usuários.
- Utilizar senhas fortes.
- Aplicar o princípio do menor privilégio.
- Restringir o acesso às portas TCP 139 e 445.
- Desabilitar compartilhamentos administrativos desnecessários.
- Manter o Samba atualizado.
- Monitorar tentativas de autenticação.

## 5. Mitigações gerais de infraestrutura

Além das recomendações específicas para cada serviço, algumas medidas gerais ajudam a melhorar a segurança do ambiente:

- Manter sistemas operacionais e serviços atualizados.
- Implementar regras de firewall.
- Utilizar segmentação de rede.
- Monitorar logs de autenticação.
- Realizar auditorias periódicas.
- Adotar políticas de senhas fortes.
- Remover serviços que não são utilizados.

## 6. Considerações finais

As atividades realizadas demonstraram como configurações inadequadas e credenciais fracas podem comprometer serviços de rede.

A combinação de reconhecimento, enumeração de usuários e testes controlados de autenticação permitiu identificar riscos importantes no ambiente analisado.

As medidas apresentadas neste documento contribuem para reduzir a superfície de ataque e melhorar a segurança dos serviços FTP, HTTP e SMB.

Todas as atividades foram realizadas em um laboratório isolado, utilizando máquinas virtuais destinadas a fins educacionais.