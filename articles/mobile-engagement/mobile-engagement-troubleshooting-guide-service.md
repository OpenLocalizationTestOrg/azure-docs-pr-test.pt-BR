---
title: "Guia de solução de problemas do Azure Mobile Engagement - serviço"
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
ms.openlocfilehash: f13fd0540b783120014b3a8d4e41f78808c7fade
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-guide-for-service-issues"></a><span data-ttu-id="d8d07-103">Guia de solução de problemas de serviço</span><span class="sxs-lookup"><span data-stu-id="d8d07-103">Troubleshooting guide for Service issues</span></span>
<span data-ttu-id="d8d07-104">A seguir, possíveis problemas que podem ser encontrados na execução do Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="d8d07-104">The following are possible issues you may encounter with how Azure Mobile Engagement runs.</span></span>

## <a name="service-outages"></a><span data-ttu-id="d8d07-105">Interrupções de serviço</span><span class="sxs-lookup"><span data-stu-id="d8d07-105">Service Outages</span></span>
### <a name="issue"></a><span data-ttu-id="d8d07-106">Problema</span><span class="sxs-lookup"><span data-stu-id="d8d07-106">Issue</span></span>
* <span data-ttu-id="d8d07-107">Problemas que parecem ser provocados por interrupções de serviços do Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="d8d07-107">Issues that appear to be caused by Azure Mobile Engagement Service Outages.</span></span>

### <a name="causes"></a><span data-ttu-id="d8d07-108">Causas</span><span class="sxs-lookup"><span data-stu-id="d8d07-108">Causes</span></span>
* <span data-ttu-id="d8d07-109">Os problemas que parecem ser provocados por interrupções de serviços do Azure Mobile Engagement podem ser causados por vários problemas diferentes:</span><span class="sxs-lookup"><span data-stu-id="d8d07-109">Issues that appear to be caused by Azure Mobile Engagement Service Outages can be caused by several different issues:</span></span>
  * <span data-ttu-id="d8d07-110">Problemas isolados que originalmente parecem sistêmicos para o Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="d8d07-110">Isolated issues that originally appear systemic to all of Azure Mobile Engagement</span></span>
  * <span data-ttu-id="d8d07-111">Problemas conhecidos causados por interrupções de servidor (nem sempre são mostrados no status do servidor):</span><span class="sxs-lookup"><span data-stu-id="d8d07-111">Known issues caused by server outages (not always shows in server status):</span></span>
  * <span data-ttu-id="d8d07-112">Atrasos de agendamento, erros de direcionamento, problemas de atualização de notificação, interrupção da coleta de estatísticas, envio por push para de funcionar, interrupção do funcionamento das APIs, não é possível criar novos aplicativos ou usuários, erros de DNS e erros de tempo limite na interface do usuário, na API ou em aplicativos em um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d8d07-112">Scheduling delays, Targeting errors, Badge update issues, Statistics stop collecting, Push stops working, API's stop working, New apps or users can't be created, DNS errors, and Timeout errors in the UI, API, or Apps on a device.</span></span>
  * <span data-ttu-id="d8d07-113">Interrupções de dependência de nuvem [Status do serviço do Azure](http://status.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="d8d07-113">Cloud Dependency Outages [Azure Service Status](http://status.azure.com/)</span></span>
  * <span data-ttu-id="d8d07-114">Interrupções de dependência de Serviços de notificação de envio (PNS)</span><span class="sxs-lookup"><span data-stu-id="d8d07-114">Push Notification Services (PNS) Dependency Outages</span></span>
  * <span data-ttu-id="d8d07-115">Interrupções de loja de aplicativos</span><span class="sxs-lookup"><span data-stu-id="d8d07-115">App Store Outages</span></span>

1) <span data-ttu-id="d8d07-116">Para testar para ver se o problema é sistemático, você pode testar a mesma função de um</span><span class="sxs-lookup"><span data-stu-id="d8d07-116">To test to see if the problem is systemic you can test the same function from a different</span></span>

* <span data-ttu-id="d8d07-117">Aplicativo integrado Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="d8d07-117">Azure Mobile Engagement integrated application</span></span>
* <span data-ttu-id="d8d07-118">Dispositivo de teste</span><span class="sxs-lookup"><span data-stu-id="d8d07-118">Test device</span></span>
* <span data-ttu-id="d8d07-119">Versão do SO do dispositivo de teste</span><span class="sxs-lookup"><span data-stu-id="d8d07-119">Test device OS version</span></span>
* <span data-ttu-id="d8d07-120">Campanha</span><span class="sxs-lookup"><span data-stu-id="d8d07-120">Campaign</span></span>
* <span data-ttu-id="d8d07-121">Conta de usuário administrador</span><span class="sxs-lookup"><span data-stu-id="d8d07-121">Administrator user account</span></span>
* <span data-ttu-id="d8d07-122">Navegador (IE, Firefox, Chrome, etc.)</span><span class="sxs-lookup"><span data-stu-id="d8d07-122">Browser (IE, Firefox, Chrome, etc.)</span></span>
* <span data-ttu-id="d8d07-123">Computador</span><span class="sxs-lookup"><span data-stu-id="d8d07-123">Computer</span></span>

2) <span data-ttu-id="d8d07-124">Para testar se o problema afeta somente a interface do usuário ou a API:</span><span class="sxs-lookup"><span data-stu-id="d8d07-124">To test if the problem only affects the UI or the API's:</span></span>

* <span data-ttu-id="d8d07-125">Teste a mesma função da IU do Azure Mobile Engagement e das APIs do Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="d8d07-125">Test the same function from both the Azure Mobile Engagement UI and the Azure Mobile Engagement API's.</span></span>

3) <span data-ttu-id="d8d07-126">Para testar se o problema é com a rede de telefone celular:</span><span class="sxs-lookup"><span data-stu-id="d8d07-126">To test if the problem is with your Cellular Phone Network:</span></span>

* <span data-ttu-id="d8d07-127">Teste tanto quando estiver conectado à Internet via WIFI quanto conectado via rede de celular 3G.</span><span class="sxs-lookup"><span data-stu-id="d8d07-127">Test while connected to the Internet via WIFI and while connected via your 3G cellular phone network.</span></span>
* <span data-ttu-id="d8d07-128">Confirme se o firewall não está bloqueando algum endereço IP ou porta do Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="d8d07-128">Confirm that your firewall is not blocking any of the Azure Mobile Engagement IP Addresses or Ports.</span></span>

4) <span data-ttu-id="d8d07-129">Para testar se o problema é com o dispositivo:</span><span class="sxs-lookup"><span data-stu-id="d8d07-129">To test if the problem is with your Device:</span></span>

* <span data-ttu-id="d8d07-130">Teste se o dispositivo é capaz de se conectar ao Azure Mobile Engagement com outro aplicativo integrado Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="d8d07-130">Test if your Device is able to connect to Azure Mobile Engagement with another Azure Mobile Engagement integrated app.</span></span>
* <span data-ttu-id="d8d07-131">Verifique se você pode gerar eventos, trabalhos e travamentos de seu telefone que podem ser vistos na interface do usuário do Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="d8d07-131">Test that you can generate Events, Jobs, and Crashes from your phone that can be seen in the Azure Mobile Engagement UI.</span></span> 
* <span data-ttu-id="d8d07-132">Teste se você pode enviar notificações por push da IU do Azure Mobile Engagement para o seu dispositivo com base em sua identificação do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d8d07-132">Test if you can send push notifications from the Azure Mobile Engagement UI to your device based on its Device ID.</span></span> 

5) <span data-ttu-id="d8d07-133">Para testar se o problema é com seu aplicativo:</span><span class="sxs-lookup"><span data-stu-id="d8d07-133">To test if the problem is with your App:</span></span>

* <span data-ttu-id="d8d07-134">Instale e teste seu aplicativo de um emulador em vez de um dispositivo físico:</span><span class="sxs-lookup"><span data-stu-id="d8d07-134">Install and test your application from an emulator instead of from a physical device:</span></span>

6) <span data-ttu-id="d8d07-135">Para testar se o problema é com as atualizações do sistema operacional para dispositivos do usuário final, que exigem uma atualização do SDK para resolver:</span><span class="sxs-lookup"><span data-stu-id="d8d07-135">To test if the problem is with OS upgrades to end user Devices, which require an SDK upgrade to resolve:</span></span>

* <span data-ttu-id="d8d07-136">Teste seu aplicativo em diferentes dispositivos com diferentes versões do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="d8d07-136">Test your application on different devices with different versions of the OS.</span></span>
* <span data-ttu-id="d8d07-137">Confirme que você está usando a versão mais recente do SDK.</span><span class="sxs-lookup"><span data-stu-id="d8d07-137">Confirm that you are using the most recent version of the SDK.</span></span>

## <a name="connectivity-and-incorrect-information-issues"></a><span data-ttu-id="d8d07-138">Conectividade e problemas de informações incorretas</span><span class="sxs-lookup"><span data-stu-id="d8d07-138">Connectivity and Incorrect Information Issues</span></span>
### <a name="issue"></a><span data-ttu-id="d8d07-139">Problema</span><span class="sxs-lookup"><span data-stu-id="d8d07-139">Issue</span></span>
* <span data-ttu-id="d8d07-140">Problemas de logon na interface do usuário do Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="d8d07-140">Problems logging into the Azure Mobile Engagement UI.</span></span>
* <span data-ttu-id="d8d07-141">Erros de conexão com as APIs do Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="d8d07-141">Connection errors with the Azure Mobile Engagement API's.</span></span>
* <span data-ttu-id="d8d07-142">Problemas ao carregar marcas de informações de aplicativo por meio da API do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d8d07-142">Problems uploading App Info Tags via the Device API.</span></span>
* <span data-ttu-id="d8d07-143">Problemas de download de logs ou de dados exportados do Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="d8d07-143">Problems downloading logs or exported data from Azure Mobile Engagement.</span></span>
* <span data-ttu-id="d8d07-144">Informações incorretas mostradas na interface do usuário do Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="d8d07-144">Incorrect information shown in the Azure Mobile Engagement UI.</span></span>
* <span data-ttu-id="d8d07-145">Informações incorretas mostradas nos logs do Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="d8d07-145">Incorrect information shown in Azure Mobile Engagement logs.</span></span>

### <a name="causes"></a><span data-ttu-id="d8d07-146">Causas</span><span class="sxs-lookup"><span data-stu-id="d8d07-146">Causes</span></span>
* <span data-ttu-id="d8d07-147">Confirme se sua conta de usuário tem permissões suficientes para executar a tarefa.</span><span class="sxs-lookup"><span data-stu-id="d8d07-147">Confirm your user account has sufficient permissions to perform the task.</span></span>
* <span data-ttu-id="d8d07-148">Confirme se o problema não está restrito a um computador ou à sua rede local.</span><span class="sxs-lookup"><span data-stu-id="d8d07-148">Confirm that the problem is not isolated to one computer or your local network.</span></span>
* <span data-ttu-id="d8d07-149">Confirme se o serviço do Azure Mobile Engagement não tem nenhuma interrupção relatada.</span><span class="sxs-lookup"><span data-stu-id="d8d07-149">Confirm that that the Azure Mobile Engagement service has no reported outages.</span></span>
* <span data-ttu-id="d8d07-150">Confirme se os arquivos de marca de informações do aplicativo seguem todas estas regras:</span><span class="sxs-lookup"><span data-stu-id="d8d07-150">Confirm that your App Info Tag files follow all of these rules:</span></span>
  * <span data-ttu-id="d8d07-151">Usam somente o conjunto de caracteres UTF8 (não há suporte para o conjunto de caracteres ANSI).</span><span class="sxs-lookup"><span data-stu-id="d8d07-151">Use only the UTF8 character set (the ANSI character set is not supported).</span></span>
  * <span data-ttu-id="d8d07-152">Usam uma vírgula "," como o caractere separador (você pode abrir uma solicitação de serviço para pedir a alteração do caractere separador do .csv de uma vírgula "," para um outro caractere, como um ponto e vírgula ";").</span><span class="sxs-lookup"><span data-stu-id="d8d07-152">Use a comma "," as the separator character (you can open a service request to request to change the .csv separator character from a comma "," to another character such as a semi-colon ";").</span></span>
  * <span data-ttu-id="d8d07-153">Usam letras maiúsculas para valores boolianos “verdadeiro” e “falso”.</span><span class="sxs-lookup"><span data-stu-id="d8d07-153">Use all lower case for Boolean values "true" and "false".</span></span>
  * <span data-ttu-id="d8d07-154">Usam um arquivo menor do que o tamanho máximo de 35 MB.</span><span class="sxs-lookup"><span data-stu-id="d8d07-154">Use a file that is smaller than the maximum file size of 35MB.</span></span>

