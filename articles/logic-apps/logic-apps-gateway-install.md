---
title: "gateway de dados local aaaInstall - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Antes de acessar fontes de dados no local, instalar o gateway de dados de local de saudação para transferência de dados rápida e criptografia entre fontes de dados no local e os aplicativos lógicos"
keywords: "acessar dados, local, transferência de dados, criptografia, fontes de dados"
services: logic-apps
documentationcenter: 
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 47e3024e-88a0-4017-8484-8f392faec89d
ms.service: logic-apps
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/13/2017
ms.author: LADocs; dimazaid; estfan
ms.openlocfilehash: 01386a904d856ff545f2eca8eb1b008dcdc08574
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-on-premises-data-gateway-for-azure-logic-apps"></a><span data-ttu-id="6bcaf-104">Instalar o gateway de dados do local de saudação para os aplicativos lógicos do Azure</span><span class="sxs-lookup"><span data-stu-id="6bcaf-104">Install hello on-premises data gateway for Azure Logic Apps</span></span>

<span data-ttu-id="6bcaf-105">Para que seus aplicativos lógicos podem acessar fontes de dados no local, você deve instalar e configurar o gateway de dados local hello.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-105">Before your logic apps can access data sources on premises, you must install and set up hello on-premises data gateway.</span></span> <span data-ttu-id="6bcaf-106">gateway de saudação atua como uma ponte que fornece transferência de dados rápida e criptografia entre sistemas locais e seus aplicativos lógicos.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-106">hello gateway acts as a bridge that provides quick data transfer and encryption between on-premises systems and your logic apps.</span></span> <span data-ttu-id="6bcaf-107">gateway Olá transmite dados de fontes locais em canais criptografados por meio de saudação do Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-107">hello gateway relays data from on-premises sources on encrypted channels through hello Azure Service Bus.</span></span> <span data-ttu-id="6bcaf-108">Todo o tráfego originado como proteger o tráfego de saída do agente de gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-108">All traffic originates as secure outbound traffic from hello gateway agent.</span></span> <span data-ttu-id="6bcaf-109">Saiba mais sobre [como funciona o gateway de dados Olá](#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="6bcaf-109">Learn more about [how hello data gateway works](#gateway-cloud-service).</span></span>

<span data-ttu-id="6bcaf-110">gateway Olá dá suporte a fontes de dados de toothese de conexões no local:</span><span class="sxs-lookup"><span data-stu-id="6bcaf-110">hello gateway supports connections toothese data sources on premises:</span></span>

*   <span data-ttu-id="6bcaf-111">BizTalk Server 2016</span><span class="sxs-lookup"><span data-stu-id="6bcaf-111">BizTalk Server 2016</span></span>
*   <span data-ttu-id="6bcaf-112">DB2</span><span class="sxs-lookup"><span data-stu-id="6bcaf-112">DB2</span></span>  
*   <span data-ttu-id="6bcaf-113">Sistema de Arquivos</span><span class="sxs-lookup"><span data-stu-id="6bcaf-113">File System</span></span>
*   <span data-ttu-id="6bcaf-114">Informix</span><span class="sxs-lookup"><span data-stu-id="6bcaf-114">Informix</span></span>
*   <span data-ttu-id="6bcaf-115">MQ</span><span class="sxs-lookup"><span data-stu-id="6bcaf-115">MQ</span></span>
*   <span data-ttu-id="6bcaf-116">MySQL</span><span class="sxs-lookup"><span data-stu-id="6bcaf-116">MySQL</span></span>
*   <span data-ttu-id="6bcaf-117">Banco de dados Oracle</span><span class="sxs-lookup"><span data-stu-id="6bcaf-117">Oracle Database</span></span>
*   <span data-ttu-id="6bcaf-118">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="6bcaf-118">PostgreSQL</span></span>
*   <span data-ttu-id="6bcaf-119">Servidor de aplicativos SAP</span><span class="sxs-lookup"><span data-stu-id="6bcaf-119">SAP Application Server</span></span> 
*   <span data-ttu-id="6bcaf-120">Servidor de mensagens SAP</span><span class="sxs-lookup"><span data-stu-id="6bcaf-120">SAP Message Server</span></span>
*   <span data-ttu-id="6bcaf-121">SharePoint</span><span class="sxs-lookup"><span data-stu-id="6bcaf-121">SharePoint</span></span>
*   <span data-ttu-id="6bcaf-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="6bcaf-122">SQL Server</span></span>
*   <span data-ttu-id="6bcaf-123">Teradata</span><span class="sxs-lookup"><span data-stu-id="6bcaf-123">Teradata</span></span>

<span data-ttu-id="6bcaf-124">Essas etapas mostram como toofirst instalação Olá no gateway de dados local antes de você [configurar uma conexão entre o gateway hello e seus aplicativos lógicos](./logic-apps-gateway-connection.md).</span><span class="sxs-lookup"><span data-stu-id="6bcaf-124">These steps show how toofirst install hello on-premises data gateway before you [set up a connection between hello gateway and your logic apps](./logic-apps-gateway-connection.md).</span></span> <span data-ttu-id="6bcaf-125">Para obter mais informações sobre os conectores com suporte, consulte [Conectores para Aplicativo Lógico do Azure](https://docs.microsoft.com/azure/connectors/apis-list).</span><span class="sxs-lookup"><span data-stu-id="6bcaf-125">For more information about supported connectors, see [Connectors for Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list).</span></span> 

<span data-ttu-id="6bcaf-126">Para obter informações sobre como toouse Olá gateway com outros serviços, consulte estes artigos:</span><span class="sxs-lookup"><span data-stu-id="6bcaf-126">For information about how toouse hello gateway with other services, see these articles:</span></span>

*   [<span data-ttu-id="6bcaf-127">Gateway de dados local do Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="6bcaf-127">Microsoft Power BI on-premises data gateway</span></span>](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [<span data-ttu-id="6bcaf-128">Gateway de dados local do Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="6bcaf-128">Azure Analysis Services on-premises data gateway</span></span>](../analysis-services/analysis-services-gateway.md)
*   [<span data-ttu-id="6bcaf-129">Gateway de dados local do Microsoft Flow</span><span class="sxs-lookup"><span data-stu-id="6bcaf-129">Microsoft Flow on-premises data gateway</span></span>](https://flow.microsoft.com/documentation/gateway-manage/)
*   [<span data-ttu-id="6bcaf-130">Gateway de dados local do Microsoft PowerApps</span><span class="sxs-lookup"><span data-stu-id="6bcaf-130">Microsoft PowerApps on-premises data gateway</span></span>](https://powerapps.microsoft.com/tutorials/gateway-management/)

<a name="requirements"></a>
## <a name="requirements"></a><span data-ttu-id="6bcaf-131">Requisitos</span><span class="sxs-lookup"><span data-stu-id="6bcaf-131">Requirements</span></span>

<span data-ttu-id="6bcaf-132">**Mínimos**:</span><span class="sxs-lookup"><span data-stu-id="6bcaf-132">**Minimum**:</span></span>

* <span data-ttu-id="6bcaf-133">.NET 4.5 Framework</span><span class="sxs-lookup"><span data-stu-id="6bcaf-133">.NET 4.5 Framework</span></span>
* <span data-ttu-id="6bcaf-134">Versão de 64 bits do Windows 7 ou Windows Server 2008 R2 (ou posterior)</span><span class="sxs-lookup"><span data-stu-id="6bcaf-134">64-bit version of Windows 7 or Windows Server 2008 R2 (or later)</span></span>

<span data-ttu-id="6bcaf-135">**Recomendados**:</span><span class="sxs-lookup"><span data-stu-id="6bcaf-135">**Recommended**:</span></span>

* <span data-ttu-id="6bcaf-136">CPU de 8 núcleos</span><span class="sxs-lookup"><span data-stu-id="6bcaf-136">8 Core CPU</span></span>
* <span data-ttu-id="6bcaf-137">Memória de 8 GB</span><span class="sxs-lookup"><span data-stu-id="6bcaf-137">8 GB Memory</span></span>
* <span data-ttu-id="6bcaf-138">Versão de 64 bits do Windows 2012 R2 (ou posterior)</span><span class="sxs-lookup"><span data-stu-id="6bcaf-138">64-bit version of Windows 2012 R2 (or later)</span></span>

<span data-ttu-id="6bcaf-139">**Considerações importantes**:</span><span class="sxs-lookup"><span data-stu-id="6bcaf-139">**Important considerations**:</span></span>

* <span data-ttu-id="6bcaf-140">Instale o gateway de dados local Olá somente em um computador local.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-140">Install hello on-premises data gateway only on a local computer.</span></span>
<span data-ttu-id="6bcaf-141">Você não pode instalar o gateway de saudação em um controlador de domínio.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-141">You can't install hello gateway on a domain controller.</span></span>

   > [!TIP]
   > <span data-ttu-id="6bcaf-142">Você não tem tooinstall gateway de Olá Olá mesmo computador como sua fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-142">You don't have tooinstall hello gateway on hello same computer as your data source.</span></span> <span data-ttu-id="6bcaf-143">toominimize latência, você pode instalar o gateway hello mais próximo que tooyour possível fonte de dados ou em Olá mesmo computador, supondo que você tenha permissões.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-143">toominimize latency, you can install hello gateway as close as possible tooyour data source, or on hello same computer, assuming that you have permissions.</span></span>

* <span data-ttu-id="6bcaf-144">Não instale o gateway Olá em um computador que desativa, vai toosleep ou não conecta toohello Internet porque o gateway de saudação não pode ser executado sob essas circunstâncias.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-144">Don't install hello gateway on a computer that turns off, goes toosleep, or doesn't connect toohello Internet because hello gateway can't run under those circumstances.</span></span> <span data-ttu-id="6bcaf-145">Além disso, o desempenho do gateway pode ser reduzido em uma rede sem fio.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-145">Also, gateway performance might suffer over a wireless network.</span></span>

* <span data-ttu-id="6bcaf-146">Durante a instalação, você deve entrar com uma [conta corporativa ou de estudante](https://docs.microsoft.com/azure/active-directory/sign-up-organization) gerenciada pelo Azure AD (Azure Active Directory), não uma conta da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-146">During installation, you must sign in with a [work or school account](https://docs.microsoft.com/azure/active-directory/sign-up-organization) that's managed by Azure Active Directory (Azure AD), not a Microsoft account.</span></span> 

  <span data-ttu-id="6bcaf-147">Você tem toouse Olá mesmo trabalho ou escola saudação do conta posteriormente no Azure portal quando você cria e associar um recurso de gateway a sua instalação do gateway.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-147">You have toouse hello same work or school account later in hello Azure portal when you create and associate a gateway resource with your gateway installation.</span></span> <span data-ttu-id="6bcaf-148">Você selecionar esse recurso de gateway ao criar conexão Olá entre sua lógica aplicativo e hello local fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-148">You then select this gateway resource when you create hello connection between your logic app and hello on-premises data source.</span></span> [<span data-ttu-id="6bcaf-149">Por que eu devo usar uma conta corporativa ou de estudante do Azure AD?</span><span class="sxs-lookup"><span data-stu-id="6bcaf-149">Why must I use an Azure AD work or school account?</span></span>](#why-azure-work-school-account)

  > [!TIP]
  > <span data-ttu-id="6bcaf-150">Se você se inscreveu para uma oferta do Office 365 e não forneceu seu email de trabalho real, o endereço de entrada pode ser semelhante a jeff@contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-150">If you signed up for an Office 365 offering and didn't supply your actual work email, your sign-in address might look like jeff@contoso.onmicrosoft.com.</span></span> 

* <span data-ttu-id="6bcaf-151">Se você tiver um gateway existente que você deseja configurar com um instalador que é anterior à versão 14.16.6317.4, é possível alterar o local do gateway pelo instalador mais recente de saudação em execução.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-151">If you have an existing gateway that you set up with an installer that's earlier than version 14.16.6317.4, you can't change your gateway's location by running hello latest installer.</span></span> <span data-ttu-id="6bcaf-152">No entanto, você pode usar o hello mais recente instalador tooset a um novo gateway com local Olá desejado em vez disso.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-152">However, you can use hello latest installer tooset up a new gateway with hello location that you want instead.</span></span>
  
  <span data-ttu-id="6bcaf-153">Se você tiver um instalador do gateway que é anterior à versão 14.16.6317.4, mas você ainda não instalou o gateway ainda, você pode baixar e usar installer mais recente hello.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-153">If you have a gateway installer that's earlier than version 14.16.6317.4, but you haven't installed your gateway yet, you can download and use hello latest installer.</span></span>

<a name="install-gateway"></a>

## <a name="install-hello-data-gateway"></a><span data-ttu-id="6bcaf-154">Instalar o gateway de dados Olá</span><span class="sxs-lookup"><span data-stu-id="6bcaf-154">Install hello data gateway</span></span>

1.  <span data-ttu-id="6bcaf-155">[Baixe e execute o instalador do gateway Olá em um computador local](http://go.microsoft.com/fwlink/?LinkID=820931&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="6bcaf-155">[Download and run hello gateway installer on a local computer](http://go.microsoft.com/fwlink/?LinkID=820931&clcid=0x409).</span></span>

2. <span data-ttu-id="6bcaf-156">Leia e aceite os termos de saudação da declaração de privacidade e de uso.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-156">Review and accept hello terms of use and privacy statement.</span></span>

3. <span data-ttu-id="6bcaf-157">Especifique o caminho de saudação no computador local onde você deseja que o gateway de saudação tooinstall.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-157">Specify hello path on your local computer where you want tooinstall hello gateway.</span></span>

4. <span data-ttu-id="6bcaf-158">Quando solicitado, entre com sua conta corporativa ou de estudante do Azure, e não com uma conta da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-158">When prompted, sign in with your Azure work or school account, not a Microsoft account.</span></span>

   ![Entrar com a conta corporativa ou de estudante do Azure](./media/logic-apps-gateway-install/sign-in-gateway-install.png)

5. <span data-ttu-id="6bcaf-160">Agora, registrar o gateway instalado com hello [serviço de nuvem do gateway](#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="6bcaf-160">Now register your installed gateway with hello [gateway cloud service](#gateway-cloud-service).</span></span> <span data-ttu-id="6bcaf-161">Escolha **Registrar um novo gateway neste computador**.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-161">Choose **Register a new gateway on this computer**.</span></span>

   <span data-ttu-id="6bcaf-162">serviço de nuvem do gateway Olá criptografa e armazena suas credenciais da fonte de dados e os detalhes do gateway.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-162">hello gateway cloud service encrypts and stores your data source credentials and gateway details.</span></span> 
   <span data-ttu-id="6bcaf-163">o serviço de saudação também encaminha consultas e seus resultados entre seu aplicativo lógico, o gateway de dados local hello e sua fonte de dados no local.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-163">hello service also routes queries and their results between your logic app, hello on-premises data gateway, and your data source on premises.</span></span>

6. <span data-ttu-id="6bcaf-164">Forneça um nome para sua instalação do gateway.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-164">Provide a name for your gateway installation.</span></span> <span data-ttu-id="6bcaf-165">Crie uma chave de recuperação, em seguida, confirme sua chave de recuperação.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-165">Create a recovery key, then confirm your recovery key.</span></span> 

   > [!IMPORTANT] 
   > <span data-ttu-id="6bcaf-166">Sua chave de recuperação deve conter pelo menos oito caracteres.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-166">Your recovery key must contain at least eight characters.</span></span> <span data-ttu-id="6bcaf-167">Certifique-se de que você salve e manter a chave de saudação em um local seguro.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-167">Make sure that you save and keep hello key in a safe place.</span></span> <span data-ttu-id="6bcaf-168">Você também precisa essa chave quando você quiser toomigrate, restaurar ou assumir um gateway existente.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-168">You also need this key when you want toomigrate, restore, or take over an existing gateway.</span></span>

   1. <span data-ttu-id="6bcaf-169">região do toochange saudação padrão para o serviço de nuvem do gateway hello e barramento de serviço do Azure usado pela instalação do gateway, escolha **alteração região**.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-169">toochange hello default region for hello gateway cloud service and Azure Service Bus used by your gateway installation, choose **Change Region**.</span></span>

      ![Alterar região](./media/logic-apps-gateway-install/change-region-gateway-install.png)

      <span data-ttu-id="6bcaf-171">saudação padrão Olá a região é associado a seu locatário do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-171">hello default region is hello region associated with your Azure AD tenant.</span></span>

   2. <span data-ttu-id="6bcaf-172">No painel da próxima Olá, abra Olá **selecionar região** muito, escolha uma região diferente.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-172">On hello next pane, open hello **Select Region** too choose a different region.</span></span>

      ![Selecionar outra região](./media/logic-apps-gateway-install/select-region-gateway-install.png)

      <span data-ttu-id="6bcaf-174">Por exemplo, você pode selecionar Olá mesma região que seu aplicativo lógico, ou para reduzir a latência da fonte de dados de local de tooyour mais próximos do hello selecione região.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-174">For example, you might select hello same region as your logic app, or select hello region closest tooyour on-premises data source so you can reduce latency.</span></span> <span data-ttu-id="6bcaf-175">Seu aplicativo lógico e recurso de gateway podem ter locais diferentes.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-175">Your gateway resource and logic app can have different locations.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="6bcaf-176">Você não pode alterar essa região após a instalação.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-176">You can't change this region after installation.</span></span> <span data-ttu-id="6bcaf-177">Esta região também determina e restringe local Olá onde você pode criar hello recursos do Azure para o gateway.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-177">This region also determines and restricts hello location where you can create hello Azure resource for your gateway.</span></span> <span data-ttu-id="6bcaf-178">Então quando você cria o recurso de gateway no Azure, verifique se local do recurso Olá corresponde região Olá selecionado durante a instalação do gateway.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-178">So when you create your gateway resource in Azure, make sure that hello resource location matches hello region that you selected during gateway installation.</span></span>
      > 
      > <span data-ttu-id="6bcaf-179">Se você quiser toouse uma região diferente para o gateway mais tarde, você deve configurar um novo gateway.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-179">If you want toouse a different region for your gateway later, you must set up a new gateway.</span></span>

   3. <span data-ttu-id="6bcaf-180">Quando estiver pronto, escolha **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-180">When you're ready, choose **Done**.</span></span>

7. <span data-ttu-id="6bcaf-181">Agora, siga estas etapas no hello portal do Azure para que você possa [criar um recurso do Azure para seu gateway](../logic-apps/logic-apps-gateway-connection.md).</span><span class="sxs-lookup"><span data-stu-id="6bcaf-181">Now follow these steps in hello Azure portal so you can [create an Azure resource for your gateway](../logic-apps/logic-apps-gateway-connection.md).</span></span> 

<span data-ttu-id="6bcaf-182">Saiba mais sobre [como funciona o gateway de dados Olá](#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="6bcaf-182">Learn more about [how hello data gateway works](#gateway-cloud-service).</span></span>

## <a name="migrate-restore-or-take-over-an-existing-gateway"></a><span data-ttu-id="6bcaf-183">Migrar, restaurar ou assumir um gateway existente</span><span class="sxs-lookup"><span data-stu-id="6bcaf-183">Migrate, restore, or take over an existing gateway</span></span>

<span data-ttu-id="6bcaf-184">tooperform essas tarefas, você deve ter a chave de recuperação de saudação que foi especificado quando Olá gateway foi instalado.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-184">tooperform these tasks, you must have hello recovery key that was specified when hello gateway was installed.</span></span>

1. <span data-ttu-id="6bcaf-185">No menu Iniciar do computador, escolha **Gateway de dados local**.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-185">From your computer's Start menu, choose **On-premises data gateway**.</span></span>

2. <span data-ttu-id="6bcaf-186">Depois de hello instalador abre, entrar com hello mesmo Azure trabalhar ou conta de escola que foi anteriormente usado tooinstall gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-186">After hello installer opens, sign in with hello same Azure work or school account that was previously used tooinstall hello gateway.</span></span>

3. <span data-ttu-id="6bcaf-187">Escolha **Migrar, restaurar ou assumir um gateway existente**.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-187">Choose **Migrate, restore, or take over an existing gateway**.</span></span>

4. <span data-ttu-id="6bcaf-188">Forneça a chave de nome e a recuperação de saudação para gateway Olá que você deseja toomigrate, restauração ou realizar failover.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-188">Provide hello name and recovery key for hello gateway that you want toomigrate, restore, or take over.</span></span>

<a name="restart-gateway"></a>
## <a name="restart-hello-gateway"></a><span data-ttu-id="6bcaf-189">Reinicie o gateway de saudação</span><span class="sxs-lookup"><span data-stu-id="6bcaf-189">Restart hello gateway</span></span>

<span data-ttu-id="6bcaf-190">gateway de saudação é executado como um serviço do Windows.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-190">hello gateway runs as a Windows service.</span></span> <span data-ttu-id="6bcaf-191">Como qualquer outro serviço do Windows, você pode iniciar e parar o serviço de saudação de várias maneiras.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-191">Like any other Windows service, you can start and stop hello service in multiple ways.</span></span> <span data-ttu-id="6bcaf-192">Por exemplo, você pode abrir um prompt de comando com permissões elevadas no computador Olá onde o gateway hello está sendo executado e executar esses comandos ou:</span><span class="sxs-lookup"><span data-stu-id="6bcaf-192">For example, you can open a command prompt with elevated permissions on hello computer where hello gateway is running, and run either these commands:</span></span>

* <span data-ttu-id="6bcaf-193">serviço de saudação toostop, execute este comando:</span><span class="sxs-lookup"><span data-stu-id="6bcaf-193">toostop hello service, run this command:</span></span>
  
    `net stop PBIEgwService`

* <span data-ttu-id="6bcaf-194">serviço de saudação toostart, execute este comando:</span><span class="sxs-lookup"><span data-stu-id="6bcaf-194">toostart hello service, run this command:</span></span>
  
    `net start PBIEgwService`

### <a name="windows-service-account"></a><span data-ttu-id="6bcaf-195">Conta de serviço do Windows</span><span class="sxs-lookup"><span data-stu-id="6bcaf-195">Windows service account</span></span>

<span data-ttu-id="6bcaf-196">gateway de dados local Olá é configurar toouse `NT SERVICE\PBIEgwService` credenciais de logon de serviço para o Windows hello.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-196">hello on-premises data gateway is set up toouse `NT SERVICE\PBIEgwService` for hello Windows service logon credentials.</span></span> <span data-ttu-id="6bcaf-197">Por padrão, o gateway Olá tem direito de "Logon como um serviço" hello máquina Olá onde você instala o gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-197">By default, hello gateway has hello "Log on as a service" right for hello machine where you install hello gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="6bcaf-198">Olá conta de serviço do Windows é diferente de saudação conta usada para se conectar a fontes de dados locais tooon e de saudação do Azure ou conta de escola usado toosign nos serviços de toocloud.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-198">hello Windows service account differs from hello account used for connecting tooon-premises data sources, and from hello Azure work or school account used toosign in toocloud services.</span></span>

## <a name="configure-a-firewall-or-proxy"></a><span data-ttu-id="6bcaf-199">Configure um firewall ou proxy</span><span class="sxs-lookup"><span data-stu-id="6bcaf-199">Configure a firewall or proxy</span></span>

<span data-ttu-id="6bcaf-200">gateway Olá cria uma conexão de saída muito [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="6bcaf-200">hello gateway creates an outbound connection too [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span></span> <span data-ttu-id="6bcaf-201">tooprovide informações de proxy para o gateway, consulte [definir configurações de proxy](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy/).</span><span class="sxs-lookup"><span data-stu-id="6bcaf-201">tooprovide proxy information for your gateway, see [Configure proxy settings](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy/).</span></span>

<span data-ttu-id="6bcaf-202">toocheck se seu firewall ou proxy, pode bloquear conexões, confirme se a sua máquina, na verdade, pode se conectar toohello internet e hello [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="6bcaf-202">toocheck whether your firewall, or proxy, might block connections, confirm whether your machine can actually connect toohello internet and hello [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span></span> <span data-ttu-id="6bcaf-203">Em um prompt do PowerShell, execute este comando:</span><span class="sxs-lookup"><span data-stu-id="6bcaf-203">From a PowerShell prompt, run this command:</span></span>

`Test-NetConnection -ComputerName watchdog.servicebus.windows.net -Port 9350`

> [!NOTE]
> <span data-ttu-id="6bcaf-204">Esse comando apenas testa a conectividade de rede e conectividade toohello barramento de serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-204">This command only tests network connectivity and connectivity toohello Azure Service Bus.</span></span> <span data-ttu-id="6bcaf-205">Para o comando Olá não tem nenhuma toodo com gateway hello ou serviço de nuvem do gateway de saudação que criptografa e armazena suas credenciais e detalhes do gateway.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-205">So hello command doesn't have anything toodo with hello gateway or hello gateway cloud service that encrypts and stores your credentials and gateway details.</span></span> 
>
> <span data-ttu-id="6bcaf-206">Além disso, esse comando só está disponível no Windows Server 2012 R2 ou posterior e no Windows 8.1 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-206">Also, this command is only available on Windows Server 2012 R2 or later, and Windows 8.1 or later.</span></span> <span data-ttu-id="6bcaf-207">Em versões anteriores do sistema operacional, você pode usar o Telnet muito testar a conectividade.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-207">On earlier OS versions, you can use Telnet too test connectivity.</span></span> <span data-ttu-id="6bcaf-208">Saiba mais sobre [Soluções híbridas e de Barramento de Serviço do Azure](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="6bcaf-208">Learn more about [Azure Service Bus and hybrid solutions](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span></span>

<span data-ttu-id="6bcaf-209">Seus resultados deverão ser exemplo toothis semelhante:</span><span class="sxs-lookup"><span data-stu-id="6bcaf-209">Your results should look similar toothis example:</span></span>

```text
ComputerName           : watchdog.servicebus.windows.net
RemoteAddress          : 70.37.104.240
RemotePort             : 5672
InterfaceAlias         : vEthernet (Broadcom NetXtreme Gigabit Ethernet - Virtual Switch)
SourceAddress          : 10.120.60.105
PingSucceeded          : False
PingReplyDetails (RTT) : 0 ms
TcpTestSucceeded       : True
```

<span data-ttu-id="6bcaf-210">Se **TcpTestSucceeded** não está definido muito**True**, você poderá estar bloqueada por um firewall.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-210">If **TcpTestSucceeded** is not set too**True**, you might be blocked by a firewall.</span></span> <span data-ttu-id="6bcaf-211">Se você quiser toobe abrangente, substitua Olá **ComputerName** e **porta** valores com hello listado em [configurar portas](#configure-ports) neste tópico.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-211">If you want toobe comprehensive, substitute hello **ComputerName** and **Port** values with hello values listed under [Configure ports](#configure-ports) in this topic.</span></span>

<span data-ttu-id="6bcaf-212">firewall de saudação também pode bloquear conexões que hello que Azure Service Bus torna toohello datacenters do Azure.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-212">hello firewall might also block connections that hello Azure Service Bus makes toohello Azure datacenters.</span></span> <span data-ttu-id="6bcaf-213">Se essa situação ocorrer, aprovar (desbloquear) todos Olá endereços IP para os data centers em sua região.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-213">If this scenario happens, approve (unblock) all hello IP addresses for those datacenters in your region.</span></span> <span data-ttu-id="6bcaf-214">Para esses endereços IP, [a lista de endereços de IP do Azure de saudação de get aqui](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="6bcaf-214">For those IP addresses, [get hello Azure IP addresses list here](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

## <a name="configure-ports"></a><span data-ttu-id="6bcaf-215">Configure portas</span><span class="sxs-lookup"><span data-stu-id="6bcaf-215">Configure ports</span></span>

<span data-ttu-id="6bcaf-216">gateway Olá cria uma conexão de saída muito[Azure Service Bus](https://azure.microsoft.com/services/service-bus/) e se comunica nas portas de saída: TCP 443 (padrão), 5671, 5672, 9350 a 9354.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-216">hello gateway creates an outbound connection too[Azure Service Bus](https://azure.microsoft.com/services/service-bus/) and communicates on outbound ports: TCP 443 (default), 5671, 5672, 9350 through 9354.</span></span> <span data-ttu-id="6bcaf-217">gateway de saudação não requer portas de entrada.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-217">hello gateway doesn't require inbound ports.</span></span> <span data-ttu-id="6bcaf-218">Saiba mais sobre [Soluções híbridas e de Barramento de Serviço do Azure](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="6bcaf-218">Learn more about [Azure Service Bus and hybrid solutions](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span></span>

| <span data-ttu-id="6bcaf-219">NOMES DE DOMÍNIO</span><span class="sxs-lookup"><span data-stu-id="6bcaf-219">DOMAIN NAMES</span></span> | <span data-ttu-id="6bcaf-220">PORTAS DE SAÍDA</span><span class="sxs-lookup"><span data-stu-id="6bcaf-220">OUTBOUND PORTS</span></span> | <span data-ttu-id="6bcaf-221">DESCRIÇÃO</span><span class="sxs-lookup"><span data-stu-id="6bcaf-221">DESCRIPTION</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6bcaf-222">*.analysis.windows.net</span><span class="sxs-lookup"><span data-stu-id="6bcaf-222">*.analysis.windows.net</span></span> | <span data-ttu-id="6bcaf-223">443</span><span class="sxs-lookup"><span data-stu-id="6bcaf-223">443</span></span> | <span data-ttu-id="6bcaf-224">HTTPS</span><span class="sxs-lookup"><span data-stu-id="6bcaf-224">HTTPS</span></span> | 
| <span data-ttu-id="6bcaf-225">*.login.windows.net</span><span class="sxs-lookup"><span data-stu-id="6bcaf-225">*.login.windows.net</span></span> | <span data-ttu-id="6bcaf-226">443</span><span class="sxs-lookup"><span data-stu-id="6bcaf-226">443</span></span> | <span data-ttu-id="6bcaf-227">HTTPS</span><span class="sxs-lookup"><span data-stu-id="6bcaf-227">HTTPS</span></span> | 
| <span data-ttu-id="6bcaf-228">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="6bcaf-228">*.servicebus.windows.net</span></span> | <span data-ttu-id="6bcaf-229">5671-5672</span><span class="sxs-lookup"><span data-stu-id="6bcaf-229">5671-5672</span></span> | <span data-ttu-id="6bcaf-230">Advanced Message Queuing Protocol (AMQP)</span><span class="sxs-lookup"><span data-stu-id="6bcaf-230">Advanced Message Queuing Protocol (AMQP)</span></span> | 
| <span data-ttu-id="6bcaf-231">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="6bcaf-231">*.servicebus.windows.net</span></span> | <span data-ttu-id="6bcaf-232">443, 9350-9354</span><span class="sxs-lookup"><span data-stu-id="6bcaf-232">443, 9350-9354</span></span> | <span data-ttu-id="6bcaf-233">Ouvintes de Retransmissão do Barramento de Serviço por meio de TCP (requer 443 para aquisição de token de Controle de Acesso)</span><span class="sxs-lookup"><span data-stu-id="6bcaf-233">Listeners on Service Bus Relay over TCP (requires 443 for Access Control token acquisition)</span></span> | 
| <span data-ttu-id="6bcaf-234">*.frontend.clouddatahub.net</span><span class="sxs-lookup"><span data-stu-id="6bcaf-234">*.frontend.clouddatahub.net</span></span> | <span data-ttu-id="6bcaf-235">443</span><span class="sxs-lookup"><span data-stu-id="6bcaf-235">443</span></span> | <span data-ttu-id="6bcaf-236">HTTPS</span><span class="sxs-lookup"><span data-stu-id="6bcaf-236">HTTPS</span></span> | 
| <span data-ttu-id="6bcaf-237">*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="6bcaf-237">*.core.windows.net</span></span> | <span data-ttu-id="6bcaf-238">443</span><span class="sxs-lookup"><span data-stu-id="6bcaf-238">443</span></span> | <span data-ttu-id="6bcaf-239">HTTPS</span><span class="sxs-lookup"><span data-stu-id="6bcaf-239">HTTPS</span></span> | 
| <span data-ttu-id="6bcaf-240">login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="6bcaf-240">login.microsoftonline.com</span></span> | <span data-ttu-id="6bcaf-241">443</span><span class="sxs-lookup"><span data-stu-id="6bcaf-241">443</span></span> | <span data-ttu-id="6bcaf-242">HTTPS</span><span class="sxs-lookup"><span data-stu-id="6bcaf-242">HTTPS</span></span> | 
| <span data-ttu-id="6bcaf-243">*.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="6bcaf-243">*.msftncsi.com</span></span> | <span data-ttu-id="6bcaf-244">443</span><span class="sxs-lookup"><span data-stu-id="6bcaf-244">443</span></span> | <span data-ttu-id="6bcaf-245">Usado tootest conectividade com a internet quando o gateway hello está inacessível por Olá serviço do Power BI.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-245">Used tootest internet connectivity when hello gateway is unreachable by hello Power BI service.</span></span> | 

<span data-ttu-id="6bcaf-246">Se você tiver tooapprove endereços IP em vez de domínios hello, você pode baixar e usar o hello [lista de intervalos de IP de Datacenter do Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="6bcaf-246">If you have tooapprove IP addresses instead of hello domains, you can download and use hello [Microsoft Azure Datacenter IP ranges list](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="6bcaf-247">Em alguns casos, são feitas conexões do barramento de serviço do Azure Olá com endereço IP em vez de nomes de domínio totalmente qualificado.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-247">In some cases, hello Azure Service Bus connections are made with IP Address rather than fully qualified domain names.</span></span>

<a name="gateway-cloud-service"></a>
## <a name="how-does-hello-data-gateway-work"></a><span data-ttu-id="6bcaf-248">Como funciona o gateway de dados Olá?</span><span class="sxs-lookup"><span data-stu-id="6bcaf-248">How does hello data gateway work?</span></span>

<span data-ttu-id="6bcaf-249">gateway de dados Olá facilita a comunicação rápida e segura entre sua lógica de aplicativo, serviço de nuvem do gateway hello e sua fonte de dados local.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-249">hello data gateway facilitates quick and secure communication between your logic app, hello gateway cloud service, and your on-premises data source.</span></span> 

![diagram-for-on-premises-data-gateway-flow](./media/logic-apps-gateway-install/how-on-premises-data-gateway-works-flow-diagram.png)

<span data-ttu-id="6bcaf-251">Portanto quando o usuário Olá na nuvem Olá interage com um elemento que tenha se conectado tooyour local fonte de dados:</span><span class="sxs-lookup"><span data-stu-id="6bcaf-251">So when hello user in hello cloud interacts with an element that's connected tooyour on-premises data source:</span></span>

1. <span data-ttu-id="6bcaf-252">serviço de nuvem do gateway Olá cria uma consulta, juntamente com hello criptografado credenciais Olá fonte de dados e envia toohello fila consulta Olá Olá gateway tooprocess.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-252">hello gateway cloud service creates a query, along with hello encrypted credentials for hello data source, and sends hello query toohello queue for hello gateway tooprocess.</span></span>

2. <span data-ttu-id="6bcaf-253">serviço de nuvem do gateway Olá analisa a consulta hello e envia Olá solicitação toohello barramento de serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-253">hello gateway cloud service analyzes hello query and pushes hello request toohello Azure Service Bus.</span></span>

3. <span data-ttu-id="6bcaf-254">gateway de dados local Olá sonda hello Azure Service Bus para solicitações pendentes.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-254">hello on-premises data gateway polls hello Azure Service Bus for pending requests.</span></span>

4. <span data-ttu-id="6bcaf-255">Olá gateway obtém Olá consulta, descriptografa Olá credenciais e conecta-se a fonte de dados toohello com essas credenciais.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-255">hello gateway gets hello query, decrypts hello credentials, and connects toohello data source with those credentials.</span></span>

5. <span data-ttu-id="6bcaf-256">gateway Olá envia a fonte de dados de toohello Olá consulta para execução.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-256">hello gateway sends hello query toohello data source for execution.</span></span>

6. <span data-ttu-id="6bcaf-257">Olá resultados são enviados da fonte de dados de saudação, gateway toohello back e toohello serviço de nuvem do gateway.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-257">hello results are sent from hello data source, back toohello gateway, and then toohello gateway cloud service.</span></span> <span data-ttu-id="6bcaf-258">Olá serviço de nuvem do gateway, em seguida, usa Olá resultados.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-258">hello gateway cloud service then uses hello results.</span></span>

<a name="faq"></a>
## <a name="frequently-asked-questions"></a><span data-ttu-id="6bcaf-259">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="6bcaf-259">Frequently asked questions</span></span>

### <a name="general"></a><span data-ttu-id="6bcaf-260">Geral</span><span class="sxs-lookup"><span data-stu-id="6bcaf-260">General</span></span>

<span data-ttu-id="6bcaf-261">**P**: É necessário um gateway para fontes de dados na nuvem hello, como SQL Azure?</span><span class="sxs-lookup"><span data-stu-id="6bcaf-261">**Q**: Do I need a gateway for data sources in hello cloud, such as SQL Azure?</span></span> <br/><span data-ttu-id="6bcaf-262">
**R:** Não.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-262">
**A**: No.</span></span> <span data-ttu-id="6bcaf-263">Um gateway se conecta a fontes de dados de locais tooon somente.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-263">A gateway connects tooon-premises data sources only.</span></span>

<span data-ttu-id="6bcaf-264">**P**: gateway de saudação tem toobe instalado Olá mesmo computador como fonte de dados Olá?</span><span class="sxs-lookup"><span data-stu-id="6bcaf-264">**Q**: Does hello gateway have toobe installed on hello same machine as hello data source?</span></span> <br/><span data-ttu-id="6bcaf-265">
**R:** Não.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-265">
**A**: No.</span></span> <span data-ttu-id="6bcaf-266">gateway de saudação conecta toohello fonte de dados usando as informações de conexão de saudação que foi fornecidas.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-266">hello gateway connects toohello data source using hello connection information that was provided.</span></span> <span data-ttu-id="6bcaf-267">Considere o gateway hello como um aplicativo cliente nesse sentido.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-267">Consider hello gateway as a client application in this sense.</span></span> <span data-ttu-id="6bcaf-268">gateway Olá precisa apenas Olá recurso tooconnect toohello nome do servidor que foi fornecido.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-268">hello gateway just needs hello capability tooconnect toohello server name that was provided.</span></span>

<a name="why-azure-work-school-account"></a>

<span data-ttu-id="6bcaf-269">**P**: por que deve, use um trabalho do Azure ou de estudante conta toosign em?</span><span class="sxs-lookup"><span data-stu-id="6bcaf-269">**Q**: Why must I use an Azure work or school account toosign in?</span></span> <br/><span data-ttu-id="6bcaf-270">
**Um**: somente, você pode usar um trabalho do Azure ou conta escolar quando você instalar o gateway de dados local hello.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-270">
**A**: You can only use an Azure work or school account when you install hello on-premises data gateway.</span></span> <span data-ttu-id="6bcaf-271">Sua conta de entrada é armazenada em um locatário gerenciado pelo Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="6bcaf-271">Your sign-in account is stored in a tenant that's managed by Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="6bcaf-272">Geralmente, o nome principal de usuário do sua conta AD do Azure (UPN) corresponde endereço de email de saudação.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-272">Usually, your Azure AD account's user principal name (UPN) matches hello email address.</span></span>

<span data-ttu-id="6bcaf-273">**P**: Em que local minhas credenciais são armazenadas?</span><span class="sxs-lookup"><span data-stu-id="6bcaf-273">**Q**: Where are my credentials stored?</span></span> <br/><span data-ttu-id="6bcaf-274">
**Um**: credenciais de saudação que você inserir para uma fonte de dados são criptografadas e armazenadas no serviço de nuvem do gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-274">
**A**: hello credentials that you enter for a data source are encrypted and stored in hello gateway cloud service.</span></span> <span data-ttu-id="6bcaf-275">as credenciais de saudação são descriptografadas no gateway de dados local hello.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-275">hello credentials are decrypted at hello on-premises data gateway.</span></span>

<span data-ttu-id="6bcaf-276">**P**: Há algum requisito de largura de banda de rede?</span><span class="sxs-lookup"><span data-stu-id="6bcaf-276">**Q**: Are there any requirements for network bandwidth?</span></span> <br/><span data-ttu-id="6bcaf-277">
**R**: recomendamos que sua conexão de rede tenha uma boa taxa de transferência.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-277">
**A**: We recommend that your network connection has good throughput.</span></span> <span data-ttu-id="6bcaf-278">Cada ambiente é diferente e quantidade de saudação do envio de dados afeta os resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-278">Every environment is different, and hello amount of data being sent affects hello results.</span></span> <span data-ttu-id="6bcaf-279">Uso da rota expressa pode ajudar a tooguarantee um nível de taxa de transferência entre locais e hello datacenters do Azure.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-279">Using ExpressRoute could help tooguarantee a level of throughput between on-premises and hello Azure datacenters.</span></span>
<span data-ttu-id="6bcaf-280">Você pode usar o hello ferramenta de terceiros Azure Speed Test aplicativo toohelp medidor a taxa de transferência.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-280">You can use hello third-party tool Azure Speed Test app toohelp gauge your throughput.</span></span>

<span data-ttu-id="6bcaf-281">**P**: o que é a latência de saudação executando consultas tooa fonte de dados do gateway Olá?</span><span class="sxs-lookup"><span data-stu-id="6bcaf-281">**Q**: What is hello latency for running queries tooa data source from hello gateway?</span></span> <span data-ttu-id="6bcaf-282">O que é a arquitetura recomendada Olá?</span><span class="sxs-lookup"><span data-stu-id="6bcaf-282">What is hello best architecture?</span></span> <br/><span data-ttu-id="6bcaf-283">
**Um**: tooreduce latência de rede, instalar Olá gateway como fonte de dados toohello fechar possível.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-283">
**A**: tooreduce network latency, install hello gateway as close toohello data source as possible.</span></span> <span data-ttu-id="6bcaf-284">Se você pode instalar o gateway de saudação na fonte de dados reais hello, essa proximidade minimiza a latência de saudação introduzida.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-284">If you can install hello gateway on hello actual data source, this proximity minimizes hello latency introduced.</span></span> <span data-ttu-id="6bcaf-285">Considere a possibilidade de datacenters Olá muito.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-285">Consider hello datacenters too.</span></span> <span data-ttu-id="6bcaf-286">Por exemplo, se o serviço usa o datacenter do Oeste dos EUA hello e você tiver o SQL Server hospedado em uma VM do Azure, sua VM do Azure deve estar no hello Oeste dos EUA muito.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-286">For example, if your service uses hello West US datacenter, and you have SQL Server hosted in an Azure VM, your Azure VM should be in hello West US too.</span></span> <span data-ttu-id="6bcaf-287">Essa proximidade minimiza a latência e evita cobranças de egresso em Olá VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-287">This proximity minimizes latency and avoids egress charges on hello Azure VM.</span></span>

<span data-ttu-id="6bcaf-288">**P**: são como os resultados enviados toohello back nuvem?</span><span class="sxs-lookup"><span data-stu-id="6bcaf-288">**Q**: How are results sent back toohello cloud?</span></span> <br/><span data-ttu-id="6bcaf-289">
**Um**: os resultados são enviados por meio de saudação do Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-289">
**A**: Results are sent through hello Azure Service Bus.</span></span>

<span data-ttu-id="6bcaf-290">**P**: há qualquer gateway toohello de conexões de entrada da nuvem Olá?</span><span class="sxs-lookup"><span data-stu-id="6bcaf-290">**Q**: Are there any inbound connections toohello gateway from hello cloud?</span></span> <br/><span data-ttu-id="6bcaf-291">
**R:** Não.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-291">
**A**: No.</span></span> <span data-ttu-id="6bcaf-292">gateway de saudação usa conexões de saída tooAzure barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-292">hello gateway uses outbound connections tooAzure Service Bus.</span></span>

<span data-ttu-id="6bcaf-293">**P**: O que acontecerá se eu bloquear conexões de saída?</span><span class="sxs-lookup"><span data-stu-id="6bcaf-293">**Q**: What if I block outbound connections?</span></span> <span data-ttu-id="6bcaf-294">O que eu preciso tooopen?</span><span class="sxs-lookup"><span data-stu-id="6bcaf-294">What do I need tooopen?</span></span> <br/><span data-ttu-id="6bcaf-295">
**Um**: Consulte portas hello e hosts que Olá gateway usa.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-295">
**A**: See hello ports and hosts that hello gateway uses.</span></span>

<span data-ttu-id="6bcaf-296">**P**: O serviço Windows real de saudação chamado?</span><span class="sxs-lookup"><span data-stu-id="6bcaf-296">**Q**: What is hello actual Windows service called?</span></span><br/><span data-ttu-id="6bcaf-297">
**Um**: em serviços, o gateway de saudação é chamado serviço do Power BI Enterprise Gateway.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-297">
**A**: In Services, hello gateway is called Power BI Enterprise Gateway Service.</span></span>

<span data-ttu-id="6bcaf-298">**P**: pode Olá serviço Windows do gateway execute com uma conta do Active Directory do Azure?</span><span class="sxs-lookup"><span data-stu-id="6bcaf-298">**Q**: Can hello gateway Windows service run with an Azure Active Directory account?</span></span> <br/><span data-ttu-id="6bcaf-299">
**R:** Não.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-299">
**A**: No.</span></span> <span data-ttu-id="6bcaf-300">saudação de serviço do Windows deve ter uma conta válida do Windows.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-300">hello Windows service must have a valid Windows account.</span></span> <span data-ttu-id="6bcaf-301">Por padrão, o serviço de saudação é executado com hello SID de serviço NT SERVICE\PBIEgwService.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-301">By default, hello service runs with hello Service SID, NT SERVICE\PBIEgwService.</span></span>

### <a name="high-availability-and-disaster-recovery"></a><span data-ttu-id="6bcaf-302">Alta disponibilidade e recuperação de desastres</span><span class="sxs-lookup"><span data-stu-id="6bcaf-302">High availability and disaster recovery</span></span>

<span data-ttu-id="6bcaf-303">**P**: Quais opções estão disponíveis para recuperação de desastre?</span><span class="sxs-lookup"><span data-stu-id="6bcaf-303">**Q**: What options are available for disaster recovery?</span></span> <br/><span data-ttu-id="6bcaf-304">
**Um**: você pode usar toorestore de chave de recuperação de saudação ou mover um gateway.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-304">
**A**: You can use hello recovery key toorestore or move a gateway.</span></span> <span data-ttu-id="6bcaf-305">Ao instalar o gateway Olá, especifique a chave de recuperação de Olá.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-305">When you install hello gateway, specify hello recovery key.</span></span>

<span data-ttu-id="6bcaf-306">**P**: qual é o benefício de saudação da chave de recuperação Olá?</span><span class="sxs-lookup"><span data-stu-id="6bcaf-306">**Q**: What is hello benefit of hello recovery key?</span></span> <br/><span data-ttu-id="6bcaf-307">
**Um**: chave de recuperação Olá fornece uma maneira toomigrate ou recuperar suas configurações de gateway após um desastre.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-307">
**A**: hello recovery key provides a way toomigrate or recover your gateway settings after a disaster.</span></span>

<span data-ttu-id="6bcaf-308">**P**: há planos para habilitar cenários de alta disponibilidade com o gateway Olá?</span><span class="sxs-lookup"><span data-stu-id="6bcaf-308">**Q**: Are there any plans for enabling high availability scenarios with hello gateway?</span></span> <br/><span data-ttu-id="6bcaf-309">
**Um**: esses cenários são roteiro hello, mas ainda não tem uma linha do tempo.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-309">
**A**: These scenarios are on hello roadmap, but we don't have a timeline yet.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="6bcaf-310">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="6bcaf-310">Troubleshooting</span></span>

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

<span data-ttu-id="6bcaf-311">**P**: como ver quais consultas estão sendo enviadas a fonte de dados local toohello?</span><span class="sxs-lookup"><span data-stu-id="6bcaf-311">**Q**: How can I see what queries are being sent toohello on-premises data source?</span></span> <br/><span data-ttu-id="6bcaf-312">
**Um**: você pode habilitar o rastreamento de consulta, que inclui as consultas de saudação que são enviadas.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-312">
**A**: You can enable query tracing, which includes hello queries that are sent.</span></span> <span data-ttu-id="6bcaf-313">Lembre-se de consulta toochange toohello valor original quando terminado de solução de problemas de rastreamento novamente.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-313">Remember toochange query tracing back toohello original value when done troubleshooting.</span></span> <span data-ttu-id="6bcaf-314">Deixar o acompanhamento de consulta ativado cria logs maiores.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-314">Leaving query tracing turned on creates larger logs.</span></span>

<span data-ttu-id="6bcaf-315">Você também pode examinar ferramentas de rastreamento de consultas disponibilizadas por sua fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-315">You can also look at tools that your data source has for tracing queries.</span></span> <span data-ttu-id="6bcaf-316">Por exemplo, você pode usar o Extended Events ou o SQL Profiler para SQL Server e Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-316">For example, you can use Extended Events or SQL Profiler for SQL Server and Analysis Services.</span></span>

<span data-ttu-id="6bcaf-317">**P**: onde estão os logs do gateway Olá?</span><span class="sxs-lookup"><span data-stu-id="6bcaf-317">**Q**: Where are hello gateway logs?</span></span> <br/><span data-ttu-id="6bcaf-318">
**R**: Consulte Ferramentas mais adiante neste tópico.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-318">
**A**: See Tools later in this topic.</span></span>

### <a name="update-toohello-latest-version"></a><span data-ttu-id="6bcaf-319">Atualizar a versão mais recente do toohello</span><span class="sxs-lookup"><span data-stu-id="6bcaf-319">Update toohello latest version</span></span>

<span data-ttu-id="6bcaf-320">Muitos problemas podem surgir quando a versão do gateway Olá ficará desatualizado.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-320">Many issues can surface when hello gateway version becomes outdated.</span></span> <span data-ttu-id="6bcaf-321">Como boa prática geral, certifique-se de que você use a versão mais recente do hello.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-321">As good general practice, make sure that you use hello latest version.</span></span> <span data-ttu-id="6bcaf-322">Se você não tiver atualizado o gateway Olá por um mês ou mais, talvez considere instalar a versão mais recente saudação do gateway de saudação e ver se você pode reproduzir o problema de saudação.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-322">If you haven't updated hello gateway for a month or longer, you might consider installing hello latest version of hello gateway, and see if you can reproduce hello issue.</span></span>

### <a name="error-failed-tooadd-user-toogroup--2147463168-pbiegwservice-performance-log-users"></a><span data-ttu-id="6bcaf-323">Erro: Falha tooadd toogroup de usuário.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-323">Error: Failed tooadd user toogroup.</span></span> <span data-ttu-id="6bcaf-324">(-2147463168 PBIEgwService Performance Log Users)</span><span class="sxs-lookup"><span data-stu-id="6bcaf-324">(-2147463168 PBIEgwService Performance Log Users)</span></span>

<span data-ttu-id="6bcaf-325">Você pode obter esse erro se você tentar tooinstall gateway de saudação em um controlador de domínio, que não tem suporte.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-325">You might get this error if you try tooinstall hello gateway on a domain controller, which isn't supported.</span></span> <span data-ttu-id="6bcaf-326">Certifique-se de que você implanta o gateway de saudação em um computador que não seja um controlador de domínio.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-326">Make sure that you deploy hello gateway on a machine that isn't a domain controller.</span></span>

## <a name="tools"></a><span data-ttu-id="6bcaf-327">Ferramentas</span><span class="sxs-lookup"><span data-stu-id="6bcaf-327">Tools</span></span>

### <a name="collect-logs-from-hello-gateway-configurer"></a><span data-ttu-id="6bcaf-328">Coletar logs do configurer de gateway Olá</span><span class="sxs-lookup"><span data-stu-id="6bcaf-328">Collect logs from hello gateway configurer</span></span>

<span data-ttu-id="6bcaf-329">Você pode coletar vários logs para o gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-329">You can collect several logs for hello gateway.</span></span> <span data-ttu-id="6bcaf-330">Inicie sempre com logs Olá!</span><span class="sxs-lookup"><span data-stu-id="6bcaf-330">Always start with hello logs!</span></span>

#### <a name="installer-logs"></a><span data-ttu-id="6bcaf-331">Logs do instalador</span><span class="sxs-lookup"><span data-stu-id="6bcaf-331">Installer logs</span></span>

`%localappdata%\Temp\Power_BI_Gateway_–Enterprise.log`

#### <a name="configuration-logs"></a><span data-ttu-id="6bcaf-332">Logs de configuração</span><span class="sxs-lookup"><span data-stu-id="6bcaf-332">Configuration logs</span></span>

`%localappdata%\Microsoft\Power BI Enterprise Gateway\GatewayConfigurator.log`

#### <a name="enterprise-gateway-service-logs"></a><span data-ttu-id="6bcaf-333">Logs de serviço do gateway corporativo</span><span class="sxs-lookup"><span data-stu-id="6bcaf-333">Enterprise gateway service logs</span></span>

`C:\Users\PBIEgwService\AppData\Local\Microsoft\Power BI Enterprise Gateway\EnterpriseGateway.log`

#### <a name="event-logs"></a><span data-ttu-id="6bcaf-334">Logs de eventos</span><span class="sxs-lookup"><span data-stu-id="6bcaf-334">Event logs</span></span>

<span data-ttu-id="6bcaf-335">Você pode encontrar hello logs do Gateway de gerenciamento de dados e PowerBIGateway em **Logs de aplicativos e serviços**.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-335">You can find hello Data Management Gateway and PowerBIGateway logs under **Application and Services Logs**.</span></span>

### <a name="fiddler-trace"></a><span data-ttu-id="6bcaf-336">Rastreamento do Fiddler</span><span class="sxs-lookup"><span data-stu-id="6bcaf-336">Fiddler Trace</span></span>

<span data-ttu-id="6bcaf-337">[Fiddler](http://www.telerik.com/fiddler) é uma ferramenta gratuita da Telerik que monitora o tráfego HTTP.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-337">[Fiddler](http://www.telerik.com/fiddler) is a free tool from Telerik that monitors HTTP traffic.</span></span> <span data-ttu-id="6bcaf-338">Você pode ver esse tráfego com hello serviço do Power BI de máquina do cliente hello.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-338">You can see this traffic with hello Power BI service from hello client machine.</span></span> <span data-ttu-id="6bcaf-339">Esse serviço pode mostrar erros e outras informações relacionadas.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-339">This service might show errors and other related information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6bcaf-340">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6bcaf-340">Next steps</span></span>
    
* [<span data-ttu-id="6bcaf-341">Conecte-se a dados locais tooon de aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="6bcaf-341">Connect tooon-premises data from logic apps</span></span>](../logic-apps/logic-apps-gateway-connection.md)
* [<span data-ttu-id="6bcaf-342">Recursos de integração corporativa</span><span class="sxs-lookup"><span data-stu-id="6bcaf-342">Enterprise integration features</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [<span data-ttu-id="6bcaf-343">Conectores de Aplicativos Lógicos do Azure</span><span class="sxs-lookup"><span data-stu-id="6bcaf-343">Connectors for Azure Logic Apps</span></span>](../connectors/apis-list.md)
