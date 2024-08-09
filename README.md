
# 📍 Criando um servidor usando um notebook antigo. 💻 

Recentemente encontrei esse HP Mini 1104 perdido na empresa, e decidimos dar um uso para ele e transforma-lo em um servidor de arquivos, inicialmente fizemos um upgrade(colocamos 2gb de memória RAM e 1tb de HD) e colocamos o sistema operacional Linux Mint, que é recomendado para notebooks fracos.




## Instalação Linux Mint

 - [Instalando Linux Mint - Curso Linux #04](https://youtu.be/ZhLjvy23rrs)
# Comandos Usados

### Comandos de instalação

``` Para descobrir ip do notebook
ifconfig
```
``` Atualizar sistema
sudo apt-get update
```
``` Instalar o Samba
sudo apt install samba
```
``` Instalar o OpenSSH
sudo apt install openssh-server
```
``` Instalar o ACL
sudo apt install acl
```
``` Criar pasta do Sistema de Arquivos
sudo mkdir /var/arquivos
```




## • Configurando o Samba

```Configurações Iniciais
sudo addgroup professores 
sudo adduser pedro
sudo adduser pedro --ingroup professores
```

```Para conferir as Pastas e os Usuários
ls -l /var/
sudo systemctl restart smbd
```

```Colocar o Grupo para conseguir mexer na pasta
sudo chgrp professores /var/conteúdo 
sudo chmod 770 /var/conteúdo/
```

```Mudar as Configurações da pasta
cd /etc/samba/
sudo cp smb.conf smb.conf.bkp
sudo nano smb.conf
```

```Exemplo de Permissões
[conteudo]
        path = /var/conteudo
        valid users = @professores
        write list = @professores
        browseable = yes

Ctrl + O        Enter       Ctrl + X
```

```Reiniciar sistema e colocar senha no Usuário
sudo systemctl restart smbd
sudo smbpasswd -a pedro
```

#### Para testar, basta colocar no Executar:
\\\IP_SERVIDOR
## • Configurando o OpenSSH

``` Para verificar status active (running)
sudo system status ssh
```

#### Para testar, basta colocar no CMD:
ssh pedro@IP_SERVIDOR
## • Configurando o ACL

``` Fazer com que ambos os grupos consigam acessar o arquivos
sudo setfacl -m g:administrativo:rwx /var/arquivos
sudo setfacl -m g:professores:rwx /var/arquivos
```

``` Verificar as ACLs
getfacl /var/arquivos
```

# Imagem do Sistema
![Imagem do Sistema](https://github.com/pedro-cursino/serverLinuxComands/blob/main/Sistema.png?raw=true)
