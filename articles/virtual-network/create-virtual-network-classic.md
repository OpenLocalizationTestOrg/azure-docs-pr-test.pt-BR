---
title: "uma rede virtual do Azure (clássica) com várias sub-redes do aaaCreate | Microsoft Docs"
description: "Saiba como toocreate uma rede virtual (clássica) com várias sub-redes no Azure."
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
ms.openlocfilehash: cc7b9ad08d5c26dba09584762bedf614d2847032
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-classic-with-multiple-subnets"></a><span data-ttu-id="280a1-103">Criar uma rede virtual (clássica) com várias sub-redes</span><span class="sxs-lookup"><span data-stu-id="280a1-103">Create a virtual network (classic) with multiple subnets</span></span>

> [!IMPORTANT]
> <span data-ttu-id="280a1-104">O Azure tem dois [modelos de implantação diferentes](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) para criar e trabalhar com recursos: Resource Manager e clássico.</span><span class="sxs-lookup"><span data-stu-id="280a1-104">Azure has two [different deployment models](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) for creating and working with resources: Resource Manager and classic.</span></span> <span data-ttu-id="280a1-105">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="280a1-105">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="280a1-106">A Microsoft recomenda criar a maioria das novas redes virtuais por meio de saudação [Gerenciador de recursos de](virtual-networks-create-vnet-arm-pportal.md) modelo de implantação.</span><span class="sxs-lookup"><span data-stu-id="280a1-106">Microsoft recommends creating most new virtual networks through hello [Resource Manager](virtual-networks-create-vnet-arm-pportal.md) deployment model.</span></span>

<span data-ttu-id="280a1-107">Neste tutorial, saiba como toocreate uma básica rede virtual do Azure (clássica) que tem separada subredes públicas e privadas.</span><span class="sxs-lookup"><span data-stu-id="280a1-107">In this tutorial, learn how toocreate a basic Azure virtual network (classic) that has separate public and private subnets.</span></span> <span data-ttu-id="280a1-108">Você pode criar recursos do Azure, como Máquinas virtuais e Serviços de nuvem em uma sub-rede.</span><span class="sxs-lookup"><span data-stu-id="280a1-108">You can create Azure resources, like Virtual machines and Cloud services in a subnet.</span></span> <span data-ttu-id="280a1-109">Recursos criados em redes virtuais (clássico) podem se comunicar entre si e com recursos em outra rede virtual de tooa conectado de redes.</span><span class="sxs-lookup"><span data-stu-id="280a1-109">Resources created in virtual networks (classic) can communicate with each other, and with resources in other networks connected tooa virtual network.</span></span>

<span data-ttu-id="280a1-110">Saiba mais sobre todas as configurações de [rede virtual](virtual-network-manage-network.md) e [sub-rede](virtual-network-manage-subnet.md).</span><span class="sxs-lookup"><span data-stu-id="280a1-110">Learn more about all [virtual network](virtual-network-manage-network.md) and [subnet](virtual-network-manage-subnet.md) settings.</span></span>

> [!WARNING]
> <span data-ttu-id="280a1-111">Redes virtuais (clássicas) são excluídas imediatamente pelo Azure quando uma [assinatura é desabilitada](../billing/billing-subscription-become-disable.md?toc=%2fazure%2fvirtual-network%2ftoc.json#you-reached-your-spending-limit).</span><span class="sxs-lookup"><span data-stu-id="280a1-111">Virtual networks (classic) are immediately deleted by Azure when a [subscription is disabled](../billing/billing-subscription-become-disable.md?toc=%2fazure%2fvirtual-network%2ftoc.json#you-reached-your-spending-limit).</span></span> <span data-ttu-id="280a1-112">Redes virtuais (clássicas) serão excluídas independentemente de existirem recursos na rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="280a1-112">Virtual networks (classic) are deleted regardless of whether resources exist in hello virtual network.</span></span> <span data-ttu-id="280a1-113">Se você habilitar mais tarde novamente assinatura hello, recursos que existiam na rede virtual Olá devem ser recriados.</span><span class="sxs-lookup"><span data-stu-id="280a1-113">If you later re-enable hello subscription, resources that existed in hello virtual network must be recreated.</span></span>

<span data-ttu-id="280a1-114">Você pode criar uma rede virtual (clássica) usando Olá [portal do Azure](#portal), Olá [Azure interface de linha de comando (CLI) 1.0](#azure-cli), ou [PowerShell](#powershell).</span><span class="sxs-lookup"><span data-stu-id="280a1-114">You can create a virtual network (classic) by using hello [Azure portal](#portal), hello [Azure command-line interface (CLI) 1.0](#azure-cli), or [PowerShell](#powershell).</span></span>

## <a name="portal"></a><span data-ttu-id="280a1-115">Portal</span><span class="sxs-lookup"><span data-stu-id="280a1-115">Portal</span></span>

1. <span data-ttu-id="280a1-116">Em um navegador da Internet, vá toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="280a1-116">In an Internet browser, go toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="280a1-117">Faça logon usando sua [conta do Azure](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="280a1-117">Log in using your [Azure account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="280a1-118">Se não tiver uma conta do Azure, você poderá assinar uma versão de [avaliação gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="280a1-118">If you don't have an Azure account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="280a1-119">Clique em **+ novo** no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="280a1-119">Click **+New** in hello portal.</span></span>
3. <span data-ttu-id="280a1-120">Digite *rede Virtual* em Olá **Olá pesquisa Marketplace** caixa na parte superior de saudação do hello **novo** folha que aparece.</span><span class="sxs-lookup"><span data-stu-id="280a1-120">Enter *Virtual network* in hello **Search hello Marketplace** box at hello top of hello **New** blade that appears.</span></span>  <span data-ttu-id="280a1-121">Clique em **rede Virtual** quando ele aparece nos resultados da pesquisa hello.</span><span class="sxs-lookup"><span data-stu-id="280a1-121">Click **Virtual network** when it appears in hello search results.</span></span>
4. <span data-ttu-id="280a1-122">Selecione **clássico** em Olá **selecionar um modelo de implantação** caixa Olá **rede Virtual** folha que aparece, clique **criar**.</span><span class="sxs-lookup"><span data-stu-id="280a1-122">Select **Classic** in hello **Select a deployment model** box in hello **Virtual Network** blade that appears, then click **Create**.</span></span> 
5. <span data-ttu-id="280a1-123">Digite hello valores a seguir no hello **criar rede virtual (clássica)** folha e depois clique em **criar**:</span><span class="sxs-lookup"><span data-stu-id="280a1-123">Enter hello following values on hello **Create virtual network (classic)** blade and then click **Create**:</span></span>

    |<span data-ttu-id="280a1-124">Configuração</span><span class="sxs-lookup"><span data-stu-id="280a1-124">Setting</span></span>|<span data-ttu-id="280a1-125">Valor</span><span class="sxs-lookup"><span data-stu-id="280a1-125">Value</span></span>|
    |---|---|
    |<span data-ttu-id="280a1-126">Nome</span><span class="sxs-lookup"><span data-stu-id="280a1-126">Name</span></span>|<span data-ttu-id="280a1-127">myVnet</span><span class="sxs-lookup"><span data-stu-id="280a1-127">myVnet</span></span>|
    |<span data-ttu-id="280a1-128">Espaço de endereço</span><span class="sxs-lookup"><span data-stu-id="280a1-128">Address space</span></span>|<span data-ttu-id="280a1-129">10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="280a1-129">10.0.0.0/16</span></span>|
    |<span data-ttu-id="280a1-130">Nome da sub-rede</span><span class="sxs-lookup"><span data-stu-id="280a1-130">Subnet name</span></span>|<span data-ttu-id="280a1-131">Público</span><span class="sxs-lookup"><span data-stu-id="280a1-131">Public</span></span>|
    |<span data-ttu-id="280a1-132">Intervalo de endereços da sub-rede</span><span class="sxs-lookup"><span data-stu-id="280a1-132">Subnet address range</span></span>|<span data-ttu-id="280a1-133">10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="280a1-133">10.0.0.0/24</span></span>|
    |<span data-ttu-id="280a1-134">Grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="280a1-134">Resource group</span></span>|<span data-ttu-id="280a1-135">Deixe **Criar novo** selecionado e digite **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="280a1-135">Leave **Create new** selected, and then enter **myResourceGroup**.</span></span>|
    |<span data-ttu-id="280a1-136">Assinatura e localização</span><span class="sxs-lookup"><span data-stu-id="280a1-136">Subscription and location</span></span>|<span data-ttu-id="280a1-137">Selecione sua assinatura e localização.</span><span class="sxs-lookup"><span data-stu-id="280a1-137">Select your subscription and location.</span></span>

    <span data-ttu-id="280a1-138">Se você for novo tooAzure, saiba mais sobre [grupos de recursos](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [assinaturas](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), e [locais](https://azure.microsoft.com/regions) (também chamado tooas *regiões*).</span><span class="sxs-lookup"><span data-stu-id="280a1-138">If you're new tooAzure, learn more about [resource groups](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [subscriptions](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), and [locations](https://azure.microsoft.com/regions) (also referred tooas *regions*).</span></span>
4. <span data-ttu-id="280a1-139">No portal de saudação, você pode criar apenas uma sub-rede quando você criar uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="280a1-139">In hello portal, you can create only one subnet when you create a virtual network.</span></span> <span data-ttu-id="280a1-140">Neste tutorial, você criará uma segunda sub-rede depois que você criar rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="280a1-140">In this tutorial, you create a second subnet after you create hello virtual network.</span></span> <span data-ttu-id="280a1-141">Você pode criar mais tarde recursos acessíveis pela Internet Olá **pública** sub-rede.</span><span class="sxs-lookup"><span data-stu-id="280a1-141">You might later create Internet-accessible resources in hello **Public** subnet.</span></span> <span data-ttu-id="280a1-142">Você também pode criar recursos que não estão acessíveis da saudação da Internet no hello **privada** sub-rede.</span><span class="sxs-lookup"><span data-stu-id="280a1-142">You also might create resources that aren't accessible from hello Internet in hello **Private** subnet.</span></span> <span data-ttu-id="280a1-143">toocreate Olá segunda sub-rede, insira **myVnet** em Olá **pesquisar recursos** caixa na parte superior de saudação da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="280a1-143">toocreate hello second subnet, enter **myVnet** in hello **Search resources** box at hello top of hello page.</span></span> <span data-ttu-id="280a1-144">Clique em **myVnet** quando ele aparece nos resultados da pesquisa hello.</span><span class="sxs-lookup"><span data-stu-id="280a1-144">Click **myVnet** when it appears in hello search results.</span></span>
5. <span data-ttu-id="280a1-145">Clique em **sub-redes** (no hello **configurações** seção) em Olá **criar rede virtual (clássica)** folha que aparece.</span><span class="sxs-lookup"><span data-stu-id="280a1-145">Click **Subnets** (in hello **SETTINGS** section) on hello **Create virtual network (classic)** blade that appears.</span></span>
6. <span data-ttu-id="280a1-146">Clique em **+ adicionar** em Olá **myVnet - sub-redes** folha que aparece.</span><span class="sxs-lookup"><span data-stu-id="280a1-146">Click **+Add** on hello **myVnet - Subnets** blade that appears.</span></span>
7. <span data-ttu-id="280a1-147">Digite **privada** para **nome** em Olá **Adicionar sub-rede** folha.</span><span class="sxs-lookup"><span data-stu-id="280a1-147">Enter **Private** for **Name** on hello **Add subnet** blade.</span></span> <span data-ttu-id="280a1-148">Digite **10.0.1.0/24** para **Intervalo de endereços**.</span><span class="sxs-lookup"><span data-stu-id="280a1-148">Enter **10.0.1.0/24** for **Address range**.</span></span>  <span data-ttu-id="280a1-149">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="280a1-149">Click **OK**.</span></span>
8. <span data-ttu-id="280a1-150">Em Olá **myVnet - sub-redes** folha, você pode ver Olá **pública** e **privada** sub-redes que você criou.</span><span class="sxs-lookup"><span data-stu-id="280a1-150">On hello **myVnet - Subnets** blade, you can see hello **Public** and **Private** subnets that you created.</span></span>
9. <span data-ttu-id="280a1-151">**Opcional**: quando você concluir este tutorial, você pode desejar que recursos de saudação toodelete que você criou, para que você não incorrer em encargos de uso:</span><span class="sxs-lookup"><span data-stu-id="280a1-151">**Optional**: When you finish this tutorial, you might want toodelete hello resources that you created, so that you don't incur usage charges:</span></span>
    - <span data-ttu-id="280a1-152">Clique em **visão geral** em Olá **myVnet** folha.</span><span class="sxs-lookup"><span data-stu-id="280a1-152">Click **Overview** on hello **myVnet** blade.</span></span>
    - <span data-ttu-id="280a1-153">Clique em Olá **excluir** ícone Olá **myVnet** folha.</span><span class="sxs-lookup"><span data-stu-id="280a1-153">Click hello **Delete** icon on hello **myVnet** blade.</span></span>
    - <span data-ttu-id="280a1-154">exclusão de saudação tooconfirm, clique em **Sim** em Olá **rede virtual Delete** caixa.</span><span class="sxs-lookup"><span data-stu-id="280a1-154">tooconfirm hello deletion, click **Yes** in hello **Delete virtual network** box.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="280a1-155">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="280a1-155">Azure CLI</span></span>

1. <span data-ttu-id="280a1-156">Você pode [instalar e configurar Olá CLI do Azure](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json), ou use Olá CLI em Olá Shell de nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="280a1-156">You can either [install and configure hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json), or use hello CLI within hello Azure Cloud Shell.</span></span> <span data-ttu-id="280a1-157">Olá Shell de nuvem do Azure é um shell Bash livre que podem ser executados diretamente no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="280a1-157">hello Azure Cloud Shell is a free Bash shell that you can run directly within hello Azure portal.</span></span> <span data-ttu-id="280a1-158">Ele tem Olá CLI do Azure pré-instalado e configurado toouse com sua conta.</span><span class="sxs-lookup"><span data-stu-id="280a1-158">It has hello Azure CLI preinstalled and configured toouse with your account.</span></span> <span data-ttu-id="280a1-159">tooget ajuda para comandos CLI, digite `azure <command> --help`.</span><span class="sxs-lookup"><span data-stu-id="280a1-159">tooget help for CLI commands, type `azure <command> --help`.</span></span> 
2. <span data-ttu-id="280a1-160">Em uma sessão CLI, faça logon em tooAzure com o comando Olá que segue.</span><span class="sxs-lookup"><span data-stu-id="280a1-160">In a CLI session, log in tooAzure with hello command that follows.</span></span> <span data-ttu-id="280a1-161">Se você clicar em **Experimente** na caixa Olá abaixo, um Shell de nuvem é aberta.</span><span class="sxs-lookup"><span data-stu-id="280a1-161">If you click **Try it** in hello box below, a Cloud Shell opens.</span></span> <span data-ttu-id="280a1-162">Você pode fazer logon no tooyour assinatura do Azure, sem inserir Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="280a1-162">You can log in tooyour Azure subscription, without entering hello following command:</span></span>

    ```azurecli-interactive
    azure login
    ```

3. <span data-ttu-id="280a1-163">Olá tooensure CLI está no modo de gerenciamento de serviço, digite Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="280a1-163">tooensure hello CLI is in Service Management mode, enter hello following command:</span></span>

    ```azurecli-interactive
    azure config mode asm
    ```

4. <span data-ttu-id="280a1-164">Crie uma rede virtual com uma sub-rede privada:</span><span class="sxs-lookup"><span data-stu-id="280a1-164">Create a virtual network with a private subnet:</span></span>

    ```azurecli-interactive
    azure network vnet create --vnet myVnet --address-space 10.0.0.0 --cidr 16  --subnet-name Private --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --location "East US"
    ```

5. <span data-ttu-id="280a1-165">Crie uma sub-rede pública na rede virtual hello:</span><span class="sxs-lookup"><span data-stu-id="280a1-165">Create a public subnet within hello virtual network:</span></span>

    ```azurecli-interactive
    azure network vnet subnet create --name Public --vnet-name myVnet --address-prefix 10.0.1.0/24
    ```    
    
6. <span data-ttu-id="280a1-166">Examinar a rede virtual hello e sub-redes:</span><span class="sxs-lookup"><span data-stu-id="280a1-166">Review hello virtual network and subnets:</span></span>

    ```azurecli-interactive
    azure network vnet show --vnet myVnet
    ```

7. <span data-ttu-id="280a1-167">**Opcional**: você pode desejar que recursos de saudação toodelete que você criou quando você concluir este tutorial, para que você não incorrer em encargos de uso:</span><span class="sxs-lookup"><span data-stu-id="280a1-167">**Optional**: You might want toodelete hello resources that you created when you finish this tutorial, so that you don't incur usage charges:</span></span>

    ```azurecli-interactive
    azure network vnet delete --vnet myVnet --quiet
    ```

> [!NOTE]
> <span data-ttu-id="280a1-168">Embora você não pode especificar um grupo de recursos toocreate uma rede virtual (clássica) usando Olá CLI, Azure cria a rede virtual Olá em um grupo de recursos denominado *rede padrão*.</span><span class="sxs-lookup"><span data-stu-id="280a1-168">Though you can't specify a resource group toocreate a virtual network (classic) in using hello CLI, Azure creates hello virtual network in a resource group named *Default-Networking*.</span></span>

## <a name="powershell"></a><span data-ttu-id="280a1-169">PowerShell</span><span class="sxs-lookup"><span data-stu-id="280a1-169">PowerShell</span></span>

1. <span data-ttu-id="280a1-170">Instale a versão mais recente Olá de saudação do PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) módulo.</span><span class="sxs-lookup"><span data-stu-id="280a1-170">Install hello latest version of hello PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) module.</span></span> <span data-ttu-id="280a1-171">Se você for novo tooAzure PowerShell, consulte [visão geral do Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="280a1-171">If you're new tooAzure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="280a1-172">Inicie uma sessão do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="280a1-172">Start a PowerShell session.</span></span>
3. <span data-ttu-id="280a1-173">No PowerShell, faça logon no tooAzure digitando Olá `Add-AzureAccount` comando.</span><span class="sxs-lookup"><span data-stu-id="280a1-173">In PowerShell, log in tooAzure by entering hello `Add-AzureAccount` command.</span></span>
4. <span data-ttu-id="280a1-174">Alterar Olá seguinte caminho e nome de arquivo, conforme apropriado, em seguida, exportar o arquivo de configuração de rede existente:</span><span class="sxs-lookup"><span data-stu-id="280a1-174">Change hello following path and filename, as appropriate, then export your existing network configuration file:</span></span>

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
    ```

5. <span data-ttu-id="280a1-175">toocreate uma rede virtual com subredes públicas e privadas, use qualquer Olá de tooadd do editor de texto **VirtualNetworkSite** elemento que segue o arquivo de configuração de rede toohello.</span><span class="sxs-lookup"><span data-stu-id="280a1-175">toocreate a virtual network with public and private subnets, use any text editor tooadd hello **VirtualNetworkSite** element that follows toohello network configuration file.</span></span>

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

    <span data-ttu-id="280a1-176">Saudação de revisão completa [esquema de arquivo de configuração de rede](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="280a1-176">Review hello full [network configuration file schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>

6. <span data-ttu-id="280a1-177">Importar arquivo de configuração de rede hello:</span><span class="sxs-lookup"><span data-stu-id="280a1-177">Import hello network configuration file:</span></span>

    ```powershell
    Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
    ```

    > [!WARNING]
    > <span data-ttu-id="280a1-178">Importar um arquivo de configuração de rede alterada pode causar alterações tooexisting de redes virtuais (clássico) na sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="280a1-178">Importing a changed network configuration file can cause changes tooexisting virtual networks (classic) in your subscription.</span></span> <span data-ttu-id="280a1-179">Verifique se você adicionar apenas a rede virtual anterior de saudação e você não alterar ou remover todas as redes virtuais existentes da sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="280a1-179">Ensure you only add hello previous virtual network and that you don't change or remove any existing virtual networks from your subscription.</span></span> 

7. <span data-ttu-id="280a1-180">Examinar a rede virtual hello e sub-redes:</span><span class="sxs-lookup"><span data-stu-id="280a1-180">Review hello virtual network and subnets:</span></span>

    ```powershell
    Get-AzureVNetSite -VNetName "myVnet"
    ```

8. <span data-ttu-id="280a1-181">**Opcional**: você pode desejar que recursos de saudação toodelete que você criou quando você concluir este tutorial, para que você não incorrer em encargos de uso.</span><span class="sxs-lookup"><span data-stu-id="280a1-181">**Optional**: You might want toodelete hello resources that you created when you finish this tutorial, so that you don't incur usage charges.</span></span> <span data-ttu-id="280a1-182">toodelete Olá rede virtual, e concluir as etapas de 4 a 6 novamente, Olá de remover esse tempo **VirtualNetworkSite** elemento que você adicionou na etapa 5.</span><span class="sxs-lookup"><span data-stu-id="280a1-182">toodelete hello virtual network, complete steps 4-6 again, this time removing hello **VirtualNetworkSite** element you added in step 5.</span></span>
 
> [!NOTE]
> <span data-ttu-id="280a1-183">Embora você não pode especificar um grupo de recursos toocreate uma rede virtual (clássica) usando o PowerShell, o Azure cria a rede virtual Olá em um grupo de recursos denominado *rede padrão*.</span><span class="sxs-lookup"><span data-stu-id="280a1-183">Though you can't specify a resource group toocreate a virtual network (classic) in using PowerShell, Azure creates hello virtual network in a resource group named *Default-Networking*.</span></span>

---

## <a name="next-steps"></a><span data-ttu-id="280a1-184">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="280a1-184">Next steps</span></span>

- <span data-ttu-id="280a1-185">Consulte toolearn sobre todas as configurações de sub-rede e rede virtual [gerenciar redes virtuais](virtual-network-manage-network.md) e [gerenciar sub-redes de rede virtual](virtual-network-manage-subnet.md).</span><span class="sxs-lookup"><span data-stu-id="280a1-185">toolearn about all virtual network and subnet settings, see [Manage virtual networks](virtual-network-manage-network.md) and [Manage virtual network subnets](virtual-network-manage-subnet.md).</span></span> <span data-ttu-id="280a1-186">Você tem várias opções para o uso de redes virtuais e sub-redes em uma produção toomeet diferente dos requisitos do ambiente.</span><span class="sxs-lookup"><span data-stu-id="280a1-186">You have various options for using virtual networks and subnets in a production environment toomeet different requirements.</span></span>
- <span data-ttu-id="280a1-187">toofilter entrada e saída de tráfego de sub-rede, criar e aplicar [grupos de segurança de rede](virtual-networks-nsg.md) toosubnets.</span><span class="sxs-lookup"><span data-stu-id="280a1-187">toofilter inbound and outbound subnet traffic, create and apply [network security groups](virtual-networks-nsg.md) toosubnets.</span></span>
- <span data-ttu-id="280a1-188">Criar um [Windows](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) ou um [Linux](../virtual-machines/linux/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) máquina virtual e, em seguida, conecte-o rede virtual existente do tooan.</span><span class="sxs-lookup"><span data-stu-id="280a1-188">Create a [Windows](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) or a [Linux](../virtual-machines/linux/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) virtual machine, and then connect it tooan existing virtual network.</span></span>
- <span data-ttu-id="280a1-189">redes virtuais tooconnect dois em Olá mesmo local do Azure, crie um [emparelhamento de rede virtual](create-peering-different-deployment-models.md) entre redes virtuais hello.</span><span class="sxs-lookup"><span data-stu-id="280a1-189">tooconnect two virtual networks in hello same Azure location, create a  [virtual network peering](create-peering-different-deployment-models.md) between hello virtual networks.</span></span> <span data-ttu-id="280a1-190">Você pode emparelhar rede virtual uma rede virtual (Gerenciador de recursos) tooa (clássico), mas não é possível criar um emparelhamento entre duas redes virtuais (clássico).</span><span class="sxs-lookup"><span data-stu-id="280a1-190">You can peer a virtual network (Resource Manager) tooa virtual network (classic), but you cannot create a peering between two virtual networks (classic).</span></span>
- <span data-ttu-id="280a1-191">Conectar-se a rede de local de tooan Olá rede virtual usando um [Gateway VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) ou [rota expressa do Azure](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) circuito.</span><span class="sxs-lookup"><span data-stu-id="280a1-191">Connect hello virtual network tooan on-premises network by using a [VPN Gateway](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) or [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) circuit.</span></span>
