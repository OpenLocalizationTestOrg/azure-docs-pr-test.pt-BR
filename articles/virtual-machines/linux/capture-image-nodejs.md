---
title: aaaCapture toouse uma VM do Linux do Azure como um modelo | Microsoft Docs
description: "Saiba como toocapture e generalizar a imagem de uma baseados em Linux do Azure máquina virtual (VM) criada com o modelo de implantação do Azure Resource Manager hello."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e608116f-f478-41be-b787-c2ad91b5a802
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 877eee5c842bebe80e755c2240cdaaef4ade6ff5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="capture-a-linux-virtual-machine-running-on-azure"></a>Capturar uma máquina virtual do Linux em execução no Azure
Siga as etapas de saudação toogeneralize neste artigo e capturar sua máquina virtual do Linux do Azure (VM) no modelo de implantação do Gerenciador de recursos de saudação. Quando você generaliza Olá VM, você remove informações pessoais da conta e preparar Olá VM toobe usado como uma imagem. Em seguida, você captura a imagem de um disco rígido virtual (VHD) generalizado para Olá SO VHDs para discos de dados anexado, e um [modelo do Gerenciador de recursos](../../azure-resource-manager/resource-group-overview.md) para novas implantações de VM. Este artigo fornece detalhes sobre como toocapture uma VM da imagem com hello 1.0 da CLI do Azure para uma máquina virtual usando discos não gerenciados. Você também pode [capturar uma VM com discos gerenciado do Azure hello Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Discos gerenciados são tratados pelo Olá plataforma Windows Azure e não exigem qualquer etapa de preparação ou local toostore-los. Para saber mais, veja [Visão geral dos Azure Managed Disks](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 

toocreate VMs usando imagem hello, configurar recursos de rede para cada nova VM e usar toodeploy de modelo (um arquivo JavaScript Object Notation ou JSON,) de saudação do hello capturar imagens de VHD. Dessa forma, você pode replicar uma VM com sua configuração atual do software, modo toohello semelhante, você use imagens em hello Azure Marketplace.

> [!TIP]
> Se você quiser toocreate uma cópia da VM Linux existente com seu estado especializado para backup ou a depuração, consulte [criar uma cópia de uma máquina virtual do Linux em execução no Azure](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). E se você quiser tooupload um VHD de uma VM do local do Linux, consulte [carregar e criar uma VM do Linux de imagem de disco personalizado](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).  

## <a name="cli-versions-toocomplete-hello-task"></a>Tarefa de saudação do CLI versões toocomplete
Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:

- [1.0 de CLI do Azure](#before-you-begin) – nosso CLI para Olá clássico e o recurso de gerenciamento modelos de implantação (Este artigo)
- [2.0 do CLI do Azure](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação

## <a name="before-you-begin"></a>Antes de começar
Certifique-se de atender Olá pré-requisitos a seguir:

* **VM do Azure criada no modelo de implantação do Gerenciador de recursos de saudação** -se você não criou uma VM do Linux, você pode usar o hello [portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), Olá [CLI do Azure](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), ou [Gerenciador de recursos modelos de](create-ssh-secured-vm-from-template.md). 
  
    Configure Olá VM conforme necessário. Por exemplo, [adicionar discos de dados](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), aplicar atualizações e instalar aplicativos. 
* **CLI do Azure** -Olá Install [CLI do Azure](../../cli-install-nodejs.md) em um computador local.

## <a name="step-1-remove-hello-azure-linux-agent"></a>Etapa 1: Remover agente do Linux Azure Olá
Primeiro execute Olá **waagent** com hello **desprovisionamento** parâmetro hello VM do Linux. Esse comando exclui os arquivos e dados toomake Olá pronto para generalizar da VM. Para obter detalhes, consulte Olá [guia do usuário do agente Linux do Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

1. Conecte-se tooyour VM do Linux usando um cliente SSH.
2. Na janela SSH hello, digite Olá comando a seguir:
   
    ```bash
    sudo waagent -deprovision+user
    ```
   > [!NOTE]
   > Somente execute esse comando em uma máquina virtual que você pretende toocapture como uma imagem. Eles não garantem imagem Olá seja limpo de todas as informações confidenciais ou é adequada para redistribuição.
 
3. Tipo **y** toocontinue. Você pode adicionar Olá **-force** parâmetro tooavoid essa etapa de confirmação.
4. Após a conclusão do comando hello, digite **sair**. Esta etapa fecha cliente SSH de saudação.

## <a name="step-2-capture-hello-vm"></a>Etapa 2: Capturar Olá VM
Use Olá CLI do Azure toogeneralize e capturar Olá VM. Em Olá exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores. Os nomes de parâmetro de exemplo incluem **myResourceGroup**, **myVnet** e **myVM**.

1. Em seu computador local, abra Olá CLI do Azure e [tooyour logon assinatura do Azure](../../xplat-cli-connect.md). 
2. Certifique-se de estar no modo Resource Manager.
   
    ```azurecli
    azure config mode arm
    ```
3. Desligar Olá VM que você já desprovisionada usando Olá comando a seguir:
   
    ```azurecli
    azure vm deallocate -g myResourceGroup -n myVM
    ```
4. Generalize Olá VM com hello comando a seguir:
   
    ```azurecli
    azure vm generalize -g myResourceGroup -n myVM
    ```
5. Agora execute Olá **captura de vm do azure** comando, que captura Olá VM. Em Olá exemplo a seguir, imagem Olá VHDs são capturados com nomes que começam com **MyVHDNamePrefix**e hello **-t** opção especifica um modelo de caminho de toohello **MyTemplate.json**. 
   
    ```azurecli
    azure vm capture -g myResourceGroup -n myVM -p myVHDNamePrefix -t myTemplate.json
    ```
   
   > [!IMPORTANT]
   > os arquivos de imagem do VHD Olá obtenham criados por padrão no hello usada da mesma conta de armazenamento que Olá VM original. Saudação de uso *mesma conta de armazenamento* toostore Olá VHDs para novas VMs criar da imagem de saudação. 

6. local de saudação toofind de uma imagem capturada, o modelo JSON Olá aberto em um editor de texto. Em Olá **storageProfile**, localize Olá **uri** de saudação **imagem** localizado em Olá **sistema** contêiner. Por exemplo, hello URI da imagem de disco Olá SO assemelha-se muito`https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`

## <a name="step-3-create-a-vm-from-hello-captured-image"></a>Etapa 3: Criar uma VM da imagem capturada de saudação
Agora use imagem Olá com um modelo toocreate uma VM do Linux. Estas etapas mostram como toouse Olá CLI do Azure e Olá capturados toocreate Olá VM em uma nova rede virtual de modelo de arquivo JSON.

### <a name="create-network-resources"></a>Criar recursos da rede
modelo de saudação toouse, primeiro é necessário tooset um NIC e de rede virtual para sua nova VM. Recomendamos que você crie um grupo de recursos para esses recursos no local de saudação onde a imagem VM é armazenada. Execute comandos semelhante toohello a seguir, substituindo os nomes de seus recursos e um local apropriado do Azure ("centralus" esses comandos):

```azurecli
azure group create myResourceGroup1 -l "centralus"

azure network vnet create myResourceGroup1 myVnet -l "centralus"

azure network vnet subnet create myResourceGroup1 myVnet mySubnet

azure network public-ip create myResourceGroup1 myPublicIP -l "centralus"

azure network nic create myResourceGroup1 myNIC -k mySubnet -m myVnet -p myPublicIP -l "centralus"
```

### <a name="get-hello-id-of-hello-nic"></a>Obter Olá Id da saudação NIC
toodeploy uma VM da imagem hello usando Olá salvo durante a captura JSON, você precisa Olá Id da saudação NIC. Obtê-lo executando Olá comando a seguir:

```azurecli
azure network nic show myResourceGroup1 myNIC
```

Olá **Id** no Olá a saída é semelhante muito`/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic`

### <a name="create-a-vm"></a>Criar uma máquina virtual
Agora o comando a seguir de execução Olá toocreate sua VM do hello capturar a imagem VM. Saudação de uso **-f** modelo de toohello parâmetro toospecify Olá caminho JSON do arquivo salvo.

```azurecli
azure group deployment create myResourceGroup1 MyDeployment -f MyTemplate.json
```

Na saída do comando hello, são solicitada toosupply um novo nome VM, nome de usuário de administrador hello e senha e Olá Id da saudação NIC que você criou anteriormente.

```bash
info:    Executing command group deployment create
info:    Supply values for hello following parameters
vmName: myNewVM
adminUserName: myAdminuser
adminPassword: ********
networkInterfaceId: /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resource Groups/myResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
```

saudação de exemplo a seguir mostra o que você vê uma implantação bem-sucedida:

```bash
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment xxxxxxx
+ Waiting for deployment toocomplete
data:    DeploymentName     : MyDeployment
data:    ResourceGroupName  : MyResourceGroup1
data:    ProvisioningState  : Succeeded
data:    Timestamp          : xxxxxxx
data:    Mode               : Incremental
data:    Name                Type          Value

data:    ------------------  ------------  -------------------------------------

data:    vmName              String        myNewVM

data:    vmSize              String        Standard_D1

data:    adminUserName       String        myAdminuser

data:    adminPassword       SecureString  undefined

data:    networkInterfaceId  String        /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
info:    group deployment create command OK
```

### <a name="verify-hello-deployment"></a>Verificar a implantação de saudação
Agora SSH toohello máquina virtual é criada a implantação de saudação tooverify e começar a usar Olá nova VM. tooconnect via SSH, localizar o endereço IP de saudação do Olá VM criada executando Olá comando a seguir:

```azurecli
azure network public-ip show myResourceGroup1 myPublicIP
```

endereço IP público de saudação é listado na saída do comando hello. Por padrão, você se conectar toohello VM Linux por SSH na porta 22.

## <a name="create-additional-vms"></a>Criar VMs adicionais
Olá Use capturados toodeploy de imagem e o modelo usar etapas Olá Olá anterior a seção de VMs adicionais. Outra opções toocreate VMs da imagem de saudação incluem usando um modelo de início rápido ou executando Olá **criar vm do azure** comando.

### <a name="use-hello-captured-template"></a>Usar modelo capturada Olá
toouse Olá capturada a imagem e o modelo, siga estas etapas (detalhadas no hello anterior seção):

* Certifique-se de que a imagem VM está em Olá mesma conta de armazenamento que hospeda o VHD da VM.
* Copie o arquivo JSON do modelo hello e especifique um nome exclusivo para o disco do sistema operacional de saudação do VHD Olá nova VM (ou VHDs). Por exemplo, em Olá **storageProfile**, em **vhd**, na **uri**, especifique um nome exclusivo para Olá **osDisk** VHD, semelhante muito`https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`
* Crie uma NIC em qualquer Olá mesmo ou em uma rede virtual diferente.
* Usando o arquivo JSON do modelo de saudação modificado, crie uma implantação no grupo de recursos de saudação em que você configura rede virtual hello.

### <a name="use-a-quickstart-template"></a>Usar um modelo de início rápido
Se você quiser rede Olá configurada automaticamente quando você cria uma VM da imagem hello, você pode especificar esses recursos em um modelo. Por exemplo, consulte Olá [modelo 101 vm de usuário imagem](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) do GitHub. Este modelo cria uma VM de sua imagem personalizada e de rede virtual necessária hello, endereço IP público e recursos NIC. Para obter uma explicação de como usar o modelo Olá em Olá portal do Azure, consulte [como uma máquina virtual de uma imagem personalizada usando um modelo do Gerenciador de recursos de toocreate](http://codeisahighway.com/how-to-create-a-virtual-machine-from-a-custom-image-using-an-arm-template/).

### <a name="use-hello-azure-vm-create-command"></a>Use hello azure vm criar comando
Geralmente, é mais fácil toouse um modelo de Gerenciador de recursos toocreate uma VM da imagem de saudação. No entanto, você pode criar hello VM *imperativa* usando Olá **criar vm do azure** com hello **-Q** (**– imagem urn**) parâmetro . Se você usar esse método, você também pode passar Olá **-d** (**vhd de disco de SO –**) local de saudação do parâmetro toospecify do arquivo. vhd Olá SO Olá nova VM. Esse arquivo deve estar no contêiner de vhds Olá Olá da conta de armazenamento onde o arquivo VHD de imagem de saudação é armazenado. Olá comando cópias hello VHD para Olá nova VM automaticamente toohello **vhds** contêiner.

Antes de executar **criar vm do azure** com imagem hello, conclua Olá etapas a seguir:

1. Criar um grupo de recursos ou identificar o grupo de recursos para implantação de saudação.
2. Criar um público recurso de endereço IP e um recurso NIC para Olá nova VM. Para etapas toocreate uma rede virtual, endereço IP público e NIC usando Olá CLI, consulte neste artigo. (**criar vm do azure** também pode criar uma NIC, mas você precisa de parâmetros adicionais de toopass para uma rede virtual e sub-rede.)

Em seguida, execute um comando que passa URIs tooboth Olá novo arquivo. VHD do sistema operacional e Olá existente de imagem. Neste exemplo, um tamanho de VM Standard_A1 é criado na região Leste dos EUA de saudação.

```azurecli
azure vm create -g myResourceGroup1 -n myNewVM -l eastus -y Linux \
-z Standard_A1 -u myAdminname -p myPassword -f myNIC \
-d "https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix.vhd" \
-Q "https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.vhd"
```

Para obter opções adicionais de comando, execute `azure help vm create`.

## <a name="next-steps"></a>Próximas etapas
toomanage suas VMs com hello CLI, consulte tarefas de saudação [implantar e gerenciar máquinas virtuais usando modelos do Gerenciador de recursos do Azure e Olá CLI do Azure](create-ssh-secured-vm-from-template.md).

