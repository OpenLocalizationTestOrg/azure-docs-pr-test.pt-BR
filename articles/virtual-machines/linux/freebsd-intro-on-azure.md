---
title: tooFreeBSD aaaIntroduction no Azure | Microsoft Docs
description: "Saiba como usar máquinas virtuais FreeBSD no Azure"
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 32b87a5f-d024-4da0-8bf0-77e233d1422b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: kyliel
ms.openlocfilehash: 43ba7a70ed21e7fb8b331f4a26db0426e098c4aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toofreebsd-on-azure"></a>Introdução tooFreeBSD no Azure
Este tópico fornece uma visão geral da execução da máquina virtual FreeBSD no Azure.

## <a name="overview"></a>Visão geral
FreeBSD do Microsoft Azure é que um sistema operacional de computador avançado usado plataformas incorporadas, áreas de trabalho e servidores modernos toopower.

Microsoft Corporation está disponibilizando imagens de FreeBSD no Azure com hello [agente convidado da VM do Azure](https://github.com/Azure/WALinuxAgent/) pré-configurado. Atualmente, hello FreeBSD versões a seguir são oferecidas como imagens pela Microsoft:

- FreeBSD 10.3-RELEASE
- FreeBSD 11.0-RELEASE

agente Olá é responsável pela comunicação entre hello FreeBSD VM e Olá malha do Azure para operações como provisionamento Olá VM no primeiro uso (nome de usuário, senha ou chave SSH, nome de host, etc.) e a funcionalidade de habilitação para extensões VM seletivas.

Para versões futuras do FreeBSD, estratégia Olá é toostay atual e disponibilize Olá versões mais recentes logo depois que forem publicados pela equipe de engenharia Olá FreeBSD versão.

## <a name="deploying-a-freebsd-virtual-machine"></a>Implantando uma máquina virtual FreeBSD
Implantar uma máquina virtual de FreeBSD é um processo simples usando uma imagem de saudação do Azure Marketplace de saudação portal do Azure:

- [10.3 FreeBSD em hello Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd103/)
- [11.0 FreeBSD em hello Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/)

### <a name="create-a-freebsd-vm-through-azure-cli-20-on-freebsd"></a>Criar uma VM do FreeBSD por meio da CLI do Azure 2.0 no FreeBSD
Primeiro é necessário tooinstall [2.0 do CLI do Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) Embora o comando a seguir em um computador FreeBSD.

```bash 
curl -L https://aka.ms/InstallAzureCli | bash
```

Se bash não estiver instalado no seu computador FreeBSD, execute o seguinte comando antes da instalação de saudação. 

```bash
sudo pkg install bash
```

Se o python não estiver instalado no seu computador FreeBSD, execute o seguinte comandos antes da instalação de saudação. 

```bash
sudo pkg install python35
cd /usr/local/bin 
sudo rm /usr/local/bin/python 
sudo ln -s /usr/local/bin/python3.5 /usr/local/bin/python
```

Durante a instalação do hello, você será solicitado `Modify profile tooupdate your $PATH and enable shell/tab completion now? (Y/n)`. Se você responder `y` e digite `/etc/rc.conf` como `a path tooan rc file tooupdate`, você poderá atender problema Olá `ERROR: [Errno 13] Permission denied`. tooresolve esse problema, você deve conceder o direito toocurrent usuário gravação Olá arquivo hello `etc/rc.conf`.

Agora você pode fazer logon no Azure e criar sua VM do FreeBSD. Abaixo está um exemplo toocreate uma VM do FreeBSD 11.0. Você também pode adicionar o parâmetro hello `--public-ip-address-dns-name` com o nome DNS exclusivo para um IP público recém-criado. 

```azurecli
az login 
az group create --name myResourceGroup --location eastus
az vm create --name myFreeBSD11 \
    --resource-group myResourceGroup \
    --image MicrosoftOSTC:FreeBSD:11.0:latest \
    --admin-username azureuser \
    --generate-ssh-keys
```

Em seguida, você pode fazer logon no tooyour FreeBSD VM pelo endereço de ip de saudação impresso na saída de saudação do acima de implantação. 

```bash
ssh azureuser@xx.xx.xx.xx -i /etc/ssh/ssh_host_rsa_key
```   

## <a name="vm-extensions-for-freebsd"></a>Extensões de VM para FreeBSD
Os itens a seguir têm suporte de extensões de VM no FreeBSD.

### <a name="vmaccess"></a>VMAccess
Olá [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) extensão pode:

* Redefina a senha de saudação do usuário original de sudo hello.
* Crie um novo usuário sudo com senha Olá especificada.
* Defina a chave de host público Olá com chave Olá fornecido.
* Redefina a chave de host público de saudação fornecido durante o provisionamento se não for fornecido a chave de saudação do host de VM.
* Abra a porta SSH de saudação (22) e restauração Olá sshd_config se reset_ssh for definido tootrue.
* Remova usuário existente hello.
* Verificar os discos.
* Reparar o disco adicionado.

### <a name="customscript"></a>CustomScript
Olá [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) extensão pode:

* Se fornecido, baixe scripts personalizada de saudação do armazenamento do Azure ou armazenamento público externo (por exemplo, GitHub).
* Execute o script de ponto de entrada hello.
* Oferecer suporte ao comando embutido.
* Converter automaticamente o estilo newline do Windows em scripts de Shell e Python.
* Remover automaticamente BOM em scripts de Shell e Python.
* Proteger dados confidenciais em CommandToExecute.

> [!NOTE]
> A VM do FreeBSD só oferece suporte ao CustomScript versão 1. x até o momento.  

## <a name="authentication-user-names-passwords-and-ssh-keys"></a>Autenticação: nomes de usuário, senhas e chaves SSH
Quando você estiver criando uma máquina virtual de FreeBSD usando Olá portal do Azure, você deve fornecer um nome de usuário, senha ou chave pública SSH.
Nomes de usuário para implantar uma máquina virtual de FreeBSD no Azure não devem corresponder aos nomes das contas do sistema (UID < 100) já está presente na máquina virtual de saudação ("raiz", por exemplo).
Atualmente, há suporte para apenas Olá RSA chave SSH. Uma chave SSH multilinha deve começar com `---- BEGIN SSH2 PUBLIC KEY ----` e terminar com `---- END SSH2 PUBLIC KEY ----`.

## <a name="obtaining-superuser-privileges"></a>Obtendo privilégios de superusuário
conta de usuário de saudação que é especificada durante a implantação de instância de máquina virtual no Azure é uma conta privilegiada. Olá pacote do sudo foi instalado no hello publicado FreeBSD imagem.
Depois que você está conectado a esta conta de usuário, você pode executar comandos como raiz usando a sintaxe do comando hello.

```
$ sudo <COMMAND>
```

Opcionalmente, é possível obter um shell root usando `sudo -s`.

## <a name="known-issues"></a>Problemas conhecidos
Olá [agente convidado da VM do Azure](https://github.com/Azure/WALinuxAgent/) versão 2.2.2 tem um [problema conhecido] (https://github.com/Azure/WALinuxAgent/pull/517) que causa falha de provisionamento de saudação para FreeBSD VM no Azure. Olá correção foi capturada por [agente convidado da VM do Azure](https://github.com/Azure/WALinuxAgent/) versão 2.2.3 e versões posteriores. 

## <a name="next-steps"></a>Próximas etapas
* Vá muito[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) toocreate uma VM FreeBSD.
* Se você quiser toobring seu próprios tooAzure FreeBSD, consulte muito[criar e carregar um VHD FreeBSD tooAzure](classic/freebsd-create-upload-vhd.md).
