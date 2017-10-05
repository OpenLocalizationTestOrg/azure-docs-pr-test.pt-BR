---
title: "Gerenciar um aplicativo Web no Serviço de Aplicativo do Azure"
description: "Links para recursos para gerenciar um aplicativo Web no Serviço de Aplicativo do Azure."
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
ms.openlocfilehash: 9e19618a1b24bbdf3163ddfc3423c5c932dcd7af
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="manage-a-web-app-in-azure-app-service"></a><span data-ttu-id="b257d-103">Gerenciar um aplicativo Web no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="b257d-103">Manage a web app in Azure App Service</span></span>
<span data-ttu-id="b257d-104">Este tópico contém links para recursos para gerenciar um aplicativo Web no [Serviço de Aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="b257d-104">This topic contains links to resources for managing a web app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="b257d-105">O gerenciamento inclui todas as tarefas que mantém seu aplicativo Web em execução perfeitamente.</span><span class="sxs-lookup"><span data-stu-id="b257d-105">Management includes all of the tasks that keep your web app running smoothly.</span></span> 

<span data-ttu-id="b257d-106">Durante o ciclo de vida de um aplicativo Web, você realizará diferentes tarefas de gerenciamento, a medida em que você move da implantação inicial à operação normal, manutenção e atualizações.</span><span class="sxs-lookup"><span data-stu-id="b257d-106">Over the lifetime of a web app, you will perform different management tasks, as you move from initial deployment to normal operation, maintenance, and updates.</span></span>

<span data-ttu-id="b257d-107">Muitas tarefas de gerenciamento de aplicativo Web podem ser realizadas no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b257d-107">Many web app management tasks can be performed in the Azure Portal.</span></span>

## <a name="before-you-deploy-your-web-app-to-production"></a><span data-ttu-id="b257d-108">Antes de implantar seu aplicativo Web para produção</span><span class="sxs-lookup"><span data-stu-id="b257d-108">Before you deploy your web app to production</span></span>
### <a name="choose-a-tier"></a><span data-ttu-id="b257d-109">Escolha uma faixa</span><span class="sxs-lookup"><span data-stu-id="b257d-109">Choose a tier</span></span>
<span data-ttu-id="b257d-110">O Serviço de Aplicativo do Azure é oferecido em cinco níveis: Gratuito, Compartilhado, Básico, Padrão e Premium.</span><span class="sxs-lookup"><span data-stu-id="b257d-110">Azure App Service is offered in five tiers: Free, Shared, Basic, Standard, and Premium.</span></span> <span data-ttu-id="b257d-111">Para obter informações sobre os recursos e preços para cada faixa, consulte [Detalhes dos preços](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="b257d-111">For information about the features and pricing for each tier, see [Pricing details](https://azure.microsoft.com/pricing/details/app-service/).</span></span> 

* <span data-ttu-id="b257d-112">[planos de Serviço de Aplicativo](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) lhe permitem agrupar vários aplicativos Web na mesma camada.</span><span class="sxs-lookup"><span data-stu-id="b257d-112">[App Service plans](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) let you group multiple web apps under the same tier.</span></span>
* <span data-ttu-id="b257d-113">Você sempre pode [alternar as camadas](web-sites-scale.md) após criar seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="b257d-113">You can always [switch tiers](web-sites-scale.md) after you create your web app.</span></span>

### <a name="configuration"></a><span data-ttu-id="b257d-114">Configuração</span><span class="sxs-lookup"><span data-stu-id="b257d-114">Configuration</span></span>
<span data-ttu-id="b257d-115">Use o [Portal do Azure](https://portal.azure.com/) para definir várias opções de configuração.</span><span class="sxs-lookup"><span data-stu-id="b257d-115">Use the [Azure Portal](https://portal.azure.com/) to set various configuration options.</span></span> <span data-ttu-id="b257d-116">Para obter detalhes, consulte [Configurar aplicativos Web no Serviço de Aplicativo do Azure](web-sites-configure.md).</span><span class="sxs-lookup"><span data-stu-id="b257d-116">For details, see [Configure web apps in Azure App Service](web-sites-configure.md).</span></span> <span data-ttu-id="b257d-117">Aqui está uma lista de verificação rápida:</span><span class="sxs-lookup"><span data-stu-id="b257d-117">Here is a quick checklist:</span></span>

* <span data-ttu-id="b257d-118">Selecione **versões de tempo de execução** para .NET, PHP, Java ou Python, se necessário.</span><span class="sxs-lookup"><span data-stu-id="b257d-118">Select **runtime versions** for .NET, PHP, Java, or Python, if needed.</span></span>
* <span data-ttu-id="b257d-119">Habilite **WebSockets** se seu aplicativo Web usa o protocolo WebSocket.</span><span class="sxs-lookup"><span data-stu-id="b257d-119">Enable **WebSockets** if your web app uses the WebSocket protocol.</span></span> <span data-ttu-id="b257d-120">(Isto inclui aplicativos que usam o [ASP.NET SignalR](http://www.asp.net/signalr) ou [socket.io](web-sites-nodejs-chat-app-socketio.md).)</span><span class="sxs-lookup"><span data-stu-id="b257d-120">(This includes apps that use [ASP.NET SignalR](http://www.asp.net/signalr) or [socket.io](web-sites-nodejs-chat-app-socketio.md).)</span></span>
* <span data-ttu-id="b257d-121">Você está executando trabalhos web contínuos?</span><span class="sxs-lookup"><span data-stu-id="b257d-121">Are you running continuous web jobs?</span></span> <span data-ttu-id="b257d-122">Se estiver, habilite **Sempre ativo**.</span><span class="sxs-lookup"><span data-stu-id="b257d-122">If so, enable **Always On**.</span></span>
* <span data-ttu-id="b257d-123">Defina o **documento padrão**, como index.html.</span><span class="sxs-lookup"><span data-stu-id="b257d-123">Set the **default document**, such as index.html.</span></span>

<span data-ttu-id="b257d-124">Além desta definições de configurações básicas, talvez você queira configurar o seguinte:</span><span class="sxs-lookup"><span data-stu-id="b257d-124">In addition to these basic configuration settings, you may want to configure the following:</span></span>

* <span data-ttu-id="b257d-125">**Secure Socket Layer (SSL)** .</span><span class="sxs-lookup"><span data-stu-id="b257d-125">**Secure Socket Layer (SSL)** encryption.</span></span> <span data-ttu-id="b257d-126">Para usar a SSL com um nome de domínio personalizado, você deve solicitar um certificado SSL e configurar seu aplicativo Web para usá-lo.</span><span class="sxs-lookup"><span data-stu-id="b257d-126">To use SSL with a custom domain name, you must get an SSL certificate and configure your web app to use it.</span></span> <span data-ttu-id="b257d-127">Consulte [Habilitar HTTPS para um aplicativo Web no Serviço de Aplicativo do Azure](app-service-web-tutorial-custom-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="b257d-127">See [Enable HTTPS for a web app in Azure App Service](app-service-web-tutorial-custom-ssl.md).</span></span>
* <span data-ttu-id="b257d-128">**Nome de domínio personalizado.**</span><span class="sxs-lookup"><span data-stu-id="b257d-128">**Custom domain name.**</span></span> <span data-ttu-id="b257d-129">Seu aplicativo Web tem automaticamente um subdomínio em azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="b257d-129">Your web app automatically has a subdomain under azurewebsites.net.</span></span> <span data-ttu-id="b257d-130">Você pode associar um nome de domínio personalizado, por exemplo, contoso.com.</span><span class="sxs-lookup"><span data-stu-id="b257d-130">You can associate a custom domain name, such as contoso.com.</span></span> <span data-ttu-id="b257d-131">Consulte [Configurar um nome de domínio personalizado no Serviço de Aplicativo do Azure](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="b257d-131">See [Configure a custom domain name in Azure App Service](app-service-web-tutorial-custom-domain.md).</span></span>

<span data-ttu-id="b257d-132">Configuração específica de idioma:</span><span class="sxs-lookup"><span data-stu-id="b257d-132">Language-specific configuration:</span></span>

* <span data-ttu-id="b257d-133">**PHP**: [configurar o PHP em aplicativos Web do Serviço de Aplicativo do Azure](web-sites-php-configure.md).</span><span class="sxs-lookup"><span data-stu-id="b257d-133">**PHP**: [Configure PHP in Azure App Service Web Apps](web-sites-php-configure.md).</span></span>
* <span data-ttu-id="b257d-134">**Python**: [configurando o Python com Aplicativos Web do Serviço de Aplicativo do Azure](web-sites-python-configure.md)</span><span class="sxs-lookup"><span data-stu-id="b257d-134">**Python**: [Configuring Python with Azure App Service Web Apps](web-sites-python-configure.md)</span></span>

## <a name="while-your-web-app-is-running"></a><span data-ttu-id="b257d-135">Enquanto seu aplicativo Web está em execução</span><span class="sxs-lookup"><span data-stu-id="b257d-135">While your web app is running</span></span>
<span data-ttu-id="b257d-136">Enquanto seu aplicativo Web estiver em execução, verifique se ele está disponível e dimensionado para atender o tráfego do usuário.</span><span class="sxs-lookup"><span data-stu-id="b257d-136">While your web app is running, you want to make sure it is available, and that it scales to meet user traffic.</span></span> <span data-ttu-id="b257d-137">Você talvez precise solucionar erros.</span><span class="sxs-lookup"><span data-stu-id="b257d-137">You may also need to troubleshoot errors.</span></span>

### <a name="monitoring"></a><span data-ttu-id="b257d-138">Monitoramento</span><span class="sxs-lookup"><span data-stu-id="b257d-138">Monitoring</span></span>
* <span data-ttu-id="b257d-139">Usando o Portal do Azure, você pode [Adicionar métricas de desempenho](web-sites-monitor.md) como uso de CPU e o número de solicitações do cliente.</span><span class="sxs-lookup"><span data-stu-id="b257d-139">Through the Azure Portal, you can [add performance metrics](web-sites-monitor.md) such as CPU usage and number of client requests.</span></span>
* <span data-ttu-id="b257d-140">[Dimensione seu aplicativo Web](web-sites-scale.md) em resposta ao tráfego.</span><span class="sxs-lookup"><span data-stu-id="b257d-140">[Scale your web app](web-sites-scale.md) in response to traffic.</span></span> <span data-ttu-id="b257d-141">Dependendo da sua faixa, você pode reduzir o número de VMs e/ou o tamanho das instâncias da VM.</span><span class="sxs-lookup"><span data-stu-id="b257d-141">Depending on your tier, you can scale the number of VMs and/or the size of the VM instances.</span></span> <span data-ttu-id="b257d-142">Nas camadas Padrão e Premium, você também pode configurar o dimensionamento automático, para que seu aplicativo Web seja dimensionado automaticamente, em uma agenda fixa ou em resposta à carga.</span><span class="sxs-lookup"><span data-stu-id="b257d-142">In the Standard and Premium tiers, you can also set up autoscaling, so your web app scales automatically, either on a fixed schedule, or in response to load.</span></span>  

### <a name="backups"></a><span data-ttu-id="b257d-143">Backups</span><span class="sxs-lookup"><span data-stu-id="b257d-143">Backups</span></span>
* <span data-ttu-id="b257d-144">Defina [backups automáticos](web-sites-backup.md) de seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="b257d-144">Set [automatic backups](web-sites-backup.md) of your web app.</span></span> <span data-ttu-id="b257d-145">Saiba mais sobre backups [neste vídeo](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/).</span><span class="sxs-lookup"><span data-stu-id="b257d-145">Learn more about backups in [this video](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/).</span></span>
* <span data-ttu-id="b257d-146">Saiba sobre as opções para a [recuperação de banco de dados](../sql-database/sql-database-business-continuity.md) no Banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="b257d-146">Learn about the options for [database recovery](../sql-database/sql-database-business-continuity.md) in Azure SQL Database.</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="b257d-147">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="b257d-147">Troubleshooting</span></span>
* <span data-ttu-id="b257d-148">Se algo der errado, você pode [solucionar no Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug), usando os logs de diagnóstico e depuração ao vivo na nuvem.</span><span class="sxs-lookup"><span data-stu-id="b257d-148">If something goes wrong, you can [troubleshoot in Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug), using diagnostic logs and live debugging in the cloud.</span></span> 
* <span data-ttu-id="b257d-149">Fora do Visual Studio, há várias maneiras de coletar os logs de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="b257d-149">Outside of Visual Studio, there are various ways to collect diagnostic logs.</span></span> <span data-ttu-id="b257d-150">Consulte [Habilitar o registro de log de diagnóstico para aplicativos Web no Serviço de Aplicativo do Azure](web-sites-enable-diagnostic-log.md).</span><span class="sxs-lookup"><span data-stu-id="b257d-150">See [Enable diagnostics logging for web apps in Azure App Service](web-sites-enable-diagnostic-log.md).</span></span>
* <span data-ttu-id="b257d-151">Para aplicativos Node.js, consulte [Como depurar um aplicativo Web Node.js no Serviço de Aplicativo do Azure](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="b257d-151">For Node.js applications, see [How to debug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>

### <a name="restoring-data"></a><span data-ttu-id="b257d-152">Restaurando dados</span><span class="sxs-lookup"><span data-stu-id="b257d-152">Restoring Data</span></span>
* <span data-ttu-id="b257d-153">[Restaure](web-sites-restore.md) um aplicativo Web no qual foi realizado o backup anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b257d-153">[Restore](web-sites-restore.md) a web app that was previously backed up.</span></span>

## <a name="when-you-update-your-web-app"></a><span data-ttu-id="b257d-154">Ao atualizar seu aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="b257d-154">When you update your web app</span></span>
<span data-ttu-id="b257d-155">Se você não habilitou os backups automáticos, você pode criar um [backup manual](web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="b257d-155">If you have not enabled automatic backups, you can create a [manual backup](web-sites-backup.md).</span></span>

<span data-ttu-id="b257d-156">Considere o uso de uma [implantação em estágios](web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="b257d-156">Consider using [staged deployment](web-sites-staged-publishing.md).</span></span> <span data-ttu-id="b257d-157">Esta opção permite que você publique atualizações para uma implantação em estágios que executam lado a lado com a sua implantação de produção.</span><span class="sxs-lookup"><span data-stu-id="b257d-157">This option lets you publish updates to a staging deployment that runs side-by-side with your production deployment.</span></span> 


<!-- Anchors. -->

[Before you deploy your site to production]: #before-you-deploy-your-site-to-production
[While your website is running]: #while-your-website-is-running
[When you update your website]: #when-you-update-your-website


