---
title: "Configurar uma rede virtual do Azure (clássico) - arquivo de configuração de rede | Microsoft Docs"
description: "Saiba como criar e modificar redes virtuais (clássico) exportando, alterando e importando um arquivo de configuração de rede."
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
ms.openlocfilehash: f1e3ae26b6525f2235a6b0d53546b334dc027b94
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="configure-a-virtual-network-classic-using-a-network-configuration-file"></a><span data-ttu-id="e1c6d-103">Configurar uma rede virtual (clássico) usando um arquivo de configuração de rede</span><span class="sxs-lookup"><span data-stu-id="e1c6d-103">Configure a virtual network (classic) using a network configuration file</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e1c6d-104">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e1c6d-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="e1c6d-105">Este artigo aborda o uso do modelo de implantação clássica.</span><span class="sxs-lookup"><span data-stu-id="e1c6d-105">This article covers using the classic deployment model.</span></span> <span data-ttu-id="e1c6d-106">A Microsoft recomenda que a maioria das implantações novas use o modelo de implantação do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="e1c6d-106">Microsoft recommends that most new deployments use the Resource Manager deployment model.</span></span>

<span data-ttu-id="e1c6d-107">Você pode criar e configurar uma rede virtual (clássica) com um arquivo de configuração de rede usando a interface de linha de comando (CLI) 1.0 do Azure ou o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e1c6d-107">You can create and configure a virtual network (classic) with a network configuration file using the Azure command-line interface (CLI) 1.0 or Azure PowerShell.</span></span> <span data-ttu-id="e1c6d-108">Não é possível criar ou modificar uma rede virtual por meio do modelo de implantação do Azure Resource Manager usando um arquivo de configuração de rede.</span><span class="sxs-lookup"><span data-stu-id="e1c6d-108">You cannot create or modify a virtual network through the Azure Resource Manager deployment model using a network configuration file.</span></span> <span data-ttu-id="e1c6d-109">Não é possível utilizar o portal do Azure para criar ou modificar uma rede virtual (clássica) utilizando um arquivo de configuração de rede, no entanto, você pode usar o portal do Azure para criar uma rede virtual (clássica) sem utilizar um arquivo de configuração de rede.</span><span class="sxs-lookup"><span data-stu-id="e1c6d-109">You cannot use the Azure portal to create or modify a virtual network (classic) using a network configuration file, however you can use the Azure portal to create a virtual network (classic), without using a network configuration file.</span></span>

<span data-ttu-id="e1c6d-110">Criar e configurar uma rede virtual (clássica) com um arquivo de configuração de rede requer exportar, alterar e importar o arquivo.</span><span class="sxs-lookup"><span data-stu-id="e1c6d-110">Creating and configuring a virtual network (classic) with a network configuration file requires exporting, changing, and importing the file.</span></span>

## <span data-ttu-id="e1c6d-111"><a name="export"></a>Exportar um arquivo de configuração de rede</span><span class="sxs-lookup"><span data-stu-id="e1c6d-111"><a name="export"></a>Export a network configuration file</span></span>

<span data-ttu-id="e1c6d-112">É possível utilizar o PowerShell ou CLI do Azure para exportar um arquivo de configuração de rede.</span><span class="sxs-lookup"><span data-stu-id="e1c6d-112">You can use PowerShell or the Azure CLI to export a network configuration file.</span></span> <span data-ttu-id="e1c6d-113">O PowerShell exporta um arquivo XML, enquanto a CLI do Azure exporta um arquivo json.</span><span class="sxs-lookup"><span data-stu-id="e1c6d-113">PowerShell exports an XML file, while the Azure CLI exports a json file.</span></span>

### <a name="powershell"></a><span data-ttu-id="e1c6d-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e1c6d-114">PowerShell</span></span>
 
1. <span data-ttu-id="e1c6d-115">[Instalar o Azure PowerShell e entrar no Azure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e1c6d-115">[Install Azure PowerShell and sign in to Azure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="e1c6d-116">Altere o diretório (e certifique-se de que ele existe) e o nome do arquivo no seguinte comando conforme desejado, em seguida, execute o comando para exportar o arquivo de configuração de rede:</span><span class="sxs-lookup"><span data-stu-id="e1c6d-116">Change the directory (and ensure it exists) and filename in the following command as desired, then run the command to export the network configuration file:</span></span>

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a><span data-ttu-id="e1c6d-117">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="e1c6d-117">Azure CLI 1.0</span></span>

1. <span data-ttu-id="e1c6d-118">[Instalar a CLI 1.0 do Azure](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e1c6d-118">[Install the Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="e1c6d-119">Conclua as etapas restantes em um prompt de comando da CLI 1.0 do Azure.</span><span class="sxs-lookup"><span data-stu-id="e1c6d-119">Complete the remaining steps from an Azure CLI 1.0 command prompt.</span></span>
2. <span data-ttu-id="e1c6d-120">Faça logon no Azure digitando o comando `azure login`.</span><span class="sxs-lookup"><span data-stu-id="e1c6d-120">Log in to Azure by entering the `azure login` command.</span></span>
3. <span data-ttu-id="e1c6d-121">Certifique-se de que está no modo de asm inserindo o `azure config mode asm` comando.</span><span class="sxs-lookup"><span data-stu-id="e1c6d-121">Ensure you're in asm mode by entering the `azure config mode asm` command.</span></span>
4. <span data-ttu-id="e1c6d-122">Altere o diretório (e certifique-se de que ele existe) e o nome do arquivo no seguinte comando conforme desejado, em seguida, execute o comando para exportar o arquivo de configuração de rede:</span><span class="sxs-lookup"><span data-stu-id="e1c6d-122">Change the directory (and ensure it exists) and filename in the following command as desired, then run the command to export the network configuration file:</span></span>
    
    ```azurecli
    azure network export c:\azure\networkconfig.json
    ```

## <a name="create-or-modify-a-network-configuration-file"></a><span data-ttu-id="e1c6d-123">Criar ou modificar um arquivo de configuração de rede</span><span class="sxs-lookup"><span data-stu-id="e1c6d-123">Create or modify a network configuration file</span></span>

<span data-ttu-id="e1c6d-124">Um arquivo de configuração de rede é um arquivo XML (ao usar o PowerShell) ou um arquivo json (ao usar a CLI do Azure).</span><span class="sxs-lookup"><span data-stu-id="e1c6d-124">A network configuration file is an XML file (when using PowerShell) or a json file (when using the Azure CLI).</span></span> <span data-ttu-id="e1c6d-125">É possível editar o arquivo em qualquer texto ou editor XML/json.</span><span class="sxs-lookup"><span data-stu-id="e1c6d-125">You can edit the file in any text, or XML/json editor.</span></span> <span data-ttu-id="e1c6d-126">O artigo [Configurações de esquema de arquivo de configuração de rede](https://msdn.microsoft.com/library/azure/jj157100.aspx) inclui detalhes de todas as configurações.</span><span class="sxs-lookup"><span data-stu-id="e1c6d-126">The [Network configuration file schema settings](https://msdn.microsoft.com/library/azure/jj157100.aspx) article includes details for all settings.</span></span> <span data-ttu-id="e1c6d-127">Para obter explicações adicionais sobre as configurações, consulte [Exibir redes virtuais e configurações](virtual-network-manage-network.md#view-vnet).</span><span class="sxs-lookup"><span data-stu-id="e1c6d-127">For additional explanation of the settings, see [View virtual networks and settings](virtual-network-manage-network.md#view-vnet).</span></span> <span data-ttu-id="e1c6d-128">As alterações feitas no arquivo:</span><span class="sxs-lookup"><span data-stu-id="e1c6d-128">The changes you make to the file:</span></span>

- <span data-ttu-id="e1c6d-129">Deverão cumprir o esquema ou a importação do arquivo de configuração da rede falhará.</span><span class="sxs-lookup"><span data-stu-id="e1c6d-129">Must comply with the schema, or importing the network configuration file will fail.</span></span>
- <span data-ttu-id="e1c6d-130">Substituirão todas as configurações de rede existentes para sua assinatura, portanto, tenha extremo cuidado ao realizar as modificações.</span><span class="sxs-lookup"><span data-stu-id="e1c6d-130">Overwrite any existing network settings for your subscription, so use extreme caution when making modifications.</span></span> <span data-ttu-id="e1c6d-131">Por exemplo, faça referência aos exemplos de arquivos de configuração de rede que se seguem.</span><span class="sxs-lookup"><span data-stu-id="e1c6d-131">For example, reference the example network configuration files that follow.</span></span> <span data-ttu-id="e1c6d-132">Digamos que o arquivo original continha duas instâncias **VirtualNetworkSite** e foram alteradas, conforme mostrado nos exemplos.</span><span class="sxs-lookup"><span data-stu-id="e1c6d-132">Say the original file contained two **VirtualNetworkSite** instances, and you changed it, as shown in the examples.</span></span> <span data-ttu-id="e1c6d-133">Ao importar o arquivo, o Azure exclui a rede virtual da instância **VirtualNetworkSite** removida no arquivo.</span><span class="sxs-lookup"><span data-stu-id="e1c6d-133">When you import the file, Azure deletes the virtual network for the **VirtualNetworkSite** instance you removed in the file.</span></span> <span data-ttu-id="e1c6d-134">Esse cenário simplificado não considera recursos na rede virtual, como se existisse, a rede virtual não poderia ser excluída e, a importação falharia.</span><span class="sxs-lookup"><span data-stu-id="e1c6d-134">This simplified scenario assumes no resources were in the virtual network, as if there were, the virtual network could not be deleted, and the import would fail.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e1c6d-135">O Azure considera uma sub-rede com algo implantado como **em uso**.</span><span class="sxs-lookup"><span data-stu-id="e1c6d-135">Azure considers a subnet that has something deployed to it as **in use**.</span></span> <span data-ttu-id="e1c6d-136">Quando uma sub-rede estiver em uso, ela não poderá ser modificada.</span><span class="sxs-lookup"><span data-stu-id="e1c6d-136">When a subnet is in use, it cannot be modified.</span></span> <span data-ttu-id="e1c6d-137">Antes de modificar as informações de sub-rede em um arquivo de configuração de rede, mova todas as implantações existentes na sub-rede para uma sub-rede diferente que não está sendo modificada.</span><span class="sxs-lookup"><span data-stu-id="e1c6d-137">Before modifying subnet information in a network configuration file, move anything that you have deployed to the subnet to a different subnet that isn't being modified.</span></span> <span data-ttu-id="e1c6d-138">Consulte [Mover uma VM ou instância de função para uma sub-rede diferente](virtual-networks-move-vm-role-to-subnet.md) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="e1c6d-138">See [Move a VM or Role Instance to a Different Subnet](virtual-networks-move-vm-role-to-subnet.md) for details.</span></span>

### <a name="example-xml-for-use-with-powershell"></a><span data-ttu-id="e1c6d-139">Exemplo de XML para uso com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="e1c6d-139">Example XML for use with PowerShell</span></span>

<span data-ttu-id="e1c6d-140">O arquivo de configuração de rede de exemplo a seguir cria uma rede virtual nomeada *myVirtualNetwork* com um espaço de endereçamento de *10.0.0.0/16* na regão *Leste dos EUA* do Azure.</span><span class="sxs-lookup"><span data-stu-id="e1c6d-140">The following example network configuration file creates a virtual network named *myVirtualNetwork* with an address space of *10.0.0.0/16* in the *East US* Azure region.</span></span> <span data-ttu-id="e1c6d-141">A rede virtual contém uma sub-rede nomeada *mySubnet* com um prefixo de endereço *10.0.0.0/24*.</span><span class="sxs-lookup"><span data-stu-id="e1c6d-141">The virtual network contains one subnet named *mySubnet* with an address prefix of *10.0.0.0/24*.</span></span>

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

<span data-ttu-id="e1c6d-142">Se o arquivo de configuração de rede que você exportou não contém conteúdo, você pode copiar o XML no exemplo anterior e colá-lo em um novo arquivo.</span><span class="sxs-lookup"><span data-stu-id="e1c6d-142">If the network configuration file you exported contains no contents, you can copy the XML in the previous example, and paste it into a new file.</span></span>

### <a name="example-json-for-use-with-the-azure-cli-10"></a><span data-ttu-id="e1c6d-143">Exemplo JSON para uso com o CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="e1c6d-143">Example JSON for use with the Azure CLI 1.0</span></span>

<span data-ttu-id="e1c6d-144">O arquivo de configuração de rede de exemplo a seguir cria uma rede virtual nomeada *myVirtualNetwork* com um espaço de endereçamento de *10.0.0.0/16* na regão *Leste dos EUA* do Azure.</span><span class="sxs-lookup"><span data-stu-id="e1c6d-144">The following example network configuration file creates a virtual network named *myVirtualNetwork* with an address space of *10.0.0.0/16* in the *East US* Azure region.</span></span> <span data-ttu-id="e1c6d-145">A rede virtual contém uma sub-rede nomeada *mySubnet* com um prefixo de endereço *10.0.0.0/24*.</span><span class="sxs-lookup"><span data-stu-id="e1c6d-145">The virtual network contains one subnet named *mySubnet* with an address prefix of *10.0.0.0/24*.</span></span>

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

<span data-ttu-id="e1c6d-146">Se o arquivo de configuração de rede que você exportou não contém conteúdo, você pode copiar o json no exemplo anterior e colá-lo em um novo arquivo.</span><span class="sxs-lookup"><span data-stu-id="e1c6d-146">If the network configuration file you exported contains no contents, you can copy the json in the previous example, and paste it into a new file.</span></span>

## <span data-ttu-id="e1c6d-147"><a name="import"></a>Importar um arquivo de configuração de rede</span><span class="sxs-lookup"><span data-stu-id="e1c6d-147"><a name="import"></a>Import a network configuration file</span></span>

<span data-ttu-id="e1c6d-148">Você pode utilizar o PowerShell ou a CLI do Azure para importar um arquivo de configuração de rede.</span><span class="sxs-lookup"><span data-stu-id="e1c6d-148">You can use PowerShell or the Azure CLI to import a network configuration file.</span></span> <span data-ttu-id="e1c6d-149">O PowerShell exporta um arquivo XML, enquanto a CLI do Azure exporta um arquivo json.</span><span class="sxs-lookup"><span data-stu-id="e1c6d-149">PowerShell imports an XML file, while the Azure CLI imports a json file.</span></span> <span data-ttu-id="e1c6d-150">Se a importação falhar, confirme se o arquivo está em conformidade com o [esquema de configuração de rede](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="e1c6d-150">If the import fails, confirm that the file complies with the [network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span> 

### <a name="powershell"></a><span data-ttu-id="e1c6d-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e1c6d-151">PowerShell</span></span>
 
1. <span data-ttu-id="e1c6d-152">[Instalar o Azure PowerShell e entrar no Azure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e1c6d-152">[Install Azure PowerShell and sign in to Azure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="e1c6d-153">Altere o diretório e o nome do arquivo no seguinte comando, conforme necessário, e execute o comando para importar o arquivo de configuração de rede:</span><span class="sxs-lookup"><span data-stu-id="e1c6d-153">Change the directory and filename in the following command as necessary, then run the command to import the network configuration file:</span></span>
 
    ```powershell
    Set-AzureVNetConfig  -ConfigurationPath c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a><span data-ttu-id="e1c6d-154">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="e1c6d-154">Azure CLI 1.0</span></span>

1. <span data-ttu-id="e1c6d-155">[Instalar a CLI 1.0 do Azure](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e1c6d-155">[Install the Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="e1c6d-156">Conclua as etapas restantes em um prompt de comando da CLI 1.0 do Azure.</span><span class="sxs-lookup"><span data-stu-id="e1c6d-156">Complete the remaining steps from an Azure CLI 1.0 command prompt.</span></span>
2. <span data-ttu-id="e1c6d-157">Faça logon no Azure digitando o comando `azure login`.</span><span class="sxs-lookup"><span data-stu-id="e1c6d-157">Log in to Azure by entering the `azure login` command.</span></span>
3. <span data-ttu-id="e1c6d-158">Certifique-se de que está no modo de asm inserindo o `azure config mode asm` comando.</span><span class="sxs-lookup"><span data-stu-id="e1c6d-158">Ensure you're in asm mode by entering the `azure config mode asm` command.</span></span>
4. <span data-ttu-id="e1c6d-159">Altere o diretório e o nome do arquivo no seguinte comando, conforme necessário, e execute o comando para importar o arquivo de configuração de rede:</span><span class="sxs-lookup"><span data-stu-id="e1c6d-159">Change the directory and filename in the following command as necessary, then run the command to import the network configuration file:</span></span>

    ```azurecli
    azure network import c:\azure\networkconfig.json
    ```
