# 2. Configuração da rede

Após preparar as duas máquinas virtuais, foi necessário configurar uma rede para permitir a comunicação entre elas.

Para isso, utilizei o recurso **Host-only Adapter** do Oracle VirtualBox, permitindo que as máquinas virtuais se comuniquem em uma rede isolada.

### 2.1. Identificação dos endereços IP

Após iniciar as máquinas, utilizei o comando `ifconfig` para identificar os endereços IP.

Os resultados encontrados foram:

| Máquina virtual | Endereço IP |
|---|---|
| Kali Linux | 192.168.56.102 |
| Metasploitable 2 | 192.168.56.101 |

### 2.2. Teste de conectividade

Com os endereços IP identificados, realizei um teste de comunicação utilizando o comando `ping` no terminal do Kali Linux.

Comando utilizado:

```bash
ping -c 4 192.168.56.102
```

O teste foi bem-sucedido, demonstrando que o Kali Linux consegue alcançar o Metasploitable 2 pela rede configurada.

### 2.3. Resultado

A comunicação entre as máquinas virtuais foi estabelecida com sucesso.

Essa configuração possibilita a realização dos testes de segurança em um ambiente controlado e isolado.