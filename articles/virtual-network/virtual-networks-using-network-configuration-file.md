---
title: "aaaConfigure uma rede Virtual do Azure (clássica) - arquivo de configuração de rede | Microsoft Docs"
description: "Saiba como toocreate e modificar as redes virtuais (clássico) exportando, alterando e importando um arquivo de configuração de rede."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: c29b9059-22b0-444e-bbfe-3e35f83cde2f
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/23/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: 009108d4315b4b7146d3f1cf2436ee211d2d89ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-classic-using-a-network-configuration-file"></a><span data-ttu-id="9102f-103">Configurar uma rede virtual (clássico) usando um arquivo de configuração de rede</span><span class="sxs-lookup"><span data-stu-id="9102f-103">Configure a virtual network (classic) using a network configuration file</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9102f-104">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9102f-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="9102f-105">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="9102f-105">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="9102f-106">A Microsoft recomenda que mais novas implantações de usam o modelo de implantação do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="9102f-106">Microsoft recommends that most new deployments use hello Resource Manager deployment model.</span></span>

<span data-ttu-id="9102f-107">Você pode criar e configurar uma rede virtual (clássica) com um arquivo de configuração de rede usando hello Azure interface de linha de comando (CLI) 1.0 ou o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="9102f-107">You can create and configure a virtual network (classic) with a network configuration file using hello Azure command-line interface (CLI) 1.0 or Azure PowerShell.</span></span> <span data-ttu-id="9102f-108">Você não pode criar ou modificar uma rede virtual por meio do modelo de implantação do Azure Resource Manager hello usando um arquivo de configuração de rede.</span><span class="sxs-lookup"><span data-stu-id="9102f-108">You cannot create or modify a virtual network through hello Azure Resource Manager deployment model using a network configuration file.</span></span> <span data-ttu-id="9102f-109">Você não pode usar Olá toocreate portal do Azure ou modificar uma rede virtual (clássica) usando um arquivo de configuração de rede, no entanto, você pode usar Olá toocreate portal do Azure uma rede virtual (clássica), sem usar um arquivo de configuração de rede.</span><span class="sxs-lookup"><span data-stu-id="9102f-109">You cannot use hello Azure portal toocreate or modify a virtual network (classic) using a network configuration file, however you can use hello Azure portal toocreate a virtual network (classic), without using a network configuration file.</span></span>

<span data-ttu-id="9102f-110">Criar e configurar uma rede virtual (clássica) com um arquivo de configuração de rede requer exportar, alterar e importar o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="9102f-110">Creating and configuring a virtual network (classic) with a network configuration file requires exporting, changing, and importing hello file.</span></span>

## <span data-ttu-id="9102f-111"><a name="export"></a>Exportar um arquivo de configuração de rede</span><span class="sxs-lookup"><span data-stu-id="9102f-111"><a name="export"></a>Export a network configuration file</span></span>

<span data-ttu-id="9102f-112">Você pode usar o PowerShell ou hello CLI do Azure tooexport um arquivo de configuração de rede.</span><span class="sxs-lookup"><span data-stu-id="9102f-112">You can use PowerShell or hello Azure CLI tooexport a network configuration file.</span></span> <span data-ttu-id="9102f-113">PowerShell exporta um arquivo XML, enquanto Olá CLI do Azure exporta um arquivo json.</span><span class="sxs-lookup"><span data-stu-id="9102f-113">PowerShell exports an XML file, while hello Azure CLI exports a json file.</span></span>

### <a name="powershell"></a><span data-ttu-id="9102f-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9102f-114">PowerShell</span></span>
 
1. <span data-ttu-id="9102f-115">[Instale o Azure PowerShell e entrar tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9102f-115">[Install Azure PowerShell and sign in tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="9102f-116">Altere o diretório de saudação (e verifique se ele existir) e o nome do arquivo hello comando como desejado, em seguida, execute Olá comando tooexport Olá rede arquivo de configuração a seguir:</span><span class="sxs-lookup"><span data-stu-id="9102f-116">Change hello directory (and ensure it exists) and filename in hello following command as desired, then run hello command tooexport hello network configuration file:</span></span>

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a><span data-ttu-id="9102f-117">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="9102f-117">Azure CLI 1.0</span></span>

1. <span data-ttu-id="9102f-118">[Instalar hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9102f-118">[Install hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="9102f-119">Concluir Olá restantes etapas em um prompt de comando do Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="9102f-119">Complete hello remaining steps from an Azure CLI 1.0 command prompt.</span></span>
2. <span data-ttu-id="9102f-120">Fazer logon tooAzure digitando Olá `azure login` comando.</span><span class="sxs-lookup"><span data-stu-id="9102f-120">Log in tooAzure by entering hello `azure login` command.</span></span>
3. <span data-ttu-id="9102f-121">Certifique-se de que você está no modo de asm inserindo Olá `azure config mode asm` comando.</span><span class="sxs-lookup"><span data-stu-id="9102f-121">Ensure you're in asm mode by entering hello `azure config mode asm` command.</span></span>
4. <span data-ttu-id="9102f-122">Altere o diretório de saudação (e verifique se ele existir) e o nome do arquivo hello comando como desejado, em seguida, execute Olá comando tooexport Olá rede arquivo de configuração a seguir:</span><span class="sxs-lookup"><span data-stu-id="9102f-122">Change hello directory (and ensure it exists) and filename in hello following command as desired, then run hello command tooexport hello network configuration file:</span></span>
    
    ```azurecli
    azure network export c:\azure\networkconfig.json
    ```

## <a name="create-or-modify-a-network-configuration-file"></a><span data-ttu-id="9102f-123">Criar ou modificar um arquivo de configuração de rede</span><span class="sxs-lookup"><span data-stu-id="9102f-123">Create or modify a network configuration file</span></span>

<span data-ttu-id="9102f-124">Um arquivo de configuração de rede é um arquivo XML (ao usar o PowerShell) ou um arquivo json (ao usar Olá CLI do Azure).</span><span class="sxs-lookup"><span data-stu-id="9102f-124">A network configuration file is an XML file (when using PowerShell) or a json file (when using hello Azure CLI).</span></span> <span data-ttu-id="9102f-125">Você pode editar o arquivo hello em qualquer texto ou editor XML/json.</span><span class="sxs-lookup"><span data-stu-id="9102f-125">You can edit hello file in any text, or XML/json editor.</span></span> <span data-ttu-id="9102f-126">Olá [configurações de esquema de arquivo de configuração de rede](https://msdn.microsoft.com/library/azure/jj157100.aspx) artigo inclui detalhes de todas as configurações.</span><span class="sxs-lookup"><span data-stu-id="9102f-126">hello [Network configuration file schema settings](https://msdn.microsoft.com/library/azure/jj157100.aspx) article includes details for all settings.</span></span> <span data-ttu-id="9102f-127">Para obter uma explicação adicional das configurações de hello, consulte [exibir configurações de redes virtuais e](virtual-network-manage-network.md#view-vnet).</span><span class="sxs-lookup"><span data-stu-id="9102f-127">For additional explanation of hello settings, see [View virtual networks and settings](virtual-network-manage-network.md#view-vnet).</span></span> <span data-ttu-id="9102f-128">Olá alterações feitas toohello arquivo:</span><span class="sxs-lookup"><span data-stu-id="9102f-128">hello changes you make toohello file:</span></span>

- <span data-ttu-id="9102f-129">Deve estar de acordo com esquema hello, ou de rede de saudação importando o arquivo de configuração falhará.</span><span class="sxs-lookup"><span data-stu-id="9102f-129">Must comply with hello schema, or importing hello network configuration file will fail.</span></span>
- <span data-ttu-id="9102f-130">Substituirão todas as configurações de rede existentes para sua assinatura, portanto, tenha extremo cuidado ao realizar as modificações.</span><span class="sxs-lookup"><span data-stu-id="9102f-130">Overwrite any existing network settings for your subscription, so use extreme caution when making modifications.</span></span> <span data-ttu-id="9102f-131">Por exemplo, fazer referência a arquivos configuração de rede de exemplo de hello que seguem.</span><span class="sxs-lookup"><span data-stu-id="9102f-131">For example, reference hello example network configuration files that follow.</span></span> <span data-ttu-id="9102f-132">Digamos que o arquivo original Olá contém dois **VirtualNetworkSite** instâncias e é alterado, conforme mostrado nos exemplos de saudação.</span><span class="sxs-lookup"><span data-stu-id="9102f-132">Say hello original file contained two **VirtualNetworkSite** instances, and you changed it, as shown in hello examples.</span></span> <span data-ttu-id="9102f-133">Quando você importa o arquivo hello, Azure exclui a rede virtual Olá Olá **VirtualNetworkSite** instância removida no arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="9102f-133">When you import hello file, Azure deletes hello virtual network for hello **VirtualNetworkSite** instance you removed in hello file.</span></span> <span data-ttu-id="9102f-134">Esse cenário simplificado assume não foram nenhum recurso na rede virtual do hello, como se houvesse, não foi possível excluir a rede virtual hello e importação de saudação falharia.</span><span class="sxs-lookup"><span data-stu-id="9102f-134">This simplified scenario assumes no resources were in hello virtual network, as if there were, hello virtual network could not be deleted, and hello import would fail.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9102f-135">O Azure considera uma sub-rede com algo implantado tooit como **em uso**.</span><span class="sxs-lookup"><span data-stu-id="9102f-135">Azure considers a subnet that has something deployed tooit as **in use**.</span></span> <span data-ttu-id="9102f-136">Quando uma sub-rede estiver em uso, ela não poderá ser modificada.</span><span class="sxs-lookup"><span data-stu-id="9102f-136">When a subnet is in use, it cannot be modified.</span></span> <span data-ttu-id="9102f-137">Antes de modificar as informações de sub-rede em um arquivo de configuração de rede, mova qualquer coisa que você implantou toohello sub-rede tooa sub-rede diferente que não está sendo modificada.</span><span class="sxs-lookup"><span data-stu-id="9102f-137">Before modifying subnet information in a network configuration file, move anything that you have deployed toohello subnet tooa different subnet that isn't being modified.</span></span> <span data-ttu-id="9102f-138">Consulte [mover uma VM ou instância de função tooa outra sub-rede](virtual-networks-move-vm-role-to-subnet.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="9102f-138">See [Move a VM or Role Instance tooa Different Subnet](virtual-networks-move-vm-role-to-subnet.md) for details.</span></span>

### <a name="example-xml-for-use-with-powershell"></a><span data-ttu-id="9102f-139">Exemplo de XML para uso com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="9102f-139">Example XML for use with PowerShell</span></span>

<span data-ttu-id="9102f-140">Olá, arquivo de configuração de rede de exemplo a seguir cria uma rede virtual denominada *myVirtualNetwork* com um espaço de endereço de *10.0.0.0/16* em Olá *Leste dos EUA* Azure região.</span><span class="sxs-lookup"><span data-stu-id="9102f-140">hello following example network configuration file creates a virtual network named *myVirtualNetwork* with an address space of *10.0.0.0/16* in hello *East US* Azure region.</span></span> <span data-ttu-id="9102f-141">rede virtual Olá contém uma sub-rede denominada *mySubnet* com um prefixo de endereço *10.0.0.0/24*.</span><span class="sxs-lookup"><span data-stu-id="9102f-141">hello virtual network contains one subnet named *mySubnet* with an address prefix of *10.0.0.0/24*.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
  <VirtualNetworkConfiguration>
    <Dns />
    <VirtualNetworkSites>
      <VirtualNetworkSite name="myVirtualNetwork" Location="East US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="mySubnet">
            <AddressPrefix>10.0.0.0/24</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    </VirtualNetworkSites>
  </VirtualNetworkConfiguration>
</NetworkConfiguration>
```

<span data-ttu-id="9102f-142">Se o arquivo de configuração de rede hello exportada não contém nenhum conteúdo, você pode copiar Olá XML no exemplo anterior de saudação e colá-lo em um novo arquivo.</span><span class="sxs-lookup"><span data-stu-id="9102f-142">If hello network configuration file you exported contains no contents, you can copy hello XML in hello previous example, and paste it into a new file.</span></span>

### <a name="example-json-for-use-with-hello-azure-cli-10"></a><span data-ttu-id="9102f-143">Exemplo de JSON para uso com hello 1.0 da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="9102f-143">Example JSON for use with hello Azure CLI 1.0</span></span>

<span data-ttu-id="9102f-144">Olá, arquivo de configuração de rede de exemplo a seguir cria uma rede virtual denominada *myVirtualNetwork* com um espaço de endereço de *10.0.0.0/16* em Olá *Leste dos EUA* Azure região.</span><span class="sxs-lookup"><span data-stu-id="9102f-144">hello following example network configuration file creates a virtual network named *myVirtualNetwork* with an address space of *10.0.0.0/16* in hello *East US* Azure region.</span></span> <span data-ttu-id="9102f-145">rede virtual Olá contém uma sub-rede denominada *mySubnet* com um prefixo de endereço *10.0.0.0/24*.</span><span class="sxs-lookup"><span data-stu-id="9102f-145">hello virtual network contains one subnet named *mySubnet* with an address prefix of *10.0.0.0/24*.</span></span>

```json
{
   "VirtualNetworkConfiguration" : {
      "Dns" : "",
      "VirtualNetworkSites" : [
         {
            "AddressSpace" : [ "10.0.0.0/16" ],
            "Location" : "East US",
            "Name" : "myVirtualNetwork",
            "Subnets" : [
               {
                  "AddressPrefix" : "10.0.0.0/24",
                  "Name" : "mySubnet"
               }
            ]
         }
      ]
   }
}
```

<span data-ttu-id="9102f-146">Se o arquivo de configuração de rede hello exportada não contém nenhum conteúdo, você pode copiar Olá json no exemplo anterior de saudação e colá-lo em um novo arquivo.</span><span class="sxs-lookup"><span data-stu-id="9102f-146">If hello network configuration file you exported contains no contents, you can copy hello json in hello previous example, and paste it into a new file.</span></span>

## <span data-ttu-id="9102f-147"><a name="import"></a>Importar um arquivo de configuração de rede</span><span class="sxs-lookup"><span data-stu-id="9102f-147"><a name="import"></a>Import a network configuration file</span></span>

<span data-ttu-id="9102f-148">Você pode usar o PowerShell ou hello CLI do Azure tooimport um arquivo de configuração de rede.</span><span class="sxs-lookup"><span data-stu-id="9102f-148">You can use PowerShell or hello Azure CLI tooimport a network configuration file.</span></span> <span data-ttu-id="9102f-149">PowerShell importa um arquivo XML, enquanto Olá CLI do Azure importa um arquivo json.</span><span class="sxs-lookup"><span data-stu-id="9102f-149">PowerShell imports an XML file, while hello Azure CLI imports a json file.</span></span> <span data-ttu-id="9102f-150">Se Olá importação falhar, confirme o arquivo hello está em conformidade com hello [esquema de configuração de rede](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="9102f-150">If hello import fails, confirm that hello file complies with hello [network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span> 

### <a name="powershell"></a><span data-ttu-id="9102f-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9102f-151">PowerShell</span></span>
 
1. <span data-ttu-id="9102f-152">[Instale o Azure PowerShell e entrar tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9102f-152">[Install Azure PowerShell and sign in tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="9102f-153">Alterar diretório Olá e nome do arquivo hello comando conforme necessário a seguir, execute o arquivo de configuração de rede Olá comando tooimport hello:</span><span class="sxs-lookup"><span data-stu-id="9102f-153">Change hello directory and filename in hello following command as necessary, then run hello command tooimport hello network configuration file:</span></span>
 
    ```powershell
    Set-AzureVNetConfig  -ConfigurationPath c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a><span data-ttu-id="9102f-154">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="9102f-154">Azure CLI 1.0</span></span>

1. <span data-ttu-id="9102f-155">[Instalar hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9102f-155">[Install hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="9102f-156">Concluir Olá restantes etapas em um prompt de comando do Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="9102f-156">Complete hello remaining steps from an Azure CLI 1.0 command prompt.</span></span>
2. <span data-ttu-id="9102f-157">Fazer logon tooAzure digitando Olá `azure login` comando.</span><span class="sxs-lookup"><span data-stu-id="9102f-157">Log in tooAzure by entering hello `azure login` command.</span></span>
3. <span data-ttu-id="9102f-158">Certifique-se de que você está no modo de asm inserindo Olá `azure config mode asm` comando.</span><span class="sxs-lookup"><span data-stu-id="9102f-158">Ensure you're in asm mode by entering hello `azure config mode asm` command.</span></span>
4. <span data-ttu-id="9102f-159">Alterar diretório Olá e nome do arquivo hello comando conforme necessário a seguir, execute o arquivo de configuração de rede Olá comando tooimport hello:</span><span class="sxs-lookup"><span data-stu-id="9102f-159">Change hello directory and filename in hello following command as necessary, then run hello command tooimport hello network configuration file:</span></span>

    ```azurecli
    azure network import c:\azure\networkconfig.json
    ```
