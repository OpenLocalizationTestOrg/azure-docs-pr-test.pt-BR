---
title: "par de chave aaaCreate um SSH para máquinas virtuais do Linux no Azure | Microsoft Docs"
description: "Crie um par de chaves SSH pública e privada para VMs Linux do Azure com segurança."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: 
ms.assetid: 34ae9482-da3e-4b2d-9d0d-9d672aa42498
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/08/2017
ms.author: rasquill
ms.openlocfilehash: c4c7cec77c9b48295f2a28c8179b30a4dc38a555
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-ssh-public-and-private-key-pair-for-linux-vms"></a>Criar um par de chaves SSH pública e privada para VMs Linux

Este artigo mostra como toogenerate um protocolo versão 2 RSA pública e privada chave SSH arquivo toouse par com VMs do Linux.  Com um par de chaves de SSH, você pode criar máquinas virtuais no Azure que padrão toousing as chaves de SSH para a autenticação, eliminando a necessidade de saudação para senhas toolog em.  As senhas podem ser adivinhadas e abra suas VMs backup toorelentless tooguess de tentativas de força bruta sua senha. Máquinas virtuais criadas com modelos do Azure ou hello `azure-cli` pode incluir a sua chave pública SSH como parte da implantação hello, removendo a etapa de configuração de implantação de postagem de desabilitar os logons de senha para o SSH.

## <a name="quick-commands"></a>Comandos rápidos

Execute Olá comandos a seguir de um shell Bash, substituindo os exemplos de saudação com suas próprias opções.

O arquivo de chave pública SSH é criado por padrão em `~/.ssh/id_rsa.pub`. Quando solicitado usando Olá comando a seguir, você deve criar um toosecure "senha" sua chave privada. (Olá senha é que uma senha usada tooencrypt sua chave privada).

```bash
ssh-keygen -t rsa -b 2048 
```

Adicionar chave Olá recém-criado muito`ssh-agent`:

```bash
ssh-add ~/.ssh/id_rsa
```

> [!IMPORTANT] 
> Olá acima comandos funcionam em sistemas operacionais de Linux de quase todas as distribuições, mas não necessariamente funcionam em contêineres, como o ambiente de saudação pode ser restringido radicalmente. 

## <a name="detailed-walkthrough"></a>Passo a passo detalhado

Usar as chaves públicas e privadas SSH é Olá toolog de maneira mais fácil em servidores Linux de tooyour. [Criptografia de chave pública](https://en.wikipedia.org/wiki/Public-key_cryptography) fornece um toolog de maneira muito mais seguro em tooyour Linux ou BSD VM no Azure que senhas, que podem ser forçado bruta muito mais facilmente.

> [!IMPORTANT]
> Sua chave pública pode ser compartilhada com qualquer pessoa; mas apenas você (ou sua infraestrutura de segurança local) possui sua chave privada.  a chave privada SSH Olá deve ter uma [senha segura muito](https://www.xkcd.com/936/) (fonte:[xkcd.com](https://xkcd.com)) toosafeguard-lo.  Esta senha é a chave SSH tooaccess apenas Olá privada e **não é** senha de conta de usuário de saudação.  Quando você adiciona uma chave SSH tooyour senha, ele criptografa chave privada de saudação usando AES de 128 bits, para que hello chave privada é inútil sem Olá senha toodecrypt-lo.  Se um invasor roubar sua chave privada e que a chave não tem uma senha, seria capaz de toouse ou privada da chave toolog em servidores tooany que tem uma chave pública correspondente de saudação.  Se uma chave privada for protegida por senha, ela não poderá ser usada por esse invasor, o que é uma camada adicional de segurança para sua infraestrutura no Azure.

Este artigo cria o protocolo SSH versão 2 RSA públicos e privados arquivos de chave, que são recomendados para implantações de saudação Gerenciador de recursos.  *SSH-rsa* as chaves são necessárias Olá [portal](https://portal.azure.com) para clássico e implantações do Gerenciador de recursos.

## <a name="disable-ssh-passwords-by-using-ssh-keys"></a>Desabilitar senhas SSH usando chaves SSH

O Azure requer chaves públicas e privadas de pelo menos 2048 bits em formato ssh-rsa. Olá toocreate chaves use `ssh-keygen`, que faz uma série de perguntas e, em seguida, grava uma chave privada e uma chave pública correspondente. Quando uma VM do Azure é criada, a chave pública Olá é copiado muito`~/.ssh/authorized_keys`.  As chaves de SSH no `~/.ssh/authorized_keys` são usados toochallenge Olá cliente toomatch Olá chave privada correspondente em uma conexão de logon SSH.  Quando uma VM do Linux do Azure é criada usando as chaves de SSH para autenticação, o Azure configura Olá SSHD server toonot permitir logons de senha, somente as chaves de SSH.  Portanto, ao criar VMs do Linux do Azure com as chaves de SSH, pode ajudam na implantação de VM Olá segura e economizar etapa de configuração de pós-implantação típica de saudação de desabilitar as senhas no arquivo de configuração sshd_config hello.

## <a name="using-ssh-keygen"></a>Usando ssh-keygen

Este comando cria uma senha protegida (criptografado) par de chaves de SSH utilizando RSA de 2048 bits e é comentado tooeasily identificá-lo.  

SSH chaves por padrão são mantido em Olá `~/.ssh` directory.  Se você não tiver um `~/.ssh` diretório, Olá `ssh-keygen` comando cria para você com hello permissões corretas.

```bash
ssh-keygen \
-t rsa \
-b 2048 
```

*Comando explicado*

`ssh-keygen`= Olá programa usado toocreate Olá chaves

`-t rsa`= tipo de chave toocreate Olá RSA formato [wikipedia](https://en.wikipedia.org/wiki/RSA_(cryptosystem)

`-b 2048`= bits da chave de saudação


## <a name="classic-portal-and-x509-certs"></a>Portal clássico e certificados x.509

Se você estiver usando hello Azure [portal clássico](https://manage.windowsazure.com/), ele requer certificados x. 509 para chaves SSH hello.  Outros tipos de chaves públicas SSH não são permitidos. Elas *devem* ser certificados x.509.

toocreate um certificado x. 509 de sua chave privada do SSH-RSA existente:

```bash
openssl req -x509 \
-key ~/.ssh/id_rsa \
-nodes \
-days 365 \
-newkey rsa:2048 \
-out ~/.ssh/id_rsa.pem
```

## <a name="classic-deploy-using-asm"></a>Implantação clássica usando `asm`

Se você estiver usando clássico Olá implantar modelo (CLI de gerenciamento de serviço do Azure `asm`), você pode usar uma chave pública SSH-RSA ou um RFC4716 formatado chave em um **. PEM** contêiner.  chave pública SSH-RSA de saudação é o que foi criado anteriormente neste artigo usando `ssh-keygen`.

toocreate um RFC4716 formatado chave de uma chave pública de SSH existente:

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a>Exemplo de ssh-keygen

```bash
ssh-keygen -t rsa -b 2048 -C "ahmet@myserver"
Generating public/private rsa key pair.
Enter file in which toosave hello key (/home/ahmet/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/ahmet/.ssh/id_rsa.
Your public key has been saved in /home/ahmet/.ssh/id_rsa.pub.
hello key fingerprint is:
14:a3:cb:3e:78:ad:25:cc:55:e9:0c:08:e5:d1:a9:08 ahmet@myserver
hello keys randomart image is:
+--[ RSA 2048]----+
|        o o. .   |
|      E. = .o    |
|      ..o...     |
|     . o....     |
|      o S =      |
|     . + O       |
|      + = =      |
|       o +       |
|        .        |
+-----------------+
```

Arquivos de chave salvos:

`Enter file in which toosave hello key (/home/ahmet/.ssh/id_rsa): ~/.ssh/id_rsa`

nome do par de chaves Olá para este artigo.  Ter um par de chaves denominado **id_rsa** saudação padrão e algumas ferramentas podem esperar Olá **id_rsa** nome de arquivo de chave privada para ter um é uma boa ideia. diretório de saudação `~/.ssh/` é saudação padrão local para os pares de chave SSH e arquivo de configuração SSH hello.  Se não for especificado com um caminho completo, `ssh-keygen` será criar chaves Olá no diretório de trabalho atual hello, Olá não padrão `~/.ssh`.

Uma lista de saudação `~/.ssh` directory.

```bash
ls -al ~/.ssh
-rw------- 1 ahmet staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 ahmet staff   410 Aug 25 18:04 rsa.pub
```

Senha da chave:

`Enter passphrase (empty for no passphrase):`

`ssh-keygen`refere-se a chave privada do hello tooa senha usada tooencrypt como "senha".  É *fortemente* recomendado tooadd pares de chave de tooyour uma frase secreta. Sem uma frase secreta proteção Olá chave privada, qualquer pessoa com o arquivo de chave Olá pode usá-lo toolog no servidor tooany que tem uma chave pública correspondente hello. Adicionar uma frase secreta oferece mais proteção caso alguém é capaz de toogain acesso tooyour arquivo de chave privada, fornecendo chaves de saudação do tempo toochange usado tooauthenticate você.

## <a name="using-ssh-agent-toostore-your-private-key-password"></a>Usando o ssh agente toostore sua senha da chave privada

senha do arquivo tooavoid digitar sua chave privada com cada logon SSH, você pode usar `ssh-agent` toocache sua senha do arquivo de chave privada. Se você estiver usando um Mac, Olá OSX chaves armazena com segurança senhas de chave particular hello quando você chamar `ssh-agent`.

Verificar e usar `ssh-agent` e `ssh-add` tooinform Olá sistema SSH sobre arquivos de chave Olá para que a senha hello, não será necessário toobe usado interativamente.

```bash
eval "$(ssh-agent -s)"
```

Agora adicione chave privada Olá muito`ssh-agent` usando o comando Olá `ssh-add`.

```bash
ssh-add ~/.ssh/id_rsa
```

senha da chave privada Olá agora é armazenada no `ssh-agent`.

## <a name="using-ssh-copy-id-tooinstall-hello-new-key"></a>Usando `ssh-copy-id` nova chave de saudação tooinstall
Se você já tiver criado uma máquina virtual, você pode instalar Olá novo SSH pública chave tooyour VM do Linux com hello comando a seguir, substituindo o nome de usuário do hello VM e o endereço do servidor de saudação com seus próprios valores:

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a>Criar e configurar um arquivo de configuração do SSH

Ele é um toocreate de prática recomendada e configurar um `~/.ssh/config` toospeed arquivo backup logons e para otimizar o comportamento do seu cliente SSH.

saudação de exemplo a seguir mostra uma configuração padrão.

### <a name="create-hello-file"></a>Criar arquivo hello

```bash
touch ~/.ssh/config
```

### <a name="edit-hello-file-tooadd-hello-new-ssh-configuration"></a>Edite saudação arquivo tooadd Olá nova configuração de SSH:

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a>Exemplo de arquivo `~/.ssh/config`:

```bash
# Azure Keys
Host fedora22
  Hostname 102.160.203.241
  User ahmet
# ./Azure Keys
# Default Settings
Host *
  PubkeyAuthentication=yes
  IdentitiesOnly=yes
  ServerAliveInterval=60
  ServerAliveCountMax=30
  ControlMaster auto
  ControlPath ~/.ssh/SSHConnections/ssh-%r@%h:%p
  ControlPersist 4h
  IdentityFile ~/.ssh/id_rsa
```

Essa configuração SSH fornece você seções para cada servidor tooenable cada toohave seu próprio par de chaves dedicado. Olá configurações padrão (`Host *`) são para os hosts que não corresponde a nenhum dos hosts Olá específicos acima no arquivo de configuração de saudação.

### <a name="config-file-explained"></a>Arquivo de configuração explicado

`Host`= nome de saudação do host hello está sendo chamado em Olá terminal.  `ssh fedora22`informa `SSH` toouse valores de saudação no bloco de configurações de saudação rotulada `Host fedora22` Observação: Host pode ser qualquer rótulo lógicas para seu uso e não representam o nome de host real de qualquer servidor de saudação.

`Hostname 102.160.203.241`= endereço IP de saudação ou nome DNS para o servidor de saudação que está sendo acessado.

`User ahmet`= Olá toouse de conta de usuário remoto ao fazer logon no servidor de toohello.

`PubKeyAuthentication yes`= informa SSH deseja toouse um toolog de chave SSH.

`IdentityFile /home/ahmet/.ssh/id_id_rsa`= a chave privada SSH hello e toouse correspondente de chave pública para autenticação.

## <a name="ssh-into-linux-without-a-password"></a>SSH no Linux sem uma senha

Agora que você tem um par de chave SSH e um arquivo de configuração de SSH configurado, será possível toolog em tooyour VM Linux rapidamente e com segurança. Olá primeira vez que você efetuar logon no servidor de tooa usando um prompts de comando Olá chave SSH você para senha Olá para esse arquivo de chave.

```bash
ssh fedora22
```

### <a name="command-explained"></a>Comando explicado

Quando `ssh fedora22` é executado SSH primeiro localiza e carrega as configurações de saudação `Host fedora22` bloco e, em seguida, carrega todos os Olá restantes Configur Olá último bloco, `Host *`.

## <a name="next-steps"></a>Próximas etapas

Próximo backup é toocreate VMs do Linux do Azure usando Olá novo Gerenciador de virtualização.  Máquinas virtuais do Azure que são criados com uma chave pública SSH como logon Olá são mais seguro que máquinas virtuais criadas com o método de logon padrão hello, as senhas.  As VMs do Azure criadas com chaves SSH são por padrão configuradas com senhas desabilitadas, evitando tentativas de adivinhação por força bruta. Se você precisa de mais ajuda na criação de par de chaves de SSH ou exige certificados adicionais, por exemplo, para uso com o portal clássico do hello, consulte [detalhadas certificados e pares de chave SSH do etapas toocreate](create-ssh-keys-detailed.md).

* [Criar uma VM do Linux segura usando um modelo do Azure](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Criar uma VM do Linux segura usando Olá portal do Azure](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Criar uma VM do Linux segura usando Olá CLI do Azure](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
