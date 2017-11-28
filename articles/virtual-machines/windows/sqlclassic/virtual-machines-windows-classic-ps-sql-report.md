---
title: "aaaUse PowerShell tooCreate uma VM com um modo de servidor de relatório nativo | Microsoft Docs"
description: "Este tópico descreve e orienta você durante implantação hello e a configuração de um servidor de relatório de modo nativo do SQL Server Reporting Services em uma máquina Virtual do Azure. "
services: virtual-machines-windows
documentationcenter: na
author: guyinacube
manager: erikre
editor: monicar
tags: azure-service-management
ms.assetid: 553af55b-d02e-4e32-904c-682bfa20fa0f
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/11/2017
ms.author: asaxton
ms.openlocfilehash: e7791199c87dff106132f1535da12de40a8dbc9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocreate-an-azure-vm-with-a-native-mode-report-server"></a><span data-ttu-id="4508d-103">Use o PowerShell tooCreate um Azure VM com um modo de servidor de relatório nativo</span><span class="sxs-lookup"><span data-stu-id="4508d-103">Use PowerShell tooCreate an Azure VM With a Native Mode Report Server</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="4508d-104">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="4508d-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="4508d-105">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="4508d-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="4508d-106">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="4508d-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="4508d-107">Este tópico descreve e orienta você durante implantação hello e a configuração de um servidor de relatório de modo nativo do SQL Server Reporting Services em uma máquina Virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="4508d-107">This topic describes and walks you through hello deployment and configuration of a SQL Server Reporting Services native mode report server in an Azure Virtual Machine.</span></span> <span data-ttu-id="4508d-108">Olá etapas neste documento, use uma combinação de etapas manuais toocreate Olá VM e um script do Windows PowerShell tooconfigure Reporting Services em Olá VM.</span><span class="sxs-lookup"><span data-stu-id="4508d-108">hello steps in this document use a combination of manual steps toocreate hello virtual machine and a Windows PowerShell script tooconfigure Reporting Services on hello VM.</span></span> <span data-ttu-id="4508d-109">script de configuração de saudação inclui a abertura de uma porta de firewall para HTTP ou HTTPs.</span><span class="sxs-lookup"><span data-stu-id="4508d-109">hello configuration script includes opening a firewall port for HTTP or HTTPs.</span></span>

> [!NOTE]
> <span data-ttu-id="4508d-110">Se você não precisa **HTTPS** no servidor de relatório hello, **pular a etapa 2**.</span><span class="sxs-lookup"><span data-stu-id="4508d-110">If you do not require **HTTPS** on hello report server, **skip step 2**.</span></span>
> 
> <span data-ttu-id="4508d-111">Depois de criar hello VM na etapa 1, acesse servidor de relatório toohello seção Use script tooconfigure hello e HTTP.</span><span class="sxs-lookup"><span data-stu-id="4508d-111">After creating hello VM in step 1, go toohello section Use script tooconfigure hello report server and HTTP.</span></span> <span data-ttu-id="4508d-112">Depois de executar o script hello, o servidor de relatório de saudação é toouse pronto.</span><span class="sxs-lookup"><span data-stu-id="4508d-112">After you run hello script, hello report server is ready toouse.</span></span>

## <a name="prerequisites-and-assumptions"></a><span data-ttu-id="4508d-113">Pré-requisitos e suposições</span><span class="sxs-lookup"><span data-stu-id="4508d-113">Prerequisites and Assumptions</span></span>
* <span data-ttu-id="4508d-114">**Assinatura do Azure**: Verifique se o número de saudação de núcleos disponíveis em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="4508d-114">**Azure Subscription**: Verify hello number of cores available in your Azure Subscription.</span></span> <span data-ttu-id="4508d-115">Se você criar hello recomendado tamanho da VM do **A3**, você precisa **4** núcleos disponíveis.</span><span class="sxs-lookup"><span data-stu-id="4508d-115">If you create hello recommended VM size of **A3**, you need **4** available cores.</span></span> <span data-ttu-id="4508d-116">Se você usar um tamanho de VM **A2**, precisará de **2** núcleos disponíveis.</span><span class="sxs-lookup"><span data-stu-id="4508d-116">If you use a VM size of **A2**, you need **2** available cores.</span></span>
  
  * <span data-ttu-id="4508d-117">limite de núcleo de saudação tooverify de sua assinatura, Olá portal clássico do Azure, clique em configurações no painel esquerdo do hello e, em seguida, clique em uso no menu superior hello.</span><span class="sxs-lookup"><span data-stu-id="4508d-117">tooverify hello core limit of your subscription, in hello Azure classic portal, click SETTINGS in hello left pane and then Click USAGE in hello top menu.</span></span>
  * <span data-ttu-id="4508d-118">cota de núcleo Olá tooincrease, entre em contato com [suporte do Azure](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="4508d-118">tooincrease hello core quota, contact [Azure Support](https://azure.microsoft.com/support/options/).</span></span> <span data-ttu-id="4508d-119">Para saber mais sobre o tamanho da VM, consulte [Tamanhos de máquinas virtuais do Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4508d-119">For VM size information, see [Virtual Machine Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="4508d-120">**Scripts do Windows PowerShell**: tópico Olá pressupõe que você tenha um conhecimento prático básico do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4508d-120">**Windows PowerShell Scripting**: hello topic assumes that you have a basic working knowledge of Windows PowerShell.</span></span> <span data-ttu-id="4508d-121">Para obter mais informações sobre como usar o Windows PowerShell, consulte o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="4508d-121">For more information about using Windows PowerShell, see hello following:</span></span>
  
  * [<span data-ttu-id="4508d-122">Iniciando o Windows PowerShell no Windows Server</span><span class="sxs-lookup"><span data-stu-id="4508d-122">Starting Windows PowerShell on Windows Server</span></span>](https://technet.microsoft.com/library/hh847814.aspx)
  * [<span data-ttu-id="4508d-123">Introdução ao Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="4508d-123">Getting Started with Windows PowerShell</span></span>](https://technet.microsoft.com/library/hh857337.aspx)

## <a name="step-1-provision-an-azure-virtual-machine"></a><span data-ttu-id="4508d-124">Etapa 1: provisionar uma máquina virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="4508d-124">Step 1: Provision an Azure Virtual Machine</span></span>
1. <span data-ttu-id="4508d-125">Procure toohello portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="4508d-125">Browse toohello Azure classic portal.</span></span>
2. <span data-ttu-id="4508d-126">Clique em **máquinas virtuais** no painel esquerdo da saudação.</span><span class="sxs-lookup"><span data-stu-id="4508d-126">Click **Virtual Machines** in hello left pane.</span></span>
   
    ![máquinas virtuais do microsoft azure](./media/virtual-machines-windows-classic-ps-sql-report/IC660124.gif)
3. <span data-ttu-id="4508d-128">Clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="4508d-128">Click **New**.</span></span>
   
    ![botão novo](./media/virtual-machines-windows-classic-ps-sql-report/IC692019.gif)
4. <span data-ttu-id="4508d-130">Clique em **Da Galeria**.</span><span class="sxs-lookup"><span data-stu-id="4508d-130">Click **From Gallery**.</span></span>
   
    ![nova vm da galeria](./media/virtual-machines-windows-classic-ps-sql-report/IC692020.gif)
5. <span data-ttu-id="4508d-132">Clique em **SQL Server 2014 RTM Standard – Windows Server 2012 R2** e, em seguida, clique em Olá seta toocontinue.</span><span class="sxs-lookup"><span data-stu-id="4508d-132">Click **SQL Server 2014 RTM Standard – Windows Server 2012 R2** and then click hello arrow toocontinue.</span></span>
   
    ![Próximo](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
   
    <span data-ttu-id="4508d-134">Se precisar de dados do Reporting Services Olá controlados por recursos de assinaturas, escolha **SQL Server 2014 RTM Enterprise – Windows Server 2012 R2**.</span><span class="sxs-lookup"><span data-stu-id="4508d-134">If you need hello Reporting Services data driven subscriptions feature, choose **SQL Server 2014 RTM Enterprise – Windows Server 2012 R2**.</span></span> <span data-ttu-id="4508d-135">Para obter mais informações sobre o suporte de recursos e edições do SQL Server, consulte [recursos com suporte Olá edições do SQL Server 2012](https://msdn.microsoft.com/library/cc645993.aspx#Reporting).</span><span class="sxs-lookup"><span data-stu-id="4508d-135">For more information on SQL Server editions and feature support, see [Features Supported by hello Editions of SQL Server 2012](https://msdn.microsoft.com/library/cc645993.aspx#Reporting).</span></span>
6. <span data-ttu-id="4508d-136">Em Olá **configuração de máquina Virtual** página, edite Olá campos a seguir:</span><span class="sxs-lookup"><span data-stu-id="4508d-136">On hello **Virtual machine configuration** page, edit hello following fields:</span></span>
   
   * <span data-ttu-id="4508d-137">Se houver mais de um **data de lançamento de versão**, selecione Olá a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="4508d-137">If there is more than one **VERSION RELEASE DATE**, select hello most recent version.</span></span>
   * <span data-ttu-id="4508d-138">**Nome da máquina virtual**: nome da máquina Olá também é usado na próxima página de configuração hello como nome de DNS do serviço de nuvem saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="4508d-138">**Virtual Machine Name**: hello machine name is also used on hello next configuration page as hello default Cloud Service DNS name.</span></span> <span data-ttu-id="4508d-139">nome DNS Olá deve ser exclusivo entre saudação do serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="4508d-139">hello DNS name must be unique across hello Azure service.</span></span> <span data-ttu-id="4508d-140">Considere configurar Olá VM com um nome de computador que descreve quais Olá VM é usada para.</span><span class="sxs-lookup"><span data-stu-id="4508d-140">Consider configuring hello VM with a computer name that describes what hello VM is used for.</span></span> <span data-ttu-id="4508d-141">Por exemplo, ssrsnativecloud.</span><span class="sxs-lookup"><span data-stu-id="4508d-141">For example ssrsnativecloud.</span></span>
   * <span data-ttu-id="4508d-142">**Camada**: Standard</span><span class="sxs-lookup"><span data-stu-id="4508d-142">**Tier**: Standard</span></span>
   * <span data-ttu-id="4508d-143">**Tamanho: A3** Olá recomenda tamanho da VM para cargas de trabalho do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4508d-143">**Size:A3** is hello recommended VM size for SQL Server workloads.</span></span> <span data-ttu-id="4508d-144">Se uma VM é usada apenas como um servidor de relatório, um tamanho VM de A2 será suficiente a menos que o servidor de relatório Olá experimente uma grande carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="4508d-144">If a VM is only used as a report server, a VM size of A2 is sufficient unless hello report server experiences a large workload.</span></span> <span data-ttu-id="4508d-145">Para saber mais sobre preços da VM, consulte [Preços das Máquinas Virtuais](https://azure.microsoft.com/pricing/details/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="4508d-145">For VM pricing information, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/).</span></span>
   * <span data-ttu-id="4508d-146">**Novo nome de usuário**: nome de saudação fornecido é criado como um administrador no hello VM.</span><span class="sxs-lookup"><span data-stu-id="4508d-146">**New User Name**: hello name you provide is created as an administrator on hello VM.</span></span>
   * <span data-ttu-id="4508d-147">**Nova Senha** e **Confirmar**.</span><span class="sxs-lookup"><span data-stu-id="4508d-147">**New Password** and **confirm**.</span></span> <span data-ttu-id="4508d-148">Essa senha é usada para a nova conta de administrador hello e é recomendável que usar uma senha forte.</span><span class="sxs-lookup"><span data-stu-id="4508d-148">This password is used for hello new administrator account and it is recommended you use a strong password.</span></span>
   * <span data-ttu-id="4508d-149">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="4508d-149">Click **Next**.</span></span> <span data-ttu-id="4508d-150">![next](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)</span><span class="sxs-lookup"><span data-stu-id="4508d-150">![next](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)</span></span>
7. <span data-ttu-id="4508d-151">Na página seguinte do hello, edite Olá campos a seguir:</span><span class="sxs-lookup"><span data-stu-id="4508d-151">On hello next page, edit hello following fields:</span></span>
   
   * <span data-ttu-id="4508d-152">**Serviço de Nuvem**: selecione **Criar um novo Serviço de Nuvem**.</span><span class="sxs-lookup"><span data-stu-id="4508d-152">**Cloud Service**: select **Create a new Cloud Service**.</span></span>
   * <span data-ttu-id="4508d-153">**Nome DNS do serviço de nuvem**: Este é o nome DNS público de saudação do hello serviço de nuvem que está associado a saudação VM.</span><span class="sxs-lookup"><span data-stu-id="4508d-153">**Cloud Service DNS Name**: This is hello public DNS name of hello Cloud Service that is associated with hello VM.</span></span> <span data-ttu-id="4508d-154">saudação padrão é Olá nome digitado no nome da VM hello.</span><span class="sxs-lookup"><span data-stu-id="4508d-154">hello default name is hello name you typed in for hello VM name.</span></span> <span data-ttu-id="4508d-155">Se em etapas posteriores do tópico hello, você cria um certificado SSL confiável e, em seguida, o nome DNS de saudação é usado para valor Olá Olá "**emitido para**" do certificado de saudação.</span><span class="sxs-lookup"><span data-stu-id="4508d-155">If in later steps of hello topic, you create a trusted SSL certificate and then hello DNS name is used for hello value of hello “**Issued to**” of hello certificate.</span></span>
   * <span data-ttu-id="4508d-156">**Afinidade de região/grupo/Rede Virtual**: escolha Olá região mais próxima tooyour os usuários finais.</span><span class="sxs-lookup"><span data-stu-id="4508d-156">**Region/Affinity Group/Virtual Network**: Choose hello region closest tooyour end users.</span></span>
   * <span data-ttu-id="4508d-157">**Conta de Armazenamento**: use uma conta de armazenamento gerada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="4508d-157">**Storage Account**: Use an automatically generated storage account.</span></span>
   * <span data-ttu-id="4508d-158">**Conjunto de Disponibilidades**: nenhum.</span><span class="sxs-lookup"><span data-stu-id="4508d-158">**Availability Set**: None.</span></span>
   * <span data-ttu-id="4508d-159">**Pontos de EXTREMIDADE** manter Olá **área de trabalho remota** e **PowerShell** pontos de extremidade e, em seguida, adicione o ponto de extremidade HTTP ou HTTPS, dependendo do seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="4508d-159">**ENDPOINTS** Keep hello **Remote Desktop** and **PowerShell** endpoints and then add either an HTTP or HTTPS endpoint, depending on your environment.</span></span>
     
     * <span data-ttu-id="4508d-160">**HTTP**: Olá padrão portas públicas e privadas são **80**.</span><span class="sxs-lookup"><span data-stu-id="4508d-160">**HTTP**: hello default public and private ports are **80**.</span></span> <span data-ttu-id="4508d-161">Observe que se você usar uma porta privada diferente de 80, modifique **$HTTPport = 80** no script de http hello.</span><span class="sxs-lookup"><span data-stu-id="4508d-161">Note that if you use a private port other than 80, modify **$HTTPport = 80** in hello http script.</span></span>
     * <span data-ttu-id="4508d-162">**HTTPS**: Olá padrão portas públicas e privadas são **443**.</span><span class="sxs-lookup"><span data-stu-id="4508d-162">**HTTPS**: hello default public and private ports are **443**.</span></span> <span data-ttu-id="4508d-163">Uma prática recomendada de segurança é a porta privada do toochange hello e configurar seu firewall e hello relatório toouse Olá privada porta do servidor.</span><span class="sxs-lookup"><span data-stu-id="4508d-163">A security best practice is toochange hello private port and configure your firewall and hello report server toouse hello private port.</span></span> <span data-ttu-id="4508d-164">Para obter mais informações sobre pontos de extremidade, consulte [como tooSet a comunicação com uma máquina Virtual](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4508d-164">For more information on endpoints, see [How tooSet Up Communication with a Virtual Machine](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="4508d-165">Observe que se você usar uma porta diferente de 443, altere o parâmetro hello **$HTTPsport = 443** em Olá script HTTPS.</span><span class="sxs-lookup"><span data-stu-id="4508d-165">Note that if you use a port other than 443, change hello parameter **$HTTPsport = 443** in hello HTTPS script.</span></span>
   * <span data-ttu-id="4508d-166">Clique em Próximo.</span><span class="sxs-lookup"><span data-stu-id="4508d-166">Click next .</span></span> ![Próximo](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
8. <span data-ttu-id="4508d-168">Na última página do Assistente de Olá Olá, mantenha o padrão de saudação **instalar agente de VM de saudação** selecionado.</span><span class="sxs-lookup"><span data-stu-id="4508d-168">On hello last page of hello wizard, keep hello default **Install hello VM agent** selected.</span></span> <span data-ttu-id="4508d-169">Olá etapas neste tópico não utilizam o agente de VM hello, mas se você planejar tookeep essa VM, extensões e agente VM Olá permitirá que você tooenhance he CM.</span><span class="sxs-lookup"><span data-stu-id="4508d-169">hello steps in this topic do not utilize hello VM agent but if you plan tookeep this VM, hello VM agent and extensions will allow you tooenhance he CM.</span></span>  <span data-ttu-id="4508d-170">Para obter mais informações sobre o agente de VM hello, consulte [agente de VM e extensões – parte 1](https://azure.microsoft.com/blog/2014/04/11/vm-agent-and-extensions-part-1/).</span><span class="sxs-lookup"><span data-stu-id="4508d-170">For more information on hello VM agent, see [VM Agent and Extensions – Part 1](https://azure.microsoft.com/blog/2014/04/11/vm-agent-and-extensions-part-1/).</span></span> <span data-ttu-id="4508d-171">Uma saudação extensões padrão instaladas em execução é extensão "BGINFO" hello exibidas na área de trabalho VM hello, informações do sistema, como IP interno e sem espaço em disco.</span><span class="sxs-lookup"><span data-stu-id="4508d-171">One of hello default extensions installed ad running is hello “BGINFO” extension that displays on hello VM desktop, system information such as internal IP and free drive space.</span></span>
9. <span data-ttu-id="4508d-172">Clique em Concluído.</span><span class="sxs-lookup"><span data-stu-id="4508d-172">Click complete .</span></span> ![Ok](./media/virtual-machines-windows-classic-ps-sql-report/IC660122.gif)
10. <span data-ttu-id="4508d-174">Olá **Status** de saudação VM exibe como **iniciando (Provisionando)** durante o processo de provisionamento de saudação e, em seguida, é exibido como **executando** quando Olá VM é provisionada e pronta toouse.</span><span class="sxs-lookup"><span data-stu-id="4508d-174">hello **Status** of hello VM displays as **Starting (Provisioning)** during hello provision process and then displays as **Running** when hello VM is provisioned and ready toouse.</span></span>

## <a name="step-2-create-a-server-certificate"></a><span data-ttu-id="4508d-175">Etapa 2: criar um certificado de servidor</span><span class="sxs-lookup"><span data-stu-id="4508d-175">Step 2: Create a Server Certificate</span></span>
> [!NOTE]
> <span data-ttu-id="4508d-176">Se você não exigir HTTPS no servidor de relatório hello, você pode **pular a etapa 2** e vá seção toohello **usar HTTP e o servidor de relatório de saudação do script tooconfigure**.</span><span class="sxs-lookup"><span data-stu-id="4508d-176">If you do not require HTTPS on hello report server, you can **skip step 2** and go toohello section **Use script tooconfigure hello report server and HTTP**.</span></span> <span data-ttu-id="4508d-177">Use Olá HTTP script tooquickly configurar servidor de relatório hello e relatório Olá servidor será toouse pronto.</span><span class="sxs-lookup"><span data-stu-id="4508d-177">Use hello HTTP script tooquickly configure hello report server and hello report server will be ready toouse.</span></span>

<span data-ttu-id="4508d-178">Na ordem toouse HTTPS na VM de Olá, é necessário um certificado SSL confiável.</span><span class="sxs-lookup"><span data-stu-id="4508d-178">In order toouse HTTPS on hello VM, you need a trusted SSL certificate.</span></span> <span data-ttu-id="4508d-179">Dependendo do cenário, você pode usar uma saudação dois métodos a seguir:</span><span class="sxs-lookup"><span data-stu-id="4508d-179">Depending on your scenario, you can use one of hello following two methods:</span></span>

* <span data-ttu-id="4508d-180">Um certificado SSL válido emitido por uma Autoridade de Certificação (CA) e de confiança da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4508d-180">A valid SSL certificate issued by a Certification Authority (CA) and trusted by Microsoft.</span></span> <span data-ttu-id="4508d-181">certificados de raiz da autoridade de certificação Olá são necessário toobe distribuído por meio de saudação Microsoft Root Certificate Program.</span><span class="sxs-lookup"><span data-stu-id="4508d-181">hello CA root certificates are required toobe distributed via hello Microsoft Root Certificate Program.</span></span> <span data-ttu-id="4508d-182">Para obter mais informações sobre este programa, consulte [Windows e Windows Phone 8 SSL Root Certificate Program (membros CAs)](http://social.technet.microsoft.com/wiki/contents/articles/14215.windows-and-windows-phone-8-ssl-root-certificate-program-member-cas.aspx) e [toohello de Introdução do Microsoft Root Certificate Program](http://social.technet.microsoft.com/wiki/contents/articles/3281.introduction-to-the-microsoft-root-certificate-program.aspx).</span><span class="sxs-lookup"><span data-stu-id="4508d-182">For more information about this program, see [Windows and Windows Phone 8 SSL Root Certificate Program (Member CAs)](http://social.technet.microsoft.com/wiki/contents/articles/14215.windows-and-windows-phone-8-ssl-root-certificate-program-member-cas.aspx) and [Introduction toohello Microsoft Root Certificate Program](http://social.technet.microsoft.com/wiki/contents/articles/3281.introduction-to-the-microsoft-root-certificate-program.aspx).</span></span>
* <span data-ttu-id="4508d-183">Um certificado autoassinado.</span><span class="sxs-lookup"><span data-stu-id="4508d-183">A self-signed certificate.</span></span> <span data-ttu-id="4508d-184">Os certificados autoassinados não são recomendados para ambientes de produção.</span><span class="sxs-lookup"><span data-stu-id="4508d-184">Self-signed certificates are not recommended for production environments.</span></span>

### <a name="toouse-a-certificate-created-by-a-trusted-certificate-authority-ca"></a><span data-ttu-id="4508d-185">toouse um certificado criado por uma autoridade de certificação confiável (CA)</span><span class="sxs-lookup"><span data-stu-id="4508d-185">toouse a certificate created by a trusted Certificate Authority (CA)</span></span>
1. <span data-ttu-id="4508d-186">**Solicitar um certificado de servidor para o site de saudação de uma autoridade de certificação**.</span><span class="sxs-lookup"><span data-stu-id="4508d-186">**Request a server certificate for hello website from a certification authority**.</span></span> 
   
    <span data-ttu-id="4508d-187">Você pode usar o hello Assistente de certificado de servidor Web ou toogenerate um arquivo de solicitação de certificado (Certreq.txt) que você enviar tooa autoridade de certificação ou toogenerate uma solicitação para uma autoridade de certificação online.</span><span class="sxs-lookup"><span data-stu-id="4508d-187">You can use hello Web Server Certificate Wizard either toogenerate a certificate request file (Certreq.txt) that you send tooa certification authority, or toogenerate a request for an online certification authority.</span></span> <span data-ttu-id="4508d-188">Por exemplo, os Serviços de Certificados da Microsoft no Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="4508d-188">For example, Microsoft Certificate Services in Windows Server 2012.</span></span> <span data-ttu-id="4508d-189">Dependendo do nível de saudação de garantia de identificação fornecida pelo certificado de servidor, é dias tooseveral meses para tooapprove de autoridade de certificação Olá sua solicitação e envie um arquivo de certificado.</span><span class="sxs-lookup"><span data-stu-id="4508d-189">Depending on hello level of identification assurance offered by your server certificate, it is several days tooseveral months for hello certification authority tooapprove your request and send you a certificate file.</span></span> 
   
    <span data-ttu-id="4508d-190">Para obter mais informações sobre como solicitar certificados de servidor, consulte o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="4508d-190">For more information about requesting a server certificates, see hello following:</span></span> 
   
   * <span data-ttu-id="4508d-191">Use [Certreq](https://technet.microsoft.com/library/cc725793.aspx), [Certreq](https://technet.microsoft.com/library/cc725793.aspx).</span><span class="sxs-lookup"><span data-stu-id="4508d-191">Use [Certreq](https://technet.microsoft.com/library/cc725793.aspx), [Certreq](https://technet.microsoft.com/library/cc725793.aspx).</span></span>
   * <span data-ttu-id="4508d-192">TooAdminister de ferramentas de segurança do Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="4508d-192">Security Tools tooAdminister Windows Server 2012.</span></span>
     
     [<span data-ttu-id="4508d-193">TooAdminister de ferramentas de segurança do Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="4508d-193">Security Tools tooAdminister Windows Server 2012</span></span>](https://technet.microsoft.com/library/jj730960.aspx)
     
     > [!NOTE]
     > <span data-ttu-id="4508d-194">Olá **emitido para** campo de saudação confiável certificado SSL deve ser Olá mesmo como Olá **nome de DNS do serviço de nuvem** você usou para Olá nova VM.</span><span class="sxs-lookup"><span data-stu-id="4508d-194">hello **issued to** field of hello trusted SSL certificate should be hello same as hello **Cloud Service DNS NAME** you used for hello new VM.</span></span>

2. <span data-ttu-id="4508d-195">**Instalar o certificado de servidor de saudação no servidor de Web hello**.</span><span class="sxs-lookup"><span data-stu-id="4508d-195">**Install hello server certificate on hello Web server**.</span></span> <span data-ttu-id="4508d-196">Nesse caso, o servidor de Web Hello é Olá VM que hospeda Olá servidor de relatório e site Olá é criado em etapas posteriores quando você configurar o Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="4508d-196">hello Web server in this case is hello VM that hosts hello report server and hello website is created in later steps when you configure Reporting Services.</span></span> <span data-ttu-id="4508d-197">Para obter mais informações sobre como instalar o certificado do servidor de saudação no servidor de Web hello usando o snap-in do MMC do certificado hello, consulte [instalar um certificado de servidor](https://technet.microsoft.com/library/cc740068).</span><span class="sxs-lookup"><span data-stu-id="4508d-197">For more information about installing hello server certificate on hello Web server by using hello Certificate MMC snap-in, see [Install a Server Certificate](https://technet.microsoft.com/library/cc740068).</span></span>
   
    <span data-ttu-id="4508d-198">Se você quiser que o script de saudação toouse incluído neste tópico, o servidor de relatório Olá tooconfigure, Olá valor de certificados Olá **impressão digital** é exigido como um parâmetro de script hello.</span><span class="sxs-lookup"><span data-stu-id="4508d-198">If you want toouse hello script included with this topic, tooconfigure hello report server, hello value of hello certificates **Thumbprint** is required as a parameter of hello script.</span></span> <span data-ttu-id="4508d-199">Consulte Olá próxima seção para obter detalhes sobre como tooobtain Olá a impressão digital do certificado de saudação.</span><span class="sxs-lookup"><span data-stu-id="4508d-199">See hello next section for details on how tooobtain hello thumbprint of hello certificate.</span></span>
3. <span data-ttu-id="4508d-200">Atribua o servidor de relatório toohello do certificado de servidor hello.</span><span class="sxs-lookup"><span data-stu-id="4508d-200">Assign hello server certificate toohello report server.</span></span> <span data-ttu-id="4508d-201">atribuição de saudação é concluída na próxima seção, hello quando você configura o servidor de relatório hello.</span><span class="sxs-lookup"><span data-stu-id="4508d-201">hello assignment is completed in hello next section when you configure hello report server.</span></span>

### <a name="toouse-hello-virtual-machines-self-signed-certificate"></a><span data-ttu-id="4508d-202">Olá toouse certificado autoassinado de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="4508d-202">toouse hello Virtual Machines Self-signed Certificate</span></span>
<span data-ttu-id="4508d-203">Um certificado autoassinado foi criado no hello VM quando Olá VM foi provisionada.</span><span class="sxs-lookup"><span data-stu-id="4508d-203">A self-signed certificate was created on hello VM when hello VM was provisioned.</span></span> <span data-ttu-id="4508d-204">certificado de saudação tem Olá mesmo nome como Olá nome DNS da VM.</span><span class="sxs-lookup"><span data-stu-id="4508d-204">hello certificate has hello same name as hello VM DNS name.</span></span> <span data-ttu-id="4508d-205">Erros de certificado tooavoid ordem, é necessário certificado Olá é confiável no hello própria VM e também por todos os usuários do site de saudação.</span><span class="sxs-lookup"><span data-stu-id="4508d-205">In order tooavoid certificate errors, it is required that hello certificate is trusted on hello VM itself, and also by all users of hello site.</span></span>

1. <span data-ttu-id="4508d-206">tootrust Olá autoridade de certificação raiz do certificado Olá Olá VM Local, adicione Olá certificado toohello **autoridades de certificação raiz confiáveis**.</span><span class="sxs-lookup"><span data-stu-id="4508d-206">tootrust hello root CA of hello certificate on hello Local VM, add hello certificate toohello **Trusted Root Certification Authorities**.</span></span> <span data-ttu-id="4508d-207">seguir Olá é um resumo das etapas de saudação necessárias.</span><span class="sxs-lookup"><span data-stu-id="4508d-207">hello following is a summary of hello steps required.</span></span> <span data-ttu-id="4508d-208">Para obter etapas detalhadas sobre como tootrust Olá autoridade de certificação, consulte [instalar um certificado de servidor](https://technet.microsoft.com/library/cc740068).</span><span class="sxs-lookup"><span data-stu-id="4508d-208">For detailed steps on how tootrust hello CA, see [Install a Server Certificate](https://technet.microsoft.com/library/cc740068).</span></span>
   
   1. <span data-ttu-id="4508d-209">Olá portal clássico do Azure, selecione Olá VM e clique em conectar.</span><span class="sxs-lookup"><span data-stu-id="4508d-209">From hello Azure classic portal, select hello VM and click connect.</span></span> <span data-ttu-id="4508d-210">Dependendo da configuração do navegador, talvez seja solicitado toosave um arquivo. rdp para conexão toohello VM.</span><span class="sxs-lookup"><span data-stu-id="4508d-210">Depending on your browser configuration, you may be prompted toosave an .rdp file for connecting toohello VM.</span></span>
      
       ![Conecte-se a máquina virtual de tooazure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="4508d-212">Use o nome da VM Olá usuário, nome de usuário e senha configurados quando você criou Olá VM.</span><span class="sxs-lookup"><span data-stu-id="4508d-212">Use hello user VM name, user name and password you configured when you created hello VM.</span></span> 
      
       <span data-ttu-id="4508d-213">Por exemplo, Olá a imagem a seguir, Olá VM nome é **ssrsnativecloud** e nome de usuário Olá **testuser**.</span><span class="sxs-lookup"><span data-stu-id="4508d-213">For example, in hello following image, hello VM name is **ssrsnativecloud** and hello user name is **testuser**.</span></span>
      
       ![o logon inclui o nome da vm](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
   2. <span data-ttu-id="4508d-215">Execute mmc.exe.</span><span class="sxs-lookup"><span data-stu-id="4508d-215">Run mmc.exe.</span></span> <span data-ttu-id="4508d-216">Para obter mais informações, consulte [como: exibir certificados com hello Snap-in do MMC](https://msdn.microsoft.com/library/ms788967.aspx).</span><span class="sxs-lookup"><span data-stu-id="4508d-216">For more information, see [How to: View Certificates with hello MMC Snap-in](https://msdn.microsoft.com/library/ms788967.aspx).</span></span>
   3. <span data-ttu-id="4508d-217">No aplicativo de console hello **arquivo** menu Adicionar Olá **certificados** snap-in, selecione **conta de computador** quando solicitado e, em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="4508d-217">In hello console application **File** menu, add hello **Certificates** snap-in, select **Computer Account** when prompted, and then click **Next**.</span></span>
   4. <span data-ttu-id="4508d-218">Selecione **computador Local** toomanage e, em seguida, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="4508d-218">Select **Local Computer** toomanage and then click **Finish**.</span></span>
   5. <span data-ttu-id="4508d-219">Clique em **Okey** e, em seguida, expanda Olá **certificados - Personal** nós e clique **certificados**.</span><span class="sxs-lookup"><span data-stu-id="4508d-219">Click **Ok** and then expand hello **Certificates -Personal** nodes and then click **Certificates**.</span></span> <span data-ttu-id="4508d-220">Olá certificado é nomeado após o nome DNS de saudação do hello VM e termina com **cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="4508d-220">hello certificate is named after hello DNS name of hello VM and ends with **cloudapp.net**.</span></span> <span data-ttu-id="4508d-221">Nome do certificado Olá de mouse e clique em **cópia**.</span><span class="sxs-lookup"><span data-stu-id="4508d-221">Right-click hello certificate name and click **Copy**.</span></span>
   6. <span data-ttu-id="4508d-222">Expanda Olá **autoridades de certificação raiz confiáveis** nó e, em seguida, clique com botão direito **certificados** e, em seguida, clique em **colar**.</span><span class="sxs-lookup"><span data-stu-id="4508d-222">Expand hello **Trusted Root Certification Authorities** node and then right-click **Certificates** and then click **Paste**.</span></span>
   7. <span data-ttu-id="4508d-223">toovalidate, duplo clique no nome do certificado de saudação em **autoridades de certificação raiz confiáveis** e verifique se não existem erros e veja seu certificado.</span><span class="sxs-lookup"><span data-stu-id="4508d-223">toovalidate, double click on hello certificate name under **Trusted Root Certification Authorities** and verify that there are no errors and you see your certificate.</span></span> <span data-ttu-id="4508d-224">Se você quiser toouse Olá HTTPS script incluído neste tópico, o servidor de relatório do tooconfigure hello, Olá valor de certificados Olá **impressão digital** é exigido como um parâmetro de script hello.</span><span class="sxs-lookup"><span data-stu-id="4508d-224">If you want toouse hello HTTPS script included with this topic, tooconfigure hello report server, hello value of hello certificates **Thumbprint** is required as a parameter of hello script.</span></span> <span data-ttu-id="4508d-225">**valor de impressão digital Olá tooget**, conclua Olá seguinte.</span><span class="sxs-lookup"><span data-stu-id="4508d-225">**tooget hello thumbprint value**, complete hello following.</span></span> <span data-ttu-id="4508d-226">Há também uma impressão digital saudação do PowerShell exemplo tooretrieve na seção [usar HTTPS e servidor de relatório do script tooconfigure Olá](#use-script-to-configure-the-report-server-and-HTTPS).</span><span class="sxs-lookup"><span data-stu-id="4508d-226">There is also a PowerShell sample tooretrieve hello thumbprint in section [Use script tooconfigure hello report server and HTTPS](#use-script-to-configure-the-report-server-and-HTTPS).</span></span>
      
      1. <span data-ttu-id="4508d-227">Clique duas vezes no nome de saudação do certificado de hello, por exemplo ssrsnativecloud.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="4508d-227">Double-click hello name of hello certificate, for example ssrsnativecloud.cloudapp.net.</span></span>
      2. <span data-ttu-id="4508d-228">Clique em Olá **detalhes** guia.</span><span class="sxs-lookup"><span data-stu-id="4508d-228">Click hello **Details** tab.</span></span>
      3. <span data-ttu-id="4508d-229">Clique em **Impressão digital**.</span><span class="sxs-lookup"><span data-stu-id="4508d-229">Click **Thumbprint**.</span></span> <span data-ttu-id="4508d-230">valor de saudação da impressão digital de saudação é exibido no campo de detalhes hello, por exemplo, a6 08 3C df f9 0b f7 e3 7c 25 ed a4 ed 7e CA 91 9C 2C fb 2f.</span><span class="sxs-lookup"><span data-stu-id="4508d-230">hello value of hello thumbprint is displayed in hello details field, for example ‎a6 08 3c df f9 0b f7 e3 7c 25 ed a4 ed 7e ac 91 9c 2c fb 2f.</span></span>
      4. <span data-ttu-id="4508d-231">Copie a impressão digital de saudação e salvar o valor de saudação para mais tarde ou edite o script hello agora.</span><span class="sxs-lookup"><span data-stu-id="4508d-231">Copy hello thumbprint and save hello value for later or edit hello script now.</span></span>
      5. <span data-ttu-id="4508d-232">(*) Antes de executar o script hello, remova os espaços de saudação entre Olá pares de valores.</span><span class="sxs-lookup"><span data-stu-id="4508d-232">(*) Before you run hello script, remove hello spaces in between hello pairs of values.</span></span> <span data-ttu-id="4508d-233">Por exemplo impressão digital de saudação observada anteriormente agora seria a6083cdff90bf7e37c25eda4ed7eac919c2cfb2f.</span><span class="sxs-lookup"><span data-stu-id="4508d-233">For example hello thumbprint noted before would now be ‎a6083cdff90bf7e37c25eda4ed7eac919c2cfb2f.</span></span>
      6. <span data-ttu-id="4508d-234">Atribua o servidor de relatório toohello do certificado de servidor hello.</span><span class="sxs-lookup"><span data-stu-id="4508d-234">Assign hello server certificate toohello report server.</span></span> <span data-ttu-id="4508d-235">atribuição de saudação é concluída na próxima seção, hello quando você configura o servidor de relatório hello.</span><span class="sxs-lookup"><span data-stu-id="4508d-235">hello assignment is completed in hello next section when you configure hello report server.</span></span>

<span data-ttu-id="4508d-236">Se você estiver usando um certificado SSL autoassinado, o nome de Olá no certificado Olá corresponde já Olá hostname de saudação VM.</span><span class="sxs-lookup"><span data-stu-id="4508d-236">If you are using a self-signed SSL certificate, hello name on hello certificate already matches hello hostname of hello VM.</span></span> <span data-ttu-id="4508d-237">Portanto, Olá DNS da máquina Olá já estará registrado globalmente e pode ser acessado de qualquer cliente.</span><span class="sxs-lookup"><span data-stu-id="4508d-237">Therefore, hello DNS of hello machine is already registered globally and can be accessed from any client.</span></span>

## <a name="step-3-configure-hello-report-server"></a><span data-ttu-id="4508d-238">Etapa 3: Configurar Olá servidor de relatório</span><span class="sxs-lookup"><span data-stu-id="4508d-238">Step 3: Configure hello Report Server</span></span>
<span data-ttu-id="4508d-239">Esta seção explica como configurar Olá VM como um servidor de relatório de modo nativo do Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="4508d-239">This section walks you through configuring hello VM as a Reporting Services native mode report server.</span></span> <span data-ttu-id="4508d-240">Você pode usar um Olá servidor de relatório de saudação de tooconfigure métodos a seguir:</span><span class="sxs-lookup"><span data-stu-id="4508d-240">You can use one of hello following methods tooconfigure hello report server:</span></span>

* <span data-ttu-id="4508d-241">Usar o servidor de relatório do hello script tooconfigure Olá</span><span class="sxs-lookup"><span data-stu-id="4508d-241">Use hello script tooconfigure hello report server</span></span>
* <span data-ttu-id="4508d-242">Olá tooConfigure Use o Gerenciador de configuração do servidor de relatório.</span><span class="sxs-lookup"><span data-stu-id="4508d-242">Use Configuration Manager tooConfigure hello Report Server.</span></span>

<span data-ttu-id="4508d-243">Para obter etapas mais detalhadas, consulte a seção de saudação [toohello conectar máquina Virtual e iniciar Olá Reporting Services Configuration Manager](virtual-machines-windows-classic-ps-sql-bi.md#connect-to-the-virtual-machine-and-start-the-reporting-services-configuration-manager).</span><span class="sxs-lookup"><span data-stu-id="4508d-243">For more detailed steps, see hello section [Connect toohello Virtual Machine and Start hello Reporting Services Configuration Manager](virtual-machines-windows-classic-ps-sql-bi.md#connect-to-the-virtual-machine-and-start-the-reporting-services-configuration-manager).</span></span>

<span data-ttu-id="4508d-244">**Observação de autenticação:** a autenticação do Windows é hello método de autenticação recomendado e é autenticação do saudação padrão do Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="4508d-244">**Authentication Note:** Windows authentication is hello recommended authentication method and it is hello default Reporting Services authentication.</span></span> <span data-ttu-id="4508d-245">Somente os usuários que estão configurados em Olá VM podem acessar o Reporting Services e atribuído tooReporting funções dos serviços.</span><span class="sxs-lookup"><span data-stu-id="4508d-245">Only users that are configured on hello VM can access Reporting Services and assigned tooReporting Services roles.</span></span>

### <a name="use-script-tooconfigure-hello-report-server-and-http"></a><span data-ttu-id="4508d-246">Usar servidor de relatório do script tooconfigure hello e HTTP</span><span class="sxs-lookup"><span data-stu-id="4508d-246">Use script tooconfigure hello report server and HTTP</span></span>
<span data-ttu-id="4508d-247">toouse saudação do Windows PowerShell script tooconfigure Olá servidor de relatório, Olá concluir as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="4508d-247">toouse hello Windows PowerShell script tooconfigure hello report server, complete hello following steps.</span></span> <span data-ttu-id="4508d-248">configuração de saudação inclui HTTP, HTTPS não:</span><span class="sxs-lookup"><span data-stu-id="4508d-248">hello configuration includes HTTP, not HTTPS:</span></span>

1. <span data-ttu-id="4508d-249">Olá portal clássico do Azure, selecione Olá VM e clique em conectar.</span><span class="sxs-lookup"><span data-stu-id="4508d-249">From hello Azure classic portal, select hello VM and click connect.</span></span> <span data-ttu-id="4508d-250">Dependendo da configuração do navegador, talvez seja solicitado toosave um arquivo. rdp para conexão toohello VM.</span><span class="sxs-lookup"><span data-stu-id="4508d-250">Depending on your browser configuration, you may be prompted toosave an .rdp file for connecting toohello VM.</span></span>
   
    ![Conecte-se a máquina virtual de tooazure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="4508d-252">Use o nome da VM Olá usuário, nome de usuário e senha configurados quando você criou Olá VM.</span><span class="sxs-lookup"><span data-stu-id="4508d-252">Use hello user VM name, user name and password you configured when you created hello VM.</span></span> 
   
    <span data-ttu-id="4508d-253">Por exemplo, Olá a imagem a seguir, Olá VM nome é **ssrsnativecloud** e nome de usuário Olá **testuser**.</span><span class="sxs-lookup"><span data-stu-id="4508d-253">For example, in hello following image, hello VM name is **ssrsnativecloud** and hello user name is **testuser**.</span></span>
   
    ![o logon inclui o nome da vm](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. <span data-ttu-id="4508d-255">No hello VM, abra **o Windows PowerShell ISE** com privilégios administrativos.</span><span class="sxs-lookup"><span data-stu-id="4508d-255">On hello VM, open **Windows PowerShell ISE** with administrative privileges.</span></span> <span data-ttu-id="4508d-256">Olá PowerShell ISE é instalado por padrão no Windows server 2012.</span><span class="sxs-lookup"><span data-stu-id="4508d-256">hello PowerShell ISE is installed by default on Windows server 2012.</span></span> <span data-ttu-id="4508d-257">É recomendável que usar Olá ISE em vez de uma janela padrão do Windows PowerShell para que colar o script hello em Olá ISE, modificar o script hello e, em seguida, execute o script hello.</span><span class="sxs-lookup"><span data-stu-id="4508d-257">It is recommended you use hello ISE instead of a standard Windows PowerShell window so that you can paste hello script into hello ISE, modify hello script, and then run hello script.</span></span>
3. <span data-ttu-id="4508d-258">No ISE do Windows PowerShell, clique em Olá **exibição** menu e clique **Mostrar painel de Script**.</span><span class="sxs-lookup"><span data-stu-id="4508d-258">In Windows PowerShell ISE, click hello **View** menu and then click **Show Script Pane**.</span></span>
4. <span data-ttu-id="4508d-259">Copiar Olá script a seguir e, em seguida, cole o script hello no painel de script do Windows PowerShell ISE hello.</span><span class="sxs-lookup"><span data-stu-id="4508d-259">Copy hello following script, and paste hello script into hello Windows PowerShell ISE script pane.</span></span>
   
        ## This script configures a Native mode report server without HTTPS
        $ErrorActionPreference = "Stop"
   
        $server = $env:COMPUTERNAME
        $HTTPport = 80 # change hello value if you used a different port for hello private HTTP endpoint when hello VM was created.
   
        ## Set PowerShell execution policy toobe able toorun scripts
        Set-ExecutionPolicy RemoteSigned -Force
   
        ## Utility method for verifying an operation's result
        function CheckResult
        {
            param($wmi_result, $actionname)
            if ($wmi_result.HRESULT -ne 0) {
                write-error "$actionname failed. Error from WMI: $($wmi_result.Error)"
            }
        }
   
        $starttime=Get-Date
        write-host -foregroundcolor DarkGray $starttime StartTime
   
        ## ReportServer Database name - this can be changed if needed
        $dbName='ReportServer'
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change hello version portion of hello path too"v11" toouse hello script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Report Server Configuration Steps
   
        ## Setting hello web service URL ##
        write-host -foregroundcolor green "Setting hello web service URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for ReportServer site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportServerWebService','ReportServer',1033)
            CheckResult $r "SetVirtualDirectory for ReportServer"
   
        ## ReserveURL for ReportServerWebService - port $HTTPport (for local usage)
            write-host "Calling ReserveURL port $HTTPport"
            $r = $RSObject.ReserveURL('ReportServerWebService',"http://+:$HTTPport",1033)
            CheckResult $r "ReserveURL for ReportServer port $HTTPport" 
   
        ## Setting hello Database ##
        write-host -foregroundcolor green "Setting hello Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating hello database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script toocreate hello database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS              ## this automatically changes toosqlserver provider
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## GenerateGrantRightsScript 
            $DBUser = "NT Service\ReportServer"
            write-host "Calling GenerateDatabaseRightsScript with user $DBUser"
            $r = $RSObject.GenerateDatabaseRightsScript($DBUser,$dbName,$false,$true)
            CheckResult $r "GenerateDatabaseRightsScript"
            $script = $r.Script
   
        ## Execute grant rights script
            write-host 'Executing Database Rights Script'
            $savedcvd = Get-Location
            cd sqlserver:\
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## SetDBConnection - uses Windows Service (type 2), username is ignored
            write-host "Calling SetDatabaseConnection server $server, DB $dbName"
            $r = $RSObject.SetDatabaseConnection($server,$dbName,2,'','')
            CheckResult $r "SetDatabaseConnection"  
   
        ## Setting hello Report Manager URL ##
   
        write-host -foregroundcolor green "Setting hello Report Manager URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for Reports (Report Manager) site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportManager','Reports',1033)
            CheckResult $r "SetVirtualDirectory"
   
        ## ReserveURL for ReportManager  - port $HTTPport
            write-host "Calling ReserveURL for ReportManager, port $HTTPport"
            $r = $RSObject.ReserveURL('ReportManager',"http://+:$HTTPport",1033)
            CheckResult $r "ReserveURL for ReportManager port $HTTPport"
   
        write-host -foregroundcolor green "Open Firewall port for $HTTPport"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## Open Firewall port for $HTTPport
            New-NetFirewallRule -DisplayName “Report Server (TCP on port $HTTPport)” -Direction Inbound –Protocol TCP –LocalPort $HTTPport
            write-host "Added rule Report Server (TCP on port $HTTPport) in Windows Firewall"
   
        write-host 'Operations completed, Report Server is ready'
        write-host -foregroundcolor DarkGray $starttime StartTime
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
5. <span data-ttu-id="4508d-260">Se você criou Olá VM com uma porta HTTP diferente de 80, modifique o parâmetro hello $HTTPport = 80.</span><span class="sxs-lookup"><span data-stu-id="4508d-260">If you created hello VM with an HTTP port other than 80, modify hello parameter $HTTPport = 80.</span></span>
6. <span data-ttu-id="4508d-261">script Hello está configurado atualmente para o Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="4508d-261">hello script is currently configured for  Reporting Services.</span></span> <span data-ttu-id="4508d-262">Se você quiser toorun script de saudação do Reporting Services, modificar a parte de saudação caminho toohello namespace versão Olá muito "v11" na instrução Olá Get-WmiObject.</span><span class="sxs-lookup"><span data-stu-id="4508d-262">If you want toorun hello script for  Reporting Services, modify hello version portion of hello path toohello namespace too“v11”, on hello Get-WmiObject statement.</span></span>
7. <span data-ttu-id="4508d-263">Execute o script hello.</span><span class="sxs-lookup"><span data-stu-id="4508d-263">Run hello script.</span></span>

<span data-ttu-id="4508d-264">**Validação**: tooverify funcionalidade de servidor de relatório básico hello está funcionando, consulte Olá [Verificar configuração de saudação](#verify-the-configuration) seção mais adiante neste tópico.</span><span class="sxs-lookup"><span data-stu-id="4508d-264">**Validation**: tooverify that hello basic report server functionality is working, see hello [Verify hello configuration](#verify-the-configuration) section later in this topic.</span></span>

### <a name="use-script-tooconfigure-hello-report-server-and-https"></a><span data-ttu-id="4508d-265">Usar o servidor de relatório do script tooconfigure hello e HTTPS</span><span class="sxs-lookup"><span data-stu-id="4508d-265">Use script tooconfigure hello report server and HTTPS</span></span>
<span data-ttu-id="4508d-266">toouse do Windows PowerShell tooconfigure Olá servidor de relatório, Olá concluir as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="4508d-266">toouse Windows PowerShell tooconfigure hello report server, complete hello following steps.</span></span> <span data-ttu-id="4508d-267">configuração de saudação inclui HTTPS, não HTTP.</span><span class="sxs-lookup"><span data-stu-id="4508d-267">hello configuration includes HTTPS, not HTTP.</span></span>

1. <span data-ttu-id="4508d-268">Olá portal clássico do Azure, selecione Olá VM e clique em conectar.</span><span class="sxs-lookup"><span data-stu-id="4508d-268">From hello Azure classic portal, select hello VM and click connect.</span></span> <span data-ttu-id="4508d-269">Dependendo da configuração do navegador, talvez seja solicitado toosave um arquivo. rdp para conexão toohello VM.</span><span class="sxs-lookup"><span data-stu-id="4508d-269">Depending on your browser configuration, you may be prompted toosave an .rdp file for connecting toohello VM.</span></span>
   
    ![Conecte-se a máquina virtual de tooazure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="4508d-271">Use o nome da VM Olá usuário, nome de usuário e senha configurados quando você criou Olá VM.</span><span class="sxs-lookup"><span data-stu-id="4508d-271">Use hello user VM name, user name and password you configured when you created hello VM.</span></span> 
   
    <span data-ttu-id="4508d-272">Por exemplo, Olá a imagem a seguir, Olá VM nome é **ssrsnativecloud** e nome de usuário Olá **testuser**.</span><span class="sxs-lookup"><span data-stu-id="4508d-272">For example, in hello following image, hello VM name is **ssrsnativecloud** and hello user name is **testuser**.</span></span>
   
    ![o logon inclui o nome da vm](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. <span data-ttu-id="4508d-274">No hello VM, abra **o Windows PowerShell ISE** com privilégios administrativos.</span><span class="sxs-lookup"><span data-stu-id="4508d-274">On hello VM, open **Windows PowerShell ISE** with administrative privileges.</span></span> <span data-ttu-id="4508d-275">Olá PowerShell ISE é instalado por padrão no Windows server 2012.</span><span class="sxs-lookup"><span data-stu-id="4508d-275">hello PowerShell ISE is installed by default on Windows server 2012.</span></span> <span data-ttu-id="4508d-276">É recomendável que usar Olá ISE em vez de uma janela padrão do Windows PowerShell para que colar o script hello em Olá ISE, modificar o script hello e, em seguida, execute o script hello.</span><span class="sxs-lookup"><span data-stu-id="4508d-276">It is recommended you use hello ISE instead of a standard Windows PowerShell window so that you can paste hello script into hello ISE, modify hello script, and then run hello script.</span></span>
3. <span data-ttu-id="4508d-277">tooenable a execução de scripts, executados Olá comando do Windows PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="4508d-277">tooenable running scripts, run hello following Windows PowerShell command:</span></span>
   
        Set-ExecutionPolicy RemoteSigned
   
    <span data-ttu-id="4508d-278">Você pode executar Olá política de saudação tooverify a seguir:</span><span class="sxs-lookup"><span data-stu-id="4508d-278">You can then run hello following tooverify hello policy:</span></span>
   
        Get-ExecutionPolicy
4. <span data-ttu-id="4508d-279">Em **o Windows PowerShell ISE**, clique em Olá **exibição** menu e clique **Mostrar painel de Script**.</span><span class="sxs-lookup"><span data-stu-id="4508d-279">In **Windows PowerShell ISE**, click hello **View** menu and then click **Show Script Pane**.</span></span>
5. <span data-ttu-id="4508d-280">Copie Olá seguinte script e cole-o no painel de script do Windows PowerShell ISE hello.</span><span class="sxs-lookup"><span data-stu-id="4508d-280">Copy hello following script and paste it into hello Windows PowerShell ISE script pane.</span></span>
   
        ## This script configures hello report server, including HTTPS
        $ErrorActionPreference = "Stop"
        $httpsport=443 # modify if you used a different port number when hello HTTPS endpoint was created.
   
        # You can run hello following command tooget (.cloudapp.net certificates) so you can copy hello thumbprint / certificate hash
        #dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
        #
        # hello certifacte hash is a REQUIRED parameter
        $certificatehash="" 
        # hello certificate hash should not contain spaces
   
        if ($certificatehash.Length -lt 1) 
        {
            write-error "certificatehash is a required parameter"
        } 
        # Certificates should be all lower case
        $certificatehash=$certificatehash.ToLower()
        $server = $env:COMPUTERNAME
        # If hello certificate is not a wildcard certificate, comment out hello following line, and enable hello full $DNSNAme reference.
        $DNSName="+"
        #$DNSName="$server.cloudapp.net"
        $DNSNameAndPort = $DNSName + ":$httpsport"
   
        ## Utility method for verifying an operation's result
        function CheckResult
        {
            param($wmi_result, $actionname)
            if ($wmi_result.HRESULT -ne 0) {
                write-error "$actionname failed. Error from WMI: $($wmi_result.Error)"
            }
        }
   
        $starttime=Get-Date
        write-host -foregroundcolor DarkGray $starttime StartTime
   
        ## ReportServer Database name - this can be changed if needed
        $dbName='ReportServer'
   
        write-host "hello script will use $DNSNameAndPort as hello DNS name and port" 
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change hello version portion of hello path too"v11" toouse hello script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Reporting Services Report Server Configuration Steps
   
        ## 1. Setting hello web service URL ##
        write-host -foregroundcolor green "Setting hello web service URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for ReportServer site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportServerWebService','ReportServer',1033)
            CheckResult $r "SetVirtualDirectory for ReportServer"
   
        ## ReserveURL for ReportServerWebService - port 80 (for local usage)
            write-host 'Calling ReserveURL port 80'
            $r = $RSObject.ReserveURL('ReportServerWebService','http://+:80',1033)
            CheckResult $r "ReserveURL for ReportServer port 80" 
   
        ## ReserveURL for ReportServerWebService - port $httpsport
            write-host "Calling ReserveURL port $httpsport, for URL: https://$DNSNameAndPort"
            $r = $RSObject.ReserveURL('ReportServerWebService',"https://$DNSNameAndPort",1033)
            CheckResult $r "ReserveURL for ReportServer port $httpsport" 
   
        ## CreateSSLCertificateBinding for ReportServerWebService port $httpsport
            write-host "Calling CreateSSLCertificateBinding port $httpsport, with certificate hash: $certificatehash"
            $r = $RSObject.CreateSSLCertificateBinding('ReportServerWebService',$certificatehash,'0.0.0.0',$httpsport,1033)
            CheckResult $r "CreateSSLCertificateBinding for ReportServer port $httpsport" 
   
        ## 2. Setting hello Database ##
        write-host -foregroundcolor green "Setting hello Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating hello database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script toocreate hello database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS                    ## this automatically changes toosqlserver provider
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## GenerateGrantRightsScript 
            $DBUser = "NT Service\ReportServer"
            write-host "Calling GenerateDatabaseRightsScript with user $DBUser"
            $r = $RSObject.GenerateDatabaseRightsScript($DBUser,$dbName,$false,$true)
            CheckResult $r "GenerateDatabaseRightsScript"
            $script = $r.Script
   
        ## Execute grant rights script
            write-host 'Executing Database Rights Script'
            $savedcvd = Get-Location
            cd sqlserver:\
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## SetDBConnection - uses Windows Service (type 2), username is ignored
            write-host "Calling SetDatabaseConnection server $server, DB $dbName"
            $r = $RSObject.SetDatabaseConnection($server,$dbName,2,'','')
            CheckResult $r "SetDatabaseConnection"  
   
        ## 3. Setting hello Report Manager URL ##
   
        write-host -foregroundcolor green "Setting hello Report Manager URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for Reports (Report Manager) site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportManager','Reports',1033)
            CheckResult $r "SetVirtualDirectory"
   
        ## ReserveURL for ReportManager  - port 80
            write-host 'Calling ReserveURL for ReportManager, port 80'
            $r = $RSObject.ReserveURL('ReportManager','http://+:80',1033)
            CheckResult $r "ReserveURL for ReportManager port 80"
   
        ## ReserveURL for ReportManager - port $httpsport
            write-host "Calling ReserveURL port $httpsport, for URL: https://$DNSNameAndPort"
            $r = $RSObject.ReserveURL('ReportManager',"https://$DNSNameAndPort",1033)
            CheckResult $r "ReserveURL for ReportManager port $httpsport" 
   
        ## CreateSSLCertificateBinding for ReportManager port $httpsport
            write-host "Calling CreateSSLCertificateBinding port $httpsport with certificate hash: $certificatehash"
            $r = $RSObject.CreateSSLCertificateBinding('ReportManager',$certificatehash,'0.0.0.0',$httpsport,1033)
            CheckResult $r "CreateSSLCertificateBinding for ReportManager port $httpsport" 
   
        write-host -foregroundcolor green "Open Firewall port for $httpsport"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## Open Firewall port for $httpsport
            New-NetFirewallRule -DisplayName “Report Server (TCP on port $httpsport)” -Direction Inbound –Protocol TCP –LocalPort $httpsport
            write-host "Added rule Report Server (TCP on port $httpsport) in Windows Firewall"
   
        write-host 'Operations completed, Report Server is ready'
        write-host -foregroundcolor DarkGray $starttime StartTime
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
6. <span data-ttu-id="4508d-281">Modificar Olá **$certificatehash** parâmetro no script hello:</span><span class="sxs-lookup"><span data-stu-id="4508d-281">Modify hello **$certificatehash** parameter in hello script:</span></span>
   
   * <span data-ttu-id="4508d-282">Esse é um parâmetro **obrigatório** .</span><span class="sxs-lookup"><span data-stu-id="4508d-282">This is a **required** parameter.</span></span> <span data-ttu-id="4508d-283">Se você não salvar o valor de saudação do certificado de etapas anteriores Olá, use um dos Olá após o valor de hash de certificado do métodos toocopy Olá da impressão digital de certificados hello.:</span><span class="sxs-lookup"><span data-stu-id="4508d-283">If you did not save hello certificate value from hello previous steps, use one of hello following methods toocopy hello certificate hash value from hello certificates thumbprint.:</span></span>
     
       <span data-ttu-id="4508d-284">No hello VM, abra o Windows PowerShell ISE e execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="4508d-284">On hello VM, open Windows PowerShell ISE and run hello following command:</span></span>
     
           dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
     
       <span data-ttu-id="4508d-285">saída de Hello procurará a seguir toohello semelhante.</span><span class="sxs-lookup"><span data-stu-id="4508d-285">hello output will look similar toohello following.</span></span> <span data-ttu-id="4508d-286">Se o script hello retorna uma linha em branco, Olá VM não tem um certificado configurado por exemplo, consulte a seção Olá [toouse Olá certificado autoassinado de máquinas virtuais](#to-use-the-virtual-machines-self-signed-certificate).</span><span class="sxs-lookup"><span data-stu-id="4508d-286">If hello script returns a blank line, hello VM does not have a certificate configured for example, see hello section [toouse hello Virtual Machines Self-signed Certificate](#to-use-the-virtual-machines-self-signed-certificate).</span></span>
     
     <span data-ttu-id="4508d-287">OU</span><span class="sxs-lookup"><span data-stu-id="4508d-287">OR</span></span>
   * <span data-ttu-id="4508d-288">Em Olá VM executar mmc.exe e adicione Olá **certificados** snap-in.</span><span class="sxs-lookup"><span data-stu-id="4508d-288">On hello VM Run mmc.exe and then add hello **Certificates** snap-in.</span></span>
   * <span data-ttu-id="4508d-289">Em Olá **autoridades de certificação raiz confiáveis** nó clique duas vezes em seu nome de certificado.</span><span class="sxs-lookup"><span data-stu-id="4508d-289">Under hello **Trusted Root Certificate Authorities** node double-click your certificate name.</span></span> <span data-ttu-id="4508d-290">Se você estiver usando um certificado autoassinado de saudação do hello VM, o certificado de saudação é nomeado após o nome DNS de saudação do hello VM e termina com **cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="4508d-290">If you are using hello self-signed certificate of hello VM, hello certificate is named after hello DNS name of hello VM and ends with **cloudapp.net**.</span></span>
   * <span data-ttu-id="4508d-291">Clique em Olá **detalhes** guia.</span><span class="sxs-lookup"><span data-stu-id="4508d-291">Click hello **Details** tab.</span></span>
   * <span data-ttu-id="4508d-292">Clique em **Impressão digital**.</span><span class="sxs-lookup"><span data-stu-id="4508d-292">Click **Thumbprint**.</span></span> <span data-ttu-id="4508d-293">valor de saudação da impressão digital de saudação é exibido no campo de detalhes hello, por exemplo af 11 60 b6 4b 28 8 d 89 0a 82 12 ff 6b a9 4f 66 c3 31 90 48</span><span class="sxs-lookup"><span data-stu-id="4508d-293">hello value of hello thumbprint is displayed in hello details field, for example af 11 60 b6 4b 28 8d 89 0a 82 12 ff 6b a9 c3 66 4f 31 90 48</span></span>
   * <span data-ttu-id="4508d-294">**Antes de executar o script hello**, remova os espaços de saudação entre Olá pares de valores.</span><span class="sxs-lookup"><span data-stu-id="4508d-294">**Before you run hello script**, remove hello spaces in between hello pairs of values.</span></span> <span data-ttu-id="4508d-295">Por exemplo, af1160b64b288d890a8212ff6ba9c3664f319048</span><span class="sxs-lookup"><span data-stu-id="4508d-295">For example af1160b64b288d890a8212ff6ba9c3664f319048</span></span>
7. <span data-ttu-id="4508d-296">Modificar Olá **$httpsport** parâmetro:</span><span class="sxs-lookup"><span data-stu-id="4508d-296">Modify hello **$httpsport** parameter:</span></span> 
   
   * <span data-ttu-id="4508d-297">Se você usou a porta 443 para o ponto de extremidade HTTPS hello, em seguida, você não é necessário tooupdate esse parâmetro no script hello.</span><span class="sxs-lookup"><span data-stu-id="4508d-297">If you used port 443 for hello HTTPS endpoint, then you do not need tooupdate this parameter in hello script.</span></span> <span data-ttu-id="4508d-298">Caso contrário, use o valor da porta Olá selecionado quando você configurou o ponto de extremidade privado de HTTPS de saudação em Olá VM.</span><span class="sxs-lookup"><span data-stu-id="4508d-298">Otherwise use hello port value you selected when you configured hello HTTPS private endpoint on hello VM.</span></span>
8. <span data-ttu-id="4508d-299">Modificar Olá **$DNSName** parâmetro:</span><span class="sxs-lookup"><span data-stu-id="4508d-299">Modify hello **$DNSName** parameter:</span></span> 
   
   * <span data-ttu-id="4508d-300">Olá script está configurado para um certificado curinga $DNSName = "+".</span><span class="sxs-lookup"><span data-stu-id="4508d-300">hello script is configured for a wild card certificate $DNSName="+".</span></span> <span data-ttu-id="4508d-301">Se você não fizer nenhuma tooconfigure desejados para uma associação de certificado curinga, comente $DNSName = "+"e habilitar Olá após a linha, referência de $DNSNAme completo hello, $DNSName="$server.cloudapp.net # #".</span><span class="sxs-lookup"><span data-stu-id="4508d-301">If you do no want tooconfigure for a wildcard certificate binding, comment out $DNSName="+" and enable hello following line, hello full $DNSNAme reference, ##$DNSName="$server.cloudapp.net".</span></span>
     
       <span data-ttu-id="4508d-302">Altere o valor de saudação $DNSName se você não quiser que o nome DNS de toouse Olá máquina virtual do Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="4508d-302">Change hello $DNSName value if you do not want toouse hello virtual machine’s DNS name for Reporting Services.</span></span> <span data-ttu-id="4508d-303">Se você usar o parâmetro hello, certificado Olá também deve usar esse nome e registrar Olá nome globalmente em um servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="4508d-303">If you use hello parameter, hello certificate must also use this name and you register hello name globally on a DNS server.</span></span>
9. <span data-ttu-id="4508d-304">script Hello está configurado atualmente para o Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="4508d-304">hello script is currently configured for  Reporting Services.</span></span> <span data-ttu-id="4508d-305">Se você quiser toorun script de saudação do Reporting Services, modificar a parte de saudação caminho toohello namespace versão Olá muito "v11" na instrução Olá Get-WmiObject.</span><span class="sxs-lookup"><span data-stu-id="4508d-305">If you want toorun hello script for  Reporting Services, modify hello version portion of hello path toohello namespace too“v11”, on hello Get-WmiObject statement.</span></span>
10. <span data-ttu-id="4508d-306">Execute o script hello.</span><span class="sxs-lookup"><span data-stu-id="4508d-306">Run hello script.</span></span>

<span data-ttu-id="4508d-307">**Validação**: tooverify funcionalidade de servidor de relatório básico hello está funcionando, consulte Olá [Verificar configuração de saudação](#verify-the-connection) seção mais adiante neste tópico.</span><span class="sxs-lookup"><span data-stu-id="4508d-307">**Validation**: tooverify that hello basic report server functionality is working, see hello [Verify hello configuration](#verify-the-connection) section later in this topic.</span></span> <span data-ttu-id="4508d-308">associação de certificado Olá tooverify abra um prompt de comando com privilégios administrativos e execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="4508d-308">tooverify hello certificate binding open a command prompt with administrative privileges, and then run hello following command:</span></span>

    netsh http show sslcert

<span data-ttu-id="4508d-309">resultado de saudação incluirá o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="4508d-309">hello result will include hello following:</span></span>

    IP:port                      : 0.0.0.0:443

    Certificate Hash             : f98adf786994c1e4a153f53fe20f94210267d0e7

### <a name="use-configuration-manager-tooconfigure-hello-report-server"></a><span data-ttu-id="4508d-310">Olá tooConfigure Use o Gerenciador de configuração do servidor de relatório</span><span class="sxs-lookup"><span data-stu-id="4508d-310">Use Configuration Manager tooConfigure hello Report Server</span></span>
<span data-ttu-id="4508d-311">Se você não quiser que servidor de relatório toorun Olá PowerShell script tooconfigure hello, siga as etapas de saudação essa seção toouse Olá Reporting Services modo nativo configuration manager tooconfigure Olá servidor de relatório.</span><span class="sxs-lookup"><span data-stu-id="4508d-311">If you do not want toorun hello PowerShell script tooconfigure hello report server, follow hello steps in this section toouse hello Reporting Services native mode configuration manager tooconfigure hello report server.</span></span>

1. <span data-ttu-id="4508d-312">Olá portal clássico do Azure, selecione Olá VM e clique em conectar.</span><span class="sxs-lookup"><span data-stu-id="4508d-312">From hello Azure classic portal, select hello VM and click connect.</span></span> <span data-ttu-id="4508d-313">Use o nome de usuário hello e senha configurados quando você criou Olá VM.</span><span class="sxs-lookup"><span data-stu-id="4508d-313">Use hello user name and password you configured when you created hello VM.</span></span>
   
    ![Conecte-se a máquina virtual de tooazure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif)
2. <span data-ttu-id="4508d-315">Execute o Windows update e instalar atualizações toohello VM.</span><span class="sxs-lookup"><span data-stu-id="4508d-315">Run Windows update and install updates toohello VM.</span></span> <span data-ttu-id="4508d-316">Se for necessária uma reinicialização de saudação VM, reiniciar Olá VM e reconecte toohello VM de saudação portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="4508d-316">If a restart of hello VM is required, restart hello VM and reconnect toohello VM from hello Azure classic portal.</span></span>
3. <span data-ttu-id="4508d-317">Saudação do menu de início em Olá VM, digite **Reporting Services** e abra **Reporting Services Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="4508d-317">From hello Start menu on hello VM, type **Reporting Services** and open **Reporting Services Configuration Manager**.</span></span>
4. <span data-ttu-id="4508d-318">Deixe valores padrão de saudação para **nome do servidor** e **instância de servidor de relatório**.</span><span class="sxs-lookup"><span data-stu-id="4508d-318">Leave hello default values for **Server Name** and **Report Server Instance**.</span></span> <span data-ttu-id="4508d-319">Clique em **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="4508d-319">Click **Connect**.</span></span>
5. <span data-ttu-id="4508d-320">No painel esquerdo do hello, clique em **URL do serviço Web**.</span><span class="sxs-lookup"><span data-stu-id="4508d-320">In hello left pane, click **Web Service URL**.</span></span>
6. <span data-ttu-id="4508d-321">Por padrão, o RS está configurado para a porta HTTP 80 com IP "Todos Atribuídos".</span><span class="sxs-lookup"><span data-stu-id="4508d-321">By default, RS is configured for HTTP port 80 with IP “All Assigned”.</span></span> <span data-ttu-id="4508d-322">tooadd HTTPS:</span><span class="sxs-lookup"><span data-stu-id="4508d-322">tooadd HTTPS:</span></span>
   
   1. <span data-ttu-id="4508d-323">Em **certificado SSL**: Olá selecione certificado toouse, por exemplo, [nome da VM]. cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="4508d-323">In **SSL Certificate**: select hello certificate you want toouse, for example [VM name].cloudapp.net.</span></span> <span data-ttu-id="4508d-324">Se nenhum certificado estiver listado, consulte a seção de saudação **etapa 2: criar um certificado de servidor** para obter informações sobre como tooinstall e confiança Olá certificado Olá VM.</span><span class="sxs-lookup"><span data-stu-id="4508d-324">If no certificates are listed, see hello section **Step 2: Create a Server Certificate** for information on how tooinstall and trust hello certificate on hello VM.</span></span>
   2. <span data-ttu-id="4508d-325">Em **Porta SSL**: escolha 443.</span><span class="sxs-lookup"><span data-stu-id="4508d-325">Under **SSL Port**: choose 443.</span></span> <span data-ttu-id="4508d-326">Se você configurou o ponto de extremidade privado de HTTPS de saudação em Olá VM com uma porta particular diferente, use esse valor aqui.</span><span class="sxs-lookup"><span data-stu-id="4508d-326">If you configured hello HTTPS private endpoint in hello VM with a different private port, use that value here.</span></span>
   3. <span data-ttu-id="4508d-327">Clique em **aplicar** e aguarde Olá operação toocomplete.</span><span class="sxs-lookup"><span data-stu-id="4508d-327">Click **Apply** and wait for hello operation toocomplete.</span></span>
7. <span data-ttu-id="4508d-328">No painel esquerdo do hello, clique em **banco de dados**.</span><span class="sxs-lookup"><span data-stu-id="4508d-328">In hello left pane, click **Database**.</span></span>
   
   1. <span data-ttu-id="4508d-329">Clique em **Alterar Banco de Dado**s.</span><span class="sxs-lookup"><span data-stu-id="4508d-329">Click **Change Databas**e.</span></span>
   2. <span data-ttu-id="4508d-330">Clique em **Criar um novo banco de dados do servidor de relatório** e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="4508d-330">Click **Create a new report server database** and then click **Next**.</span></span>
   3. <span data-ttu-id="4508d-331">Deixe o padrão de saudação **nome do servidor**: Nomeie Olá VM e deixe o padrão de saudação **tipo de autenticação** como **usuário atual** – **asegurançaintegrada**.</span><span class="sxs-lookup"><span data-stu-id="4508d-331">Leave hello default **Server Name**: as hello VM name and leave hello default **Authentication Type** as **Current User** – **Integrated Security**.</span></span> <span data-ttu-id="4508d-332">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="4508d-332">Click **Next**.</span></span>
   4. <span data-ttu-id="4508d-333">Deixe o padrão de saudação **nome do banco de dados** como **ReportServer** e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="4508d-333">Leave hello default **Database Name** as **ReportServer** and click **Next**.</span></span>
   5. <span data-ttu-id="4508d-334">Deixe o padrão de saudação **tipo de autenticação** como **credenciais de serviço** e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="4508d-334">Leave hello default **Authentication Type** as **Service Credentials** and click **Next**.</span></span>
   6. <span data-ttu-id="4508d-335">Clique em **próximo** em Olá **resumo** página.</span><span class="sxs-lookup"><span data-stu-id="4508d-335">Click **Next** on hello **Summary** page.</span></span>
   7. <span data-ttu-id="4508d-336">Quando a configuração de saudação estiver concluída, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="4508d-336">When hello configuration is complete, click **Finish**.</span></span>
8. <span data-ttu-id="4508d-337">No painel esquerdo do hello, clique em **URL do Report Manager**.</span><span class="sxs-lookup"><span data-stu-id="4508d-337">In hello left pane, click **Report Manager URL**.</span></span> <span data-ttu-id="4508d-338">Deixe o padrão de saudação **Diretório Virtual** como **relatórios** e clique em **aplicar**.</span><span class="sxs-lookup"><span data-stu-id="4508d-338">Leave hello default **Virtual Directory** as **Reports** and click **Apply**.</span></span>
9. <span data-ttu-id="4508d-339">Clique em **Exit** tooclose Olá Reporting Services Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="4508d-339">Click **Exit** tooclose hello Reporting Services Configuration Manager.</span></span>

## <a name="step-4-open-windows-firewall-port"></a><span data-ttu-id="4508d-340">Etapa 4: abrir a porta do Firewall do Windows</span><span class="sxs-lookup"><span data-stu-id="4508d-340">Step 4: Open Windows Firewall Port</span></span>
> [!NOTE]
> <span data-ttu-id="4508d-341">Se você tiver usado um Olá scripts tooconfigure saudação do servidor de relatório, você poderá ignorar esta seção.</span><span class="sxs-lookup"><span data-stu-id="4508d-341">If you used one of hello scripts tooconfigure hello report server, you can skip this section.</span></span> <span data-ttu-id="4508d-342">script Hello incluída uma porta de firewall etapa tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="4508d-342">hello script included a step tooopen hello firewall port.</span></span> <span data-ttu-id="4508d-343">padrão de saudação era a porta 80 para HTTP e 443 para HTTPS.</span><span class="sxs-lookup"><span data-stu-id="4508d-343">hello default was port 80 for HTTP and port 443 for HTTPS.</span></span>
> 
> 

<span data-ttu-id="4508d-344">tooconnect remotamente tooReport Manager ou Olá relatório Server na máquina virtual de saudação, um ponto de extremidade TCP é necessária no hello VM.</span><span class="sxs-lookup"><span data-stu-id="4508d-344">tooconnect remotely tooReport Manager or hello Report Server on hello virtual machine, a TCP Endpoint is required on hello VM.</span></span> <span data-ttu-id="4508d-345">É necessário tooopen Olá mesma porta no firewall da VM Olá.</span><span class="sxs-lookup"><span data-stu-id="4508d-345">It is required tooopen hello same port in hello VM’s firewall.</span></span> <span data-ttu-id="4508d-346">ponto de extremidade de saudação foi criado quando Olá VM foi provisionada.</span><span class="sxs-lookup"><span data-stu-id="4508d-346">hello endpoint was created when hello VM was provisioned.</span></span>

<span data-ttu-id="4508d-347">Esta seção fornece informações básicas sobre como tooopen Olá porta do firewall.</span><span class="sxs-lookup"><span data-stu-id="4508d-347">This section provides basic information on how tooopen hello firewall port.</span></span> <span data-ttu-id="4508d-348">Para saber mais, consulte [Configurar um firewall para acesso ao servidor de relatório](https://technet.microsoft.com/library/bb934283.aspx)</span><span class="sxs-lookup"><span data-stu-id="4508d-348">For more information, see [Configure a Firewall for Report Server Access](https://technet.microsoft.com/library/bb934283.aspx)</span></span>

> [!NOTE]
> <span data-ttu-id="4508d-349">Se você usou o servidor de relatório do hello script tooconfigure hello, você poderá ignorar esta seção.</span><span class="sxs-lookup"><span data-stu-id="4508d-349">If you used hello script tooconfigure hello report server, you can skip this section.</span></span> <span data-ttu-id="4508d-350">script Hello incluída uma porta de firewall etapa tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="4508d-350">hello script included a step tooopen hello firewall port.</span></span>
> 
> 

<span data-ttu-id="4508d-351">Se você configurou uma porta privada para HTTPS diferente de 443, modifique Olá script a seguir apropriadamente.</span><span class="sxs-lookup"><span data-stu-id="4508d-351">If you configured a private port for HTTPS other than 443, modify hello following script appropriately.</span></span> <span data-ttu-id="4508d-352">porta tooopen **443** no hello Firewall do Windows, conclua o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="4508d-352">tooopen port **443** on hello Windows Firewall, complete hello following:</span></span>

1. <span data-ttu-id="4508d-353">Abra uma janela do Windows PowerShell com privilégios administrativos.</span><span class="sxs-lookup"><span data-stu-id="4508d-353">Open a Windows PowerShell window with administrative privileges.</span></span>
2. <span data-ttu-id="4508d-354">Se você usou uma porta diferente de 443 ao configurar o ponto de extremidade HTTPS de saudação em Olá VM, atualizar porta Olá Olá comando a seguir e, em seguida, execute o comando de saudação:</span><span class="sxs-lookup"><span data-stu-id="4508d-354">If you used a port other than 443 when you configured hello HTTPS endpoint on hello VM, update hello port in hello following command and then run hello command:</span></span>
   
        New-NetFirewallRule -DisplayName “Report Server (TCP on port 443)” -Direction Inbound –Protocol TCP –LocalPort 443
3. <span data-ttu-id="4508d-355">Quando o comando Olá for concluído, **Okey** é exibido no prompt de comando hello.</span><span class="sxs-lookup"><span data-stu-id="4508d-355">When hello command completes, **Ok** is displayed in hello command prompt.</span></span>

<span data-ttu-id="4508d-356">tooverify que porta Olá é aberta, abra uma janela de Windows PowerShell e a execução Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="4508d-356">tooverify that hello port is opened, open a Windows PowerShell window and run hello following command:</span></span>

    get-netfirewallrule | where {$_.displayname -like "*report*"} | select displayname,enabled,action

## <a name="verify-hello-configuration"></a><span data-ttu-id="4508d-357">Verificar a configuração de saudação</span><span class="sxs-lookup"><span data-stu-id="4508d-357">Verify hello configuration</span></span>
<span data-ttu-id="4508d-358">tooverify a funcionalidade do servidor de relatório básico hello está funcionando agora, abra seu navegador com privilégios administrativos e, em seguida, procura toohello seguinte relatório Gerenciador de relatórios do servidor ad URLS:</span><span class="sxs-lookup"><span data-stu-id="4508d-358">tooverify that hello basic report server functionality is now working, open your browser with administrative privileges and then browse toohello following report server ad report manager URLS:</span></span>

* <span data-ttu-id="4508d-359">Na VM do hello, procure toohello URL do servidor de relatório:</span><span class="sxs-lookup"><span data-stu-id="4508d-359">On hello VM, browse toohello report server URL:</span></span>
  
        http://localhost/reportserver
* <span data-ttu-id="4508d-360">Na VM do hello, procure toohello URL do Gerenciador de relatórios:</span><span class="sxs-lookup"><span data-stu-id="4508d-360">On hello VM, browse toohello report manger URL:</span></span>
  
        http://localhost/Reports
* <span data-ttu-id="4508d-361">No computador local, navegue toohello **remoto** Gerenciador de relatórios em Olá VM.</span><span class="sxs-lookup"><span data-stu-id="4508d-361">From your local computer, browse toohello **remote** report Manager on hello VM.</span></span> <span data-ttu-id="4508d-362">Atualize o nome de DNS Olá Olá seguinte exemplo conforme apropriado.</span><span class="sxs-lookup"><span data-stu-id="4508d-362">Update hello DNS name in hello following example as appropriate.</span></span> <span data-ttu-id="4508d-363">Quando for solicitada uma senha, use credenciais de administrador de saudação criado quando Olá VM foi provisionada.</span><span class="sxs-lookup"><span data-stu-id="4508d-363">When prompted for a password, use hello administrator credentials you created when hello VM was provisioned.</span></span> <span data-ttu-id="4508d-364">nome de usuário Hello está em Olá [domínio]\[nome de usuário] formato, onde o domínio de saudação é o nome do computador VM hello, por exemplo ssrsnativecloud\testuser.</span><span class="sxs-lookup"><span data-stu-id="4508d-364">hello user name is in hello [Domain]\[user name] format, where hello domain is hello VM computer name, for example ssrsnativecloud\testuser.</span></span> <span data-ttu-id="4508d-365">Se você não estiver usando HTTP**S**, remover Olá **s** na URL de saudação.</span><span class="sxs-lookup"><span data-stu-id="4508d-365">If you are not using HTTP**S**, remove hello **s** in hello URL.</span></span> <span data-ttu-id="4508d-366">Consulte a próxima seção Olá para obter informações sobre como criar usuários adicionais na VM.</span><span class="sxs-lookup"><span data-stu-id="4508d-366">See hello next section for information on creating additional users on VM.</span></span>
  
        https://ssrsnativecloud.cloudapp.net/Reports
* <span data-ttu-id="4508d-367">No computador local, procure toohello URL do servidor de relatório remoto.</span><span class="sxs-lookup"><span data-stu-id="4508d-367">From your local computer, browse toohello remote report server URL.</span></span> <span data-ttu-id="4508d-368">Atualize o nome de DNS Olá Olá seguinte exemplo conforme apropriado.</span><span class="sxs-lookup"><span data-stu-id="4508d-368">Update hello DNS name in hello following example as appropriate.</span></span> <span data-ttu-id="4508d-369">Se você não estiver usando HTTPS, remova s Olá Olá URL.</span><span class="sxs-lookup"><span data-stu-id="4508d-369">If you are not using HTTPS, remove hello s in hello URL.</span></span>
  
        https://ssrsnativecloud.cloudapp.net/ReportServer

## <a name="create-users-and-assign-roles"></a><span data-ttu-id="4508d-370">Criar usuários e atribuir funções</span><span class="sxs-lookup"><span data-stu-id="4508d-370">Create Users and Assign Roles</span></span>
<span data-ttu-id="4508d-371">Depois de configurar e verificar a saudação de servidor de relatório, uma tarefa administrativa comum é toocreate um ou mais usuários e atribuir usuários a funções de serviços tooReporting.</span><span class="sxs-lookup"><span data-stu-id="4508d-371">After configuring and verifying hello report server, a common administrative task is toocreate one or more users and assign users tooReporting Services roles.</span></span> <span data-ttu-id="4508d-372">Para obter mais informações, consulte o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="4508d-372">For more information, see hello following:</span></span>

* [<span data-ttu-id="4508d-373">Criar uma conta de usuário local</span><span class="sxs-lookup"><span data-stu-id="4508d-373">Create a local user account</span></span>](https://technet.microsoft.com/library/cc770642.aspx)
* <span data-ttu-id="4508d-374">[Conceder acesso ao usuário tooa o servidor de relatório (Gerenciador de relatórios)](https://msdn.microsoft.com/library/ms156034.aspx))</span><span class="sxs-lookup"><span data-stu-id="4508d-374">[Grant User Access tooa Report Server (Report Manager)](https://msdn.microsoft.com/library/ms156034.aspx))</span></span>
* [<span data-ttu-id="4508d-375">Criar e gerenciar atribuições de função</span><span class="sxs-lookup"><span data-stu-id="4508d-375">Create and Manage Role Assignments</span></span>](https://msdn.microsoft.com/library/ms155843.aspx)

## <a name="toocreate-and-publish-reports-toohello-azure-virtual-machine"></a><span data-ttu-id="4508d-376">tooCreate e publicar relatórios toohello Máquina Virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="4508d-376">tooCreate and Publish Reports toohello Azure Virtual Machine</span></span>
<span data-ttu-id="4508d-377">Olá tabela a seguir resume alguns dos relatórios existentes do hello opções toopublish disponíveis de um servidor de relatório local computador toohello hospedado em Olá Máquina Virtual do Microsoft Azure:</span><span class="sxs-lookup"><span data-stu-id="4508d-377">hello following table summarizes some of hello options available toopublish existing reports from an on-premises computer toohello report server hosted on hello Microsoft Azure Virtual Machine:</span></span>

* <span data-ttu-id="4508d-378">**Script RS.exe**: itens de relatório Use RS.exe script toocopy do e tooyour de servidor de relatório existente Máquina Virtual do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="4508d-378">**RS.exe script**: Use RS.exe script toocopy report items from and existing report server tooyour Microsoft Azure Virtual Machine.</span></span> <span data-ttu-id="4508d-379">Para obter mais informações, consulte a seção de hello "tooNative de modo nativo – modo de máquina Virtual do Microsoft Azure" em [Sample Reporting Services rs.exe Script tooMigrate conteúdo entre servidores de relatório](https://msdn.microsoft.com/library/dn531017.aspx).</span><span class="sxs-lookup"><span data-stu-id="4508d-379">For more information, see hello section “Native mode tooNative Mode – Microsoft Azure Virtual Machine” in [Sample Reporting Services rs.exe Script tooMigrate Content between Report Servers](https://msdn.microsoft.com/library/dn531017.aspx).</span></span>
* <span data-ttu-id="4508d-380">**Construtor de relatórios**: máquina virtual de saudação inclui Olá clique-uma vez a versão do construtor de relatórios do Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4508d-380">**Report Builder**: hello virtual machine includes hello click-once version of Microsoft SQL Server Report Builder.</span></span> <span data-ttu-id="4508d-381">saudação de construtor relatório toostart primeira vez na máquina virtual de saudação:</span><span class="sxs-lookup"><span data-stu-id="4508d-381">toostart Report builder hello first time on hello virtual machine:</span></span>
  
  1. <span data-ttu-id="4508d-382">Inicie o navegador com privilégios administrativos.</span><span class="sxs-lookup"><span data-stu-id="4508d-382">Start your browser with administrative privileges.</span></span>
  2. <span data-ttu-id="4508d-383">Procurar tooreport manager na máquina virtual de saudação e clique em **Report Builder** na faixa de opções de saudação.</span><span class="sxs-lookup"><span data-stu-id="4508d-383">Browse tooreport manager on hello virtual machine and click **Report Builder**  in hello ribbon.</span></span>
     
     <span data-ttu-id="4508d-384">Para saber mais, consulte [Instalando, Desinstalando e Dando Suporte ao Construtor de Relatórios](https://technet.microsoft.com/library/dd207038.aspx).</span><span class="sxs-lookup"><span data-stu-id="4508d-384">For more information, see [Installing, Uninstalling, and Supporting Report Builder](https://technet.microsoft.com/library/dd207038.aspx).</span></span>
* <span data-ttu-id="4508d-385">**SQL Server Data Tools: VM**: se você criou Olá VM com o SQL Server 2012, SQL Server Data Tools está instalado na máquina virtual de saudação e pode ser usado toocreate **projetos do servidor de relatório** e relatórios sobre Olá virtual máquina.</span><span class="sxs-lookup"><span data-stu-id="4508d-385">**SQL Server Data Tools: VM**:  If you created hello VM with SQL Server 2012, then SQL Server Data Tools is installed on hello virtual machine and can be used toocreate **Report Server Projects** and reports on hello virtual machine.</span></span> <span data-ttu-id="4508d-386">SQL Server Data Tools pode publicar o servidor de relatório de toohello Olá relatórios na máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="4508d-386">SQL Server Data Tools can publish hello reports toohello report server on hello virtual machine.</span></span>
  
    <span data-ttu-id="4508d-387">Se você criou Olá VM com o SQL server 2014, você pode instalar o SQL Server Data Tools - BI para visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4508d-387">If you created hello VM with SQL server 2014, you can install SQL Server Data Tools- BI for visual Studio.</span></span> <span data-ttu-id="4508d-388">Para obter mais informações, consulte o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="4508d-388">For more information, see hello following:</span></span>
  
  * [<span data-ttu-id="4508d-389">Microsoft SQL Server Data Tools - Business Intelligence para Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="4508d-389">Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2013</span></span>](https://www.microsoft.com/download/details.aspx?id=42313)
  * [<span data-ttu-id="4508d-390">Microsoft SQL Server Data Tools - Business Intelligence para Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="4508d-390">Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2012</span></span>](https://www.microsoft.com/download/details.aspx?id=36843)
  * [<span data-ttu-id="4508d-391">SQL Server Data Tools e SQL Server Business Intelligence (SSDT-BI)</span><span class="sxs-lookup"><span data-stu-id="4508d-391">SQL Server Data Tools and SQL Server Business Intelligence (SSDT-BI)</span></span>](http://curah.microsoft.com/30004/sql-server-data-tools-ssdt-and-sql-server-business-intelligence)
* <span data-ttu-id="4508d-392">**SQL Server Data Tools: Remoto**: no computador local, crie um projeto do Reporting Services no SQL Server Data Tools que contenha os relatórios do Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="4508d-392">**SQL Server Data Tools: Remote**:  On your local computer, create a Reporting Services project in SQL Server Data Tools that contains Reporting Services reports.</span></span> <span data-ttu-id="4508d-393">Configure projeto Olá toohello tooconnect URL do serviço web.</span><span class="sxs-lookup"><span data-stu-id="4508d-393">Configure hello project tooconnect toohello web service URL.</span></span>
  
    ![propriedades de projeto ssdt para projeto SSRS](./media/virtual-machines-windows-classic-ps-sql-report/IC650114.gif)
* <span data-ttu-id="4508d-395">**Usar script**: usar o conteúdo do servidor de relatório de toocopy de script.</span><span class="sxs-lookup"><span data-stu-id="4508d-395">**Use script**: Use script toocopy report server content.</span></span> <span data-ttu-id="4508d-396">Para obter mais informações, consulte [Sample Reporting Services rs.exe Script tooMigrate conteúdo entre servidores de relatório](https://msdn.microsoft.com/library/dn531017.aspx).</span><span class="sxs-lookup"><span data-stu-id="4508d-396">For more information, see [Sample Reporting Services rs.exe Script tooMigrate Content between Report Servers](https://msdn.microsoft.com/library/dn531017.aspx).</span></span>

## <a name="minimize-cost-if-you-are-not-using-hello-vm"></a><span data-ttu-id="4508d-397">Minimizar o custo se você não estiver usando Olá VM</span><span class="sxs-lookup"><span data-stu-id="4508d-397">Minimize cost if you are not using hello VM</span></span>
> [!NOTE]
> <span data-ttu-id="4508d-398">toominimize encargos para suas máquinas virtuais do Azure quando não estiver em uso, desligue Olá VM de saudação portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="4508d-398">toominimize charges for your Azure Virtual Machines when not in use, shut down hello VM from hello Azure classic portal.</span></span> <span data-ttu-id="4508d-399">Se você usar opções de energia do Windows hello dentro de um tooshut VM para baixo Olá VM, você ainda será cobrado Olá mesmo valor para Olá VM.</span><span class="sxs-lookup"><span data-stu-id="4508d-399">If you use hello Windows power options inside a VM tooshut down hello VM, you are still charged hello same amount for hello VM.</span></span> <span data-ttu-id="4508d-400">tooreduce encargos, você precisa tooshut inativo saudação VM no portal clássico do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="4508d-400">tooreduce charges, you need tooshut down hello VM in hello Azure classic portal.</span></span> <span data-ttu-id="4508d-401">Se você não precisar mais Olá VM, lembre-se de toodelete Olá VM e Olá encargos de armazenamento de tooavoid de arquivos. vhd associado. Para obter mais informações, consulte a seção de saudação perguntas Frequentes em [detalhes de preços de máquinas virtuais](https://azure.microsoft.com/pricing/details/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="4508d-401">If you no longer need hello VM, remember toodelete hello VM and hello associated .vhd files tooavoid storage charges.For more information, see hello FAQ section at [Virtual Machines Pricing Details](https://azure.microsoft.com/pricing/details/virtual-machines/).</span></span>

## <a name="more-information"></a><span data-ttu-id="4508d-402">Mais informações</span><span class="sxs-lookup"><span data-stu-id="4508d-402">More Information</span></span>
### <a name="resources"></a><span data-ttu-id="4508d-403">Recursos</span><span class="sxs-lookup"><span data-stu-id="4508d-403">Resources</span></span>
* <span data-ttu-id="4508d-404">Para obter conteúdo semelhante relacionado a implantação de servidor único tooa do Business Intelligence do SQL Server e SharePoint 2013, consulte [tooCreate de usar o Windows PowerShell uma VM do Azure com SQL Server BI e SharePoint 2013](https://msdn.microsoft.com/library/azure/dn385843.aspx).</span><span class="sxs-lookup"><span data-stu-id="4508d-404">For similar content related tooa single server deployment of SQL Server Business Intelligence and SharePoint 2013, see [Use Windows PowerShell tooCreate an Azure VM With SQL Server BI and SharePoint 2013](https://msdn.microsoft.com/library/azure/dn385843.aspx).</span></span>
* <span data-ttu-id="4508d-405">Para tooa relacionado de conteúdo semelhante a implantação de vários servidores de Business Intelligence do SQL Server e SharePoint 2013, consulte [implantar o SQL Server Business Intelligence em máquinas virtuais Azure](https://msdn.microsoft.com/library/dn321998.aspx).</span><span class="sxs-lookup"><span data-stu-id="4508d-405">For similar content related tooa multi-server deployment of SQL Server Business Intelligence and SharePoint 2013, see [Deploy SQL Server Business Intelligence in Azure Virtual Machines](https://msdn.microsoft.com/library/dn321998.aspx).</span></span>
* <span data-ttu-id="4508d-406">Para obter informações gerais relacionadas toodeployments do SQL Server Business Intelligence em máquinas de virtuais do Azure, consulte [SQL Server Business Intelligence em máquinas virtuais Azure](virtual-machines-windows-classic-ps-sql-bi.md).</span><span class="sxs-lookup"><span data-stu-id="4508d-406">For General information related toodeployments of SQL Server Business Intelligence in Azure Virtual Machines, see [SQL Server Business Intelligence in Azure Virtual Machines](virtual-machines-windows-classic-ps-sql-bi.md).</span></span>
* <span data-ttu-id="4508d-407">Para obter mais informações sobre o custo de saudação de encargos de computação do Azure, consulte o guia de máquinas virtuais de saudação do [Calculadora de preços do Azure](https://azure.microsoft.com/pricing/calculator/?scenario=virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="4508d-407">For more information about hello cost of Azure compute charges, see hello Virtual Machines tab of [Azure pricing calculator](https://azure.microsoft.com/pricing/calculator/?scenario=virtual-machines).</span></span>

### <a name="community-content"></a><span data-ttu-id="4508d-408">Conteúdo da comunidade</span><span class="sxs-lookup"><span data-stu-id="4508d-408">Community Content</span></span>
* <span data-ttu-id="4508d-409">Para obter instruções passo a passo sobre como toocreate um modo nativo do Reporting Services servidor de relatório sem usar o script, consulte [hospedando SQL Reporting Service na máquina Virtual Azure](http://adititechnologiesblog.blogspot.in/2012/07/hosting-sql-reporting-service-on-azure.html).</span><span class="sxs-lookup"><span data-stu-id="4508d-409">For step by step instructions on how toocreate a Reporting Services Native mode report server without using script, see [Hosting SQL Reporting Service on Azure Virtual Machine](http://adititechnologiesblog.blogspot.in/2012/07/hosting-sql-reporting-service-on-azure.html).</span></span>

### <a name="links-tooother-resources-for-sql-server-in-azure-vms"></a><span data-ttu-id="4508d-410">Recursos de tooother links para o SQL Server em VMs do Azure</span><span class="sxs-lookup"><span data-stu-id="4508d-410">Links tooother resources for SQL Server in Azure VMs</span></span>
[<span data-ttu-id="4508d-411">Visão geral do SQL Server em máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="4508d-411">SQL Server on Azure Virtual Machines Overview</span></span>](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

