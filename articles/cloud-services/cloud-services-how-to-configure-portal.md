---
title: "aaaHow tooconfigure um serviço de nuvem (portal) | Microsoft Docs"
description: "Saiba como os serviços de nuvem tooconfigure no Azure. Aprenda a configuração do serviço de nuvem tooupdate hello e configurar instâncias de toorole de acesso remoto. Esses exemplos usam Olá portal do Azure."
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
ms.openlocfilehash: 969a08558473e8c79153192942bfda587eb5ada5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-cloud-services"></a><span data-ttu-id="d60fe-105">Como os serviços de nuvem tooConfigure</span><span class="sxs-lookup"><span data-stu-id="d60fe-105">How tooConfigure Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d60fe-106">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d60fe-106">Azure portal</span></span>](cloud-services-how-to-configure-portal.md)
> * [<span data-ttu-id="d60fe-107">Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="d60fe-107">Azure classic portal</span></span>](cloud-services-how-to-configure.md)
>
>

<span data-ttu-id="d60fe-108">Você pode definir configurações de hello mais comumente usada para um serviço de nuvem no portal do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="d60fe-108">You can configure hello most commonly used settings for a cloud service in hello Azure portal.</span></span> <span data-ttu-id="d60fe-109">Ou, se desejar tooupdate seus arquivos de configuração diretamente, baixar um tooupdate de arquivo de configuração de serviço e, em seguida, carregar Olá atualizado de arquivo e atualização Olá serviço de nuvem com as alterações de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="d60fe-109">Or, if you like tooupdate your configuration files directly, download a service configuration file tooupdate, and then upload hello updated file and update hello cloud service with hello configuration changes.</span></span> <span data-ttu-id="d60fe-110">De qualquer forma, as atualizações de configuração de saudação são enviados por push tooall instâncias de função.</span><span class="sxs-lookup"><span data-stu-id="d60fe-110">Either way, hello configuration updates are pushed out tooall role instances.</span></span>

<span data-ttu-id="d60fe-111">Você também pode gerenciar instâncias de saudação do funções de serviço de nuvem, ou área de trabalho remota-los.</span><span class="sxs-lookup"><span data-stu-id="d60fe-111">You can also manage hello instances of your cloud service roles, or remote desktop into them.</span></span>

<span data-ttu-id="d60fe-112">Azure pode apenas certifique-se de 99,95% de disponibilidade durante a saudação atualizações de configuração se você tem pelo menos duas instâncias de função para cada função.</span><span class="sxs-lookup"><span data-stu-id="d60fe-112">Azure can only ensure 99.95 percent service availability during hello configuration updates if you have at least two role instances for every role.</span></span> <span data-ttu-id="d60fe-113">Que permite que uma máquina virtual tooprocess cliente solicitações enquanto outros hello está sendo atualizada.</span><span class="sxs-lookup"><span data-stu-id="d60fe-113">That enables one virtual machine tooprocess client requests while hello other is being updated.</span></span> <span data-ttu-id="d60fe-114">Para obter mais informações, consulte [Contratos de Nível de Serviço](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="d60fe-114">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

## <a name="change-a-cloud-service"></a><span data-ttu-id="d60fe-115">Alterar um serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="d60fe-115">Change a cloud service</span></span>
<span data-ttu-id="d60fe-116">Após a abertura Olá [portal do Azure](https://portal.azure.com/), navegar tooyour serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="d60fe-116">After opening hello [Azure portal](https://portal.azure.com/), navigate tooyour cloud service.</span></span> <span data-ttu-id="d60fe-117">Daqui, você gerencia muitos aspectos dele.</span><span class="sxs-lookup"><span data-stu-id="d60fe-117">From here, you manage many aspects of it.</span></span>

![Página de configurações](./media/cloud-services-how-to-configure-portal/cloud-service.png)

<span data-ttu-id="d60fe-119">Olá **configurações** ou **todas as configurações** links abrirá Olá **configurações** folha de onde você pode alterar Olá **propriedades**, alterar Olá **Configuração**, gerenciar Olá **certificados**, instalação **regras de alerta**e gerenciar Olá **usuários** que têm acesso toothis serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="d60fe-119">hello **Settings** or **All settings** links will open up hello **Settings** blade where you can change hello **Properties**, change hello **Configuration**, manage hello **Certificates**, setup **Alert rules**, and manage hello **Users** who have access toothis cloud service.</span></span>

![Folha de configurações do serviço de nuvem do Azure](./media/cloud-services-how-to-configure-portal/cs-settings-blade.png)

### <a name="manage-guest-os-version"></a><span data-ttu-id="d60fe-121">Gerenciar versão do SO Convidado</span><span class="sxs-lookup"><span data-stu-id="d60fe-121">Manage Guest OS version</span></span>

<span data-ttu-id="d60fe-122">Por padrão, o Azure atualiza periodicamente a convidado toohello mais recente com suporte imagem do sistema operacional em Olá família do sistema operacional que você especificou na sua configuração de serviço (. cscfg), como Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="d60fe-122">By default, Azure periodically updates your guest OS toohello latest supported image within hello OS family that you've specified in your service configuration (.cscfg), such as Windows Server 2016.</span></span>

<span data-ttu-id="d60fe-123">Se você precisar tootarget uma versão específica do sistema operacional, você pode defini-lo no hello **configuração** folha.</span><span class="sxs-lookup"><span data-stu-id="d60fe-123">If you need tootarget a specific OS version, you can set it in hello **Configuration** blade.</span></span>

![Definir versão do SO](./media/cloud-services-how-to-configure-portal/cs-settings-config-guestosversion.png)


>[!IMPORTANT]
> <span data-ttu-id="d60fe-125">Escolher uma versão específica do SO desabilita as atualizações automáticas do sistema operacional e torna os patches sua responsabilidade.</span><span class="sxs-lookup"><span data-stu-id="d60fe-125">Choosing a specific OS version disables automatic OS updates and makes patching your responsibility.</span></span> <span data-ttu-id="d60fe-126">Você deve garantir que suas instâncias de função estão recebendo atualizações ou você pode expor vulnerabilidades de toosecurity seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d60fe-126">You must ensure that your role instances are receiving updates or you may expose your application toosecurity vulnerabilities.</span></span>

## <a name="monitoring"></a><span data-ttu-id="d60fe-127">Monitoramento</span><span class="sxs-lookup"><span data-stu-id="d60fe-127">Monitoring</span></span>
<span data-ttu-id="d60fe-128">Você pode adicionar o serviço de nuvem tooyour alertas.</span><span class="sxs-lookup"><span data-stu-id="d60fe-128">You can add alerts tooyour cloud service.</span></span> <span data-ttu-id="d60fe-129">Clique em **Configurações** > **Regras de Alerta** > **Adicionar alerta**.</span><span class="sxs-lookup"><span data-stu-id="d60fe-129">Click **Settings** > **Alert Rules** > **Add alert**.</span></span>

![](./media/cloud-services-how-to-configure-portal/cs-alerts.png)

<span data-ttu-id="d60fe-130">Daqui, você pode configurar um alerta.</span><span class="sxs-lookup"><span data-stu-id="d60fe-130">From here, you can setup an alert.</span></span> <span data-ttu-id="d60fe-131">Com hello **métrica** caixa suspensa, você pode configurar um alerta para Olá seguintes tipos de dados.</span><span class="sxs-lookup"><span data-stu-id="d60fe-131">With hello **Metric** drop down box, you can setup an alert for hello following types of data.</span></span>

* <span data-ttu-id="d60fe-132">Leitura de disco</span><span class="sxs-lookup"><span data-stu-id="d60fe-132">Disk read</span></span>
* <span data-ttu-id="d60fe-133">Gravação de disco</span><span class="sxs-lookup"><span data-stu-id="d60fe-133">Disk write</span></span>
* <span data-ttu-id="d60fe-134">Rede no</span><span class="sxs-lookup"><span data-stu-id="d60fe-134">Network in</span></span>
* <span data-ttu-id="d60fe-135">Limite de rede</span><span class="sxs-lookup"><span data-stu-id="d60fe-135">Network out</span></span>
* <span data-ttu-id="d60fe-136">Percentual de CPU</span><span class="sxs-lookup"><span data-stu-id="d60fe-136">CPU percentage</span></span>

![](./media/cloud-services-how-to-configure-portal/cs-alert-item.png)

### <a name="configure-monitoring-from-a-metric-tile"></a><span data-ttu-id="d60fe-137">Configurar o monitoramento de um bloco de métrica</span><span class="sxs-lookup"><span data-stu-id="d60fe-137">Configure monitoring from a metric tile</span></span>
<span data-ttu-id="d60fe-138">Em vez de usar **configurações** > **regras de alerta**, você pode clicar em um dos blocos da métrica no Olá Olá **monitoramento** seção Olá **nuvem serviço** folha.</span><span class="sxs-lookup"><span data-stu-id="d60fe-138">Instead of using **Settings** > **Alert Rules**, you can click on one of hello metric tiles in hello **Monitoring** section of hello **Cloud service** blade.</span></span>

![Monitoramento de Serviço de Nuvem](./media/cloud-services-how-to-configure-portal/cs-monitoring.png)

<span data-ttu-id="d60fe-140">Aqui você pode personalizar Olá gráfico usado com o bloco de saudação ou adicionar uma regra de alerta.</span><span class="sxs-lookup"><span data-stu-id="d60fe-140">From here you can customize hello chart used with hello tile, or add an alert rule.</span></span>

## <a name="reboot-reimage-or-remote-desktop"></a><span data-ttu-id="d60fe-141">Reinicializar, refazer imagem ou a área de trabalho remota</span><span class="sxs-lookup"><span data-stu-id="d60fe-141">Reboot, reimage, or remote desktop</span></span>
<span data-ttu-id="d60fe-142">Neste momento, você não pode configurar a área de trabalho remota usando Olá **portal do Azure**.</span><span class="sxs-lookup"><span data-stu-id="d60fe-142">At this time you cannot configure remote desktop using hello **Azure portal**.</span></span> <span data-ttu-id="d60fe-143">No entanto, você pode configurá-lo por meio de saudação [portal clássico do Azure](cloud-services-role-enable-remote-desktop.md), [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md), ou por meio [Visual Studio](../vs-azure-tools-remote-desktop-roles.md).</span><span class="sxs-lookup"><span data-stu-id="d60fe-143">However, you can set it up through hello [Azure classic portal](cloud-services-role-enable-remote-desktop.md), [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md), or through [Visual Studio](../vs-azure-tools-remote-desktop-roles.md).</span></span>

<span data-ttu-id="d60fe-144">Primeiro, clique na instância de serviço de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="d60fe-144">First, click on hello cloud service instance.</span></span>

![Instância de Serviço de Nuvem](./media/cloud-services-how-to-configure-portal/cs-instance.png)

<span data-ttu-id="d60fe-146">De saudação folha que abre, você pode iniciar uma conexão de área de trabalho remota, reinicializar a instância de hello, ou remotamente a instância de saudação de refazer (com uma nova imagem de inicialização).</span><span class="sxs-lookup"><span data-stu-id="d60fe-146">From hello blade that opens you can initiate a remote desktop connection, remotely reboot hello instance, or remotely reimage (start with a fresh image) hello instance.</span></span>

![Botões de instância de serviço de nuvem](./media/cloud-services-how-to-configure-portal/cs-instance-buttons.png)

## <a name="reconfigure-your-cscfg"></a><span data-ttu-id="d60fe-148">Reconfigurar seu .cscfg</span><span class="sxs-lookup"><span data-stu-id="d60fe-148">Reconfigure your .cscfg</span></span>
<span data-ttu-id="d60fe-149">Talvez seja necessário tooreconfigure seu serviço de nuvem por meio de saudação [a configuração de serviço (cscfg)](cloud-services-model-and-package.md#cscfg) arquivo.</span><span class="sxs-lookup"><span data-stu-id="d60fe-149">You may need tooreconfigure your cloud service through hello [service config (cscfg)](cloud-services-model-and-package.md#cscfg) file.</span></span> <span data-ttu-id="d60fe-150">Primeiro é necessário toodownload o. cscfg do arquivo, modificá-la e carregá-lo.</span><span class="sxs-lookup"><span data-stu-id="d60fe-150">First you need toodownload your .cscfg file, modify it, then upload it.</span></span>

1. <span data-ttu-id="d60fe-151">Clique em hello **configurações** ícone ou hello **todas as configurações** link tooopen backup Olá **configurações** folha.</span><span class="sxs-lookup"><span data-stu-id="d60fe-151">Click on hello **Settings** icon or hello **All settings** link tooopen up hello **Settings** blade.</span></span>

    ![Página de configurações](./media/cloud-services-how-to-configure-portal/cloud-service.png)
2. <span data-ttu-id="d60fe-153">Clique em Olá **configuração** item.</span><span class="sxs-lookup"><span data-stu-id="d60fe-153">Click on hello **Configuration** item.</span></span>

    ![Folha de configuração](./media/cloud-services-how-to-configure-portal/cs-settings-config.png)
3. <span data-ttu-id="d60fe-155">Clique em Olá **baixar** botão.</span><span class="sxs-lookup"><span data-stu-id="d60fe-155">Click on hello **Download** button.</span></span>

    ![Baixar](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-download.png)
4. <span data-ttu-id="d60fe-157">Depois de atualizar o arquivo de configuração de serviço hello, carregar e aplicar as atualizações de configuração de saudação:</span><span class="sxs-lookup"><span data-stu-id="d60fe-157">After you update hello service configuration file, upload and apply hello configuration updates:</span></span>

    ![Carregar](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-upload.png)
5. <span data-ttu-id="d60fe-159">Selecione o arquivo do hello. cscfg e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="d60fe-159">Select hello .cscfg file and click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d60fe-160">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d60fe-160">Next steps</span></span>
* <span data-ttu-id="d60fe-161">Saiba como muito[implantar um serviço de nuvem](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d60fe-161">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="d60fe-162">Configurar um [nome de domínio personalizado](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d60fe-162">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="d60fe-163">[Gerenciar seu serviço de nuvem](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d60fe-163">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
* <span data-ttu-id="d60fe-164">Configurar [certificados SSL](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d60fe-164">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
