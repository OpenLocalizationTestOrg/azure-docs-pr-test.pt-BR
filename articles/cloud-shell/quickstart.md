---
title: "início rápido do Shell de nuvem (visualização) aaaAzure | Microsoft Docs"
description: "Início rápido para Olá Shell de nuvem do Azure"
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: juluk
ms.openlocfilehash: e60700b92c10c331910dd8bb3c627fe1a024091c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-for-using-hello-azure-cloud-shell"></a>Guia de início rápido para usar o hello Shell de nuvem do Azure

Este documento detalha como toouse Olá Shell de nuvem do Azure no hello [portal do Azure](https://ms.portal.azure.com/).

## <a name="start-cloud-shell"></a>Iniciar o Cloud Shell
1. Iniciar **nuvem Shell** de navegação superior Olá Olá portal do Azure <br>
![](media/shell-icon.png)
2. Selecione uma assinatura toocreate uma conta de armazenamento e compartilhamento de arquivos do Azure
3. Selecione "Criar armazenamento"

> [!TIP]
> Você é autenticado automaticamente na CLI do Azure 2.0 em cada sessão.

### <a name="set-your-subscription"></a>Definir sua assinatura
1. Liste as assinaturas a que você tem acesso: <br>
`az account list`
2. Defina sua assinatura preferencial: <br>
`az account set --subscription my-subscription-name`

> [!TIP]
> Sua assinatura será lembrada em sessões futuras com o uso de `/home/<user>/.azure/azureProfile.json`.

### <a name="create-a-resource-group"></a>Criar um grupo de recursos
Crie um novo grupo de recursos no Oeste dos EUA chamado "MyRG": <br>
`az group create -l westus -n MyRG` <br>

### <a name="create-a-linux-vm"></a>Criar uma VM do Linux
Crie uma VM do Ubuntu em seu novo grupo de recursos. Olá 2.0 do CLI do Azure criará as chaves de SSH e Olá instalação VM com eles. <br>
`az vm create -n my_vm_name -g MyRG --image UbuntuLTS --generate-ssh-keys`

> [!NOTE]
> Olá tooauthenticate de chaves públicas e privadas usadas sua VM são colocados em `/User/.ssh/id_rsa` e `/User/.ssh/id_rsa.pub` pelo Azure CLI 2.0 por padrão. Sua pasta .ssh é mantida na imagem de 5 GB do compartilhamento de arquivos anexado do Azure.

Seu nome de usuário nessa VM será o nome de usuário usado no Cloud Shell ($User@Azure:).

### <a name="ssh-into-your-linux-vm"></a>SSH em sua VM Linux
1. Procurar o nome VM na barra de pesquisa do portal do Azure Olá
2. Clique em "Conectar" e execute: `ssh username@ipaddress`

![](media/sshcmd-copy.png)

Após estabelecer a conexão de SSH hello, você verá um prompt de boas-vinda de Ubuntu de saudação.
![](media/ubuntu-welcome.png)

## <a name="cleaning-up"></a>Limpando 
Exclua o grupo de recursos e todos os recursos dentro dele: <br>
Execute o `az group delete -n MyRG`

## <a name="next-steps"></a>Próximas etapas
[Saiba mais sobre o armazenamento persistente no Cloud Shell](persisting-shell-storage.md) <br>
[Saiba mais sobre a CLI do Azure 2.0](https://docs.microsoft.com/cli/azure/) <br>
[Saiba mais sobre o armazenamento de Arquivos do Azure](../storage/files/storage-files-introduction.md) <br>