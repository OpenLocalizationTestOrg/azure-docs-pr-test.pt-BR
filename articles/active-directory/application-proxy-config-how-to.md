---
title: aaaHow tooconfigure um aplicativo de Proxy de aplicativo | Microsoft Docs
description: Saiba como toocreate um configurar um aplicativo de Proxy de aplicativo em algumas etapas simples
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: c64019098fc124e4fe10b8288830bcd2b7239d3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-an-application-proxy-application"></a><span data-ttu-id="e7221-103">Como tooconfigure um aplicativo de Proxy de aplicativo</span><span class="sxs-lookup"><span data-stu-id="e7221-103">How tooconfigure an Application Proxy application</span></span>

<span data-ttu-id="e7221-104">Este artigo ajuda toounderstand como tooconfigure um aplicativo de Proxy de aplicativo no AD do Azure tooexpose seu toohello de aplicativos local nuvem.</span><span class="sxs-lookup"><span data-stu-id="e7221-104">This article help you toounderstand how tooconfigure an Application Proxy application within Azure AD tooexpose your on-premises applications toohello cloud.</span></span>

## <a name="recommended-documents"></a><span data-ttu-id="e7221-105">Documentos recomendados</span><span class="sxs-lookup"><span data-stu-id="e7221-105">Recommended documents</span></span> 

<span data-ttu-id="e7221-106">toolearn sobre configurações iniciais hello e criação de um aplicativo de Proxy de aplicativo por meio do Portal de administração de saudação siga Olá [publicar aplicativos usando o Proxy de aplicativo do Azure AD](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="e7221-106">toolearn about hello initial configurations and creation of an Application Proxy application through hello Admin Portal, follow hello [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span></span>

<span data-ttu-id="e7221-107">Para obter detalhes sobre como configurar conectores, consulte [habilitar Proxy de aplicativo no portal do Azure de saudação](active-directory-application-proxy-enable.md).</span><span class="sxs-lookup"><span data-stu-id="e7221-107">For details on configuring Connectors, see [Enable Application Proxy in hello Azure portal](active-directory-application-proxy-enable.md).</span></span>

<span data-ttu-id="e7221-108">Para obter informações sobre como carregar certificados e usar domínios personalizados, consulte [trabalhando com domínios personalizados no Application Proxy do Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span><span class="sxs-lookup"><span data-stu-id="e7221-108">For information on uploading certificates and using custom domains, see [Working with custom domains in Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span></span>

## <a name="create-hello-applicationsetting-hello-urls"></a><span data-ttu-id="e7221-109">Criar hello URLs de saudação de configuração do aplicativo</span><span class="sxs-lookup"><span data-stu-id="e7221-109">Create hello Application/Setting hello URLs</span></span>

<span data-ttu-id="e7221-110">Se você estiver seguindo as etapas em Olá Olá [publicar aplicativos usando o Proxy de aplicativo do Azure AD](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal) documentação e estão obtendo um erro ao criar o aplicativo hello, consulte detalhes do erro Olá para obter informações e sugestões para aplicativo de hello toofix.</span><span class="sxs-lookup"><span data-stu-id="e7221-110">If you are following hello steps in hello [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal) documentation and are getting an error creating hello application, see hello error details for information and suggestions for how toofix hello application.</span></span> <span data-ttu-id="e7221-111">A maioria das mensagens de erro incluem uma correção sugerida.</span><span class="sxs-lookup"><span data-stu-id="e7221-111">Most error messages include a suggested fix.</span></span> <span data-ttu-id="e7221-112">erros comuns de tooavoid, verifique se:</span><span class="sxs-lookup"><span data-stu-id="e7221-112">tooavoid common errors, verify:</span></span>

-   <span data-ttu-id="e7221-113">Você é um administrador com permissão toocreate um aplicativo de Proxy de aplicativo</span><span class="sxs-lookup"><span data-stu-id="e7221-113">You are an administrator with permission toocreate an Application Proxy application</span></span>

-   <span data-ttu-id="e7221-114">URL interna Olá é exclusivo</span><span class="sxs-lookup"><span data-stu-id="e7221-114">hello internal URL is unique</span></span>

-   <span data-ttu-id="e7221-115">URL externa de saudação é exclusivo</span><span class="sxs-lookup"><span data-stu-id="e7221-115">hello external URL is unique</span></span>

-   <span data-ttu-id="e7221-116">Olá início URLs com http ou https e terminar com um "/"</span><span class="sxs-lookup"><span data-stu-id="e7221-116">hello URLs start with http or https, and end with a “/”</span></span>

-   <span data-ttu-id="e7221-117">Olá URL deve ser um nome de domínio, não um endereço IP</span><span class="sxs-lookup"><span data-stu-id="e7221-117">hello URL should be a domain name, not an IP address</span></span>

<span data-ttu-id="e7221-118">mensagem de erro de saudação deve exibir no canto superior direito da saudação quando você cria o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="e7221-118">hello error message should display in hello top right corner when you create hello application.</span></span> <span data-ttu-id="e7221-119">Você também pode selecionar as mensagens de erro de Olá Olá notificação ícone toosee.</span><span class="sxs-lookup"><span data-stu-id="e7221-119">You can also select hello notification icon toosee hello error messages.</span></span>

   ![Prompt de notificação](./media/application-proxy-config-how-to/error-message.png)

## <a name="configure-connectorsconnector-groups"></a><span data-ttu-id="e7221-121">Configurar grupos de conectores/conectores</span><span class="sxs-lookup"><span data-stu-id="e7221-121">Configure connectors/connector groups</span></span>

<span data-ttu-id="e7221-122">Se você estiver tendo dificuldades para configurar seu aplicativo por causa de aviso sobre conectores hello e grupos de conector, consulte as instruções sobre como habilitar o Proxy de aplicativo para obter detalhes sobre como conectores toodownload.</span><span class="sxs-lookup"><span data-stu-id="e7221-122">If you are having difficulty configuring your application because of warning about hello connectors and connector groups, see instructions on enabling Application Proxy for details on how toodownload connectors.</span></span> <span data-ttu-id="e7221-123">Se você quiser toolearn mais sobre conectores, consulte Olá [documentação conectores](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors).</span><span class="sxs-lookup"><span data-stu-id="e7221-123">If you want toolearn more about connectors, see hello [connectors documentation](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors).</span></span>

<span data-ttu-id="e7221-124">Se os conectores estão inativos, isso significa que eles são o serviço de saudação tooreach não é possível.</span><span class="sxs-lookup"><span data-stu-id="e7221-124">If your connectors are inactive, this means that they are unable tooreach hello service.</span></span> <span data-ttu-id="e7221-125">Isso geralmente é porque todas as portas de saudação necessários não estiverem abertas.</span><span class="sxs-lookup"><span data-stu-id="e7221-125">This is often because all hello required ports are not open.</span></span> <span data-ttu-id="e7221-126">toosee uma lista de portas necessárias, consulte seção pré-requisitos Olá Olá habilitando a documentação do Proxy de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e7221-126">toosee a list of required ports, see hello pre-requisites section of hello enabling Application Proxy documentation.</span></span>

## <a name="upload-certificates-for-custom-domains"></a><span data-ttu-id="e7221-127">Carregar certificados para domínios personalizados</span><span class="sxs-lookup"><span data-stu-id="e7221-127">Upload certificates for custom domains</span></span>

<span data-ttu-id="e7221-128">Domínios personalizados permitem que você toospecify domínio Olá suas URLs externas.</span><span class="sxs-lookup"><span data-stu-id="e7221-128">Custom Domains allow you toospecify hello domain of your external URLs.</span></span> <span data-ttu-id="e7221-129">toouse de domínios personalizados, você precisa de tooupload Olá certificado para esse domínio.</span><span class="sxs-lookup"><span data-stu-id="e7221-129">toouse custom domains, you need tooupload hello certificate for that domain.</span></span> <span data-ttu-id="e7221-130">Para obter informações sobre como usar domínios personalizados e certificados, consulte [trabalhando com domínios personalizados no Application Proxy do Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span><span class="sxs-lookup"><span data-stu-id="e7221-130">For information on using custom domains and certificates, see [Working with custom domains in Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span></span> 

<span data-ttu-id="e7221-131">Se você estiver encontrando problemas ao carregar o certificado, procure por mensagens de erro Olá no portal de saudação para obter informações adicionais sobre o problema de saudação com certificado de saudação.</span><span class="sxs-lookup"><span data-stu-id="e7221-131">If you are encountering issues uploading your certificate, look for hello error messages in hello portal for additional information on hello problem with hello certificate.</span></span> <span data-ttu-id="e7221-132">Problemas de certificado comuns incluem:</span><span class="sxs-lookup"><span data-stu-id="e7221-132">Common certificate problems include:</span></span>

-   <span data-ttu-id="e7221-133">Certificado expirado</span><span class="sxs-lookup"><span data-stu-id="e7221-133">Expired certificate</span></span>

-   <span data-ttu-id="e7221-134">O certificado é auto-assinado</span><span class="sxs-lookup"><span data-stu-id="e7221-134">Certificate is self-signed</span></span>

-   <span data-ttu-id="e7221-135">Certificado está faltando a chave privada Olá</span><span class="sxs-lookup"><span data-stu-id="e7221-135">Certificate is missing hello private key</span></span>

<span data-ttu-id="e7221-136">exibição de mensagem de erro Olá no hello canto superior direito, tente o certificado de saudação tooupload.</span><span class="sxs-lookup"><span data-stu-id="e7221-136">hello error message display in hello top right corner as you try tooupload hello certificate.</span></span> <span data-ttu-id="e7221-137">Você também pode selecionar as mensagens de erro de Olá Olá notificação ícone toosee.</span><span class="sxs-lookup"><span data-stu-id="e7221-137">You can also select hello notification icon toosee hello error messages.</span></span>

   ![Prompt de notificação](./media/application-proxy-config-how-to/error-message2.png)

## <a name="next-steps"></a><span data-ttu-id="e7221-139">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e7221-139">Next steps</span></span>
[<span data-ttu-id="e7221-140">Publicar aplicativos usando o Proxy de Aplicativo do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e7221-140">Publish applications using Azure AD Application Proxy</span></span>](application-proxy-publish-azure-portal.md)
