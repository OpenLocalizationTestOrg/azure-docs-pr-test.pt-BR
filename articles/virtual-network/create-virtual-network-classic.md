---
title: "Criar uma rede virtual do Azure (clássica) com várias sub-redes | Microsoft Docs"
description: "Saiba como criar uma rede virtual (clássica) com várias sub-redes no Azure."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: 95c2f4fe40590a8d809f634fb5b2c92d07421bb0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-virtual-network-classic-with-multiple-subnets"></a><span data-ttu-id="a407b-103">Criar uma rede virtual (clássica) com várias sub-redes</span><span class="sxs-lookup"><span data-stu-id="a407b-103">Create a virtual network (classic) with multiple subnets</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a407b-104">O Azure tem dois [modelos de implantação diferentes](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) para criar e trabalhar com recursos: Resource Manager e clássico.</span><span class="sxs-lookup"><span data-stu-id="a407b-104">Azure has two [different deployment models](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) for creating and working with resources: Resource Manager and classic.</span></span> <span data-ttu-id="a407b-105">Este artigo aborda o uso do modelo de implantação clássica.</span><span class="sxs-lookup"><span data-stu-id="a407b-105">This article covers using the classic deployment model.</span></span> <span data-ttu-id="a407b-106">A Microsoft recomenda criar a maioria das novas redes virtuais por meio do modelo de implantação do [Resource Manager](virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="a407b-106">Microsoft recommends creating most new virtual networks through the [Resource Manager](virtual-networks-create-vnet-arm-pportal.md) deployment model.</span></span>

<span data-ttu-id="a407b-107">Neste tutorial, aprenda como criar uma rede virtual do Azure básica (clássica) que tenha sub-redes públicas e privadas separadas.</span><span class="sxs-lookup"><span data-stu-id="a407b-107">In this tutorial, learn how to create a basic Azure virtual network (classic) that has separate public and private subnets.</span></span> <span data-ttu-id="a407b-108">Você pode criar recursos do Azure, como Máquinas virtuais e Serviços de nuvem em uma sub-rede.</span><span class="sxs-lookup"><span data-stu-id="a407b-108">You can create Azure resources, like Virtual machines and Cloud services in a subnet.</span></span> <span data-ttu-id="a407b-109">Recursos criados em redes virtuais (clássicas) podem se comunicar entre si e com os recursos em outras redes conectadas a uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="a407b-109">Resources created in virtual networks (classic) can communicate with each other, and with resources in other networks connected to a virtual network.</span></span>

<span data-ttu-id="a407b-110">Saiba mais sobre todas as configurações de [rede virtual](virtual-network-manage-network.md) e [sub-rede](virtual-network-manage-subnet.md).</span><span class="sxs-lookup"><span data-stu-id="a407b-110">Learn more about all [virtual network](virtual-network-manage-network.md) and [subnet](virtual-network-manage-subnet.md) settings.</span></span>

> [!WARNING]
> <span data-ttu-id="a407b-111">Redes virtuais (clássicas) são excluídas imediatamente pelo Azure quando uma [assinatura é desabilitada](../billing/billing-subscription-become-disable.md?toc=%2fazure%2fvirtual-network%2ftoc.json#you-reached-your-spending-limit).</span><span class="sxs-lookup"><span data-stu-id="a407b-111">Virtual networks (classic) are immediately deleted by Azure when a [subscription is disabled](../billing/billing-subscription-become-disable.md?toc=%2fazure%2fvirtual-network%2ftoc.json#you-reached-your-spending-limit).</span></span> <span data-ttu-id="a407b-112">Redes virtuais (clássicas) são excluídas independentemente de existirem recursos na rede virtual.</span><span class="sxs-lookup"><span data-stu-id="a407b-112">Virtual networks (classic) are deleted regardless of whether resources exist in the virtual network.</span></span> <span data-ttu-id="a407b-113">Se você depois voltar a habilitar a assinatura, os recursos que existiam na rede virtual deverão ser recriados.</span><span class="sxs-lookup"><span data-stu-id="a407b-113">If you later re-enable the subscription, resources that existed in the virtual network must be recreated.</span></span>

<span data-ttu-id="a407b-114">Você pode criar uma rede virtual (clássica) usando o [portal do Azure](#portal), o [a CLI (interface de linha de comando) 1.0 do Azure](#azure-cli) ou o [PowerShell](#powershell).</span><span class="sxs-lookup"><span data-stu-id="a407b-114">You can create a virtual network (classic) by using the [Azure portal](#portal), the [Azure command-line interface (CLI) 1.0](#azure-cli), or [PowerShell](#powershell).</span></span>

## <a name="portal"></a><span data-ttu-id="a407b-115">Portal</span><span class="sxs-lookup"><span data-stu-id="a407b-115">Portal</span></span>

1. <span data-ttu-id="a407b-116">Em um navegador da Internet, vá para o [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a407b-116">In an Internet browser, go to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="a407b-117">Faça logon usando sua [conta do Azure](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="a407b-117">Log in using your [Azure account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="a407b-118">Se não tiver uma conta do Azure, você poderá assinar uma versão de [avaliação gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="a407b-118">If you don't have an Azure account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="a407b-119">Clique em **+Novo** no portal.</span><span class="sxs-lookup"><span data-stu-id="a407b-119">Click **+New** in the portal.</span></span>
3. <span data-ttu-id="a407b-120">Digite *Rede virtual* na caixa **Pesquisar no Marketplace** na parte superior da folha **Novo** que aparece.</span><span class="sxs-lookup"><span data-stu-id="a407b-120">Enter *Virtual network* in the **Search the Marketplace** box at the top of the **New** blade that appears.</span></span>  <span data-ttu-id="a407b-121">Clique em **Rede virtual** quando essa opção aparecer entre os resultados da pesquisa.</span><span class="sxs-lookup"><span data-stu-id="a407b-121">Click **Virtual network** when it appears in the search results.</span></span>
4. <span data-ttu-id="a407b-122">Selecione **Clássico** na caixa **Selecionar um modelo de implantação** na folha **Rede Virtual** que aparece e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="a407b-122">Select **Classic** in the **Select a deployment model** box in the **Virtual Network** blade that appears, then click **Create**.</span></span> 
5. <span data-ttu-id="a407b-123">Insira os seguintes valores na folha **Criar rede virtual (clássica)** e depois clique em **Criar**:</span><span class="sxs-lookup"><span data-stu-id="a407b-123">Enter the following values on the **Create virtual network (classic)** blade and then click **Create**:</span></span>

    |<span data-ttu-id="a407b-124">Configuração</span><span class="sxs-lookup"><span data-stu-id="a407b-124">Setting</span></span>|<span data-ttu-id="a407b-125">Valor</span><span class="sxs-lookup"><span data-stu-id="a407b-125">Value</span></span>|
    |---|---|
    |<span data-ttu-id="a407b-126">Nome</span><span class="sxs-lookup"><span data-stu-id="a407b-126">Name</span></span>|<span data-ttu-id="a407b-127">myVnet</span><span class="sxs-lookup"><span data-stu-id="a407b-127">myVnet</span></span>|
    |<span data-ttu-id="a407b-128">Espaço de endereço</span><span class="sxs-lookup"><span data-stu-id="a407b-128">Address space</span></span>|<span data-ttu-id="a407b-129">10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="a407b-129">10.0.0.0/16</span></span>|
    |<span data-ttu-id="a407b-130">Nome da sub-rede</span><span class="sxs-lookup"><span data-stu-id="a407b-130">Subnet name</span></span>|<span data-ttu-id="a407b-131">Público</span><span class="sxs-lookup"><span data-stu-id="a407b-131">Public</span></span>|
    |<span data-ttu-id="a407b-132">Intervalo de endereços da sub-rede</span><span class="sxs-lookup"><span data-stu-id="a407b-132">Subnet address range</span></span>|<span data-ttu-id="a407b-133">10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="a407b-133">10.0.0.0/24</span></span>|
    |<span data-ttu-id="a407b-134">Grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="a407b-134">Resource group</span></span>|<span data-ttu-id="a407b-135">Deixe **Criar novo** selecionado e digite **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="a407b-135">Leave **Create new** selected, and then enter **myResourceGroup**.</span></span>|
    |<span data-ttu-id="a407b-136">Assinatura e localização</span><span class="sxs-lookup"><span data-stu-id="a407b-136">Subscription and location</span></span>|<span data-ttu-id="a407b-137">Selecione sua assinatura e localização.</span><span class="sxs-lookup"><span data-stu-id="a407b-137">Select your subscription and location.</span></span>

    <span data-ttu-id="a407b-138">Se você for novo no Azure, saiba mais sobre [grupos de recursos](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [assinaturas](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription) e [locais](https://azure.microsoft.com/regions) (também conhecido como *regiões*).</span><span class="sxs-lookup"><span data-stu-id="a407b-138">If you're new to Azure, learn more about [resource groups](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [subscriptions](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), and [locations](https://azure.microsoft.com/regions) (also referred to as *regions*).</span></span>
4. <span data-ttu-id="a407b-139">No portal, você pode criar apenas uma sub-rede quando você criar uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="a407b-139">In the portal, you can create only one subnet when you create a virtual network.</span></span> <span data-ttu-id="a407b-140">Neste tutorial, você cria uma segunda sub-rede após criar a rede virtual.</span><span class="sxs-lookup"><span data-stu-id="a407b-140">In this tutorial, you create a second subnet after you create the virtual network.</span></span> <span data-ttu-id="a407b-141">Posteriormente, você pode criar recursos acessíveis pela Internet na sub-rede **Pública**.</span><span class="sxs-lookup"><span data-stu-id="a407b-141">You might later create Internet-accessible resources in the **Public** subnet.</span></span> <span data-ttu-id="a407b-142">Você também pode criar recursos que não são acessíveis pela Internet para na sub-rede **Privada**.</span><span class="sxs-lookup"><span data-stu-id="a407b-142">You also might create resources that aren't accessible from the Internet in the **Private** subnet.</span></span> <span data-ttu-id="a407b-143">Para criar a segunda sub-rede, digite **myVnet** na caixa **Pesquisar recursos** na parte superior da página.</span><span class="sxs-lookup"><span data-stu-id="a407b-143">To create the second subnet, enter **myVnet** in the **Search resources** box at the top of the page.</span></span> <span data-ttu-id="a407b-144">Clique em **myVnet** quando ele for exibido nos resultados da pesquisa.</span><span class="sxs-lookup"><span data-stu-id="a407b-144">Click **myVnet** when it appears in the search results.</span></span>
5. <span data-ttu-id="a407b-145">Clique em **Sub-redes** (na seção **CONFIGURAÇÕES**) na folha **Criar rede virtual (clássica)** que aparece.</span><span class="sxs-lookup"><span data-stu-id="a407b-145">Click **Subnets** (in the **SETTINGS** section) on the **Create virtual network (classic)** blade that appears.</span></span>
6. <span data-ttu-id="a407b-146">Clique em **+Adicionar** na folha **myVnet – Sub-redes** que aparece.</span><span class="sxs-lookup"><span data-stu-id="a407b-146">Click **+Add** on the **myVnet - Subnets** blade that appears.</span></span>
7. <span data-ttu-id="a407b-147">Digite **Privada** para **Nome** na folha **Adicionar sub-rede**.</span><span class="sxs-lookup"><span data-stu-id="a407b-147">Enter **Private** for **Name** on the **Add subnet** blade.</span></span> <span data-ttu-id="a407b-148">Digite **10.0.1.0/24** para **Intervalo de endereços**.</span><span class="sxs-lookup"><span data-stu-id="a407b-148">Enter **10.0.1.0/24** for **Address range**.</span></span>  <span data-ttu-id="a407b-149">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="a407b-149">Click **OK**.</span></span>
8. <span data-ttu-id="a407b-150">Na folha **myVnet – Sub-redes**, você pode ver as sub-redes **Pública** e **Privada** que você criou.</span><span class="sxs-lookup"><span data-stu-id="a407b-150">On the **myVnet - Subnets** blade, you can see the **Public** and **Private** subnets that you created.</span></span>
9. <span data-ttu-id="a407b-151">**Opcional**: quando você concluir este tutorial, talvez queira excluir os recursos criados para não incorrer em encargos de uso:</span><span class="sxs-lookup"><span data-stu-id="a407b-151">**Optional**: When you finish this tutorial, you might want to delete the resources that you created, so that you don't incur usage charges:</span></span>
    - <span data-ttu-id="a407b-152">Clique em **Visão geral** na folha **myVnet**.</span><span class="sxs-lookup"><span data-stu-id="a407b-152">Click **Overview** on the **myVnet** blade.</span></span>
    - <span data-ttu-id="a407b-153">Clique no ícone **Excluir** na folha **myVnet**.</span><span class="sxs-lookup"><span data-stu-id="a407b-153">Click the **Delete** icon on the **myVnet** blade.</span></span>
    - <span data-ttu-id="a407b-154">Para confirmar a exclusão, clique em **Sim** na caixa **Excluir rede virtual**.</span><span class="sxs-lookup"><span data-stu-id="a407b-154">To confirm the deletion, click **Yes** in the **Delete virtual network** box.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="a407b-155">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="a407b-155">Azure CLI</span></span>

1. <span data-ttu-id="a407b-156">Você pode [instalar e configurar a CLI do Azure](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) ou usar a CLI no Azure Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="a407b-156">You can either [install and configure the Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json), or use the CLI within the Azure Cloud Shell.</span></span> <span data-ttu-id="a407b-157">O Azure Cloud Shell é um shell Bash gratuito que podem ser executado diretamente no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a407b-157">The Azure Cloud Shell is a free Bash shell that you can run directly within the Azure portal.</span></span> <span data-ttu-id="a407b-158">Ele tem a CLI do Azure instalada e configurada para usar com sua conta.</span><span class="sxs-lookup"><span data-stu-id="a407b-158">It has the Azure CLI preinstalled and configured to use with your account.</span></span> <span data-ttu-id="a407b-159">Para obter ajuda sobre os comandos da CLI, digite `azure <command> --help`.</span><span class="sxs-lookup"><span data-stu-id="a407b-159">To get help for CLI commands, type `azure <command> --help`.</span></span> 
2. <span data-ttu-id="a407b-160">Em uma sessão da CLI, faça logon no Azure com o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="a407b-160">In a CLI session, log in to Azure with the command that follows.</span></span> <span data-ttu-id="a407b-161">Se você clicar em **Experimente** na caixa abaixo, um Cloud Shell será aberto.</span><span class="sxs-lookup"><span data-stu-id="a407b-161">If you click **Try it** in the box below, a Cloud Shell opens.</span></span> <span data-ttu-id="a407b-162">Você pode fazer logon sua assinatura do Azure sem digitar o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="a407b-162">You can log in to your Azure subscription, without entering the following command:</span></span>

    ```azurecli-interactive
    azure login
    ```

3. <span data-ttu-id="a407b-163">Para garantir que a CLI esteja no modo de Gerenciamento de Serviço, digite o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="a407b-163">To ensure the CLI is in Service Management mode, enter the following command:</span></span>

    ```azurecli-interactive
    azure config mode asm
    ```

4. <span data-ttu-id="a407b-164">Crie uma rede virtual com uma sub-rede privada:</span><span class="sxs-lookup"><span data-stu-id="a407b-164">Create a virtual network with a private subnet:</span></span>

    ```azurecli-interactive
    azure network vnet create --vnet myVnet --address-space 10.0.0.0 --cidr 16  --subnet-name Private --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --location "East US"
    ```

5. <span data-ttu-id="a407b-165">Crie uma sub-rede pública dentro da rede virtual:</span><span class="sxs-lookup"><span data-stu-id="a407b-165">Create a public subnet within the virtual network:</span></span>

    ```azurecli-interactive
    azure network vnet subnet create --name Public --vnet-name myVnet --address-prefix 10.0.1.0/24
    ```    
    
6. <span data-ttu-id="a407b-166">Examine a rede virtual e as sub-redes:</span><span class="sxs-lookup"><span data-stu-id="a407b-166">Review the virtual network and subnets:</span></span>

    ```azurecli-interactive
    azure network vnet show --vnet myVnet
    ```

7. <span data-ttu-id="a407b-167">**Opcional**: talvez queira excluir os recursos criados quando você concluir este tutorial para não incorrer em encargos de uso:</span><span class="sxs-lookup"><span data-stu-id="a407b-167">**Optional**: You might want to delete the resources that you created when you finish this tutorial, so that you don't incur usage charges:</span></span>

    ```azurecli-interactive
    azure network vnet delete --vnet myVnet --quiet
    ```

> [!NOTE]
> <span data-ttu-id="a407b-168">Embora você não possa especificar um grupo de recursos para criar uma rede virtual (clássica) usando a CLI, o Azure cria a rede virtual em um grupo de recursos denominado *Rede Padrão*.</span><span class="sxs-lookup"><span data-stu-id="a407b-168">Though you can't specify a resource group to create a virtual network (classic) in using the CLI, Azure creates the virtual network in a resource group named *Default-Networking*.</span></span>

## <a name="powershell"></a><span data-ttu-id="a407b-169">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a407b-169">PowerShell</span></span>

1. <span data-ttu-id="a407b-170">Instale a última versão do módulo [Azure](https://www.powershellgallery.com/packages/Azure) do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a407b-170">Install the latest version of the PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) module.</span></span> <span data-ttu-id="a407b-171">Se você for novo no Azure PowerShell, consulte [Visão geral do Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a407b-171">If you're new to Azure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="a407b-172">Inicie uma sessão do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a407b-172">Start a PowerShell session.</span></span>
3. <span data-ttu-id="a407b-173">No PowerShell, faça logon no Azure inserindo o comando `Add-AzureAccount`.</span><span class="sxs-lookup"><span data-stu-id="a407b-173">In PowerShell, log in to Azure by entering the `Add-AzureAccount` command.</span></span>
4. <span data-ttu-id="a407b-174">Altere o seguinte caminho e nome de arquivo, conforme apropriado, então exporte o arquivo de configuração de rede existente:</span><span class="sxs-lookup"><span data-stu-id="a407b-174">Change the following path and filename, as appropriate, then export your existing network configuration file:</span></span>

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
    ```

5. <span data-ttu-id="a407b-175">Para criar uma rede virtual com sub-redes públicas e privadas, use qualquer editor de texto para adicionar elemento **VirtualNetworkSite** que segue o arquivo de configuração de rede.</span><span class="sxs-lookup"><span data-stu-id="a407b-175">To create a virtual network with public and private subnets, use any text editor to add the **VirtualNetworkSite** element that follows to the network configuration file.</span></span>

    ```xml
    <VirtualNetworkSite name="myVnet" Location="East US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Private">
            <AddressPrefix>10.0.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Public">
            <AddressPrefix>10.0.1.0/24</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    ```

    <span data-ttu-id="a407b-176">Examine o [esquema de arquivo de configuração de rede](https://msdn.microsoft.com/library/azure/jj157100.aspx) completo.</span><span class="sxs-lookup"><span data-stu-id="a407b-176">Review the full [network configuration file schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>

6. <span data-ttu-id="a407b-177">Importe o arquivo de configuração de rede:</span><span class="sxs-lookup"><span data-stu-id="a407b-177">Import the network configuration file:</span></span>

    ```powershell
    Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
    ```

    > [!WARNING]
    > <span data-ttu-id="a407b-178">Importar um arquivo de configuração de rede alterado pode causar alterações em redes virtuais existentes (clássico) na sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="a407b-178">Importing a changed network configuration file can cause changes to existing virtual networks (classic) in your subscription.</span></span> <span data-ttu-id="a407b-179">Verifique se você adicionou apenas a rede virtual anterior e se você não alterou nem removeu nenhuma rede virtual existente da sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="a407b-179">Ensure you only add the previous virtual network and that you don't change or remove any existing virtual networks from your subscription.</span></span> 

7. <span data-ttu-id="a407b-180">Examine a rede virtual e as sub-redes:</span><span class="sxs-lookup"><span data-stu-id="a407b-180">Review the virtual network and subnets:</span></span>

    ```powershell
    Get-AzureVNetSite -VNetName "myVnet"
    ```

8. <span data-ttu-id="a407b-181">**Opcional**: talvez você queira excluir os recursos criados ao concluir este tutorial para não incorrer em encargos de uso.</span><span class="sxs-lookup"><span data-stu-id="a407b-181">**Optional**: You might want to delete the resources that you created when you finish this tutorial, so that you don't incur usage charges.</span></span> <span data-ttu-id="a407b-182">Para excluir a rede virtual, conclua as etapas 4 a 6 novamente, desta vez removendo o elemento **VirtualNetworkSite** adicionado na etapa 5.</span><span class="sxs-lookup"><span data-stu-id="a407b-182">To delete the virtual network, complete steps 4-6 again, this time removing the **VirtualNetworkSite** element you added in step 5.</span></span>
 
> [!NOTE]
> <span data-ttu-id="a407b-183">Embora você não possa especificar um grupo de recursos para criar uma rede virtual (clássica) usando a o PowerShell, o Azure cria a rede virtual em um grupo de recursos denominado *Default-Networking*.</span><span class="sxs-lookup"><span data-stu-id="a407b-183">Though you can't specify a resource group to create a virtual network (classic) in using PowerShell, Azure creates the virtual network in a resource group named *Default-Networking*.</span></span>

---

## <a name="next-steps"></a><span data-ttu-id="a407b-184">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a407b-184">Next steps</span></span>

- <span data-ttu-id="a407b-185">Para saber mais sobre todas as configurações de sub-rede e rede virtual, confira [Gerenciar redes virtuais](virtual-network-manage-network.md) e [Gerenciar sub-redes da rede virtual](virtual-network-manage-subnet.md).</span><span class="sxs-lookup"><span data-stu-id="a407b-185">To learn about all virtual network and subnet settings, see [Manage virtual networks](virtual-network-manage-network.md) and [Manage virtual network subnets](virtual-network-manage-subnet.md).</span></span> <span data-ttu-id="a407b-186">Você tem várias opções para o uso de redes virtuais e sub-redes em um ambiente de produção para atender aos requisitos diferentes.</span><span class="sxs-lookup"><span data-stu-id="a407b-186">You have various options for using virtual networks and subnets in a production environment to meet different requirements.</span></span>
- <span data-ttu-id="a407b-187">Para filtrar o tráfego de entrada e saída da sub-rede, crie e aplique [grupos de segurança de rede](virtual-networks-nsg.md) às sub-redes.</span><span class="sxs-lookup"><span data-stu-id="a407b-187">To filter inbound and outbound subnet traffic, create and apply [network security groups](virtual-networks-nsg.md) to subnets.</span></span>
- <span data-ttu-id="a407b-188">Crie uma máquina virtual [Windows](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) ou [Linux](../virtual-machines/linux/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) e a conecte a uma rede virtual existente.</span><span class="sxs-lookup"><span data-stu-id="a407b-188">Create a [Windows](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) or a [Linux](../virtual-machines/linux/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) virtual machine, and then connect it to an existing virtual network.</span></span>
- <span data-ttu-id="a407b-189">Para conectar duas redes virtuais no mesmo local do Azure, crie um [emparelhamento de rede virtual](create-peering-different-deployment-models.md) entre as redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="a407b-189">To connect two virtual networks in the same Azure location, create a  [virtual network peering](create-peering-different-deployment-models.md) between the virtual networks.</span></span> <span data-ttu-id="a407b-190">Você pode emparelhar uma rede virtual (Resource Manager) a uma rede virtual (clássica), mas não é possível criar um emparelhamento entre duas redes virtuais (clássicas).</span><span class="sxs-lookup"><span data-stu-id="a407b-190">You can peer a virtual network (Resource Manager) to a virtual network (classic), but you cannot create a peering between two virtual networks (classic).</span></span>
- <span data-ttu-id="a407b-191">Conecte a rede virtual a uma rede local usando um [Gateway de VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) ou circuito do [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a407b-191">Connect the virtual network to an on-premises network by using a [VPN Gateway](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) or [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) circuit.</span></span>
