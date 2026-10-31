# 1. Preparação do ambiente

Para iniciar o projeto, foram criadas duas máquinas virtuais utilizando o Oracle VirtualBox.

A primeira máquina utiliza a distribuição **Kali Linux**, que será utilizada para executar ferramentas de reconhecimento e auditoria de segurança.

A segunda máquina utiliza o **Metasploitable 2**, um ambiente Linux propositalmente vulnerável, desenvolvido para fins educacionais e utilizado como alvo dos testes de segurança.

### 1.1. Identificação dos endereços IP

Após iniciar as máquinas virtuais, utilizei o comando `ifconfig` para identificar os endereços IP de cada máquina.

Os resultados encontrados foram:

| Máquina virtual | Sistema operacional | Endereço IP |
|---|---|---|
| Máquina de auditoria | Kali Linux | 192.168.56.101 |
| Máquina vulnerável | Metasploitable 2 | 192.168.56.102 |

### 1.2. Validação da comunicação

Após identificar os endereços IP, realizei um teste de conectividade utilizando o comando `ping` a partir do Kali Linux.

O teste foi bem-sucedido, confirmando que as duas máquinas conseguem se comunicar pela rede configurada no VirtualBox.

Essa configuração permite realizar os testes de segurança em um ambiente controlado e isolado.