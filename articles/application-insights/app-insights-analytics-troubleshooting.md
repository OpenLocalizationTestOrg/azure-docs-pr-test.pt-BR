---
title: Solucionar problemas do Analytics no Azure Application Insights | Microsoft Docs
description: 'Problemas com a Application Insights Analytics? Comece por aqui. '
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 9bbd5859-3584-4d80-9b6d-d5910fa48baa
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/11/2016
ms.author: bwren
ms.openlocfilehash: 02df117908fc1790e8cfb9ec0a7218c1b8be856c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-analytics-in-application-insights"></a><span data-ttu-id="ba742-104">Solução de problemas do Analytics no Application Insights</span><span class="sxs-lookup"><span data-stu-id="ba742-104">Troubleshoot Analytics in Application Insights</span></span>
<span data-ttu-id="ba742-105">Problemas com a [Application Insights Analytics](app-insights-analytics.md)?</span><span class="sxs-lookup"><span data-stu-id="ba742-105">Problems with [Application Insights Analytics](app-insights-analytics.md)?</span></span> <span data-ttu-id="ba742-106">Comece por aqui.</span><span class="sxs-lookup"><span data-stu-id="ba742-106">Start here.</span></span> <span data-ttu-id="ba742-107">A análise é a poderosa ferramenta de pesquisa do Azure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ba742-107">Analytics is the powerful search tool of Azure Application Insights.</span></span>

## <a name="limits"></a><span data-ttu-id="ba742-108">Limites</span><span class="sxs-lookup"><span data-stu-id="ba742-108">Limits</span></span>
* <span data-ttu-id="ba742-109">No momento, os resultados da consulta são limitados apenas a uma semana de dados anteriores.</span><span class="sxs-lookup"><span data-stu-id="ba742-109">At present, query results are limited to just over a week of past data.</span></span>
* <span data-ttu-id="ba742-110">Navegadores em que testamos: edições mais recentes do Chrome, Edge e Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="ba742-110">Browsers we test on: latest editions of Chrome, Edge, and Internet Explorer.</span></span>

## <a name="known-incompatible-browser-extensions"></a><span data-ttu-id="ba742-111">Extensões do navegador incompatíveis conhecidas</span><span class="sxs-lookup"><span data-stu-id="ba742-111">Known incompatible browser extensions</span></span>
* <span data-ttu-id="ba742-112">Ghostery</span><span class="sxs-lookup"><span data-stu-id="ba742-112">Ghostery</span></span>

<span data-ttu-id="ba742-113">Desabilite a extensão ou use um navegador diferente.</span><span class="sxs-lookup"><span data-stu-id="ba742-113">Disable the extension or use a different browser.</span></span>

## <span data-ttu-id="ba742-114"><a name="e-a"></a> "Erro inesperado"</span><span class="sxs-lookup"><span data-stu-id="ba742-114"><a name="e-a"></a> "Unexpected error"</span></span>
![Tela de erro inesperado](./media/app-insights-analytics-troubleshooting/010.png)

<span data-ttu-id="ba742-116">Ocorreu um erro interno durante o tempo de execução do portal. Exceção sem tratamento.</span><span class="sxs-lookup"><span data-stu-id="ba742-116">Internal error occurred during portal runtime – unhandled exception.</span></span>

* <span data-ttu-id="ba742-117">Limpe o cache do navegador.</span><span class="sxs-lookup"><span data-stu-id="ba742-117">Clean the browser's cache.</span></span> 

## <span data-ttu-id="ba742-118"><a name="e-b"></a>403... tentar recarregar</span><span class="sxs-lookup"><span data-stu-id="ba742-118"><a name="e-b"></a>403 ... please try to reload</span></span>
![403... tente recarregar](./media/app-insights-analytics-troubleshooting/020.png)

<span data-ttu-id="ba742-120">Ocorreu um erro de autenticação (durante a autenticação ou durante a geração de token de acesso).</span><span class="sxs-lookup"><span data-stu-id="ba742-120">An authentication related error occurred (during authentication or during access token generation).</span></span> <span data-ttu-id="ba742-121">O portal pode não ter como se recuperar sem alterar as configurações do navegador.</span><span class="sxs-lookup"><span data-stu-id="ba742-121">The portal may have no way to  recover without changing browser settings.</span></span>

* <span data-ttu-id="ba742-122">Verifique [se os cookies de terceiros estão habilitados](#cookies) no navegador.</span><span class="sxs-lookup"><span data-stu-id="ba742-122">Verify [third party cookies are enabled](#cookies) in the browser.</span></span> 

## <span data-ttu-id="ba742-123"><a name="authentication"></a>403... verificar zona de segurança</span><span class="sxs-lookup"><span data-stu-id="ba742-123"><a name="authentication"></a>403 ... verify security zone</span></span>
![403... verifique a zona de segurança](./media/app-insights-analytics-troubleshooting/030.png)

<span data-ttu-id="ba742-125">Ocorreu um erro de autenticação (durante a autenticação ou durante a geração de token de acesso).</span><span class="sxs-lookup"><span data-stu-id="ba742-125">An authentication related error occurred (during authentication or during access token generation).</span></span> <span data-ttu-id="ba742-126">O portal pode não ter como se recuperar sem alterar as configurações do navegador.</span><span class="sxs-lookup"><span data-stu-id="ba742-126">The portal may have no way to  recover without changing browser settings.</span></span>

1. <span data-ttu-id="ba742-127">Verifique [se os cookies de terceiros estão habilitados](#cookies) no navegador.</span><span class="sxs-lookup"><span data-stu-id="ba742-127">Verify [third party cookies are enabled](#cookies) in the browser.</span></span> 
2. <span data-ttu-id="ba742-128">Você usou um favorito, indicador ou link salvo para abrir o portal do Analytics?</span><span class="sxs-lookup"><span data-stu-id="ba742-128">Did you use a favorite, bookmark or saved link to open the Analytics portal?</span></span> <span data-ttu-id="ba742-129">Você entrou com credenciais diferentes daquelas usadas ao salvar o link?</span><span class="sxs-lookup"><span data-stu-id="ba742-129">Are you signed in with different credentials than you used when you saved the link?</span></span>
3. <span data-ttu-id="ba742-130">Tente usar uma janela do navegador privada/anônima (depois de fechar todas as janelas desse tipo).</span><span class="sxs-lookup"><span data-stu-id="ba742-130">Try using an in-private/incognito browser window (after closing all such windows).</span></span> <span data-ttu-id="ba742-131">Você precisará fornecer suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="ba742-131">You'll have to provide your credentials.</span></span> 
4. <span data-ttu-id="ba742-132">Abra outra janela do navegador (comum) e vá para [Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ba742-132">Open another (ordinary) browser window and go to [Azure](https://portal.azure.com).</span></span> <span data-ttu-id="ba742-133">Saia. Em seguida, abra o link e entre com as credenciais corretas.</span><span class="sxs-lookup"><span data-stu-id="ba742-133">Sign out. Then open your link and sign in with the correct credentials.</span></span>
5. <span data-ttu-id="ba742-134">Os usuários do Edge e do Internet Explorer também podem receber esse erro quando não há suporte para as configurações de zona confiável.</span><span class="sxs-lookup"><span data-stu-id="ba742-134">Edge and Internet Explorer users can also get this error when trusted zone settings are not supported.</span></span>
   
    <span data-ttu-id="ba742-135">Verifique se o [portal Analytics](https://analytics.applicationinsights.io) e o [portal do Azure Active Directory](https://portal.azure.com) estão na mesma zona de segurança:</span><span class="sxs-lookup"><span data-stu-id="ba742-135">Verify both [Analytics portal](https://analytics.applicationinsights.io) and [Azure Active Directory portal](https://portal.azure.com) are in the same security zone:</span></span>
   
   * <span data-ttu-id="ba742-136">No Internet Explorer, abra **Opções da Internet**, **Segurança**, **Sites Confiáveis**, **Sites**:</span><span class="sxs-lookup"><span data-stu-id="ba742-136">In Internet Explorer, open **Internet Options**, **Security**, **Trusted sites**, **Sites**:</span></span>
     
     ![Caixa de diálogo Opções da Internet, adicionando um site aos Sites Confiáveis](./media/app-insights-analytics-troubleshooting/033.png)
     
     <span data-ttu-id="ba742-138">Na Lista de sites, se qualquer uma das seguintes URLs estiverem incluídas, verifique se as outras também estão:</span><span class="sxs-lookup"><span data-stu-id="ba742-138">In the Websites list, if any of the following URLs are included, make sure that the others are included also:</span></span>
     
     <span data-ttu-id="ba742-139">https://analytics.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="ba742-139">https://analytics.applicationinsights.io</span></span><br/>
     <span data-ttu-id="ba742-140">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="ba742-140">https://login.microsoftonline.com</span></span><br/>
     <span data-ttu-id="ba742-141">https://login.windows.net</span><span class="sxs-lookup"><span data-stu-id="ba742-141">https://login.windows.net</span></span>

## <span data-ttu-id="ba742-142"><a name="e-d"></a>404 ... Recurso não encontrado</span><span class="sxs-lookup"><span data-stu-id="ba742-142"><a name="e-d"></a>404 ... Resource not found</span></span>
![404... recurso não encontrado](./media/app-insights-analytics-troubleshooting/040.png)

<span data-ttu-id="ba742-144">O recurso de aplicativo foi excluído do Application Insights e não está mais disponível.</span><span class="sxs-lookup"><span data-stu-id="ba742-144">Application resource was deleted from Application Insights and isn’t available anymore.</span></span> <span data-ttu-id="ba742-145">Isso pode acontecer se você salvou a URL para a página do Analytics.</span><span class="sxs-lookup"><span data-stu-id="ba742-145">This can happen if you saved the URL to the Analytics page.</span></span>

## <span data-ttu-id="ba742-146"><a name="e-e"></a>403 ... Sem autorização</span><span class="sxs-lookup"><span data-stu-id="ba742-146"><a name="e-e"></a>403 ... No authorization</span></span>
![403 ... não autorizado](./media/app-insights-analytics-troubleshooting/050.png)

<span data-ttu-id="ba742-148">Você não tem permissão para abrir este aplicativo no Analytics.</span><span class="sxs-lookup"><span data-stu-id="ba742-148">You don't have permission to open this application in Analytics.</span></span>

* <span data-ttu-id="ba742-149">Você obteve o link com outra pessoa?</span><span class="sxs-lookup"><span data-stu-id="ba742-149">Did you get the link from someone else?</span></span> <span data-ttu-id="ba742-150">Peça a ela para verificar se você está incluído como [leitor ou colaborador para esse grupo de recursos](app-insights-resources-roles-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="ba742-150">Ask them to make sure you are in the [readers or contributors for this resource group](app-insights-resources-roles-access-control.md).</span></span>
* <span data-ttu-id="ba742-151">Você salvou o link usando credenciais diferentes?</span><span class="sxs-lookup"><span data-stu-id="ba742-151">Did you save the link using different credentials?</span></span> <span data-ttu-id="ba742-152">Abra o [Portal do Azure](https://portal.azure.com), saia e tente acessar novamente esse link fornecendo as credenciais corretas.</span><span class="sxs-lookup"><span data-stu-id="ba742-152">Open the [Azure portal](https://portal.azure.com), sign out, and then try this link again, providing the correct credentials.</span></span>

## <span data-ttu-id="ba742-153"><a name="html-storage"></a>403 ... Armazenamento HTML5</span><span class="sxs-lookup"><span data-stu-id="ba742-153"><a name="html-storage"></a>403 ... HTML5 Storage</span></span>
<span data-ttu-id="ba742-154">Nosso portal usa sessionStorage e localStorage do HTML5.</span><span class="sxs-lookup"><span data-stu-id="ba742-154">Our portal uses HTML5 localStorage and sessionStorage.</span></span>

* <span data-ttu-id="ba742-155">Chrome: configurações, privacidade, configurações de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="ba742-155">Chrome: Settings, privacy, content settings.</span></span>
* <span data-ttu-id="ba742-156">Internet Explorer: Opções da Internet, guia Avançado, Segurança, Habilitar o armazenamento DOM</span><span class="sxs-lookup"><span data-stu-id="ba742-156">Internet Explorer: Internet Options, Advanced tab, Security, Enable DOM Storage</span></span>

![403... tente habilitar o armazenamento HTML5](./media/app-insights-analytics-troubleshooting/060.png)

## <span data-ttu-id="ba742-158"><a name="e-g"></a>404 ... Assinatura não encontrada</span><span class="sxs-lookup"><span data-stu-id="ba742-158"><a name="e-g"></a>404 ... Subscription not found</span></span>
![404 ... Assinatura não encontrada](./media/app-insights-analytics-troubleshooting/070.png)

<span data-ttu-id="ba742-160">A URL é inválida.</span><span class="sxs-lookup"><span data-stu-id="ba742-160">The URL is invalid.</span></span> 

* <span data-ttu-id="ba742-161">Abra o recurso de aplicativo no [Portal do Application Insights](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ba742-161">Open the app resource in [Application Insights portal](https://portal.azure.com).</span></span> <span data-ttu-id="ba742-162">Use então o botão Analytics.</span><span class="sxs-lookup"><span data-stu-id="ba742-162">Then use the Analytics button.</span></span>

## <span data-ttu-id="ba742-163"><a name="e-h"></a>404... a página não existe</span><span class="sxs-lookup"><span data-stu-id="ba742-163"><a name="e-h"></a>404 ... page doesn't exist</span></span>
![404 ... A página não existe](./media/app-insights-analytics-troubleshooting/080.png)

<span data-ttu-id="ba742-165">A URL é inválida.</span><span class="sxs-lookup"><span data-stu-id="ba742-165">The URL is invalid.</span></span>

* <span data-ttu-id="ba742-166">Abra o recurso de aplicativo no [Portal do Application Insights](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ba742-166">Open the app resource in [Application Insights portal](https://portal.azure.com).</span></span> <span data-ttu-id="ba742-167">Use então o botão Analytics.</span><span class="sxs-lookup"><span data-stu-id="ba742-167">Then use the Analytics button.</span></span>

## <span data-ttu-id="ba742-168"><a name="cookies"></a>Habilitar cookies de terceiros</span><span class="sxs-lookup"><span data-stu-id="ba742-168"><a name="cookies"></a>Enable third-party cookies</span></span>
  <span data-ttu-id="ba742-169">Consulte [como desabilitar cookies de terceiros](http://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers), porém observe que precisamos **habilitá-los** .</span><span class="sxs-lookup"><span data-stu-id="ba742-169">See [how to disable third party cookies](http://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers), but notice we need to **enable** them.</span></span>


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

