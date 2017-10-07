---
title: imagens VM personalizadas aaaCreate com hello CLI do Azure | Microsoft Docs
description: "Tutorial - criar uma imagem VM personalizada usando Olá CLI do Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/21/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 217a993c0c1d48939b74108ac6c5f7a1a619416c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-hello-cli"></a>Criar uma imagem personalizada de uma VM do Azure usando Olá CLI

Imagens personalizadas são como imagens do marketplace, mas você mesmo as cria. Imagens personalizadas podem ser usado toobootstrap configurações como pré-carregamento de aplicativos, configurações de aplicativo e outras configurações do sistema operacional. Neste tutorial, você criará sua própria imagem personalizada de uma máquina virtual do Azure. Você aprenderá como:

> [!div class="checklist"]
> * Desprovisionar e generalizar VMs
> * Criar uma imagem personalizada
> * Criar uma VM por meio de uma imagem personalizada
> * Lista todas as imagens de saudação em sua assinatura
> * Excluir uma imagem


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se você escolher tooinstall e usa o hello CLI localmente, este tutorial requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="before-you-begin"></a>Antes de começar

etapas de saudação abaixo detalham como tootake uma VM existente e desative-o para um personalizado pode ser reutilizado da imagem que você podem usar toocreate novas instâncias VM.

exemplo de hello toocomplete neste tutorial, você deve ter uma máquina virtual existente. Se necessário, este [exemplo de script](../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md) pode criar uma para você. Trabalho tutorial hello, substitua VM e o grupo de recursos de saudação nomes onde for necessário.

## <a name="create-a-custom-image"></a>Criar uma imagem personalizada

toocreate uma imagem de uma máquina virtual, você precisa tooprepare Olá VM, desprovisionamento, desalocando e, em seguida, marcando fonte Olá VM como generalizado. Uma vez Olá que VM tenha sido preparada, você pode criar uma imagem.

### <a name="deprovision-hello-vm"></a>Saudação de desprovisionamento VM 

Desprovisionamento generaliza Olá VM removendo informações específicas de computador. Este generalização torna possível toodeploy muitas máquinas virtuais de uma única imagem. Durante o desprovisionamento, nome de host de saudação é redefinido muito*localdomain*. As chaves de host de SSH, as configurações de nameserver, a senha raiz e as concessões de DHCP em cache também são excluídas.

Olá toodeprovision VM, usar o agente de VM do Azure hello (waagent). Agente de VM do Azure Olá Olá VM está instalado e gerencia o provisionamento e interagir com hello controlador de malha do Azure. Para obter mais informações, consulte Olá [guia do usuário do agente Linux do Azure](agent-user-guide.md).

Conecte-se tooyour VM usando SSH e execução Olá comando toodeprovision Olá VM. Com hello `+user` argumento, a última conta de usuário provisionado hello e quaisquer dados associados também serão excluídos. Substitua o endereço IP de exemplo hello com endereço IP público de saudação da VM.

SSH toohello VM.
```bash
ssh azureuser@52.174.34.95
```
Saudação de desprovisionamento VM.

```bash
sudo waagent -deprovision+user -force
```
Feche a sessão SSH hello.

```bash
exit
```

### <a name="deallocate-and-mark-hello-vm-as-generalized"></a>Desalocar e marcar Olá VM como generalizado

toocreate uma imagem, Olá VM precisa toobe desalocada. Desalocar Olá VM usando [az vm desalocar](/cli//azure/vm#deallocate). 
   
```azurecli-interactive 
az vm deallocate --resource-group myResourceGroup --name myVM
```

Por fim, definir estado de saudação do hello VM como generalizado com [az vm generalizar](/cli//azure/vm#generalize) para Olá plataforma Windows Azure Saiba Olá VM tenha sido generalizada. Você só pode criar uma imagem por meio de uma VM generalizada.
   
```azurecli-interactive 
az vm generalize --resource-group myResourceGroup --name myVM
```

### <a name="create-hello-image"></a>Criar imagem Olá

Agora você pode criar uma imagem de VM de saudação usando [criar imagem az](/cli//azure/image#create). Olá, exemplo a seguir cria uma imagem chamada *myImage* de uma VM denominada *myVM*.
   
```azurecli-interactive 
az image create \
    --resource-group myResourceGroup \
    --name myImage \
    --source myVM
```
 
## <a name="create-vms-from-hello-image"></a>Criar VMs de imagem Olá

Agora que você tem uma imagem, você pode criar um ou mais novas VMs do uso de imagem Olá [criar vm az](/cli/azure/vm#create). Olá, exemplo a seguir cria uma VM denominada *myVMfromImage* de imagem Olá chamada *myImage*.

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVMfromImage \
    --image myImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

## <a name="image-management"></a>Gerenciamento de imagens 

Aqui estão alguns exemplos de tarefas comuns de gerenciamento de imagem e como toocomplete-los usando Olá CLI do Azure.

Liste todas as imagens por nome em um formato de tabela.

```azurecli-interactive 
az image list \
  --resource-group myResourceGroup
```

Exclua uma imagem. Este exemplo exclui Olá imagem chamada *myOldImage* de saudação *myResourceGroup*.

```azurecli-interactive 
az image delete \
    --name myOldImage \
    --resource-group myResourceGroup
```

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você criou uma imagem de VM personalizada. Você aprendeu como:

> [!div class="checklist"]
> * Desprovisionar e generalizar VMs
> * Criar uma imagem personalizada
> * Criar uma VM por meio de uma imagem personalizada
> * Lista todas as imagens de saudação em sua assinatura
> * Excluir uma imagem

Avançar toohello toolearn próximo de tutorial sobre máquinas virtuais altamente disponíveis.

> [!div class="nextstepaction"]
> [Criar VMs altamente disponíveis](tutorial-availability-sets.md).

