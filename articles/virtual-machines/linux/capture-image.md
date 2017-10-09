---
title: aaaCapture uma imagem de uma VM do Linux no Azure usando a CLI 2.0 | Microsoft Docs
description: "Capture uma imagem de toouse uma VM do Azure para implantações em massa usando Olá 2.0 do CLI do Azure."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e608116f-f478-41be-b787-c2ad91b5a802
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 07/10/2017
ms.author: cynthn
ms.openlocfilehash: 9558332a86186b282775097428df462709373012
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-image-of-a-virtual-machine-or-vhd"></a>Como toocreate uma imagem de uma máquina virtual ou um VHD

<!-- generalize, image - extended version of hello tutorial-->

toocreate várias cópias de um toouse de máquina virtual (VM) no Azure, capturar uma imagem de VM de saudação ou Olá VHD do sistema operacional. toocreate uma imagem, você precisa remover informações pessoais da conta que torna mais segura toodeploy várias vezes. Em Olá etapas cancelar o provisionamento de uma VM existente, desalocar e criar uma imagem. Você pode usar essa imagem toocreate VMs em qualquer grupo de recursos dentro de sua assinatura.

Se você deseja toocreate uma cópia da VM Linux existente para backup ou de depuração ou carrega um VHD Linux especializadas de uma VM local, consulte [carregar e criar uma VM do Linux de imagem de disco personalizado](upload-vhd.md).  

Você também pode usar **Packer** toocreate sua configuração personalizada. Para obter mais informações sobre como usar Packer, consulte [como as imagens de máquina virtual do toouse Packer toocreate Linux no Azure](build-image-with-packer.md).


## <a name="before-you-begin"></a>Antes de começar
Certifique-se de atender Olá pré-requisitos a seguir:

* Você precisa de uma VM do Azure criada no modelo de implantação do Gerenciador de recursos do hello usando discos gerenciados. Se você ainda não criou uma VM do Linux, você pode usar o hello [portal](quick-create-portal.md), Olá [CLI do Azure](quick-create-cli.md), ou [modelos do Gerenciador de recursos](create-ssh-secured-vm-from-template.md). Configure Olá VM conforme necessário. Por exemplo, [adicionar discos de dados](add-disk.md), aplicar atualizações e instalar aplicativos. 

* Você também precisa toohave hello mais recente [2.0 do CLI do Azure](/cli/azure/install-az-cli2) instalado e registrado na conta do Azure usando o tooan [logon az](/cli/azure/#login).

## <a name="quick-commands"></a>Comandos rápidos

Para uma versão simplificada deste tópico, para testar, avaliando ou aprender sobre máquinas virtuais no Azure, consulte [criar uma imagem personalizada de uma VM do Azure usando Olá CLI](tutorial-custom-images.md).


## <a name="step-1-deprovision-hello-vm"></a>Etapa 1: Desprovisionar Olá VM
Desprovisionar o hello VM, usando o agente de VM do Azure hello, toodelete arquivos específicos da máquina e dados. Saudação de uso `waagent` com hello *-desprovisionamento + user* parâmetro em sua fonte de VM do Linux. Para obter mais informações, consulte Olá [guia do usuário do agente Linux do Azure](../windows/agent-user-guide.md).

1. Conecte-se tooyour VM do Linux usando um cliente SSH.
2. Na janela SSH hello, digite Olá comando a seguir:
   
    ```bash
    sudo waagent -deprovision+user
    ```
<br>
   > [!NOTE]
   > Somente execute esse comando em uma máquina virtual que você pretende toocapture como uma imagem. Eles não garantem imagem Olá seja limpo de todas as informações confidenciais ou é adequada para redistribuição. Olá *+ user* parâmetro também remove a última conta de usuário provisionado hello. Se você quiser tookeep credenciais da conta no hello VM, basta usar *-desprovisionamento* tooleave conta de usuário de saudação em vigor.
 
3. Tipo **y** toocontinue. Você pode adicionar Olá **-force** parâmetro tooavoid essa etapa de confirmação.
4. Após a conclusão do comando hello, digite **sair**. Esta etapa fecha cliente SSH de saudação.

## <a name="step-2-create-vm-image"></a>Etapa 2: Criar a imagem de VM
Usar Olá 2.0 do CLI do Azure toomark Olá VM generalizado e capturar a imagem de saudação. Em Olá exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores. Os nomes de parâmetro de exemplo incluem *myResourceGroup*, *myVnet* e *myVM*.

1. Desalocar Olá VM desprovisionada com [az vm desalocar](/cli//azure/vm#deallocate). exemplo a seguir Hello desaloca Olá VM denominada *myVM* no grupo de recursos de saudação denominado *myResourceGroup*:
   
    ```azurecli
    az vm deallocate \
      --resource-group myResourceGroup \
      --name myVM
    ```

2. Saudação de marca VM como generalizado com [az vm generalizar](/cli//azure/vm#generalize). Olá seguinte exemplo marcas Olá Olá VM denominada *myVM* no grupo de recursos de saudação denominado *myResourceGroup* como generalizado:
   
    ```azurecli
    az vm generalize \
      --resource-group myResourceGroup \
      --name myVM
    ```

3. Agora crie uma imagem do recurso VM Olá com [criar imagem az](/cli//azure/image#create). Olá, exemplo a seguir cria uma imagem chamada *myImage* no grupo de recursos de saudação denominado *myResourceGroup* usando o recurso VM Olá denominado *myVM*:
   
    ```azurecli
    az image create \
      --resource-group myResourceGroup \
      --name myImage --source myVM
    ```
   
   > [!NOTE]
   > Olá imagem é criada no hello mesmo grupo de recursos como a fonte de VM. Você pode criar VMs em qualquer grupo de recursos em sua assinatura desde esta imagem. De uma perspectiva de gerenciamento, talvez você queira toocreate um grupo de recursos específicos para seus recursos VM e imagens.

## <a name="step-3-create-a-vm-from-hello-captured-image"></a>Etapa 3: Criar uma VM da imagem capturada de saudação
Criar uma VM usando a imagem de saudação criado com [criar vm az](/cli/azure/vm#create). Olá, exemplo a seguir cria uma VM denominada *myVMDeployed* de imagem Olá chamada *myImage*:

```azurecli
az vm create \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --image myImage\
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```

### <a name="creating-hello-vm-in-another-resource-group"></a>Criando Olá VM em outro grupo de recursos 

Com os discos gerenciados, você pode criar VMs de uma imagem em qualquer grupo de recursos em sua assinatura. toocreate uma VM em um grupo de recursos diferente que a imagem Olá, especifique a imagem de tooyour de ID de recurso completo de saudação. Use [lista de imagens az](/cli/azure/image#list) tooview uma lista de imagens. saudação de saída é similar toohello exemplo a seguir:

```json
"id": "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage",
   "location": "westus",
   "name": "myImage",
```

Olá exemplo a seguir usa [criar vm az](/cli/azure/vm#create) toocreate uma VM em um grupo de recursos diferente que a imagem de origem Olá especificando a ID de recurso de imagem de saudação:

```azurecli
az vm create \
   --resource-group myOtherResourceGroup \
   --name myOtherVMDeployed \
   --image "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage" \
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```


## <a name="step-4-verify-hello-deployment"></a>Etapa 4: Verificar a implantação de saudação

Agora SSH toohello máquina virtual é criada a implantação de saudação tooverify e começar a usar Olá nova VM. tooconnect via SSH, localizar o endereço IP de saudação ou FQDN da VM com [Mostrar de vm az](/cli/azure/vm#show):

```azurecli
az vm show \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --show-details
```

## <a name="next-steps"></a>Próximas etapas
Você pode criar várias máquinas virtuais da sua imagem de VM de origem. Se você precisa de imagem de tooyour toomake alterações: 

- Crie uma VM usando sua imagem.
- Faça quaisquer atualizações ou alterações de configuração.
- Siga Olá etapas novamente toodeprovision, desalocar, generalizar e criar uma imagem.
- Use essa nova imagem para implantações futuras. Se desejar, exclua imagem original hello.

Para obter mais informações sobre como gerenciar suas VMs com hello CLI, consulte [Azure CLI 2.0](/cli/azure/overview).
