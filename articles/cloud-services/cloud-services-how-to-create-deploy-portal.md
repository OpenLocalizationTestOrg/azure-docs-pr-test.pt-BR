---
title: "aaaHow toocreate e implantar um serviço de nuvem | Microsoft Docs"
description: "Saiba como toocreate e implantar um serviço de nuvem usando Olá portal do Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 56ea2f14-34a2-4ed9-857c-82be4c9d0579
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: dc8b81a594f3514e662c49c9a46a33da8a551f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-deploy-a-cloud-service"></a><span data-ttu-id="6840b-103">Como toocreate e implantar um serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="6840b-103">How toocreate and deploy a cloud service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6840b-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6840b-104">Azure portal</span></span>](cloud-services-how-to-create-deploy-portal.md)
> * [<span data-ttu-id="6840b-105">Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="6840b-105">Azure classic portal</span></span>](cloud-services-how-to-create-deploy.md)
>
>

<span data-ttu-id="6840b-106">Olá portal do Azure fornece duas maneiras para você toocreate e implantar um serviço de nuvem: *criação rápida* e *criação personalizada*.</span><span class="sxs-lookup"><span data-stu-id="6840b-106">hello Azure portal provides two ways for you toocreate and deploy a cloud service: *Quick Create* and *Custom Create*.</span></span>

<span data-ttu-id="6840b-107">Este artigo explica como toouse Olá toocreate de método rápido criar um novo serviço de nuvem e, em seguida, usar **carregar** tooupload e implantar um pacote de serviço de nuvem no Azure.</span><span class="sxs-lookup"><span data-stu-id="6840b-107">This article explains how toouse hello Quick Create method toocreate a new cloud service and then use **Upload** tooupload and deploy a cloud service package in Azure.</span></span> <span data-ttu-id="6840b-108">Quando você usar esse método, Olá portal do Azure torna disponível links convenientes para a conclusão de todos os requisitos conforme você avança.</span><span class="sxs-lookup"><span data-stu-id="6840b-108">When you use this method, hello Azure portal makes available convenient links for completing all requirements as you go.</span></span> <span data-ttu-id="6840b-109">Se você estiver pronto toodeploy sua nuvem de serviço quando você criá-lo, você pode fazer ao Olá mesmo tempo usando criação personalizada.</span><span class="sxs-lookup"><span data-stu-id="6840b-109">If you're ready toodeploy your cloud service when you create it, you can do both at hello same time using Custom Create.</span></span>

> [!NOTE]
> <span data-ttu-id="6840b-110">Se você planejar toopublish seu serviço de nuvem do Visual Studio Team Services (VSTS), usar a criação rápida e, em seguida, configure a publicação do VSTS do painel de início rápido do Azure ou Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="6840b-110">If you plan toopublish your cloud service from Visual Studio Team Services (VSTS), use Quick Create, and then set up VSTS publishing from hello Azure Quickstart or hello dashboard.</span></span> <span data-ttu-id="6840b-111">Para obter mais informações, consulte [tooAzure entrega contínua, usando o Visual Studio Team Services][TFSTutorialForCloudService], ou consulte a Ajuda para Olá **início rápido** página.</span><span class="sxs-lookup"><span data-stu-id="6840b-111">For more information, see [Continuous Delivery tooAzure by Using Visual Studio Team Services][TFSTutorialForCloudService], or see help for hello **Quick Start** page.</span></span>
>
>

## <a name="concepts"></a><span data-ttu-id="6840b-112">Conceitos</span><span class="sxs-lookup"><span data-stu-id="6840b-112">Concepts</span></span>
<span data-ttu-id="6840b-113">Três componentes são necessário toodeploy um aplicativo como um serviço de nuvem no Azure:</span><span class="sxs-lookup"><span data-stu-id="6840b-113">Three components are required toodeploy an application as a cloud service in Azure:</span></span>

* <span data-ttu-id="6840b-114">**Definição de serviço**</span><span class="sxs-lookup"><span data-stu-id="6840b-114">**Service Definition**</span></span>  
  <span data-ttu-id="6840b-115">arquivo de definição de serviço de nuvem da saudação (. csdef) define o modelo de serviço hello, incluindo o número de funções hello.</span><span class="sxs-lookup"><span data-stu-id="6840b-115">hello cloud service definition file (.csdef) defines hello service model, including hello number of roles.</span></span>
* <span data-ttu-id="6840b-116">**Configuração de serviço**</span><span class="sxs-lookup"><span data-stu-id="6840b-116">**Service Configuration**</span></span>  
  <span data-ttu-id="6840b-117">arquivo de configuração de serviço de nuvem da saudação (. cscfg) fornece definições de configuração para o serviço de nuvem hello e funções individuais, incluindo Olá número de instâncias de função.</span><span class="sxs-lookup"><span data-stu-id="6840b-117">hello cloud service configuration file (.cscfg) provides configuration settings for hello cloud service and individual roles, including hello number of role instances.</span></span>
* <span data-ttu-id="6840b-118">**Pacote de serviço**</span><span class="sxs-lookup"><span data-stu-id="6840b-118">**Service Package**</span></span>  
  <span data-ttu-id="6840b-119">pacote de serviço da saudação (. cspkg) contém o código do aplicativo hello e configurações e o arquivo de definição de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="6840b-119">hello service package (.cspkg) contains hello application code and configurations and hello service definition file.</span></span>

<span data-ttu-id="6840b-120">Você pode aprender mais sobre essas e como um pacote de toocreate [aqui](cloud-services-model-and-package.md).</span><span class="sxs-lookup"><span data-stu-id="6840b-120">You can learn more about these and how toocreate a package [here](cloud-services-model-and-package.md).</span></span>

## <a name="prepare-your-app"></a><span data-ttu-id="6840b-121">Preparação do aplicativo</span><span class="sxs-lookup"><span data-stu-id="6840b-121">Prepare your app</span></span>
<span data-ttu-id="6840b-122">Antes de implantar um serviço de nuvem, você deve criar o pacote de serviço de nuvem hello (. cspkg) do seu código de aplicativo e um arquivo de configuração de serviço de nuvem (. cscfg).</span><span class="sxs-lookup"><span data-stu-id="6840b-122">Before you can deploy a cloud service, you must create hello cloud service package (.cspkg) from your application code and a cloud service configuration file (.cscfg).</span></span> <span data-ttu-id="6840b-123">Olá SDK do Azure fornece ferramentas para preparar a esses arquivos de implantação necessária.</span><span class="sxs-lookup"><span data-stu-id="6840b-123">hello Azure SDK provides tools for preparing these required deployment files.</span></span> <span data-ttu-id="6840b-124">Você pode instalar o SDK de saudação do hello [Downloads do Azure](https://azure.microsoft.com/downloads/) página, na linguagem de saudação em que você preferir toodevelop seu código de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6840b-124">You can install hello SDK from hello [Azure Downloads](https://azure.microsoft.com/downloads/) page, in hello language in which you prefer toodevelop your application code.</span></span>

<span data-ttu-id="6840b-125">Três recursos de serviço de nuvem precisam de configurações especiais antes que você exporte um pacote de serviço:</span><span class="sxs-lookup"><span data-stu-id="6840b-125">Three cloud service features require special configurations before you export a service package:</span></span>

* <span data-ttu-id="6840b-126">Se você quiser toodeploy um serviço de nuvem que usa o protocolo (SSL) para criptografia de dados, [configurar seu aplicativo](cloud-services-configure-ssl-certificate-portal.md#modify) para SSL.</span><span class="sxs-lookup"><span data-stu-id="6840b-126">If you want toodeploy a cloud service that uses Secure Sockets Layer (SSL) for data encryption, [configure your application](cloud-services-configure-ssl-certificate-portal.md#modify) for SSL.</span></span>
* <span data-ttu-id="6840b-127">Se você quiser instâncias de toorole de conexões de área de trabalho remota tooconfigure, [configurar funções hello](cloud-services-role-enable-remote-desktop-new-portal.md) para área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="6840b-127">If you want tooconfigure Remote Desktop connections toorole instances, [configure hello roles](cloud-services-role-enable-remote-desktop-new-portal.md) for Remote Desktop.</span></span>
* <span data-ttu-id="6840b-128">Se você quiser tooconfigure detalhado de monitoramento para seu serviço de nuvem, habilite o diagnóstico do Azure para serviço de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="6840b-128">If you want tooconfigure verbose monitoring for your cloud service, enable Azure Diagnostics for hello cloud service.</span></span> <span data-ttu-id="6840b-129">*Monitoramento mínimo* (Olá nível padrão de monitoração) usa contadores de desempenho coletados a partir de sistemas operacionais do hello host para instâncias de função (máquinas virtuais).</span><span class="sxs-lookup"><span data-stu-id="6840b-129">*Minimal monitoring* (hello default monitoring level) uses performance counters gathered from hello host operating systems for role instances (virtual machines).</span></span> <span data-ttu-id="6840b-130">*O monitoramento detalhado* coleta métricas adicionais com base nos dados de desempenho em Olá função instâncias tooenable uma análise mais próxima dos problemas que ocorrem durante o processamento do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6840b-130">*Verbose monitoring* gathers additional metrics based on performance data within hello role instances tooenable closer analysis of issues that occur during application processing.</span></span> <span data-ttu-id="6840b-131">toofind como tooenable diagnóstico do Azure, consulte [habilitando diagnósticos no Azure](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="6840b-131">toofind out how tooenable Azure Diagnostics, see [Enabling diagnostics in Azure](cloud-services-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="6840b-132">toocreate um serviço de nuvem com implantações de funções web ou funções de trabalho, você deve [criar pacote de serviço Olá](cloud-services-model-and-package.md#servicepackagecspkg).</span><span class="sxs-lookup"><span data-stu-id="6840b-132">toocreate a cloud service with deployments of web roles or worker roles, you must [create hello service package](cloud-services-model-and-package.md#servicepackagecspkg).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6840b-133">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="6840b-133">Before you begin</span></span>
* <span data-ttu-id="6840b-134">Se você ainda não instalou Olá SDK do Azure, clique em **instalar SDK do Azure** tooopen Olá [página Downloads do Azure](https://azure.microsoft.com/downloads/)e, em seguida, baixe Olá SDK para o idioma de saudação em que você preferir toodevelop seu código.</span><span class="sxs-lookup"><span data-stu-id="6840b-134">If you haven't installed hello Azure SDK, click **Install Azure SDK** tooopen hello [Azure Downloads page](https://azure.microsoft.com/downloads/), and then download hello SDK for hello language in which you prefer toodevelop your code.</span></span> <span data-ttu-id="6840b-135">(Você terá uma oportunidade toodo isso mais tarde.)</span><span class="sxs-lookup"><span data-stu-id="6840b-135">(You'll have an opportunity toodo this later.)</span></span>
* <span data-ttu-id="6840b-136">Se quaisquer instâncias de função exigem um certificado, crie certificados hello.</span><span class="sxs-lookup"><span data-stu-id="6840b-136">If any role instances require a certificate, create hello certificates.</span></span> <span data-ttu-id="6840b-137">Os serviços de nuvem requerem um arquivo .pfx e uma chave privada.</span><span class="sxs-lookup"><span data-stu-id="6840b-137">Cloud services require a .pfx file with a private key.</span></span> <span data-ttu-id="6840b-138">Você pode carregar Olá certificados tooAzure como criar e implantar o serviço de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="6840b-138">You can upload hello certificates tooAzure as you create and deploy hello cloud service.</span></span>

## <a name="create-and-deploy"></a><span data-ttu-id="6840b-139">Criar e implantar</span><span class="sxs-lookup"><span data-stu-id="6840b-139">Create and deploy</span></span>
1. <span data-ttu-id="6840b-140">Faça logon no toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="6840b-140">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="6840b-141">Clique em **Novo > computação**e, em seguida, role para baixo clique tooand **serviço de nuvem**.</span><span class="sxs-lookup"><span data-stu-id="6840b-141">Click **New > Compute**, and then scroll down tooand click **Cloud Service**.</span></span>

    ![Publicar o serviço de nuvem](media/cloud-services-how-to-create-deploy-portal/create-cloud-service.png)
3. <span data-ttu-id="6840b-143">Em Olá novo **serviço de nuvem** folha, insira um valor para Olá **nome DNS**.</span><span class="sxs-lookup"><span data-stu-id="6840b-143">In hello new **Cloud Service** blade, enter a value for hello **DNS name**.</span></span>
4. <span data-ttu-id="6840b-144">Crie um novo **Grupo de Recursos** ou selecione um existente.</span><span class="sxs-lookup"><span data-stu-id="6840b-144">Create a new **Resource Group** or select an existing one.</span></span>
5. <span data-ttu-id="6840b-145">Selecione um **Local**.</span><span class="sxs-lookup"><span data-stu-id="6840b-145">Select a **Location**.</span></span>
6. <span data-ttu-id="6840b-146">Clique em **Pacote**.</span><span class="sxs-lookup"><span data-stu-id="6840b-146">Click **Package**.</span></span> <span data-ttu-id="6840b-147">Isso abrirá o hello **carregar um pacote** folha.</span><span class="sxs-lookup"><span data-stu-id="6840b-147">This will open hello **Upload a package** blade.</span></span> <span data-ttu-id="6840b-148">Preencha os campos de saudação necessário.</span><span class="sxs-lookup"><span data-stu-id="6840b-148">Fill in hello required fields.</span></span> <span data-ttu-id="6840b-149">Se alguma das funções contiver uma única instância, verifique se **Implantar mesmo se uma ou mais funções contiverem uma única instância** está marcado.</span><span class="sxs-lookup"><span data-stu-id="6840b-149">If any of your roles contain a single instance, ensure **Deploy even if one or more roles contain a single instance** is selected.</span></span>
7. <span data-ttu-id="6840b-150">Verifique se a opção **Iniciar implantação** está selecionada.</span><span class="sxs-lookup"><span data-stu-id="6840b-150">Make sure that **Start deployment** is selected.</span></span>
8. <span data-ttu-id="6840b-151">Clique em **Okey** que fechará Olá **carregar um pacote** folha.</span><span class="sxs-lookup"><span data-stu-id="6840b-151">Click **OK** which will close hello **Upload a package** blade.</span></span>
9. <span data-ttu-id="6840b-152">Se você não tem qualquer tooadd de certificados, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="6840b-152">If you do not have any certificates tooadd, click **Create**.</span></span>

    ![Publicar o serviço de nuvem](media/cloud-services-how-to-create-deploy-portal/select-package.png)

## <a name="upload-a-certificate"></a><span data-ttu-id="6840b-154">Carregar um certificado</span><span class="sxs-lookup"><span data-stu-id="6840b-154">Upload a certificate</span></span>
<span data-ttu-id="6840b-155">Se o pacote de implantação foi [configurado certificados toouse](cloud-services-configure-ssl-certificate-portal.md#modify), você pode carregar o certificado de saudação agora.</span><span class="sxs-lookup"><span data-stu-id="6840b-155">If your deployment package was [configured toouse certificates](cloud-services-configure-ssl-certificate-portal.md#modify), you can upload hello certificate now.</span></span>

1. <span data-ttu-id="6840b-156">Selecione **certificados**e em Olá **adicionar certificados** folha, selecione o arquivo de. pfx de certificado SSL hello e forneça Olá **senha** certificado Olá,</span><span class="sxs-lookup"><span data-stu-id="6840b-156">Select **Certificates**, and on hello **Add certificates** blade, select hello SSL certificate .pfx file, and then provide hello **Password** for hello certificate,</span></span>
2. <span data-ttu-id="6840b-157">Clique em **anexar certificado**e, em seguida, clique em **Okey** em Olá **adicionar certificados** folha.</span><span class="sxs-lookup"><span data-stu-id="6840b-157">Click **Attach certificate**, and then click **OK** on hello **Add certificates** blade.</span></span>
3. <span data-ttu-id="6840b-158">Clique em **criar** em Olá **serviço de nuvem** folha.</span><span class="sxs-lookup"><span data-stu-id="6840b-158">Click **Create** on hello **Cloud Service** blade.</span></span> <span data-ttu-id="6840b-159">Quando a implantação de saudação atingiu Olá **pronto** status, você poderá toohello próximas etapas.</span><span class="sxs-lookup"><span data-stu-id="6840b-159">When hello deployment has reached hello **Ready** status, you can proceed toohello next steps.</span></span>

    ![Publicar o serviço de nuvem](media/cloud-services-how-to-create-deploy-portal/attach-cert.png)

## <a name="verify-your-deployment-completed-successfully"></a><span data-ttu-id="6840b-161">Verifique se a implantação foi concluída com êxito</span><span class="sxs-lookup"><span data-stu-id="6840b-161">Verify your deployment completed successfully</span></span>
1. <span data-ttu-id="6840b-162">Clique em instância de serviço de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="6840b-162">Click hello cloud service instance.</span></span>

    <span data-ttu-id="6840b-163">Hello status deve mostrar que o serviço de saudação **executando**.</span><span class="sxs-lookup"><span data-stu-id="6840b-163">hello status should show that hello service is **Running**.</span></span>
2. <span data-ttu-id="6840b-164">Em **Essentials**, clique em Olá **URL do Site** tooopen sua nuvem de serviço em um navegador da web.</span><span class="sxs-lookup"><span data-stu-id="6840b-164">Under **Essentials**, click hello **Site URL** tooopen your cloud service in a web browser.</span></span>

    ![CloudServices_QuickGlance](./media/cloud-services-how-to-create-deploy-portal/running.png)

[TFSTutorialForCloudService]: http://go.microsoft.com/fwlink/?LinkID=251796

## <a name="next-steps"></a><span data-ttu-id="6840b-166">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6840b-166">Next steps</span></span>
* <span data-ttu-id="6840b-167">[Configuração geral do serviço de nuvem](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6840b-167">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="6840b-168">Configurar um [nome de domínio personalizado](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6840b-168">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="6840b-169">[Gerenciar seu serviço de nuvem](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6840b-169">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
* <span data-ttu-id="6840b-170">Configurar [certificados SSL](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6840b-170">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
