---
title: "Como configurar um serviço de nuvem (portal) | Microsoft Docs"
description: "Saiba como configurar serviços de nuvem no Azure. Saiba como atualizar a configuração do serviço de nuvem e configurar acesso remoto às instâncias de função. Esses exemplos usam o portal do Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 7308f3c0-825e-499d-bfa5-c60f86371921
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/07/2016
ms.author: adegeo
ms.openlocfilehash: a7e891d05ffe4cc2b4f68dce072a81499cc6de80
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-configure-cloud-services"></a><span data-ttu-id="0161a-105">Como configurar serviços de nuvem</span><span class="sxs-lookup"><span data-stu-id="0161a-105">How to Configure Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0161a-106">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0161a-106">Azure portal</span></span>](cloud-services-how-to-configure-portal.md)
> * [<span data-ttu-id="0161a-107">Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="0161a-107">Azure classic portal</span></span>](cloud-services-how-to-configure.md)
>
>

<span data-ttu-id="0161a-108">Você pode definir as configurações usadas mais frequentemente para um Serviço de Nuvem no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0161a-108">You can configure the most commonly used settings for a cloud service in the Azure portal.</span></span> <span data-ttu-id="0161a-109">Ou então, se desejar atualizar diretamente seus arquivos de configuração, baixe um arquivo de configuração de serviço para atualizar e carregue o arquivo atualizado e atualize o serviço de nuvem com as alterações de configuração.</span><span class="sxs-lookup"><span data-stu-id="0161a-109">Or, if you like to update your configuration files directly, download a service configuration file to update, and then upload the updated file and update the cloud service with the configuration changes.</span></span> <span data-ttu-id="0161a-110">De qualquer maneira, as atualizações da configuração são enviadas por push a todas as instâncias de função.</span><span class="sxs-lookup"><span data-stu-id="0161a-110">Either way, the configuration updates are pushed out to all role instances.</span></span>

<span data-ttu-id="0161a-111">Você também pode gerenciar as instâncias de suas funções de serviço de nuvem ou da área de trabalho remota para elas.</span><span class="sxs-lookup"><span data-stu-id="0161a-111">You can also manage the instances of your cloud service roles, or remote desktop into them.</span></span>

<span data-ttu-id="0161a-112">O Azure pode garantir apenas 99,95 por cento de disponibilidade do serviço durante as atualizações de configuração se você tiver, pelo menos, duas instâncias de função para cada função.</span><span class="sxs-lookup"><span data-stu-id="0161a-112">Azure can only ensure 99.95 percent service availability during the configuration updates if you have at least two role instances for every role.</span></span> <span data-ttu-id="0161a-113">Isso permite que uma máquina virtual processe as solicitações do cliente enquanto a outra é atualizada.</span><span class="sxs-lookup"><span data-stu-id="0161a-113">That enables one virtual machine to process client requests while the other is being updated.</span></span> <span data-ttu-id="0161a-114">Para obter mais informações, consulte [Contratos de Nível de Serviço](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="0161a-114">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

## <a name="change-a-cloud-service"></a><span data-ttu-id="0161a-115">Alterar um serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="0161a-115">Change a cloud service</span></span>
<span data-ttu-id="0161a-116">Após abrir o [Portal do Azure](https://portal.azure.com/), navegue até seu serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="0161a-116">After opening the [Azure portal](https://portal.azure.com/), navigate to your cloud service.</span></span> <span data-ttu-id="0161a-117">Daqui, você gerencia muitos aspectos dele.</span><span class="sxs-lookup"><span data-stu-id="0161a-117">From here, you manage many aspects of it.</span></span>

![Página de configurações](./media/cloud-services-how-to-configure-portal/cloud-service.png)

<span data-ttu-id="0161a-119">Os links **Configurações** ou **Todas as configurações** abrirão a folha **Configurações**, na qual você pode alterar as **Propriedades** e a **Configuração**, gerenciar os **Certificados**, instalar **Regras de alerta** e gerenciar os **Usuários** que têm acesso a esse serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="0161a-119">The **Settings** or **All settings** links will open up the **Settings** blade where you can change the **Properties**, change the **Configuration**, manage the **Certificates**, setup **Alert rules**, and manage the **Users** who have access to this cloud service.</span></span>

![Folha de configurações do serviço de nuvem do Azure](./media/cloud-services-how-to-configure-portal/cs-settings-blade.png)

### <a name="manage-guest-os-version"></a><span data-ttu-id="0161a-121">Gerenciar versão do SO Convidado</span><span class="sxs-lookup"><span data-stu-id="0161a-121">Manage Guest OS version</span></span>

<span data-ttu-id="0161a-122">Por padrão, o Azure atualiza periodicamente o sistema operacional convidado com a imagem mais recente com suporte dentro da família de sistema operacional que você especificou em sua configuração de serviço (.cscfg), como o Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="0161a-122">By default, Azure periodically updates your guest OS to the latest supported image within the OS family that you've specified in your service configuration (.cscfg), such as Windows Server 2016.</span></span>

<span data-ttu-id="0161a-123">Se você precisar de uma versão específica do sistema operacional de destino, defina-a na folha **Configuração**.</span><span class="sxs-lookup"><span data-stu-id="0161a-123">If you need to target a specific OS version, you can set it in the **Configuration** blade.</span></span>

![Definir versão do SO](./media/cloud-services-how-to-configure-portal/cs-settings-config-guestosversion.png)


>[!IMPORTANT]
> <span data-ttu-id="0161a-125">Escolher uma versão específica do SO desabilita as atualizações automáticas do sistema operacional e torna os patches sua responsabilidade.</span><span class="sxs-lookup"><span data-stu-id="0161a-125">Choosing a specific OS version disables automatic OS updates and makes patching your responsibility.</span></span> <span data-ttu-id="0161a-126">Você deve garantir que suas instâncias de função recebam as atualizações, caso contrário você pode expor seu aplicativo a vulnerabilidades de segurança.</span><span class="sxs-lookup"><span data-stu-id="0161a-126">You must ensure that your role instances are receiving updates or you may expose your application to security vulnerabilities.</span></span>

## <a name="monitoring"></a><span data-ttu-id="0161a-127">Monitoramento</span><span class="sxs-lookup"><span data-stu-id="0161a-127">Monitoring</span></span>
<span data-ttu-id="0161a-128">Você pode adicionar alertas para o seu serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="0161a-128">You can add alerts to your cloud service.</span></span> <span data-ttu-id="0161a-129">Clique em **Configurações** > **Regras de Alerta** > **Adicionar alerta**.</span><span class="sxs-lookup"><span data-stu-id="0161a-129">Click **Settings** > **Alert Rules** > **Add alert**.</span></span>

![](./media/cloud-services-how-to-configure-portal/cs-alerts.png)

<span data-ttu-id="0161a-130">Daqui, você pode configurar um alerta.</span><span class="sxs-lookup"><span data-stu-id="0161a-130">From here, you can setup an alert.</span></span> <span data-ttu-id="0161a-131">Com a caixa suspensa **Métrica**, você pode configurar um alerta para os seguintes tipos de dados.</span><span class="sxs-lookup"><span data-stu-id="0161a-131">With the **Metric** drop down box, you can setup an alert for the following types of data.</span></span>

* <span data-ttu-id="0161a-132">Leitura de disco</span><span class="sxs-lookup"><span data-stu-id="0161a-132">Disk read</span></span>
* <span data-ttu-id="0161a-133">Gravação de disco</span><span class="sxs-lookup"><span data-stu-id="0161a-133">Disk write</span></span>
* <span data-ttu-id="0161a-134">Rede no</span><span class="sxs-lookup"><span data-stu-id="0161a-134">Network in</span></span>
* <span data-ttu-id="0161a-135">Limite de rede</span><span class="sxs-lookup"><span data-stu-id="0161a-135">Network out</span></span>
* <span data-ttu-id="0161a-136">Percentual de CPU</span><span class="sxs-lookup"><span data-stu-id="0161a-136">CPU percentage</span></span>

![](./media/cloud-services-how-to-configure-portal/cs-alert-item.png)

### <a name="configure-monitoring-from-a-metric-tile"></a><span data-ttu-id="0161a-137">Configurar o monitoramento de um bloco de métrica</span><span class="sxs-lookup"><span data-stu-id="0161a-137">Configure monitoring from a metric tile</span></span>
<span data-ttu-id="0161a-138">Em vez de usar **Configurações** > **Regras de alerta**, você pode clicar em um dos blocos de métrica na seção **Monitoramento** da folha **Serviço de nuvem**.</span><span class="sxs-lookup"><span data-stu-id="0161a-138">Instead of using **Settings** > **Alert Rules**, you can click on one of the metric tiles in the **Monitoring** section of the **Cloud service** blade.</span></span>

![Monitoramento de Serviço de Nuvem](./media/cloud-services-how-to-configure-portal/cs-monitoring.png)

<span data-ttu-id="0161a-140">Daqui, você pode personalizar o gráfico usado com o bloco ou adicionar uma regra de alerta.</span><span class="sxs-lookup"><span data-stu-id="0161a-140">From here you can customize the chart used with the tile, or add an alert rule.</span></span>

## <a name="reboot-reimage-or-remote-desktop"></a><span data-ttu-id="0161a-141">Reinicializar, refazer imagem ou a área de trabalho remota</span><span class="sxs-lookup"><span data-stu-id="0161a-141">Reboot, reimage, or remote desktop</span></span>
<span data-ttu-id="0161a-142">Neste momento, você não pode configurar a área de trabalho remota usando o **Portal do Azure**.</span><span class="sxs-lookup"><span data-stu-id="0161a-142">At this time you cannot configure remote desktop using the **Azure portal**.</span></span> <span data-ttu-id="0161a-143">No entanto, você pode defini-la por meio do [Portal Clássico do Azure](cloud-services-role-enable-remote-desktop.md), [do PowerShell](cloud-services-role-enable-remote-desktop-powershell.md) ou do [Visual Studio](../vs-azure-tools-remote-desktop-roles.md).</span><span class="sxs-lookup"><span data-stu-id="0161a-143">However, you can set it up through the [Azure classic portal](cloud-services-role-enable-remote-desktop.md), [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md), or through [Visual Studio](../vs-azure-tools-remote-desktop-roles.md).</span></span>

<span data-ttu-id="0161a-144">Primeiro, clique na instância do serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="0161a-144">First, click on the cloud service instance.</span></span>

![Instância de Serviço de Nuvem](./media/cloud-services-how-to-configure-portal/cs-instance.png)

<span data-ttu-id="0161a-146">Na folha que é aberta, você pode iniciar uma conexão de área de trabalho remota, reinicializar a instância ou refazer a imagem da instância remotamente (inicia com uma imagem atualizada).</span><span class="sxs-lookup"><span data-stu-id="0161a-146">From the blade that opens you can initiate a remote desktop connection, remotely reboot the instance, or remotely reimage (start with a fresh image) the instance.</span></span>

![Botões de instância de serviço de nuvem](./media/cloud-services-how-to-configure-portal/cs-instance-buttons.png)

## <a name="reconfigure-your-cscfg"></a><span data-ttu-id="0161a-148">Reconfigurar seu .cscfg</span><span class="sxs-lookup"><span data-stu-id="0161a-148">Reconfigure your .cscfg</span></span>
<span data-ttu-id="0161a-149">Talvez seja necessário reconfigurar o serviço de nuvem por meio do arquivo da [configuração de serviço (cscfg)](cloud-services-model-and-package.md#cscfg).</span><span class="sxs-lookup"><span data-stu-id="0161a-149">You may need to reconfigure your cloud service through the [service config (cscfg)](cloud-services-model-and-package.md#cscfg) file.</span></span> <span data-ttu-id="0161a-150">Primeiro, você precisa baixar o arquivo .cscfg, modificá-lo e carregá-lo.</span><span class="sxs-lookup"><span data-stu-id="0161a-150">First you need to download your .cscfg file, modify it, then upload it.</span></span>

1. <span data-ttu-id="0161a-151">Clique no ícone **Configurações** ou no link **Todas as configurações** para abrir a folha **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="0161a-151">Click on the **Settings** icon or the **All settings** link to open up the **Settings** blade.</span></span>

    ![Página de configurações](./media/cloud-services-how-to-configure-portal/cloud-service.png)
2. <span data-ttu-id="0161a-153">Clique no item **Configurações** .</span><span class="sxs-lookup"><span data-stu-id="0161a-153">Click on the **Configuration** item.</span></span>

    ![Folha de configuração](./media/cloud-services-how-to-configure-portal/cs-settings-config.png)
3. <span data-ttu-id="0161a-155">Clique no botão **Baixar** .</span><span class="sxs-lookup"><span data-stu-id="0161a-155">Click on the **Download** button.</span></span>

    ![Baixar](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-download.png)
4. <span data-ttu-id="0161a-157">Após atualizar o arquivo de configuração de serviço, carregue e aplique as atualizações da configuração:</span><span class="sxs-lookup"><span data-stu-id="0161a-157">After you update the service configuration file, upload and apply the configuration updates:</span></span>

    ![Carregar](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-upload.png)
5. <span data-ttu-id="0161a-159">Selecione o arquivo .cscfg e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="0161a-159">Select the .cscfg file and click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0161a-160">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0161a-160">Next steps</span></span>
* <span data-ttu-id="0161a-161">Saiba como [implantar um serviço de nuvem](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0161a-161">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="0161a-162">Configurar um [nome de domínio personalizado](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0161a-162">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="0161a-163">[Gerenciar seu serviço de nuvem](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0161a-163">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
* <span data-ttu-id="0161a-164">Configurar [certificados SSL](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0161a-164">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
