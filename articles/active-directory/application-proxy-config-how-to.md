---
title: Como configurar um aplicativo de Application Proxy| Microsoft Docs
description: Saiba como criar e configurar um aplicativo de Application Proxy em poucas etapas simples
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
ms.openlocfilehash: c8f98536048a85ebb3f061d840457130579196d9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-an-application-proxy-application"></a><span data-ttu-id="f1fa6-103">Como configurar um aplicativo de Application Proxy</span><span class="sxs-lookup"><span data-stu-id="f1fa6-103">How to configure an Application Proxy application</span></span>

<span data-ttu-id="f1fa6-104">Este artigo o ajudará a compreender como configurar um aplicativo de Application Proxy no Azure AD para expor seus aplicativos locais para a nuvem.</span><span class="sxs-lookup"><span data-stu-id="f1fa6-104">This article help you to understand how to configure an Application Proxy application within Azure AD to expose your on-premises applications to the cloud.</span></span>

## <a name="recommended-documents"></a><span data-ttu-id="f1fa6-105">Documentos recomendados</span><span class="sxs-lookup"><span data-stu-id="f1fa6-105">Recommended documents</span></span> 

<span data-ttu-id="f1fa6-106">Para saber mais sobre a criação de um aplicativo de Application Proxy por meio do Portal de administração e configurações iniciais, siga o [publicar aplicativos usando o Application Proxy do Azure AD](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="f1fa6-106">To learn about the initial configurations and creation of an Application Proxy application through the Admin Portal, follow the [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span></span>

<span data-ttu-id="f1fa6-107">Para obter detalhes sobre como configurar conectores, consulte [habilitar Application Proxy no portal do Azure](active-directory-application-proxy-enable.md).</span><span class="sxs-lookup"><span data-stu-id="f1fa6-107">For details on configuring Connectors, see [Enable Application Proxy in the Azure portal](active-directory-application-proxy-enable.md).</span></span>

<span data-ttu-id="f1fa6-108">Para obter informações sobre como carregar certificados e usar domínios personalizados, consulte [trabalhando com domínios personalizados no Application Proxy do Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span><span class="sxs-lookup"><span data-stu-id="f1fa6-108">For information on uploading certificates and using custom domains, see [Working with custom domains in Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span></span>

## <a name="create-the-applicationsetting-the-urls"></a><span data-ttu-id="f1fa6-109">Criar o aplicativo/Definindo as URLs</span><span class="sxs-lookup"><span data-stu-id="f1fa6-109">Create the Application/Setting the URLs</span></span>

<span data-ttu-id="f1fa6-110">Se você estiver seguindo as etapas na documentação [publicar aplicativos usando o Application Proxy do Azure AD](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal) e está recebendo um erro ao criar o aplicativo, consulte os detalhes do erro para obter informações e sugestões para corrigir o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f1fa6-110">If you are following the steps in the [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal) documentation and are getting an error creating the application, see the error details for information and suggestions for how to fix the application.</span></span> <span data-ttu-id="f1fa6-111">A maioria das mensagens de erro incluem uma correção sugerida.</span><span class="sxs-lookup"><span data-stu-id="f1fa6-111">Most error messages include a suggested fix.</span></span> <span data-ttu-id="f1fa6-112">Para evitar erros comuns, verifique se:</span><span class="sxs-lookup"><span data-stu-id="f1fa6-112">To avoid common errors, verify:</span></span>

-   <span data-ttu-id="f1fa6-113">Você é um administrador com permissão para criar um aplicativo de Application Proxy</span><span class="sxs-lookup"><span data-stu-id="f1fa6-113">You are an administrator with permission to create an Application Proxy application</span></span>

-   <span data-ttu-id="f1fa6-114">A URL interna é exclusiva</span><span class="sxs-lookup"><span data-stu-id="f1fa6-114">The internal URL is unique</span></span>

-   <span data-ttu-id="f1fa6-115">A URL externa é exclusiva</span><span class="sxs-lookup"><span data-stu-id="f1fa6-115">The external URL is unique</span></span>

-   <span data-ttu-id="f1fa6-116">As URLs começam com http ou https e terminam com um "/"</span><span class="sxs-lookup"><span data-stu-id="f1fa6-116">The URLs start with http or https, and end with a “/”</span></span>

-   <span data-ttu-id="f1fa6-117">A URL deve ser um nome de domínio, não um endereço IP</span><span class="sxs-lookup"><span data-stu-id="f1fa6-117">The URL should be a domain name, not an IP address</span></span>

<span data-ttu-id="f1fa6-118">A mensagem de erro deve ser exibida no canto superior direito ao criar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f1fa6-118">The error message should display in the top right corner when you create the application.</span></span> <span data-ttu-id="f1fa6-119">Você também pode selecionar o ícone de notificação para ver as mensagens de erro.</span><span class="sxs-lookup"><span data-stu-id="f1fa6-119">You can also select the notification icon to see the error messages.</span></span>

   ![Prompt de notificação](./media/application-proxy-config-how-to/error-message.png)

## <a name="configure-connectorsconnector-groups"></a><span data-ttu-id="f1fa6-121">Configurar grupos de conectores/conectores</span><span class="sxs-lookup"><span data-stu-id="f1fa6-121">Configure connectors/connector groups</span></span>

<span data-ttu-id="f1fa6-122">Se você tiver dificuldades para configurar seu aplicativo por causa de aviso sobre conectores e grupos de conector, consulte as instruções sobre como habilitar o Application Proxy para obter detalhes sobre como baixar conectores.</span><span class="sxs-lookup"><span data-stu-id="f1fa6-122">If you are having difficulty configuring your application because of warning about the connectors and connector groups, see instructions on enabling Application Proxy for details on how to download connectors.</span></span> <span data-ttu-id="f1fa6-123">Se você quiser saber mais sobre conectores, consulte a [documentação de conectores](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors).</span><span class="sxs-lookup"><span data-stu-id="f1fa6-123">If you want to learn more about connectors, see the [connectors documentation](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors).</span></span>

<span data-ttu-id="f1fa6-124">Se os conectores estão inativos, isso significa que eles são incapazes de alcançar o serviço.</span><span class="sxs-lookup"><span data-stu-id="f1fa6-124">If your connectors are inactive, this means that they are unable to reach the service.</span></span> <span data-ttu-id="f1fa6-125">Isso geralmente é porque todas as portas necessárias não estão abertas.</span><span class="sxs-lookup"><span data-stu-id="f1fa6-125">This is often because all the required ports are not open.</span></span> <span data-ttu-id="f1fa6-126">Para ver uma lista de portas necessárias, consulte a seção de pré-requisitos da documentação para habilitação do Application Proxy.</span><span class="sxs-lookup"><span data-stu-id="f1fa6-126">To see a list of required ports, see the pre-requisites section of the enabling Application Proxy documentation.</span></span>

## <a name="upload-certificates-for-custom-domains"></a><span data-ttu-id="f1fa6-127">Carregar certificados para domínios personalizados</span><span class="sxs-lookup"><span data-stu-id="f1fa6-127">Upload certificates for custom domains</span></span>

<span data-ttu-id="f1fa6-128">Domínios personalizados permitem que você especifique o domínio de suas URLs externas.</span><span class="sxs-lookup"><span data-stu-id="f1fa6-128">Custom Domains allow you to specify the domain of your external URLs.</span></span> <span data-ttu-id="f1fa6-129">Para usar domínios personalizados, você precisa carregar o certificado para esse domínio.</span><span class="sxs-lookup"><span data-stu-id="f1fa6-129">To use custom domains, you need to upload the certificate for that domain.</span></span> <span data-ttu-id="f1fa6-130">Para obter informações sobre como usar domínios personalizados e certificados, consulte [trabalhando com domínios personalizados no Application Proxy do Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span><span class="sxs-lookup"><span data-stu-id="f1fa6-130">For information on using custom domains and certificates, see [Working with custom domains in Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span></span> 

<span data-ttu-id="f1fa6-131">Se você estiver encontrando problemas ao carregar o certificado, procure as mensagens de erro no portal para obter informações adicionais sobre o problema com o certificado.</span><span class="sxs-lookup"><span data-stu-id="f1fa6-131">If you are encountering issues uploading your certificate, look for the error messages in the portal for additional information on the problem with the certificate.</span></span> <span data-ttu-id="f1fa6-132">Problemas de certificado comuns incluem:</span><span class="sxs-lookup"><span data-stu-id="f1fa6-132">Common certificate problems include:</span></span>

-   <span data-ttu-id="f1fa6-133">Certificado expirado</span><span class="sxs-lookup"><span data-stu-id="f1fa6-133">Expired certificate</span></span>

-   <span data-ttu-id="f1fa6-134">O certificado é auto-assinado</span><span class="sxs-lookup"><span data-stu-id="f1fa6-134">Certificate is self-signed</span></span>

-   <span data-ttu-id="f1fa6-135">Certificado está sem a chave privada</span><span class="sxs-lookup"><span data-stu-id="f1fa6-135">Certificate is missing the private key</span></span>

<span data-ttu-id="f1fa6-136">A mensagem de erro é exibida no canto superior direito ao tentar carregar o certificado.</span><span class="sxs-lookup"><span data-stu-id="f1fa6-136">The error message display in the top right corner as you try to upload the certificate.</span></span> <span data-ttu-id="f1fa6-137">Você também pode selecionar o ícone de notificação para ver as mensagens de erro.</span><span class="sxs-lookup"><span data-stu-id="f1fa6-137">You can also select the notification icon to see the error messages.</span></span>

   ![Prompt de notificação](./media/application-proxy-config-how-to/error-message2.png)

## <a name="next-steps"></a><span data-ttu-id="f1fa6-139">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f1fa6-139">Next steps</span></span>
[<span data-ttu-id="f1fa6-140">Publicar aplicativos usando o Proxy de Aplicativo do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="f1fa6-140">Publish applications using Azure AD Application Proxy</span></span>](application-proxy-publish-azure-portal.md)
