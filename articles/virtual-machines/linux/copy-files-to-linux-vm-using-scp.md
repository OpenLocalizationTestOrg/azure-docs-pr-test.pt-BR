---
title: aaaMove arquivos tooand de VMs do Linux do Azure com SCP | Microsoft Docs
description: "Mova arquivos tooand com segurança de uma VM do Linux no Azure usando o SCP e um par de chaves SSH."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: danlep
ms.openlocfilehash: 9e4dce667aa581df74aec3d45a6ba5e52f777d1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-files-tooand-from-a-linux-vm-using-scp"></a>Mover arquivos tooand de uma VM do Linux usando o SCP

Este artigo mostra como toomove arquivos de backup tooan VM do Linux do Azure em sua estação de trabalho ou de uma VM do Linux do Azure para baixo tooyour estação de trabalho, usando cópia segura (SCP). Mover arquivos entre a estação de trabalho e uma VM Linux, de forma rápida e segura, é uma parte crítica do gerenciamento da infraestrutura do Azure. 

Para este artigo, você precisa de uma VM Linux implantada no Azure usando [arquivos de chave SSH pública e privada](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Você também precisa de um cliente SCP para o computador local. É criado com base em SSH e incluído no shell de Bash saudação padrão da maioria dos computadores Linux e Mac e alguns shells do Windows.

## <a name="quick-commands"></a>Comandos rápidos

Copiar um arquivo de backup toohello VM do Linux

```bash
scp file azureuser@azurehost:directory/targetfile
```

Copiar um arquivo para baixo de saudação VM do Linux

```bash
scp azureuser@azurehost:directory/file targetfile
```

## <a name="detailed-walkthrough"></a>Passo a passo detalhado

Como exemplos, mover um arquivo de configuração do Azure backup tooa VM do Linux e baixar um diretório de arquivos de log, usando chaves SCP e SSH.   

## <a name="ssh-key-pair-authentication"></a>Autenticação de par de chaves SSH

SCP usa SSH para a camada de transporte hello. Identificadores de SSH Olá autenticação no host de destino hello e ele move o arquivo hello em um túnel criptografado fornecido por padrão com o SSH. Para autenticação de SSH, nomes de usuário e senhas podem ser usados. No entanto, a autenticação de chaves SSH públicas e privadas é recomendada como uma melhor prática de segurança. Depois de SSH autenticou conexão hello, SCP começa, em seguida, copiar o arquivo hello. Usando um adequadamente configurado `~/.ssh/config` e as chaves públicas e privadas de SSH, conexão Olá SCP podem ser estabelecidas usando apenas um nome de servidor (ou endereço IP). Se você tiver apenas uma chave SSH, SCP procura por ele no hello `~/.ssh/` directory e usa por padrão toolog em toohello VM.

Para obter mais informações sobre como configurar o `~/.ssh/config` e chaves SSH pública e privada, veja [Create SSH keys](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Criar chaves SSH).

## <a name="scp-a-file-tooa-linux-vm"></a>SCP tooa um arquivo VM do Linux

Por exemplo, primeiro hello, podemos copiar um arquivo de configuração do Azure backup tooa VM do Linux que é automação toodeploy usado. Já que esse arquivo contém credenciais de API do Azure, as quais incluem segredos, a segurança é importante. túnel criptografado Hello, fornecido pelo SSH protege o conteúdo de saudação do arquivo hello.

Olá seguintes comando cópias Olá local *.azure/config* tooan VM do Azure com o FQDN do arquivo *myserver.eastus.cloudapp.azure.com*. nome de usuário de administrador Olá em hello Azure VM é *azureuser* . arquivo Hello é destino toohello */home/azureuser/* directory. Substitua seus próprios valores nesse comando.

```bash
scp ~/.azure/config azureuser@myserver.eastus.cloudapp.com:/home/azureuser/config
```

## <a name="scp-a-directory-from-a-linux-vm"></a>Usar o SCP para copiar um diretório de uma VM Linux

Neste exemplo, podemos copiar um diretório de arquivos de log da saudação VM Linux para baixo tooyour estação de trabalho. Um arquivo de log pode ou não conter dados confidenciais ou segredos. No entanto, usar o SCP garante conteúdo Olá Olá dos arquivos de log é criptografado. Usando arquivos de saudação do SCP tootransfer é tooget de maneira mais fácil Olá Olá diretório de log e arquivos para baixo da estação de trabalho tooyour ao mesmo tempo, além de ser seguro.

Olá comando a seguir copia arquivos de saudação *inicial/azureuser/logs/* diretório no diretório do hello Azure VM toohello /tmp local:

```bash
scp -r azureuser@myserver.eastus.cloudapp.com:/home/azureuser/logs/. /tmp/
```

Olá `-r` cli sinalizador instrui SCP toorecursively copiar Olá arquivos e diretórios de ponto de saudação do diretório Olá listado no comando hello.  Também Observe que Olá sintaxe de linha de comando é semelhante tooa `cp` comando Copiar.

## <a name="next-steps"></a>Próximas etapas

* [Gerenciar usuários, SSH e seleção ou discos de reparo em máquinas virtuais do Linux do Azure usando Olá extensão VMAccess](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
