---
title: gateway de dados local aaaInstall | Microsoft Docs
description: Saiba como tooinstall e configure um gateway de dados local.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/22/2017
ms.author: owend
ms.openlocfilehash: e2878bf765c82910d452ae2cdd9264a343ec1990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-an-on-premises-data-gateway"></a><span data-ttu-id="5c24a-103">Instalar e configurar um gateway de dados local</span><span class="sxs-lookup"><span data-stu-id="5c24a-103">Install and configure an on-premises data gateway</span></span>
<span data-ttu-id="5c24a-104">Um gateway de dados local é necessário quando um ou mais servidores de serviços de análise do Azure no hello mesmo região se conectar a fontes de dados locais tooon.</span><span class="sxs-lookup"><span data-stu-id="5c24a-104">An on-premises data gateway is required when one or more Azure Analysis Services servers in hello same region connect tooon-premises data sources.</span></span> <span data-ttu-id="5c24a-105">toolearn mais sobre o gateway hello, consulte [gateway de dados no local](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="5c24a-105">toolearn more about hello gateway, see [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c24a-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5c24a-106">Prerequisites</span></span>
<span data-ttu-id="5c24a-107">**Requisitos mínimos:**</span><span class="sxs-lookup"><span data-stu-id="5c24a-107">**Minimum Requirements:**</span></span>

* <span data-ttu-id="5c24a-108">.NET 4.5 Framework</span><span class="sxs-lookup"><span data-stu-id="5c24a-108">.NET 4.5 Framework</span></span>
* <span data-ttu-id="5c24a-109">Versão de 64 bits do Windows 7/Windows Server 2008 R2 (ou posterior)</span><span class="sxs-lookup"><span data-stu-id="5c24a-109">64-bit version of Windows 7 / Windows Server 2008 R2 (or later)</span></span>

<span data-ttu-id="5c24a-110">**Recomendados:**</span><span class="sxs-lookup"><span data-stu-id="5c24a-110">**Recommended:**</span></span>

* <span data-ttu-id="5c24a-111">CPU de 8 núcleos</span><span class="sxs-lookup"><span data-stu-id="5c24a-111">8 Core CPU</span></span>
* <span data-ttu-id="5c24a-112">Memória de 8 GB</span><span class="sxs-lookup"><span data-stu-id="5c24a-112">8 GB Memory</span></span>
* <span data-ttu-id="5c24a-113">Versão de 64 bits do Windows 2012 R2 (ou posterior)</span><span class="sxs-lookup"><span data-stu-id="5c24a-113">64-bit version of Windows 2012 R2 (or later)</span></span>

<span data-ttu-id="5c24a-114">**Considerações importantes:**</span><span class="sxs-lookup"><span data-stu-id="5c24a-114">**Important considerations:**</span></span>

* <span data-ttu-id="5c24a-115">Durante a instalação, ao registrar o gateway com o Azure, a região de padrão de saudação para sua assinatura está selecionada.</span><span class="sxs-lookup"><span data-stu-id="5c24a-115">During setup, when registering your gateway with Azure, hello default region for your subscription is selected.</span></span> <span data-ttu-id="5c24a-116">Você pode escolher uma região diferente.</span><span class="sxs-lookup"><span data-stu-id="5c24a-116">You can choose a different region.</span></span> <span data-ttu-id="5c24a-117">Se tiver servidores em mais de uma região, você precisará instalar um gateway para cada região.</span><span class="sxs-lookup"><span data-stu-id="5c24a-117">If you have servers in more than one region, you must install a gateway for each region.</span></span> 
* <span data-ttu-id="5c24a-118">gateway de saudação não pode ser instalado em um controlador de domínio.</span><span class="sxs-lookup"><span data-stu-id="5c24a-118">hello gateway cannot be installed on a domain controller.</span></span>
* <span data-ttu-id="5c24a-119">Apenas um gateway pode ser instalado em um computador.</span><span class="sxs-lookup"><span data-stu-id="5c24a-119">Only one gateway can be installed on a single computer.</span></span>
* <span data-ttu-id="5c24a-120">Instale o gateway de saudação em um computador que permanece no e não vai toosleep.</span><span class="sxs-lookup"><span data-stu-id="5c24a-120">Install hello gateway on a computer that remains on and does not go toosleep.</span></span>
* <span data-ttu-id="5c24a-121">Não instale o gateway de saudação em uma rede sem fio conectada tooyour de computador.</span><span class="sxs-lookup"><span data-stu-id="5c24a-121">Do not install hello gateway on a computer wirelessly connected tooyour network.</span></span> <span data-ttu-id="5c24a-122">O desempenho pode ser prejudicado.</span><span class="sxs-lookup"><span data-stu-id="5c24a-122">Performance can be diminished.</span></span>


## <span data-ttu-id="5c24a-123"><a name="download"></a>Baixar</span><span class="sxs-lookup"><span data-stu-id="5c24a-123"><a name="download"></a>Download</span></span>
 [<span data-ttu-id="5c24a-124">Baixar o gateway Olá</span><span class="sxs-lookup"><span data-stu-id="5c24a-124">Download hello gateway</span></span>](https://aka.ms/azureasgateway)

## <span data-ttu-id="5c24a-125"><a name="install"></a>Instalar</span><span class="sxs-lookup"><span data-stu-id="5c24a-125"><a name="install"></a>Install</span></span>

1. <span data-ttu-id="5c24a-126">Execute a instalação.</span><span class="sxs-lookup"><span data-stu-id="5c24a-126">Run setup.</span></span>

2. <span data-ttu-id="5c24a-127">Selecione um local, aceite os termos de saudação e, em seguida, clique em **instalar**.</span><span class="sxs-lookup"><span data-stu-id="5c24a-127">Select a location, accept hello terms, and then click **Install**.</span></span>

   ![Instale os termos de licença e de local](media/analysis-services-gateway-install/aas-gateway-installer-accept.png)

3. <span data-ttu-id="5c24a-129">Selecione **Gateway de dados local (recomendado)**.</span><span class="sxs-lookup"><span data-stu-id="5c24a-129">Select **On-premises data gateway (recommended)**.</span></span> <span data-ttu-id="5c24a-130">O Azure Analysis Services não dá suporte ao modo pessoal.</span><span class="sxs-lookup"><span data-stu-id="5c24a-130">Azure Analysis Services does not support personal mode.</span></span>

   ![Escolha o tipo de gateway](media/analysis-services-gateway-install/aas-gateway-installer-shared.png)

4. <span data-ttu-id="5c24a-132">Insira uma conta toosign em tooAzure.</span><span class="sxs-lookup"><span data-stu-id="5c24a-132">Enter an account toosign in tooAzure.</span></span> <span data-ttu-id="5c24a-133">Olá conta deve ser no Azure Active Directory do seu locatário.</span><span class="sxs-lookup"><span data-stu-id="5c24a-133">hello account must be in your tenant's Azure Active Directory.</span></span> <span data-ttu-id="5c24a-134">Essa conta é usada para o administrador do gateway hello.</span><span class="sxs-lookup"><span data-stu-id="5c24a-134">This account is used for hello gateway administrator.</span></span> 

   ![Insira uma conta toosign em tooAzure](media/analysis-services-gateway-install/aas-gateway-installer-account.png)

   > [!NOTE]
   > <span data-ttu-id="5c24a-136">Se você entrar com uma conta de domínio, ele será mapeado conta organizacional tooyour no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="5c24a-136">If you sign in with a domain account, it will be mapped tooyour organizational account in Azure AD.</span></span> <span data-ttu-id="5c24a-137">Sua conta organizacional será usada como o administrador do gateway Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="5c24a-137">Your organizational account will be used as hello hello gateway administrator.</span></span>

## <span data-ttu-id="5c24a-138"><a name="register"></a>Registrar</span><span class="sxs-lookup"><span data-stu-id="5c24a-138"><a name="register"></a>Register</span></span>
<span data-ttu-id="5c24a-139">Ordem toocreate um recurso de gateway no Azure, você deve registrar instância local do hello instalado com hello serviço de nuvem do Gateway.</span><span class="sxs-lookup"><span data-stu-id="5c24a-139">In order toocreate a gateway resource in Azure, you must register hello local instance you installed with hello Gateway Cloud Service.</span></span> 

1.  <span data-ttu-id="5c24a-140">Selecione **Registrar um novo gateway neste computador**.</span><span class="sxs-lookup"><span data-stu-id="5c24a-140">Select **Register a new gateway on this computer**.</span></span>

    ![Registrar](media/analysis-services-gateway-install/aas-gateway-register-new.png)

2. <span data-ttu-id="5c24a-142">Digite um nome e uma chave de recuperação para o gateway.</span><span class="sxs-lookup"><span data-stu-id="5c24a-142">Type a name and recovery key for your gateway.</span></span> <span data-ttu-id="5c24a-143">Por padrão, o gateway Olá usa região padrão de sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="5c24a-143">By default, hello gateway uses your subscription's default region.</span></span> <span data-ttu-id="5c24a-144">Se você precisar tooselect uma região diferente, selecione **alteração região**.</span><span class="sxs-lookup"><span data-stu-id="5c24a-144">If you need tooselect a different region, select **Change Region**.</span></span>

   ![Registrar](media/analysis-services-gateway-install/aas-gateway-register-name.png)


## <span data-ttu-id="5c24a-146"><a name="create-resource"></a>Criar um recurso de gateway do Azure</span><span class="sxs-lookup"><span data-stu-id="5c24a-146"><a name="create-resource"></a>Create an Azure gateway resource</span></span>
<span data-ttu-id="5c24a-147">Depois de instalado e registrado seu gateway, você precisa toocreate um recurso de gateway na sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="5c24a-147">After you've installed and registered your gateway, you need toocreate a gateway resource in your Azure subscription.</span></span> <span data-ttu-id="5c24a-148">Entrar tooAzure com hello mesma conta usada ao registrar o gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="5c24a-148">Sign in tooAzure with hello same account you used when registering hello gateway.</span></span>

1. <span data-ttu-id="5c24a-149">No portal do Azure, clique em **Criar um novo serviço** > **Enterprise Integration** > **Gateway de dados local** > **Criar**.</span><span class="sxs-lookup"><span data-stu-id="5c24a-149">In Azure portal, click **Create a new service** > **Enterprise Integration** > **On-premises data gateway** > **Create**.</span></span>

   ![Criar um recurso de gateway](media/analysis-services-gateway-install/aas-gateway-new-azure-resource.png)

2. <span data-ttu-id="5c24a-151">Em **Criar gateway de conexão**, insira estas configurações:</span><span class="sxs-lookup"><span data-stu-id="5c24a-151">In **Create connection gateway**, enter these settings:</span></span>

    * <span data-ttu-id="5c24a-152">**Nome**: insira um nome para o recurso do gateway.</span><span class="sxs-lookup"><span data-stu-id="5c24a-152">**Name**: Enter a name for your gateway resource.</span></span> 

    * <span data-ttu-id="5c24a-153">**Assinatura**: selecione Olá tooassociate de assinatura do Azure com o recurso de gateway.</span><span class="sxs-lookup"><span data-stu-id="5c24a-153">**Subscription**: Select hello Azure subscription tooassociate with your gateway resource.</span></span> 
    <span data-ttu-id="5c24a-154">Essa assinatura deve ser Olá a mesma assinatura que seus servidores estão em.</span><span class="sxs-lookup"><span data-stu-id="5c24a-154">This subscription should be hello same subscription your servers are in.</span></span>
   
      <span data-ttu-id="5c24a-155">assinatura do saudação padrão baseia-se em Olá conta do Azure que você usou toosign no.</span><span class="sxs-lookup"><span data-stu-id="5c24a-155">hello default subscription is based on hello Azure account that you used toosign in.</span></span>

    * <span data-ttu-id="5c24a-156">**Grupo de recursos**: Crie um novo grupo de recursos ou escolha um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="5c24a-156">**Resource group**: Create a resource group or select an existing resource group.</span></span>

    * <span data-ttu-id="5c24a-157">**Local**: região Olá selecione registrado o gateway.</span><span class="sxs-lookup"><span data-stu-id="5c24a-157">**Location**: Select hello region you registered your gateway in.</span></span>

    * <span data-ttu-id="5c24a-158">**Nome da instalação**: se a instalação do gateway não estiver selecionada, o gateway de saudação selecione registrado.</span><span class="sxs-lookup"><span data-stu-id="5c24a-158">**Installation Name**: If your gateway installation isn't already selected, select hello gateway registered.</span></span> 

    <span data-ttu-id="5c24a-159">Quando tiver concluído, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="5c24a-159">When you're done, click **Create**.</span></span>

## <span data-ttu-id="5c24a-160"><a name="connect-servers"></a>Conecte-se a recursos de servidores de gateway toohello</span><span class="sxs-lookup"><span data-stu-id="5c24a-160"><a name="connect-servers"></a>Connect servers toohello gateway resource</span></span>

1. <span data-ttu-id="5c24a-161">Na visão geral de seu servidor do Azure Analysis Services, clique em **Gateway de Dados Local**.</span><span class="sxs-lookup"><span data-stu-id="5c24a-161">In your Azure Analysis Services server overview, click **On-Premises Data Gateway**.</span></span>

   ![Conecte-se o servidor toogateway](media/analysis-services-gateway-install/aas-gateway-connect-server.png)

2. <span data-ttu-id="5c24a-163">Em **escolher um Gateway de dados local tooconnect**, selecione o recurso de gateway e, em seguida, clique em **gateway selecionado conectar**.</span><span class="sxs-lookup"><span data-stu-id="5c24a-163">In **Pick an On-Premises Data Gateway tooconnect**, select your gateway resource, and then click **Connect selected gateway**.</span></span>

   ![Conecte-se o recurso do servidor toogateway](media/analysis-services-gateway-install/aas-gateway-connect-resource.png)

    > [!NOTE]
    > <span data-ttu-id="5c24a-165">Se o gateway não aparecer na lista de saudação, seu servidor provavelmente não está em Olá mesma região que a região Olá você especificou ao registrar o gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="5c24a-165">If your gateway does not appear in hello list, your server is likely not in hello same region as hello region you specified when registering hello gateway.</span></span> 

<span data-ttu-id="5c24a-166">É isso.</span><span class="sxs-lookup"><span data-stu-id="5c24a-166">That's it.</span></span> <span data-ttu-id="5c24a-167">Se você precisa tooopen portas ou fazer qualquer solução de problemas, ser toocheck se out [gateway de dados no local](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="5c24a-167">If you need tooopen ports or do any troubleshooting, be sure toocheck out [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c24a-168">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5c24a-168">Next steps</span></span>
* [<span data-ttu-id="5c24a-169">Gerenciar o Analysis Services</span><span class="sxs-lookup"><span data-stu-id="5c24a-169">Manage Analysis Services</span></span>](analysis-services-manage.md)   
* [<span data-ttu-id="5c24a-170">Obter dados do Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="5c24a-170">Get data from Azure Analysis Services</span></span>](analysis-services-connect.md)
