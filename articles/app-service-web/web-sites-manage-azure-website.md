---
title: "aaaManage um aplicativo web no serviço de aplicativo do Azure"
description: "Links tooresources para gerenciar um aplicativo web no serviço de aplicativo do Azure."
services: app-service\web
documentationcenter: 
author: erikre
manager: erikre
editor: 
ms.assetid: d5e2887a-84f9-4747-a573-867635cb8b39
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: rachelap
ms.openlocfilehash: daf69245e66068b0e97e3ae1c3fb5fce45605b91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-web-app-in-azure-app-service"></a><span data-ttu-id="b2fe1-103">Gerenciar um aplicativo Web no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="b2fe1-103">Manage a web app in Azure App Service</span></span>
<span data-ttu-id="b2fe1-104">Este tópico contém links tooresources para gerenciar um aplicativo web no [do serviço de aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="b2fe1-104">This topic contains links tooresources for managing a web app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="b2fe1-105">O gerenciamento inclui todas as tarefas de saudação que manter seu aplicativo web funcionando sem problemas.</span><span class="sxs-lookup"><span data-stu-id="b2fe1-105">Management includes all of hello tasks that keep your web app running smoothly.</span></span> 

<span data-ttu-id="b2fe1-106">Em tempo de vida de saudação de um aplicativo web, você executará diversas tarefas de gerenciamento, quando você vai de atualizações, manutenção e operação de toonormal implantação inicial.</span><span class="sxs-lookup"><span data-stu-id="b2fe1-106">Over hello lifetime of a web app, you will perform different management tasks, as you move from initial deployment toonormal operation, maintenance, and updates.</span></span>

<span data-ttu-id="b2fe1-107">Muitas tarefas de gerenciamento de aplicativo da web podem ser executadas em Olá Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b2fe1-107">Many web app management tasks can be performed in hello Azure Portal.</span></span>

## <a name="before-you-deploy-your-web-app-tooproduction"></a><span data-ttu-id="b2fe1-108">Antes de implantar seu tooproduction de aplicativo web</span><span class="sxs-lookup"><span data-stu-id="b2fe1-108">Before you deploy your web app tooproduction</span></span>
### <a name="choose-a-tier"></a><span data-ttu-id="b2fe1-109">Escolha uma faixa</span><span class="sxs-lookup"><span data-stu-id="b2fe1-109">Choose a tier</span></span>
<span data-ttu-id="b2fe1-110">O Serviço de Aplicativo do Azure é oferecido em cinco níveis: Gratuito, Compartilhado, Básico, Padrão e Premium.</span><span class="sxs-lookup"><span data-stu-id="b2fe1-110">Azure App Service is offered in five tiers: Free, Shared, Basic, Standard, and Premium.</span></span> <span data-ttu-id="b2fe1-111">Para obter informações sobre os recursos de saudação e preços para cada camada, consulte [detalhes de preços](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="b2fe1-111">For information about hello features and pricing for each tier, see [Pricing details](https://azure.microsoft.com/pricing/details/app-service/).</span></span> 

* <span data-ttu-id="b2fe1-112">[Planos de serviço de aplicativo](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) permitem agrupar vários aplicativos web em Olá mesma camada.</span><span class="sxs-lookup"><span data-stu-id="b2fe1-112">[App Service plans](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) let you group multiple web apps under hello same tier.</span></span>
* <span data-ttu-id="b2fe1-113">Você sempre pode [alternar as camadas](web-sites-scale.md) após criar seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="b2fe1-113">You can always [switch tiers](web-sites-scale.md) after you create your web app.</span></span>

### <a name="configuration"></a><span data-ttu-id="b2fe1-114">Configuração</span><span class="sxs-lookup"><span data-stu-id="b2fe1-114">Configuration</span></span>
<span data-ttu-id="b2fe1-115">Saudação de uso [Portal do Azure](https://portal.azure.com/) tooset várias opções de configuração.</span><span class="sxs-lookup"><span data-stu-id="b2fe1-115">Use hello [Azure Portal](https://portal.azure.com/) tooset various configuration options.</span></span> <span data-ttu-id="b2fe1-116">Para obter detalhes, consulte [Configurar aplicativos Web no Serviço de Aplicativo do Azure](web-sites-configure.md).</span><span class="sxs-lookup"><span data-stu-id="b2fe1-116">For details, see [Configure web apps in Azure App Service](web-sites-configure.md).</span></span> <span data-ttu-id="b2fe1-117">Aqui está uma lista de verificação rápida:</span><span class="sxs-lookup"><span data-stu-id="b2fe1-117">Here is a quick checklist:</span></span>

* <span data-ttu-id="b2fe1-118">Selecione **versões de tempo de execução** para .NET, PHP, Java ou Python, se necessário.</span><span class="sxs-lookup"><span data-stu-id="b2fe1-118">Select **runtime versions** for .NET, PHP, Java, or Python, if needed.</span></span>
* <span data-ttu-id="b2fe1-119">Habilitar **WebSockets** se seu aplicativo web usa o protocolo WebSocket de saudação.</span><span class="sxs-lookup"><span data-stu-id="b2fe1-119">Enable **WebSockets** if your web app uses hello WebSocket protocol.</span></span> <span data-ttu-id="b2fe1-120">(Isto inclui aplicativos que usam o [ASP.NET SignalR](http://www.asp.net/signalr) ou [socket.io](web-sites-nodejs-chat-app-socketio.md).)</span><span class="sxs-lookup"><span data-stu-id="b2fe1-120">(This includes apps that use [ASP.NET SignalR](http://www.asp.net/signalr) or [socket.io](web-sites-nodejs-chat-app-socketio.md).)</span></span>
* <span data-ttu-id="b2fe1-121">Você está executando trabalhos web contínuos?</span><span class="sxs-lookup"><span data-stu-id="b2fe1-121">Are you running continuous web jobs?</span></span> <span data-ttu-id="b2fe1-122">Se estiver, habilite **Sempre ativo**.</span><span class="sxs-lookup"><span data-stu-id="b2fe1-122">If so, enable **Always On**.</span></span>
* <span data-ttu-id="b2fe1-123">Saudação de conjunto **documento padrão**, como index. HTML.</span><span class="sxs-lookup"><span data-stu-id="b2fe1-123">Set hello **default document**, such as index.html.</span></span>

<span data-ttu-id="b2fe1-124">Adição toothese configurações básicas, convém a seguir Olá tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="b2fe1-124">In addition toothese basic configuration settings, you may want tooconfigure hello following:</span></span>

* <span data-ttu-id="b2fe1-125">**Secure Socket Layer (SSL)** .</span><span class="sxs-lookup"><span data-stu-id="b2fe1-125">**Secure Socket Layer (SSL)** encryption.</span></span> <span data-ttu-id="b2fe1-126">toouse SSL com um nome de domínio personalizado, você deve obter um SSL de certificados e configurar seu toouse de aplicativo web-lo.</span><span class="sxs-lookup"><span data-stu-id="b2fe1-126">toouse SSL with a custom domain name, you must get an SSL certificate and configure your web app toouse it.</span></span> <span data-ttu-id="b2fe1-127">Consulte [Habilitar HTTPS para um aplicativo Web no Serviço de Aplicativo do Azure](app-service-web-tutorial-custom-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="b2fe1-127">See [Enable HTTPS for a web app in Azure App Service](app-service-web-tutorial-custom-ssl.md).</span></span>
* <span data-ttu-id="b2fe1-128">**Nome de domínio personalizado.**</span><span class="sxs-lookup"><span data-stu-id="b2fe1-128">**Custom domain name.**</span></span> <span data-ttu-id="b2fe1-129">Seu aplicativo Web tem automaticamente um subdomínio em azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="b2fe1-129">Your web app automatically has a subdomain under azurewebsites.net.</span></span> <span data-ttu-id="b2fe1-130">Você pode associar um nome de domínio personalizado, por exemplo, contoso.com. Consulte [Configurar um nome de domínio personalizado no Serviço de Aplicativo do Azure](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="b2fe1-130">You can associate a custom domain name, such as contoso.com. See [Configure a custom domain name in Azure App Service](app-service-web-tutorial-custom-domain.md).</span></span>

<span data-ttu-id="b2fe1-131">Configuração específica de idioma:</span><span class="sxs-lookup"><span data-stu-id="b2fe1-131">Language-specific configuration:</span></span>

* <span data-ttu-id="b2fe1-132">**PHP**: [configurar o PHP em aplicativos Web do Serviço de Aplicativo do Azure](web-sites-php-configure.md).</span><span class="sxs-lookup"><span data-stu-id="b2fe1-132">**PHP**: [Configure PHP in Azure App Service Web Apps](web-sites-php-configure.md).</span></span>
* <span data-ttu-id="b2fe1-133">**Python**: [configurando o Python com Aplicativos Web do Serviço de Aplicativo do Azure](web-sites-python-configure.md)</span><span class="sxs-lookup"><span data-stu-id="b2fe1-133">**Python**: [Configuring Python with Azure App Service Web Apps](web-sites-python-configure.md)</span></span>

## <a name="while-your-web-app-is-running"></a><span data-ttu-id="b2fe1-134">Enquanto seu aplicativo Web está em execução</span><span class="sxs-lookup"><span data-stu-id="b2fe1-134">While your web app is running</span></span>
<span data-ttu-id="b2fe1-135">Enquanto seu aplicativo web é executado, você deseja toomake se ele está disponível e que ele é dimensionado toomeet tráfego do usuário.</span><span class="sxs-lookup"><span data-stu-id="b2fe1-135">While your web app is running, you want toomake sure it is available, and that it scales toomeet user traffic.</span></span> <span data-ttu-id="b2fe1-136">Talvez também seja necessário tootroubleshoot erros.</span><span class="sxs-lookup"><span data-stu-id="b2fe1-136">You may also need tootroubleshoot errors.</span></span>

### <a name="monitoring"></a><span data-ttu-id="b2fe1-137">Monitoramento</span><span class="sxs-lookup"><span data-stu-id="b2fe1-137">Monitoring</span></span>
* <span data-ttu-id="b2fe1-138">Por meio de Olá Portal do Azure, você pode [adicionar métricas de desempenho](web-sites-monitor.md) como uso de CPU e o número de solicitações de cliente.</span><span class="sxs-lookup"><span data-stu-id="b2fe1-138">Through hello Azure Portal, you can [add performance metrics](web-sites-monitor.md) such as CPU usage and number of client requests.</span></span>
* <span data-ttu-id="b2fe1-139">[Dimensionar seu aplicativo web](web-sites-scale.md) em tootraffic de resposta.</span><span class="sxs-lookup"><span data-stu-id="b2fe1-139">[Scale your web app](web-sites-scale.md) in response tootraffic.</span></span> <span data-ttu-id="b2fe1-140">Dependendo de sua camada, você pode dimensionar o número de saudação de máquinas virtuais e/ou tamanho Olá Olá de instâncias de VM.</span><span class="sxs-lookup"><span data-stu-id="b2fe1-140">Depending on your tier, you can scale hello number of VMs and/or hello size of hello VM instances.</span></span> <span data-ttu-id="b2fe1-141">Saudação padrão e as camadas Premium, você também pode configurar dimensionamento automático, para que seu aplicativo web é dimensionado automaticamente, em uma cronograma fixo ou em tooload de resposta.</span><span class="sxs-lookup"><span data-stu-id="b2fe1-141">In hello Standard and Premium tiers, you can also set up autoscaling, so your web app scales automatically, either on a fixed schedule, or in response tooload.</span></span>  

### <a name="backups"></a><span data-ttu-id="b2fe1-142">Backups</span><span class="sxs-lookup"><span data-stu-id="b2fe1-142">Backups</span></span>
* <span data-ttu-id="b2fe1-143">Defina [backups automáticos](web-sites-backup.md) de seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="b2fe1-143">Set [automatic backups](web-sites-backup.md) of your web app.</span></span> <span data-ttu-id="b2fe1-144">Saiba mais sobre backups [neste vídeo](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/).</span><span class="sxs-lookup"><span data-stu-id="b2fe1-144">Learn more about backups in [this video](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/).</span></span>
* <span data-ttu-id="b2fe1-145">Saiba mais sobre opções de saudação para [recuperação de banco de dados](../sql-database/sql-database-business-continuity.md) no banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="b2fe1-145">Learn about hello options for [database recovery](../sql-database/sql-database-business-continuity.md) in Azure SQL Database.</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="b2fe1-146">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="b2fe1-146">Troubleshooting</span></span>
* <span data-ttu-id="b2fe1-147">Se algo der errado, você pode [solucionar problemas no Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug), usando logs de diagnóstico e de depuração na nuvem Olá dinâmica.</span><span class="sxs-lookup"><span data-stu-id="b2fe1-147">If something goes wrong, you can [troubleshoot in Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug), using diagnostic logs and live debugging in hello cloud.</span></span> 
* <span data-ttu-id="b2fe1-148">Fora do Visual Studio, existem vários logs de diagnóstico toocollect maneiras.</span><span class="sxs-lookup"><span data-stu-id="b2fe1-148">Outside of Visual Studio, there are various ways toocollect diagnostic logs.</span></span> <span data-ttu-id="b2fe1-149">Consulte [Habilitar o registro de log de diagnóstico para aplicativos Web no Serviço de Aplicativo do Azure](web-sites-enable-diagnostic-log.md).</span><span class="sxs-lookup"><span data-stu-id="b2fe1-149">See [Enable diagnostics logging for web apps in Azure App Service](web-sites-enable-diagnostic-log.md).</span></span>
* <span data-ttu-id="b2fe1-150">Para aplicativos do Node.js, consulte [como toodebug um Node. js web app no serviço de aplicativo do Azure](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="b2fe1-150">For Node.js applications, see [How toodebug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>

### <a name="restoring-data"></a><span data-ttu-id="b2fe1-151">Restaurando dados</span><span class="sxs-lookup"><span data-stu-id="b2fe1-151">Restoring Data</span></span>
* <span data-ttu-id="b2fe1-152">[Restaure](web-sites-restore.md) um aplicativo Web no qual foi realizado o backup anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b2fe1-152">[Restore](web-sites-restore.md) a web app that was previously backed up.</span></span>

## <a name="when-you-update-your-web-app"></a><span data-ttu-id="b2fe1-153">Ao atualizar seu aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="b2fe1-153">When you update your web app</span></span>
<span data-ttu-id="b2fe1-154">Se você não habilitou os backups automáticos, você pode criar um [backup manual](web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="b2fe1-154">If you have not enabled automatic backups, you can create a [manual backup](web-sites-backup.md).</span></span>

<span data-ttu-id="b2fe1-155">Considere o uso de uma [implantação em estágios](web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="b2fe1-155">Consider using [staged deployment](web-sites-staged-publishing.md).</span></span> <span data-ttu-id="b2fe1-156">Essa opção permite que você publique atualizações tooa preparação de implantação que executa lado a lado com a implantação de produção.</span><span class="sxs-lookup"><span data-stu-id="b2fe1-156">This option lets you publish updates tooa staging deployment that runs side-by-side with your production deployment.</span></span> 


<!-- Anchors. -->

[Before you deploy your site tooproduction]: #before-you-deploy-your-site-to-production
[While your website is running]: #while-your-website-is-running
[When you update your website]: #when-you-update-your-website


