---
title: "aaaAzure Mobile Engagement Troubleshooting Guide - serviço"
description: "Guias de solução de problemas para o Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8b4275da-c0b4-4690-824a-48e9d7a1fc6e
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: cf48db323a873ccef95946f7bb26e8d7473c002f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-service-issues"></a><span data-ttu-id="7e57b-103">Guia de solução de problemas de serviço</span><span class="sxs-lookup"><span data-stu-id="7e57b-103">Troubleshooting guide for Service issues</span></span>
<span data-ttu-id="7e57b-104">Olá seguem possíveis problemas que podem ocorrer com a execução do Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="7e57b-104">hello following are possible issues you may encounter with how Azure Mobile Engagement runs.</span></span>

## <a name="service-outages"></a><span data-ttu-id="7e57b-105">Interrupções de serviço</span><span class="sxs-lookup"><span data-stu-id="7e57b-105">Service Outages</span></span>
### <a name="issue"></a><span data-ttu-id="7e57b-106">Problema</span><span class="sxs-lookup"><span data-stu-id="7e57b-106">Issue</span></span>
* <span data-ttu-id="7e57b-107">Problemas que aparecem toobe causado por interrupções no serviço do Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="7e57b-107">Issues that appear toobe caused by Azure Mobile Engagement Service Outages.</span></span>

### <a name="causes"></a><span data-ttu-id="7e57b-108">Causas</span><span class="sxs-lookup"><span data-stu-id="7e57b-108">Causes</span></span>
* <span data-ttu-id="7e57b-109">Problemas que aparecem toobe causado por interrupções no serviço do Azure Mobile Engagement podem ser causados por vários problemas diferentes:</span><span class="sxs-lookup"><span data-stu-id="7e57b-109">Issues that appear toobe caused by Azure Mobile Engagement Service Outages can be caused by several different issues:</span></span>
  * <span data-ttu-id="7e57b-110">Problemas isolados que originalmente aparecem tooall sistemática do Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="7e57b-110">Isolated issues that originally appear systemic tooall of Azure Mobile Engagement</span></span>
  * <span data-ttu-id="7e57b-111">Problemas conhecidos causados por interrupções de servidor (nem sempre são mostrados no status do servidor):</span><span class="sxs-lookup"><span data-stu-id="7e57b-111">Known issues caused by server outages (not always shows in server status):</span></span>
  * <span data-ttu-id="7e57b-112">Agendando atrasos, erros de direcionamento, problemas de atualização do selo, parada estatísticas coletando Push parar de funcionar, da API pararem de funcionar, novos aplicativos ou usuários não pode ser criado, erros DNS e tempo limite Olá da interface do usuário, a API ou aplicativos em um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7e57b-112">Scheduling delays, Targeting errors, Badge update issues, Statistics stop collecting, Push stops working, API's stop working, New apps or users can't be created, DNS errors, and Timeout errors in hello UI, API, or Apps on a device.</span></span>
  * <span data-ttu-id="7e57b-113">Interrupções de dependência de nuvem [Status do serviço do Azure](http://status.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="7e57b-113">Cloud Dependency Outages [Azure Service Status](http://status.azure.com/)</span></span>
  * <span data-ttu-id="7e57b-114">Interrupções de dependência de Serviços de notificação de envio (PNS)</span><span class="sxs-lookup"><span data-stu-id="7e57b-114">Push Notification Services (PNS) Dependency Outages</span></span>
  * <span data-ttu-id="7e57b-115">Interrupções de loja de aplicativos</span><span class="sxs-lookup"><span data-stu-id="7e57b-115">App Store Outages</span></span>

1) <span data-ttu-id="7e57b-116">tootest toosee se problema de saudação sistemático, você pode testar Olá a mesma função de outro</span><span class="sxs-lookup"><span data-stu-id="7e57b-116">tootest toosee if hello problem is systemic you can test hello same function from a different</span></span>

* <span data-ttu-id="7e57b-117">Aplicativo integrado Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="7e57b-117">Azure Mobile Engagement integrated application</span></span>
* <span data-ttu-id="7e57b-118">Dispositivo de teste</span><span class="sxs-lookup"><span data-stu-id="7e57b-118">Test device</span></span>
* <span data-ttu-id="7e57b-119">Versão do SO do dispositivo de teste</span><span class="sxs-lookup"><span data-stu-id="7e57b-119">Test device OS version</span></span>
* <span data-ttu-id="7e57b-120">Campanha</span><span class="sxs-lookup"><span data-stu-id="7e57b-120">Campaign</span></span>
* <span data-ttu-id="7e57b-121">Conta de usuário administrador</span><span class="sxs-lookup"><span data-stu-id="7e57b-121">Administrator user account</span></span>
* <span data-ttu-id="7e57b-122">Navegador (IE, Firefox, Chrome, etc.)</span><span class="sxs-lookup"><span data-stu-id="7e57b-122">Browser (IE, Firefox, Chrome, etc.)</span></span>
* <span data-ttu-id="7e57b-123">Computador</span><span class="sxs-lookup"><span data-stu-id="7e57b-123">Computer</span></span>

2) <span data-ttu-id="7e57b-124">tootest se Olá afeta apenas Olá Olá ou interface do usuário da API:</span><span class="sxs-lookup"><span data-stu-id="7e57b-124">tootest if hello problem only affects hello UI or hello API's:</span></span>

* <span data-ttu-id="7e57b-125">Saudação de teste mesma função de ambos os Olá interface de usuário do Azure Mobile Engagement e Olá da API do Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="7e57b-125">Test hello same function from both hello Azure Mobile Engagement UI and hello Azure Mobile Engagement API's.</span></span>

3) <span data-ttu-id="7e57b-126">tootest se o problema de saudação à sua rede de celular:</span><span class="sxs-lookup"><span data-stu-id="7e57b-126">tootest if hello problem is with your Cellular Phone Network:</span></span>

* <span data-ttu-id="7e57b-127">Testar enquanto toohello conectado à Internet por meio de WIFI e enquanto estiver conectado por meio de sua rede de celular 3G.</span><span class="sxs-lookup"><span data-stu-id="7e57b-127">Test while connected toohello Internet via WIFI and while connected via your 3G cellular phone network.</span></span>
* <span data-ttu-id="7e57b-128">Confirme se o firewall não está bloqueando qualquer um dos endereços IP do hello Azure Mobile Engagement ou portas.</span><span class="sxs-lookup"><span data-stu-id="7e57b-128">Confirm that your firewall is not blocking any of hello Azure Mobile Engagement IP Addresses or Ports.</span></span>

4) <span data-ttu-id="7e57b-129">tootest se Olá problema com seu dispositivo:</span><span class="sxs-lookup"><span data-stu-id="7e57b-129">tootest if hello problem is with your Device:</span></span>

* <span data-ttu-id="7e57b-130">Teste se o dispositivo é capaz de tooconnect tooAzure Mobile Engagement com outro aplicativo integrado do Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="7e57b-130">Test if your Device is able tooconnect tooAzure Mobile Engagement with another Azure Mobile Engagement integrated app.</span></span>
* <span data-ttu-id="7e57b-131">Verifique se você pode gerar eventos, trabalhos e falhas de seu telefone que pode ser visto no hello interface de usuário do Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="7e57b-131">Test that you can generate Events, Jobs, and Crashes from your phone that can be seen in hello Azure Mobile Engagement UI.</span></span> 
* <span data-ttu-id="7e57b-132">Testar se você pode enviar notificações por push do dispositivo de tooyour de interface de usuário do Azure Mobile Engagement Olá com base em sua ID de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7e57b-132">Test if you can send push notifications from hello Azure Mobile Engagement UI tooyour device based on its Device ID.</span></span> 

5) <span data-ttu-id="7e57b-133">tootest se Olá problema com seu aplicativo:</span><span class="sxs-lookup"><span data-stu-id="7e57b-133">tootest if hello problem is with your App:</span></span>

* <span data-ttu-id="7e57b-134">Instale e teste seu aplicativo de um emulador em vez de um dispositivo físico:</span><span class="sxs-lookup"><span data-stu-id="7e57b-134">Install and test your application from an emulator instead of from a physical device:</span></span>

6) <span data-ttu-id="7e57b-135">tootest se Olá problema com o sistema operacional atualizado tooend usuário dispositivos, o que requer um tooresolve de atualização do SDK:</span><span class="sxs-lookup"><span data-stu-id="7e57b-135">tootest if hello problem is with OS upgrades tooend user Devices, which require an SDK upgrade tooresolve:</span></span>

* <span data-ttu-id="7e57b-136">Teste seu aplicativo em dispositivos diferentes com diferentes versões do SO de saudação.</span><span class="sxs-lookup"><span data-stu-id="7e57b-136">Test your application on different devices with different versions of hello OS.</span></span>
* <span data-ttu-id="7e57b-137">Confirme que você estiver usando a versão mais recente de saudação do hello SDK.</span><span class="sxs-lookup"><span data-stu-id="7e57b-137">Confirm that you are using hello most recent version of hello SDK.</span></span>

## <a name="connectivity-and-incorrect-information-issues"></a><span data-ttu-id="7e57b-138">Conectividade e problemas de informações incorretas</span><span class="sxs-lookup"><span data-stu-id="7e57b-138">Connectivity and Incorrect Information Issues</span></span>
### <a name="issue"></a><span data-ttu-id="7e57b-139">Problema</span><span class="sxs-lookup"><span data-stu-id="7e57b-139">Issue</span></span>
* <span data-ttu-id="7e57b-140">Problemas ao efetuar logon em Olá interface de usuário do Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="7e57b-140">Problems logging into hello Azure Mobile Engagement UI.</span></span>
* <span data-ttu-id="7e57b-141">Erros de Conexão com hello API do Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="7e57b-141">Connection errors with hello Azure Mobile Engagement API's.</span></span>
* <span data-ttu-id="7e57b-142">Problemas ao carregar marcas de informações do aplicativo por meio de saudação API do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7e57b-142">Problems uploading App Info Tags via hello Device API.</span></span>
* <span data-ttu-id="7e57b-143">Problemas de download de logs ou de dados exportados do Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="7e57b-143">Problems downloading logs or exported data from Azure Mobile Engagement.</span></span>
* <span data-ttu-id="7e57b-144">Informações incorretas mostradas no hello interface de usuário do Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="7e57b-144">Incorrect information shown in hello Azure Mobile Engagement UI.</span></span>
* <span data-ttu-id="7e57b-145">Informações incorretas mostradas nos logs do Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="7e57b-145">Incorrect information shown in Azure Mobile Engagement logs.</span></span>

### <a name="causes"></a><span data-ttu-id="7e57b-146">Causas</span><span class="sxs-lookup"><span data-stu-id="7e57b-146">Causes</span></span>
* <span data-ttu-id="7e57b-147">Confirme que sua conta de usuário tem a tarefa de saudação de tooperform permissões suficientes.</span><span class="sxs-lookup"><span data-stu-id="7e57b-147">Confirm your user account has sufficient permissions tooperform hello task.</span></span>
* <span data-ttu-id="7e57b-148">Confirme que esse problema Olá não é isolado tooone ou sua rede local.</span><span class="sxs-lookup"><span data-stu-id="7e57b-148">Confirm that hello problem is not isolated tooone computer or your local network.</span></span>
* <span data-ttu-id="7e57b-149">Verifique se esse serviço do Azure Mobile Engagement Olá tem sem interrupções relatadas.</span><span class="sxs-lookup"><span data-stu-id="7e57b-149">Confirm that that hello Azure Mobile Engagement service has no reported outages.</span></span>
* <span data-ttu-id="7e57b-150">Confirme se os arquivos de marca de informações do aplicativo seguem todas estas regras:</span><span class="sxs-lookup"><span data-stu-id="7e57b-150">Confirm that your App Info Tag files follow all of these rules:</span></span>
  * <span data-ttu-id="7e57b-151">Use Olá apenas o conjunto de caracteres UTF8 (conjunto de caracteres ANSI Olá não tem suporte).</span><span class="sxs-lookup"><span data-stu-id="7e57b-151">Use only hello UTF8 character set (hello ANSI character set is not supported).</span></span>
  * <span data-ttu-id="7e57b-152">Use uma vírgula "," como o caractere separador hello (você pode abrir um serviço toorequest toochange hello. csv separador de caracteres de solicitação de uma vírgula "," caractere tooanother como um ponto e vírgula ";").</span><span class="sxs-lookup"><span data-stu-id="7e57b-152">Use a comma "," as hello separator character (you can open a service request toorequest toochange hello .csv separator character from a comma "," tooanother character such as a semi-colon ";").</span></span>
  * <span data-ttu-id="7e57b-153">Usam letras maiúsculas para valores boolianos “verdadeiro” e “falso”.</span><span class="sxs-lookup"><span data-stu-id="7e57b-153">Use all lower case for Boolean values "true" and "false".</span></span>
  * <span data-ttu-id="7e57b-154">Use um arquivo que é menor do que o tamanho máximo do arquivo de saudação de 35MB.</span><span class="sxs-lookup"><span data-stu-id="7e57b-154">Use a file that is smaller than hello maximum file size of 35MB.</span></span>

