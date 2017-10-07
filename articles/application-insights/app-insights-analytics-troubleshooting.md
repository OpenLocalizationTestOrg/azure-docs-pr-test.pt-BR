---
title: "aaaTroubleshoot análise no Insights de aplicativo do Azure | Microsoft Docs"
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
ms.openlocfilehash: e3be2fbc0237440d3b8a736484434a9f276296c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-analytics-in-application-insights"></a><span data-ttu-id="a70fc-104">Solução de problemas do Analytics no Application Insights</span><span class="sxs-lookup"><span data-stu-id="a70fc-104">Troubleshoot Analytics in Application Insights</span></span>
<span data-ttu-id="a70fc-105">Problemas com a [Application Insights Analytics](app-insights-analytics.md)?</span><span class="sxs-lookup"><span data-stu-id="a70fc-105">Problems with [Application Insights Analytics](app-insights-analytics.md)?</span></span> <span data-ttu-id="a70fc-106">Comece por aqui.</span><span class="sxs-lookup"><span data-stu-id="a70fc-106">Start here.</span></span> <span data-ttu-id="a70fc-107">A análise é Olá poderosa ferramenta de pesquisa de informações de aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="a70fc-107">Analytics is hello powerful search tool of Azure Application Insights.</span></span>

## <a name="limits"></a><span data-ttu-id="a70fc-108">limites</span><span class="sxs-lookup"><span data-stu-id="a70fc-108">Limits</span></span>
* <span data-ttu-id="a70fc-109">No momento, os resultados da consulta são limitado toojust mais de uma semana de dados passados.</span><span class="sxs-lookup"><span data-stu-id="a70fc-109">At present, query results are limited toojust over a week of past data.</span></span>
* <span data-ttu-id="a70fc-110">Navegadores em que testamos: edições mais recentes do Chrome, Edge e Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="a70fc-110">Browsers we test on: latest editions of Chrome, Edge, and Internet Explorer.</span></span>

## <a name="known-incompatible-browser-extensions"></a><span data-ttu-id="a70fc-111">Extensões do navegador incompatíveis conhecidas</span><span class="sxs-lookup"><span data-stu-id="a70fc-111">Known incompatible browser extensions</span></span>
* <span data-ttu-id="a70fc-112">Ghostery</span><span class="sxs-lookup"><span data-stu-id="a70fc-112">Ghostery</span></span>

<span data-ttu-id="a70fc-113">Desabilitar extensão hello, ou use um navegador diferente.</span><span class="sxs-lookup"><span data-stu-id="a70fc-113">Disable hello extension or use a different browser.</span></span>

## <span data-ttu-id="a70fc-114"><a name="e-a"></a> "Erro inesperado"</span><span class="sxs-lookup"><span data-stu-id="a70fc-114"><a name="e-a"></a> "Unexpected error"</span></span>
![Tela de erro inesperado](./media/app-insights-analytics-troubleshooting/010.png)

<span data-ttu-id="a70fc-116">Ocorreu um erro interno durante o tempo de execução do portal. Exceção sem tratamento.</span><span class="sxs-lookup"><span data-stu-id="a70fc-116">Internal error occurred during portal runtime – unhandled exception.</span></span>

* <span data-ttu-id="a70fc-117">Limpe o cache do navegador hello.</span><span class="sxs-lookup"><span data-stu-id="a70fc-117">Clean hello browser's cache.</span></span> 

## <span data-ttu-id="a70fc-118"><a name="e-b"></a>403.... Tente tooreload</span><span class="sxs-lookup"><span data-stu-id="a70fc-118"><a name="e-b"></a>403 ... please try tooreload</span></span>
![403.... Tente tooreload](./media/app-insights-analytics-troubleshooting/020.png)

<span data-ttu-id="a70fc-120">Ocorreu um erro de autenticação (durante a autenticação ou durante a geração de token de acesso).</span><span class="sxs-lookup"><span data-stu-id="a70fc-120">An authentication related error occurred (during authentication or during access token generation).</span></span> <span data-ttu-id="a70fc-121">portal de saudação não pode ter nenhuma maneira muito recuperar sem alterar as configurações do navegador.</span><span class="sxs-lookup"><span data-stu-id="a70fc-121">hello portal may have no way too recover without changing browser settings.</span></span>

* <span data-ttu-id="a70fc-122">Verifique se [cookies de terceiros são habilitados](#cookies) no navegador de saudação.</span><span class="sxs-lookup"><span data-stu-id="a70fc-122">Verify [third party cookies are enabled](#cookies) in hello browser.</span></span> 

## <span data-ttu-id="a70fc-123"><a name="authentication"></a>403... verificar zona de segurança</span><span class="sxs-lookup"><span data-stu-id="a70fc-123"><a name="authentication"></a>403 ... verify security zone</span></span>
![403... verifique a zona de segurança](./media/app-insights-analytics-troubleshooting/030.png)

<span data-ttu-id="a70fc-125">Ocorreu um erro de autenticação (durante a autenticação ou durante a geração de token de acesso).</span><span class="sxs-lookup"><span data-stu-id="a70fc-125">An authentication related error occurred (during authentication or during access token generation).</span></span> <span data-ttu-id="a70fc-126">portal de saudação não pode ter nenhuma maneira muito recuperar sem alterar as configurações do navegador.</span><span class="sxs-lookup"><span data-stu-id="a70fc-126">hello portal may have no way too recover without changing browser settings.</span></span>

1. <span data-ttu-id="a70fc-127">Verifique se [cookies de terceiros são habilitados](#cookies) no navegador de saudação.</span><span class="sxs-lookup"><span data-stu-id="a70fc-127">Verify [third party cookies are enabled](#cookies) in hello browser.</span></span> 
2. <span data-ttu-id="a70fc-128">Você usou um favorito, o marcador ou o portal da análise de link salvo tooopen Olá?</span><span class="sxs-lookup"><span data-stu-id="a70fc-128">Did you use a favorite, bookmark or saved link tooopen hello Analytics portal?</span></span> <span data-ttu-id="a70fc-129">Conectado com credenciais diferentes que você usou quando salvo link Olá?</span><span class="sxs-lookup"><span data-stu-id="a70fc-129">Are you signed in with different credentials than you used when you saved hello link?</span></span>
3. <span data-ttu-id="a70fc-130">Tente usar uma janela do navegador privada/anônima (depois de fechar todas as janelas desse tipo).</span><span class="sxs-lookup"><span data-stu-id="a70fc-130">Try using an in-private/incognito browser window (after closing all such windows).</span></span> <span data-ttu-id="a70fc-131">Você terá tooprovide suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="a70fc-131">You'll have tooprovide your credentials.</span></span> 
4. <span data-ttu-id="a70fc-132">Abrir outra janela do navegador (comum) e vá muito[Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a70fc-132">Open another (ordinary) browser window and go too[Azure](https://portal.azure.com).</span></span> <span data-ttu-id="a70fc-133">Saia. Em seguida, abra o link e entrar com as credenciais corretas de saudação.</span><span class="sxs-lookup"><span data-stu-id="a70fc-133">Sign out. Then open your link and sign in with hello correct credentials.</span></span>
5. <span data-ttu-id="a70fc-134">Os usuários do Edge e do Internet Explorer também podem receber esse erro quando não há suporte para as configurações de zona confiável.</span><span class="sxs-lookup"><span data-stu-id="a70fc-134">Edge and Internet Explorer users can also get this error when trusted zone settings are not supported.</span></span>
   
    <span data-ttu-id="a70fc-135">Verifique se ambos [portal da análise de](https://analytics.applicationinsights.io) e [portal do Azure Active Directory](https://portal.azure.com) estão em Olá mesma zona de segurança:</span><span class="sxs-lookup"><span data-stu-id="a70fc-135">Verify both [Analytics portal](https://analytics.applicationinsights.io) and [Azure Active Directory portal](https://portal.azure.com) are in hello same security zone:</span></span>
   
   * <span data-ttu-id="a70fc-136">No Internet Explorer, abra **Opções da Internet**, **Segurança**, **Sites Confiáveis**, **Sites**:</span><span class="sxs-lookup"><span data-stu-id="a70fc-136">In Internet Explorer, open **Internet Options**, **Security**, **Trusted sites**, **Sites**:</span></span>
     
     ![Caixa de diálogo Opções da Internet, adição de um site tooTrusted Sites](./media/app-insights-analytics-troubleshooting/033.png)
     
     <span data-ttu-id="a70fc-138">Na lista de sites hello, se qualquer uma das seguintes URLs de saudação são incluídos, certifique-se que Olá outros também estão incluídos:</span><span class="sxs-lookup"><span data-stu-id="a70fc-138">In hello Websites list, if any of hello following URLs are included, make sure that hello others are included also:</span></span>
     
     <span data-ttu-id="a70fc-139">https://analytics.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="a70fc-139">https://analytics.applicationinsights.io</span></span><br/>
     <span data-ttu-id="a70fc-140">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="a70fc-140">https://login.microsoftonline.com</span></span><br/>
     <span data-ttu-id="a70fc-141">https://login.windows.net</span><span class="sxs-lookup"><span data-stu-id="a70fc-141">https://login.windows.net</span></span>

## <span data-ttu-id="a70fc-142"><a name="e-d"></a>404 ... Recurso não encontrado</span><span class="sxs-lookup"><span data-stu-id="a70fc-142"><a name="e-d"></a>404 ... Resource not found</span></span>
![404... recurso não encontrado](./media/app-insights-analytics-troubleshooting/040.png)

<span data-ttu-id="a70fc-144">O recurso de aplicativo foi excluído do Application Insights e não está mais disponível.</span><span class="sxs-lookup"><span data-stu-id="a70fc-144">Application resource was deleted from Application Insights and isn’t available anymore.</span></span> <span data-ttu-id="a70fc-145">Isso pode acontecer se você salvou a página de análise de toohello Olá URL.</span><span class="sxs-lookup"><span data-stu-id="a70fc-145">This can happen if you saved hello URL toohello Analytics page.</span></span>

## <span data-ttu-id="a70fc-146"><a name="e-e"></a>403 ... Sem autorização</span><span class="sxs-lookup"><span data-stu-id="a70fc-146"><a name="e-e"></a>403 ... No authorization</span></span>
![403 ... não autorizado](./media/app-insights-analytics-troubleshooting/050.png)

<span data-ttu-id="a70fc-148">Você não tem permissão tooopen esse aplicativo na análise.</span><span class="sxs-lookup"><span data-stu-id="a70fc-148">You don't have permission tooopen this application in Analytics.</span></span>

* <span data-ttu-id="a70fc-149">Você obteve Olá link de outra pessoa?</span><span class="sxs-lookup"><span data-stu-id="a70fc-149">Did you get hello link from someone else?</span></span> <span data-ttu-id="a70fc-150">Solicite toomake certeza Olá [colaboradores para este grupo de recursos ou leitores](app-insights-resources-roles-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="a70fc-150">Ask them toomake sure you are in hello [readers or contributors for this resource group](app-insights-resources-roles-access-control.md).</span></span>
* <span data-ttu-id="a70fc-151">Você salvou link hello usando credenciais diferentes?</span><span class="sxs-lookup"><span data-stu-id="a70fc-151">Did you save hello link using different credentials?</span></span> <span data-ttu-id="a70fc-152">Olá abrir [portal do Azure](https://portal.azure.com), sair e, em seguida, tente novamente, esse link fornecer as credenciais corretas de saudação.</span><span class="sxs-lookup"><span data-stu-id="a70fc-152">Open hello [Azure portal](https://portal.azure.com), sign out, and then try this link again, providing hello correct credentials.</span></span>

## <span data-ttu-id="a70fc-153"><a name="html-storage"></a>403 ... Armazenamento HTML5</span><span class="sxs-lookup"><span data-stu-id="a70fc-153"><a name="html-storage"></a>403 ... HTML5 Storage</span></span>
<span data-ttu-id="a70fc-154">Nosso portal usa sessionStorage e localStorage do HTML5.</span><span class="sxs-lookup"><span data-stu-id="a70fc-154">Our portal uses HTML5 localStorage and sessionStorage.</span></span>

* <span data-ttu-id="a70fc-155">Chrome: configurações, privacidade, configurações de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="a70fc-155">Chrome: Settings, privacy, content settings.</span></span>
* <span data-ttu-id="a70fc-156">Internet Explorer: Opções da Internet, guia Avançado, Segurança, Habilitar o armazenamento DOM</span><span class="sxs-lookup"><span data-stu-id="a70fc-156">Internet Explorer: Internet Options, Advanced tab, Security, Enable DOM Storage</span></span>

![403... Tente armazenamento tooenable HTML5](./media/app-insights-analytics-troubleshooting/060.png)

## <span data-ttu-id="a70fc-158"><a name="e-g"></a>404 ... Assinatura não encontrada</span><span class="sxs-lookup"><span data-stu-id="a70fc-158"><a name="e-g"></a>404 ... Subscription not found</span></span>
![404 ... Assinatura não encontrada](./media/app-insights-analytics-troubleshooting/070.png)

<span data-ttu-id="a70fc-160">Olá URL é inválida.</span><span class="sxs-lookup"><span data-stu-id="a70fc-160">hello URL is invalid.</span></span> 

* <span data-ttu-id="a70fc-161">Abrir o recurso de aplicativo hello em [portal do Application Insights](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a70fc-161">Open hello app resource in [Application Insights portal](https://portal.azure.com).</span></span> <span data-ttu-id="a70fc-162">Em seguida, use o botão de análise de saudação.</span><span class="sxs-lookup"><span data-stu-id="a70fc-162">Then use hello Analytics button.</span></span>

## <span data-ttu-id="a70fc-163"><a name="e-h"></a>404... a página não existe</span><span class="sxs-lookup"><span data-stu-id="a70fc-163"><a name="e-h"></a>404 ... page doesn't exist</span></span>
![404 ... A página não existe](./media/app-insights-analytics-troubleshooting/080.png)

<span data-ttu-id="a70fc-165">Olá URL é inválida.</span><span class="sxs-lookup"><span data-stu-id="a70fc-165">hello URL is invalid.</span></span>

* <span data-ttu-id="a70fc-166">Abrir o recurso de aplicativo hello em [portal do Application Insights](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a70fc-166">Open hello app resource in [Application Insights portal](https://portal.azure.com).</span></span> <span data-ttu-id="a70fc-167">Em seguida, use o botão de análise de saudação.</span><span class="sxs-lookup"><span data-stu-id="a70fc-167">Then use hello Analytics button.</span></span>

## <span data-ttu-id="a70fc-168"><a name="cookies"></a>Habilitar cookies de terceiros</span><span class="sxs-lookup"><span data-stu-id="a70fc-168"><a name="cookies"></a>Enable third-party cookies</span></span>
  <span data-ttu-id="a70fc-169">Consulte [como toodisable terceiros cookies](http://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers), mas observe é preciso muito**habilitar** -los.</span><span class="sxs-lookup"><span data-stu-id="a70fc-169">See [how toodisable third party cookies](http://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers), but notice we need too**enable** them.</span></span>


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

