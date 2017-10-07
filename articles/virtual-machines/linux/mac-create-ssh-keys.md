---
title: aaaCreate e use um SSH par de chaves para VMs do Linux no Azure | Microsoft Docs
description: "Como toocreate e use um par de chamadas chaves público e privado SSH para VMs do Linux no Azure tooimprove Olá segurança saudação do processo de autenticação."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 34ae9482-da3e-4b2d-9d0d-9d672aa42498
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/14/2017
ms.author: iainfou
ms.openlocfilehash: 7fb94841d34d5bc006f3134adf91102ddce5f174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-use-an-ssh-public-and-private-key-pair-for-linux-vms-in-azure"></a>Como toocreate e usar uma chave pública e privada do SSH par para VMs do Linux no Azure
Com um par de chaves de SSH (secure shell), você pode criar máquinas virtuais (VMs) no Azure que usam as chaves de SSH para autenticação, eliminando a necessidade de saudação para senhas toolog em. Este artigo mostra como tooquickly gerar e usar um par de arquivo de chave pública e privada SSH versão 2 do protocolo RSA para VMs do Linux. Para obter mais etapas e exemplos adicionais, consulte [detalhadas certificados e pares de chave SSH do etapas toocreate](create-ssh-keys-detailed.md).

## <a name="create-an-ssh-key-pair"></a>Criar um par de chaves SSH
Saudação de uso `ssh-keygen` arquivos de comando toocreate SSH públicos e privados chave por padrão criado no hello `~/.ssh` diretório, mas você pode especificar um local diferente e senha adicional (uma senha tooaccess Olá arquivo de chave privada) quando solicitado. Execute Olá comando a seguir de um shell Bash, responder a prompts Olá com suas próprias informações.

```bash
ssh-keygen -t rsa -b 2048
```

## <a name="use-hello-ssh-key-pair"></a>Use o par de chaves de SSH Olá
chave pública de saudação que você coloca na sua VM do Linux no Azure é armazenados por padrão em `~/.ssh/id_rsa.pub`, a menos que você alterou o local de hello quando você criou. Se você usar o hello [2.0 do CLI do Azure](/cli/azure) toocreate sua VM, especifique o local de saudação dessa chave pública quando você usar o hello [criar vm az](/cli/azure/vm#create) com hello `--ssh-key-path` opção. Se você copia e cola conteúdo de saudação de toouse do arquivo de chave pública Olá Olá portal do Azure ou um modelo do Gerenciador de recursos, certifique-se de que não copiar nenhum espaço em branco adicional. Por exemplo, se você usar OS X, você pode direcionar o arquivo de chave pública hello (por padrão, **~/.ssh/id_rsa.pub**) muito**pbcopy** toocopy conteúdo de saudação (há outros programas de Linux que Olá a mesma coisa, como `xclip`).

Se você não estiver familiarizado com as chaves públicas SSH, veja sua chave pública executando `cat` da seguinte forma, substituindo `~/.ssh/id_rsa.pub` por seu próprio local de arquivo de chave pública:

```bash
cat ~/.ssh/id_rsa.pub
```

Com a chave pública de saudação em sua VM do Azure, usando o SSH tooyour VM Olá endereço IP ou nome DNS da VM (Lembre-se de tooreplace `azureuser` e `myvm.westus.cloudapp.azure.com` abaixo com o nome de usuário de administrador hello e IP ou nome de domínio totalmente qualificado do hello-- endereço):

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

Se você forneceu uma senha quando você criou o par de chaves, insira a senha de saudação quando solicitado durante o processo de logon hello. (servidor de saudação é adicionado tooyour `~/.ssh/known_hosts` pasta e você não será solicitado tooconnect novamente até que a chave pública de saudação em suas alterações de VM do Azure ou o nome do servidor de saudação é removido do `~/.ssh/known_hosts`.)

## <a name="next-steps"></a>Próximas etapas

Máquinas virtuais criadas usando as chaves de SSH são por padrão configurado com senhas desabilitadas, toomake forçada bruta adivinhação tentativas muito mais caro e, portanto, difícil. Este tópico descreve como criar um par de chaves SSH simples para uso rápido. Se você precisa de mais ajuda na criação de par de chaves de SSH ou exige certificados adicionais, consulte [detalhadas certificados e pares de chave SSH do etapas toocreate](create-ssh-keys-detailed.md).

Você pode criar máquinas virtuais que usam o par de chaves de SSH usando Olá portal do Azure, CLI e modelos:

* [Criar uma VM do Linux segura usando Olá portal do Azure](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Criar uma VM do Linux segura usando hello Azure CLI 2.0)](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Criar uma VM do Linux segura usando um modelo do Azure](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
