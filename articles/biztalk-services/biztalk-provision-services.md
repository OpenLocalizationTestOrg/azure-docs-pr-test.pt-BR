---
title: "aaaCreate Serviços BizTalk do Azure no portal do Azure de saudação | Microsoft Docs"
description: "Saiba como tooprovision ou criar serviços BizTalk do Azure no hello portal do Azure; MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 3ad18876-a649-40d6-9aa0-1509c1d62c43
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 6781cadada8ac9c84e1fe045d2b0f995811f75b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-biztalk-services-using-hello-azure-portal"></a><span data-ttu-id="e24bf-103">Criar serviços do BizTalk usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e24bf-103">Create BizTalk Services using hello Azure portal</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]


> [!TIP]
> <span data-ttu-id="e24bf-104">toosign em toohello portal do Azure, você precisa de uma conta do Azure e a assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="e24bf-104">toosign in toohello Azure portal, you need an Azure account and Azure subscription.</span></span> <span data-ttu-id="e24bf-105">Se você não tiver uma conta, será possível criar uma conta de avaliação gratuita em questão de minutos.</span><span class="sxs-lookup"><span data-stu-id="e24bf-105">If you don't have an account, you can create a free trial account within a few minutes.</span></span> <span data-ttu-id="e24bf-106">Consulte [Avaliação gratuita do Azure](http://go.microsoft.com/fwlink/p/?LinkID=239738).</span><span class="sxs-lookup"><span data-stu-id="e24bf-106">See [Azure Free Trial](http://go.microsoft.com/fwlink/p/?LinkID=239738).</span></span>


## <span data-ttu-id="e24bf-107"><a name="CreateService"></a>Criar um Serviço do BizTalk</span><span class="sxs-lookup"><span data-stu-id="e24bf-107"><a name="CreateService"></a>Create a BizTalk Service</span></span>
<span data-ttu-id="e24bf-108">Dependendo da saudação edição que você escolher, nem todas as configurações do BizTalk Service podem estar disponíveis.</span><span class="sxs-lookup"><span data-stu-id="e24bf-108">Depending on hello Edition you choose, not all BizTalk Service settings may be available.</span></span>

1. <span data-ttu-id="e24bf-109">Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="e24bf-109">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="e24bf-110">No painel de navegação inferior hello, selecione **novo**:</span><span class="sxs-lookup"><span data-stu-id="e24bf-110">In hello bottom navigation pane, select **NEW**:</span></span>  
   <span data-ttu-id="e24bf-111">![Selecione o botão novo Olá][NEWButton]</span><span class="sxs-lookup"><span data-stu-id="e24bf-111">![Select hello New button][NEWButton]</span></span>
3. <span data-ttu-id="e24bf-112">Selecione **SERVIÇOS DE APLICATIVOS** > **SERVIÇO BIZTALK** > **CRIAÇÃO PERSONALIZADA**:</span><span class="sxs-lookup"><span data-stu-id="e24bf-112">Select **APP SERVICES** > **BIZTALK SERVICE** > **CUSTOM CREATE**:</span></span>  
   <span data-ttu-id="e24bf-113">![Selecionar Serviço BizTalk e Criação Personalizada][NewBizTalkService]</span><span class="sxs-lookup"><span data-stu-id="e24bf-113">![Select BizTalk Service and select Custom Create][NewBizTalkService]</span></span>
4. <span data-ttu-id="e24bf-114">Insira as configurações do serviço BizTalk hello:</span><span class="sxs-lookup"><span data-stu-id="e24bf-114">Enter hello BizTalk Service settings:</span></span>
   
    <table border="1">
    <tr>
    <td><span data-ttu-id="e24bf-115"><strong>Nome do Serviço BizTalk</strong></span><span class="sxs-lookup"><span data-stu-id="e24bf-115"><strong>BizTalk service name</strong></span></span></td>
    <td><span data-ttu-id="e24bf-116">Você pode inserir qualquer nome, mas seja específico.</span><span class="sxs-lookup"><span data-stu-id="e24bf-116">You can enter any name but be specific.</span></span> <span data-ttu-id="e24bf-117">Alguns exemplos incluem:</span><span class="sxs-lookup"><span data-stu-id="e24bf-117">Some examples include:</span></span><br/><br/><span data-ttu-id="e24bf-118">
    <em>mycompany</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="e24bf-118">
    <em>mycompany</em>.biztalk.windows.net</span></span><br/><span data-ttu-id="e24bf-119">
    <em>mycompanymyapplication</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="e24bf-119">
    <em>mycompanymyapplication</em>.biztalk.windows.net</span></span><br/><span data-ttu-id="e24bf-120">
    <em>myapplication</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="e24bf-120">
    <em>myapplication</em>.biztalk.windows.net</span></span><br/><br/><span data-ttu-id="e24bf-121">". <yourbiztalkservicename>.BizTalk.Windows.NET" é automaticamente adicionado toohello nome digitado.</span><span class="sxs-lookup"><span data-stu-id="e24bf-121">".biztalk.windows.net" is automatically added toohello name you enter.</span></span> <span data-ttu-id="e24bf-122">Isso cria uma URL que é usado tooaccess o BizTalk de serviço, como <strong>https://<em>myapplication</em>. <yourbiztalkservicename>.BizTalk.Windows.NET</strong>.</span><span class="sxs-lookup"><span data-stu-id="e24bf-122">This creates a URL that is used tooaccess your BizTalk Service, like <strong>https://<em>myapplication</em>.biztalk.windows.net</strong>.</span></span>
    </td>
    </tr>
    <tr>
    <td><span data-ttu-id="e24bf-123"><strong>Edição</strong></span><span class="sxs-lookup"><span data-stu-id="e24bf-123"><strong>Edition</strong></span></span></td>
    <td><span data-ttu-id="e24bf-124">Se você estiver na fase de teste/desenvolvimento hello, escolha <strong>desenvolvedor</strong>.</span><span class="sxs-lookup"><span data-stu-id="e24bf-124">If you are in hello testing/development phase, choose <strong>Developer</strong>.</span></span> <span data-ttu-id="e24bf-125">Se você estiver na fase de produção de hello, use Olá <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302279">Serviços BizTalk: gráfico de edições</a> toodetermine se <strong>Premium</strong>, <strong>padrão</strong>, ou <strong>Basic</strong>é Olá a opção correta para seu cenário de negócios.</span><span class="sxs-lookup"><span data-stu-id="e24bf-125">If you are in hello production phase, use hello <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302279">BizTalk Services: Editions Chart</a> toodetermine if <strong>Premium</strong>, <strong>Standard</strong>, or <strong>Basic</strong> is hello correct choice for your business scenario.</span></span>
    </td>
    </tr>
    <tr>
    <td><span data-ttu-id="e24bf-126"><strong>Região</strong></span><span class="sxs-lookup"><span data-stu-id="e24bf-126"><strong>Region</strong></span></span></td>
    <td><span data-ttu-id="e24bf-127">Selecione Olá região geográfica toohost o BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="e24bf-127">Select hello geographic region toohost your BizTalk Service.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="e24bf-128"><strong>URL do Domínio</strong></span><span class="sxs-lookup"><span data-stu-id="e24bf-128"><strong>Domain URL</strong></span></span></td>
    <td><span data-ttu-id="e24bf-129"><strong>Opcional</strong>.</span><span class="sxs-lookup"><span data-stu-id="e24bf-129"><strong>Optional</strong>.</span></span> <span data-ttu-id="e24bf-130">Por padrão, a URL do domínio Olá é <em>Nomedeseuserviçobiztalk</em>. <yourbiztalkservicename>.BizTalk.Windows.NET.</span><span class="sxs-lookup"><span data-stu-id="e24bf-130">By default, hello domain URL is <em>YourBizTalkServiceName</em>.biztalk.windows.net.</span></span> <span data-ttu-id="e24bf-131">Um domínio personalizado também pode ser inserido.</span><span class="sxs-lookup"><span data-stu-id="e24bf-131">A custom domain can also be entered.</span></span> <span data-ttu-id="e24bf-132">Por exemplo, se seu domínio for <em>contoso</em>, insira:</span><span class="sxs-lookup"><span data-stu-id="e24bf-132">For example, if your domain is <em>contoso</em>, you can enter:</span></span> <br/><br/><span data-ttu-id="e24bf-133">
    <em>MyCompany</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="e24bf-133">
    <em>MyCompany</em>.contoso.com</span></span><br/><span data-ttu-id="e24bf-134">
    <em>MyCompanyMyApplication</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="e24bf-134">
    <em>MyCompanyMyApplication</em>.contoso.com</span></span><br/><span data-ttu-id="e24bf-135">
    <em>MyApplication</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="e24bf-135">
    <em>MyApplication</em>.contoso.com</span></span><br/><span data-ttu-id="e24bf-136">
    <em>YourBizTalkServiceName</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="e24bf-136">
    <em>YourBizTalkServiceName</em>.contoso.com</span></span><br/>
    </td>
    </tr>
    </table>
<span data-ttu-id="e24bf-137">Selecione a seta Avançar hello.</span><span class="sxs-lookup"><span data-stu-id="e24bf-137">Select hello NEXT arrow.</span></span>
<span data-ttu-id="e24bf-138">5.</span><span class="sxs-lookup"><span data-stu-id="e24bf-138">5.</span></span> <span data-ttu-id="e24bf-139">Digite hello armazenamento e as configurações de banco de dados:</span><span class="sxs-lookup"><span data-stu-id="e24bf-139">Enter hello Storage and Database Settings:</span></span>  <table border="1">
    <tr>
    <td><span data-ttu-id="e24bf-140"><strong>Conta de armazenamento de Monitoramento/Arquivamento</strong></span><span class="sxs-lookup"><span data-stu-id="e24bf-140"><strong>Monitoring/Archiving storage account</strong></span></span></td>
    <td><span data-ttu-id="e24bf-141">Selecione uma conta de armazenamento existente ou crie uma nova.</span><span class="sxs-lookup"><span data-stu-id="e24bf-141">Select an existing storage account or create a new storage account.</span></span> <br/><br/><span data-ttu-id="e24bf-142">Se você criar uma nova conta de armazenamento, digite Olá <strong>nome da conta de armazenamento</strong>.</span><span class="sxs-lookup"><span data-stu-id="e24bf-142">If you create a new Storage account, enter hello <strong>Storage Account Name</strong>.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="e24bf-143"><strong>Acompanhamento de banco de dados</strong></span><span class="sxs-lookup"><span data-stu-id="e24bf-143"><strong>Tracking database</strong></span></span></td>
    <td><span data-ttu-id="e24bf-144">Se você usar um banco de dados SQL do Azure, não poderá ser usado por outro Serviço do BizTalk.</span><span class="sxs-lookup"><span data-stu-id="e24bf-144">If you use an existing Azure SQL Database, it cannot be used by another BizTalk Service.</span></span> <span data-ttu-id="e24bf-145">É necessário o nome de logon de saudação e a senha inserida quando esse servidor de banco de dados do SQL Azure foi criada.</span><span class="sxs-lookup"><span data-stu-id="e24bf-145">You need hello login name and password entered when that Azure SQL Database Server was created.</span></span><br/><br/><span data-ttu-id="e24bf-146"><strong>Dica</strong> criar banco de dados de rastreamento de saudação e conta de armazenamento de monitoramento/arquivamento em Olá mesma região como Olá BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="e24bf-146"><strong>TIP</strong> Create hello Tracking database and Monitoring/Archiving storage account in hello same region as hello BizTalk Service.</span></span></td>
    </tr>
    </table>
<span data-ttu-id="e24bf-147">Selecione a seta Avançar hello.</span><span class="sxs-lookup"><span data-stu-id="e24bf-147">Select hello NEXT arrow.</span></span>
<span data-ttu-id="e24bf-148">6.</span><span class="sxs-lookup"><span data-stu-id="e24bf-148">6.</span></span> <span data-ttu-id="e24bf-149">Insira as configurações de banco de dados de saudação:</span><span class="sxs-lookup"><span data-stu-id="e24bf-149">Enter hello Database settings:</span></span>  <table border="1">
    <tr>
    <td><span data-ttu-id="e24bf-150"><strong>Nome</strong></span><span class="sxs-lookup"><span data-stu-id="e24bf-150"><strong>Name</strong></span></span></td>
    <td><span data-ttu-id="e24bf-151">Disponível quando <strong>criar uma nova instância de banco de dados SQL</strong> está selecionado na tela anterior hello.</span><span class="sxs-lookup"><span data-stu-id="e24bf-151">Available when <strong>Create a new SQL Database instance</strong> is selected in hello previous screen.</span></span>
    <br/><br/>
<span data-ttu-id="e24bf-152">Insira um toobe de nome de banco de dados SQL usado pelo seu BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="e24bf-152">Enter a SQL Database name toobe used by your BizTalk Service.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="e24bf-153"><strong>Servidor</strong></span><span class="sxs-lookup"><span data-stu-id="e24bf-153"><strong>Server</strong></span></span></td>
    <td><span data-ttu-id="e24bf-154">Disponível quando <strong>criar uma nova instância de banco de dados SQL</strong> está selecionado na tela anterior hello.</span><span class="sxs-lookup"><span data-stu-id="e24bf-154">Available when <strong>Create a new SQL Database instance</strong> is selected in hello previous screen.</span></span>
    <br/><br/>
<span data-ttu-id="e24bf-155">Selecione um Servidor de Banco de Dados SQL ou crie um novo servidor de Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="e24bf-155">Select an existing SQL Database Server or create a new SQL Database server.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="e24bf-156"><strong>Nome de logon do servidor</strong></span><span class="sxs-lookup"><span data-stu-id="e24bf-156"><strong>Server login name</strong></span></span></td>
    <td><span data-ttu-id="e24bf-157">Digite o nome de usuário de logon de saudação.</span><span class="sxs-lookup"><span data-stu-id="e24bf-157">Enter hello login user name.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="e24bf-158"><strong>Senha de logon do servidor</strong></span><span class="sxs-lookup"><span data-stu-id="e24bf-158"><strong>Server login password</strong></span></span></td>
    <td><span data-ttu-id="e24bf-159">Insira a senha de logon de saudação.</span><span class="sxs-lookup"><span data-stu-id="e24bf-159">Enter hello login password.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="e24bf-160"><strong>Região</strong></span><span class="sxs-lookup"><span data-stu-id="e24bf-160"><strong>Region</strong></span></span></td>
    <td><span data-ttu-id="e24bf-161">Disponível quando a opção <strong>Criar uma nova instância do Banco de Dados SQL</strong> é selecionada.</span><span class="sxs-lookup"><span data-stu-id="e24bf-161">Available when <strong>Create a new SQL Database instance</strong> is selected.</span></span> <span data-ttu-id="e24bf-162">Selecione Olá região geográfica toohost seu banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="e24bf-162">Select hello geographic region toohost your SQL Database.</span></span></td>
    </tr>
    </table>

<span data-ttu-id="e24bf-163">Selecione Olá marca de seleção toocomplete Olá assistente.</span><span class="sxs-lookup"><span data-stu-id="e24bf-163">Select hello check mark toocomplete hello wizard.</span></span> <span data-ttu-id="e24bf-164">Olá progresso ícone será exibido:</span><span class="sxs-lookup"><span data-stu-id="e24bf-164">hello progress icon appears:</span></span>  
![O ícone de progresso é exibido após a conclusão][ProgressComplete]

<span data-ttu-id="e24bf-166">Ao concluir, Olá serviço BizTalk do Azure é criado e está pronto para seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="e24bf-166">When complete, hello Azure BizTalk Service is created and ready for your applications.</span></span> <span data-ttu-id="e24bf-167">as configurações padrão de saudação são suficientes.</span><span class="sxs-lookup"><span data-stu-id="e24bf-167">hello default settings are sufficient.</span></span> <span data-ttu-id="e24bf-168">Se quiser que as configurações padrão de saudação toochange, selecione **serviços BIZTALK** Olá painel de navegação esquerdo e, em seguida, selecione o BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="e24bf-168">If you want toochange hello default settings, select **BIZTALK SERVICES** in hello left navigation pane, and then select your BizTalk Service.</span></span> <span data-ttu-id="e24bf-169">Configurações adicionais são exibidas em Olá [guias painel, monitorar e escala](biztalk-dashboard-monitor-scale-tabs.md) na parte superior da saudação.</span><span class="sxs-lookup"><span data-stu-id="e24bf-169">Additional settings are displayed in hello [Dashboard, Monitor, and Scale tabs](biztalk-dashboard-monitor-scale-tabs.md) at hello top.</span></span>

<span data-ttu-id="e24bf-170">Dependendo do estado de saudação do hello BizTalk Service, existem algumas operações que não podem ser concluídas.</span><span class="sxs-lookup"><span data-stu-id="e24bf-170">Depending on hello state of hello BizTalk Service, there are some operations that cannot be completed.</span></span> <span data-ttu-id="e24bf-171">Para obter uma lista dessas operações, vá muito[gráfico de estado dos serviços do BizTalk](biztalk-service-state-chart.md).</span><span class="sxs-lookup"><span data-stu-id="e24bf-171">For a list of these operations, go too[BizTalk Services State Chart](biztalk-service-state-chart.md).</span></span>

## <a name="post-provisioning-steps"></a><span data-ttu-id="e24bf-172">Etapas pós-provisionamento</span><span class="sxs-lookup"><span data-stu-id="e24bf-172">Post-provisioning steps</span></span>
* [<span data-ttu-id="e24bf-173">Instalar o certificado de saudação em um computador local</span><span class="sxs-lookup"><span data-stu-id="e24bf-173">Install hello certificate on a local computer</span></span>](#InstallCert)
* [<span data-ttu-id="e24bf-174">Adicionar um certificado pronto para produção</span><span class="sxs-lookup"><span data-stu-id="e24bf-174">Add a production-ready certificate</span></span>](#AddCert)
* [<span data-ttu-id="e24bf-175">Obter o namespace do Access Control Olá</span><span class="sxs-lookup"><span data-stu-id="e24bf-175">Get hello Access Control namespace</span></span>](#ACS)

#### <span data-ttu-id="e24bf-176"><a name="InstallCert"></a>Instalar o certificado de saudação em um computador local</span><span class="sxs-lookup"><span data-stu-id="e24bf-176"><a name="InstallCert"></a>Install hello certificate on a local computer</span></span>
<span data-ttu-id="e24bf-177">Como parte do provisionamento do Serviço do BizTalk, um certificado autoassinado é criado e associado com a assinatura do seu serviço do BizTalk.</span><span class="sxs-lookup"><span data-stu-id="e24bf-177">As part of BizTalk Service provisioning, a self-signed certificate is created and associated with your BizTalk Service subscription.</span></span> <span data-ttu-id="e24bf-178">Você deve baixar o certificado e instalá-lo em computadores em que você implante aplicativos do BizTalk Service ou envia mensagens tooa ponto de extremidade do BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="e24bf-178">You must download this certificate and install it on computers from where you either deploy BizTalk Service applications or send messages tooa BizTalk Service endpoint.</span></span>

1. <span data-ttu-id="e24bf-179">Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="e24bf-179">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="e24bf-180">Selecione **serviços BIZTALK** Olá painel de navegação esquerdo e, em seguida, selecione sua assinatura do BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="e24bf-180">Select **BIZTALK SERVICES** in hello left navigation pane, and then select your BizTalk Service subscription.</span></span>
3. <span data-ttu-id="e24bf-181">Selecione Olá **painel** guia.</span><span class="sxs-lookup"><span data-stu-id="e24bf-181">Select hello **Dashboard** tab.</span></span>
4. <span data-ttu-id="e24bf-182">Selecione **Baixar Certificado SSL**:</span><span class="sxs-lookup"><span data-stu-id="e24bf-182">Select **Download SSL Certificate**:</span></span>  
   <span data-ttu-id="e24bf-183">![Modificar certificado SSL][QuickGlance]</span><span class="sxs-lookup"><span data-stu-id="e24bf-183">![Modify SSL Certificate][QuickGlance]</span></span>
5. <span data-ttu-id="e24bf-184">Clique duas vezes no certificado hello e execute através do certificado de Olá Olá Assistente tooinstall.</span><span class="sxs-lookup"><span data-stu-id="e24bf-184">Double-click hello certificate and run through hello wizard tooinstall hello certificate.</span></span> <span data-ttu-id="e24bf-185">Verifique se você instalou o certificado de saudação sob Olá **autoridades de certificação raiz confiáveis** armazenar.</span><span class="sxs-lookup"><span data-stu-id="e24bf-185">Make sure you install hello certificate under hello **Trusted Root Certificate Authorities** store.</span></span>

#### <span data-ttu-id="e24bf-186"><a name="AddCert"></a>Adicionar um certificado pronto para produção</span><span class="sxs-lookup"><span data-stu-id="e24bf-186"><a name="AddCert"></a>Add a production-ready certificate</span></span>
<span data-ttu-id="e24bf-187">certificado autoassinado Olá que é criado automaticamente quando a criação de Serviços BizTalk é destinado ao uso em ambientes de desenvolvimento somente.</span><span class="sxs-lookup"><span data-stu-id="e24bf-187">hello self-signed certificate that is automatically created when creating BizTalk Services is intended for use in development environments only.</span></span> <span data-ttu-id="e24bf-188">Para cenários de produção, substitua-o por um certificado pronto para produção.</span><span class="sxs-lookup"><span data-stu-id="e24bf-188">For production scenarios, replace it with a production-ready certificate.</span></span>

1. <span data-ttu-id="e24bf-189">Em Olá **painel** guia, selecione **certificado de SSL da atualização**.</span><span class="sxs-lookup"><span data-stu-id="e24bf-189">On hello **Dashboard** tab, select **Update SSL Certificate**.</span></span>
2. <span data-ttu-id="e24bf-190">Procurar o certificado SSL privado tooyour (*CertificateName*. pfx) que inclui o nome do BizTalk Service, digite a senha de saudação e clique em marca de seleção de saudação.</span><span class="sxs-lookup"><span data-stu-id="e24bf-190">Browse tooyour private SSL certificate (*CertificateName*.pfx) that includes your BizTalk Service name, enter hello password, and then click hello check mark.</span></span>

#### <span data-ttu-id="e24bf-191"><a name="ACS"></a>Obter o namespace do Access Control Olá</span><span class="sxs-lookup"><span data-stu-id="e24bf-191"><a name="ACS"></a>Get hello Access Control namespace</span></span>
1. <span data-ttu-id="e24bf-192">Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="e24bf-192">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="e24bf-193">Selecione **serviços BIZTALK** Olá painel de navegação esquerdo e, em seguida, selecione o BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="e24bf-193">Select **BIZTALK SERVICES** in hello left navigation pane, and then select your BizTalk Service.</span></span>
3. <span data-ttu-id="e24bf-194">Na barra de tarefas hello, selecione **informações de Conexão**:</span><span class="sxs-lookup"><span data-stu-id="e24bf-194">In hello task bar, select **Connection Information**:</span></span>  
   <span data-ttu-id="e24bf-195">![Selecionar Informações de conexão][ACSConnectInfo]</span><span class="sxs-lookup"><span data-stu-id="e24bf-195">![Select Connection Information][ACSConnectInfo]</span></span>
4. <span data-ttu-id="e24bf-196">Copie os valores de controle de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="e24bf-196">Copy hello Access Control values.</span></span>

<span data-ttu-id="e24bf-197">Ao implantar um projeto do Serviço BizTalk no Visual Studio, você insere esse namespace do Controle de Acesso.</span><span class="sxs-lookup"><span data-stu-id="e24bf-197">When you deploy a BizTalk Service project from Visual Studio, you enter this Access Control namespace.</span></span> <span data-ttu-id="e24bf-198">Olá namespace de controle de acesso é automaticamente criado para o BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="e24bf-198">hello Access Control namespace is automatically created for your BizTalk Service.</span></span>

<span data-ttu-id="e24bf-199">valores de controle de acesso de saudação podem ser usados com qualquer aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e24bf-199">hello Access Control values can be used with any application.</span></span> <span data-ttu-id="e24bf-200">Quando os Serviços BizTalk do Azure é criado, esse namespace de controle de acesso controla autenticação Olá com a implantação do BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="e24bf-200">When Azure BizTalk Services is created, this Access Control namespace controls hello authentication with your BizTalk Service deployment.</span></span> <span data-ttu-id="e24bf-201">Se você quiser toochange Olá assinatura ou gerenciar namespace hello, selecione **do ACTIVE DIRECTORY** Olá painel de navegação esquerdo e, em seguida, selecione seu namespace.</span><span class="sxs-lookup"><span data-stu-id="e24bf-201">If you want toochange hello subscription or manage hello namespace, select **ACTIVE DIRECTORY** in hello left navigation pane and then select your namespace.</span></span> <span data-ttu-id="e24bf-202">barra de tarefas Olá lista as opções.</span><span class="sxs-lookup"><span data-stu-id="e24bf-202">hello task bar lists your options.</span></span>

<span data-ttu-id="e24bf-203">Clicando em **gerenciar** abre Olá Portal de gerenciamento de controle de acesso.</span><span class="sxs-lookup"><span data-stu-id="e24bf-203">Clicking **Manage** opens hello Access Control Management Portal.</span></span> <span data-ttu-id="e24bf-204">No Portal de gerenciamento de controle de acesso do hello, Olá usa o BizTalk Service **identidades de serviço**:</span><span class="sxs-lookup"><span data-stu-id="e24bf-204">In hello Access Control Management Portal, hello BizTalk Service uses **Service identities**:</span></span>  
<span data-ttu-id="e24bf-205">![Identidades de serviço do ACS no Portal de gerenciamento de controle de acesso de saudação][ACSServiceIdentities]</span><span class="sxs-lookup"><span data-stu-id="e24bf-205">![ACS Service Identities in hello Access Control Management Portal][ACSServiceIdentities]</span></span>

<span data-ttu-id="e24bf-206">Olá identidade de serviço de controle de acesso é um conjunto de credenciais que permitem que aplicativos ou clientes tooauthenticate diretamente com o controle de acesso e receber um token.</span><span class="sxs-lookup"><span data-stu-id="e24bf-206">hello Access Control service identity is a set of credentials that allow applications or clients tooauthenticate directly with Access Control and receive a token.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e24bf-207">Olá BizTalk Service usa **proprietário** para identidade de serviço padrão hello e hello **senha** valor.</span><span class="sxs-lookup"><span data-stu-id="e24bf-207">hello BizTalk Service uses **Owner** for hello default service identity and hello **Password** value.</span></span> <span data-ttu-id="e24bf-208">Se você usar o valor de chave simétrica de saudação em vez da saudação valor da senha, hello seguinte erro poderá ocorrer.</span><span class="sxs-lookup"><span data-stu-id="e24bf-208">If you use hello Symmetric Key value instead of hello Password value, hello following error may occur.</span></span><br/><br/><span data-ttu-id="e24bf-209">*Não foi possível conectar a conta de serviço de gerenciamento de controle de acesso de toohello com hello especificado credenciais*</span><span class="sxs-lookup"><span data-stu-id="e24bf-209">*Could not connect toohello Access Control Management Service account with hello specified credentials*</span></span>
> 
> 

<span data-ttu-id="e24bf-210">[Gerenciando o namespace de seu ACS](https://msdn.microsoft.com/library/azure/hh674478.aspx) lista algumas diretrizes e recomendações.</span><span class="sxs-lookup"><span data-stu-id="e24bf-210">[Managing Your ACS Namespace](https://msdn.microsoft.com/library/azure/hh674478.aspx) lists some guidelines and recommendations.</span></span>

## <a name="requirements-explained"></a><span data-ttu-id="e24bf-211">Requisitos explicados</span><span class="sxs-lookup"><span data-stu-id="e24bf-211">Requirements explained</span></span>
<span data-ttu-id="e24bf-212">Esses requisitos não se aplicam a toohello edição gratuita.</span><span class="sxs-lookup"><span data-stu-id="e24bf-212">These requirements do not apply toohello Free Edition.</span></span>

<table border="1">
<tr bgcolor="FAF9F9">
        <td><span data-ttu-id="e24bf-213"><strong>O que você precisa</strong></span><span class="sxs-lookup"><span data-stu-id="e24bf-213"><strong>What you need</strong></span></span></td>
        <td><span data-ttu-id="e24bf-214"><strong>Por que você precisa disto</strong></span><span class="sxs-lookup"><span data-stu-id="e24bf-214"><strong>Why you need it</strong></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="e24bf-215">Assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="e24bf-215">Azure subscription</span></span></td>
<td><span data-ttu-id="e24bf-216">assinatura de saudação determina quem pode entrar toohello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e24bf-216">hello subscription determines who can sign in toohello Azure portal.</span></span> <span data-ttu-id="e24bf-217">proprietário de conta Olá cria a assinatura de saudação em <a HREF="https://account.windowsazure.com/Subscriptions"> assinaturas do Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="e24bf-217">hello Account holder creates hello subscription at <a HREF="https://account.windowsazure.com/Subscriptions"> Azure Subscriptions</a>.</span></span>
<br/><br/>
<span data-ttu-id="e24bf-218">Olá conta do Azure pode ter várias assinaturas e pode ser gerenciada por qualquer pessoa que é permitido.</span><span class="sxs-lookup"><span data-stu-id="e24bf-218">hello Azure account can have multiple subscriptions and can be managed by anyone who is permitted.</span></span> <span data-ttu-id="e24bf-219">Por exemplo, o proprietário de conta do Azure cria uma assinatura chamada <em>BizTalkServiceSubscription</em> e fornece Olá administradores do BizTalk dentro da sua empresa (por exemplo, ContosoBTSAdmins@live.com) toothis assinatura de acesso.</span><span class="sxs-lookup"><span data-stu-id="e24bf-219">For example, your Azure account holder creates a subscription named <em>BizTalkServiceSubscription</em> and gives hello BizTalk Administrators within your company (for example, ContosoBTSAdmins@live.com) access toothis subscription.</span></span> <span data-ttu-id="e24bf-220">Nesse cenário, administradores do BizTalk Olá entrar toohello portal do Azure e ter serviços completos de administrador direitos tooall Olá hospedado na assinatura de hello, incluindo Serviços BizTalk do Azure.</span><span class="sxs-lookup"><span data-stu-id="e24bf-220">In this scenario, hello BizTalk Administrators sign in toohello Azure portal and have full Administrator rights tooall hello hosted services in hello subscription, including Azure BizTalk Services.</span></span> <span data-ttu-id="e24bf-221">Administradores do BizTalk Olá não são proprietários da conta do Azure de saudação e, portanto, não tem acesso tooany as informações de cobrança.</span><span class="sxs-lookup"><span data-stu-id="e24bf-221">hello BizTalk Administrators are not hello Azure account holders and therefore don't have access tooany billing information.</span></span>
<br/><br/><span data-ttu-id="e24bf-222">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=267577">Gerenciar assinaturas e contas de armazenamento no portal do Azure de saudação</a> fornece mais informações.</span><span class="sxs-lookup"><span data-stu-id="e24bf-222">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=267577"> Manage Subscriptions and Storage Accounts in hello Azure portal</a> provides more information.</span></span>
</td>
</tr>
<tr>
<td><span data-ttu-id="e24bf-223">Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="e24bf-223">Azure SQL Database</span></span></td>
<td><span data-ttu-id="e24bf-224">Armazena Olá tabelas, exibições e procedimentos armazenados usados pelo Olá BizTalk Service, incluindo dados de controle de saudação.</span><span class="sxs-lookup"><span data-stu-id="e24bf-224">Stores hello tables, views, and stored procedures used by hello BizTalk Service, including hello Tracking data.</span></span>
<br/><br/>
<span data-ttu-id="e24bf-225">Ao criar um Serviço BizTalk, você pode usar um SQL Server do Azure ou um Banco de Dados SQL do Azure ou criar automaticamente um novo servidor ou banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e24bf-225">When you create a BizTalk Service, you can use an existing Azure SQL Server, Azure SQL Database, or automatically create a new Server or Database.</span></span>
<br/><br/>
<span data-ttu-id="e24bf-226">Olá escala de banco de dados SQL é configurado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e24bf-226">hello SQL Database scale is automatically configured.</span></span> <span data-ttu-id="e24bf-227">Normalmente, a escala do saudação padrão é suficiente para um BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="e24bf-227">Typically, hello default scale is sufficient for a BizTalk Service.</span></span> <span data-ttu-id="e24bf-228">Escala de saudação alteração afeta o preço.</span><span class="sxs-lookup"><span data-stu-id="e24bf-228">Changing hello scale impacts pricing.</span></span> <span data-ttu-id="e24bf-229">Confira <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=234930">Contas e faturamento no banco de dados SQL do Azure</a>
</span><span class="sxs-lookup"><span data-stu-id="e24bf-229">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=234930"> Accounts and Billing in Azure SQL Database</a>
</span></span><br/><br/><span data-ttu-id="e24bf-230">
<strong>Observações</strong>
</span><span class="sxs-lookup"><span data-stu-id="e24bf-230">
<strong>Notes</strong>
</span></span><br/>
<ul>
<li> <span data-ttu-id="e24bf-231">Quando você criar um novo SQL Server e Banco de Dados do Azure, os Serviços do Azure são habilitados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e24bf-231">When you create a new Azure SQL Server and Database, Azure Services is automatically enabled.</span></span> <span data-ttu-id="e24bf-232">Olá BizTalk Service requer os serviços do Azure ser habilitado.</span><span class="sxs-lookup"><span data-stu-id="e24bf-232">hello BizTalk Service requires Azure Services be enabled.</span></span></li>
<li><span data-ttu-id="e24bf-233">Se você criar um novo banco de dados SQL em um servidor existente do SQL Azure, Olá regras de firewall do hello Server não são alterados.</span><span class="sxs-lookup"><span data-stu-id="e24bf-233">If you create a new Azure SQL Database on an existing Azure SQL Server, hello firewall rules of hello Server are not changed.</span></span> <span data-ttu-id="e24bf-234">Como resultado, é possível de que outros serviços do Azure não são permitidos para bancos de dados do servidor de acesso toohello.</span><span class="sxs-lookup"><span data-stu-id="e24bf-234">As a result, it's possible other Azure Services are not allowed access toohello Server's databases.</span></span></li>
</ul>
</td>
</tr>
<tr>
<td><span data-ttu-id="e24bf-235">Namespace do Controle de Acesso do Azure</span><span class="sxs-lookup"><span data-stu-id="e24bf-235">Azure Access Control namespace</span></span></td>
<td><span data-ttu-id="e24bf-236">Autenticados com os Serviços do BizTalk do Azure.</span><span class="sxs-lookup"><span data-stu-id="e24bf-236">Authenticates with Azure BizTalk Services.</span></span> <span data-ttu-id="e24bf-237">Ao implantar um projeto do Serviço BizTalk no Visual Studio, você insere esse namespace do Controle de Acesso.</span><span class="sxs-lookup"><span data-stu-id="e24bf-237">When you deploy a BizTalk Service project from Visual Studio, you enter this Access Control namespace.</span></span> <span data-ttu-id="e24bf-238">Quando você cria um BizTalk Service, Olá namespace de controle de acesso é criado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e24bf-238">When you create a BizTalk Service, hello Access Control namespace is automatically created.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="e24bf-239">Conta de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="e24bf-239">Azure Storage account</span></span></td>
<td><span data-ttu-id="e24bf-240">Fornece acesso tootables, blobs e filas usadas pelo seu seguinte de saudação do BizTalk Service toosave:</span><span class="sxs-lookup"><span data-stu-id="e24bf-240">Gives access tootables, blobs, and queues used by your BizTalk Service toosave hello following:</span></span>

<ul>
<li><span data-ttu-id="e24bf-241">Os arquivos de log que Olá monitor BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="e24bf-241">Log files that monitor hello BizTalk Service.</span></span> <span data-ttu-id="e24bf-242">Olá monitoramento saída também é exibida no hello **monitoramento** guia Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e24bf-242">hello monitoring output is also displayed in hello **Monitoring** tab in hello Azure portal.</span></span></li>
<li><span data-ttu-id="e24bf-243">Ao criar um X12 ou AS2 acordo entre parceiros, você pode habilitar as propriedades de mensagem do hello arquivamento recurso toostore.</span><span class="sxs-lookup"><span data-stu-id="e24bf-243">When creating an X12 or AS2 agreement between partners, you can enable hello Archiving feature toostore message properties.</span></span> <span data-ttu-id="e24bf-244">Esses dados são salvos no hello conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e24bf-244">This data is saved in hello Storage account.</span></span></li>
</ul>
<br/>
<span data-ttu-id="e24bf-245">Ao criar um Serviço BizTalk, você pode usar uma conta de Armazenamento existente ou criar automaticamente uma nova conta de Armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e24bf-245">When you create a BizTalk Service, you can use an existing Storage account or automatically create a new Storage account.</span></span>
<br/><br/>
<span data-ttu-id="e24bf-246">configurações de armazenamento saudação padrão são suficientes para um BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="e24bf-246">hello default Storage settings are sufficient for a BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="e24bf-247">Quando você cria uma Conta de Armazenamento, uma chave primária e uma chave secundária são criadas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e24bf-247">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="e24bf-248">Essas chaves controlam acesso tooyour conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e24bf-248">These Keys control access tooyour Storage account.</span></span> <span data-ttu-id="e24bf-249">Olá BizTalk Service usa automaticamente Olá chave primária.</span><span class="sxs-lookup"><span data-stu-id="e24bf-249">hello BizTalk Service automatically uses hello Primary Key.</span></span>
<br/><br/>
<span data-ttu-id="e24bf-250">Consulte <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285671">Armazenamento</a> para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="e24bf-250">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285671"> Storage</a> for more information.</span></span>
</td>
</tr>

<tr>
<td><span data-ttu-id="e24bf-251">Certificado SSL privado</span><span class="sxs-lookup"><span data-stu-id="e24bf-251">SSL private certificate</span></span></td>
<td>
<span data-ttu-id="e24bf-252">Quando um Serviço do BizTalk do Azure for criado, uma URL HTTPS que inclui o nome do seu Serviço do BizTalk também é criado.</span><span class="sxs-lookup"><span data-stu-id="e24bf-252">When an Azure BizTalk Service is created, an HTTPS URL that includes your BizTalk Service name is also created.</span></span> <span data-ttu-id="e24bf-253">Essa URL é toouse configurada automaticamente um certificado autoassinado somente para desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="e24bf-253">This URL is automatically configured toouse a self-signed development-only certificate.</span></span> <span data-ttu-id="e24bf-254">Para produção, você necessita um certificado SSL privado.</span><span class="sxs-lookup"><span data-stu-id="e24bf-254">For production, you need a private SSL certificate.</span></span>
<br/><br/><span data-ttu-id="e24bf-255">
<strong>Informações importantes sobre o Certificado SSL</strong>

</span><span class="sxs-lookup"><span data-stu-id="e24bf-255">
<strong>Important SSL Certificate Information</strong>

</span></span><ul>
<li><span data-ttu-id="e24bf-256">Data de validade do certificado Olá deve ser inferior a 5 anos.</span><span class="sxs-lookup"><span data-stu-id="e24bf-256">hello certificate expiration date must be less than 5 years.</span></span></li>
<li><span data-ttu-id="e24bf-257">Todos os certificados privados exigem uma senha.</span><span class="sxs-lookup"><span data-stu-id="e24bf-257">All private certificates require a password.</span></span> <span data-ttu-id="e24bf-258">Saiba essa senha e, como uma prática recomendada, compartilhe essa senha com seus administradores.</span><span class="sxs-lookup"><span data-stu-id="e24bf-258">Know this password and as a best practice, share this password with your administrators.</span></span></li>
<li><span data-ttu-id="e24bf-259">Os certificados autoassinados são usados em um ambientes de desenvolvimento/teste.</span><span class="sxs-lookup"><span data-stu-id="e24bf-259">Self-signed certificates are used in a test/development environment.</span></span> <span data-ttu-id="e24bf-260">Ao usar certificados autoassinados, importar o repositório de certificados pessoais do hello certificado tooyour e Olá repositório de certificados de autoridades de certificação raiz confiáveis.</span><span class="sxs-lookup"><span data-stu-id="e24bf-260">When using self-signed certificates, import hello certificate tooyour Personal certificate store and hello Trusted Root Certification Authorities certificate store.</span></span></li>
</ul>
<br/><span data-ttu-id="e24bf-261">Ao enviar a autoridade de certificação tooyour do solicitação de certificado de produção hello, dar Olá propriedades do certificado a seguir:</span><span class="sxs-lookup"><span data-stu-id="e24bf-261">When sending hello production certificate request tooyour certification authority, give hello following certificate properties:</span></span>
<br/>

<ul>
<li><span data-ttu-id="e24bf-262"><strong>Uso avançado de chave</strong>: no mínimo, os Serviços BizTalk do Azure exigem a Autenticação de Servidor.</span><span class="sxs-lookup"><span data-stu-id="e24bf-262"><strong>Enhanced Key Usage</strong>: At a minimum, Azure BizTalk Services requires Server Authentication.</span></span></li>
<li><span data-ttu-id="e24bf-263"><strong>Nome comum</strong>: insira o nome de domínio totalmente qualificado (FQDN) Olá de sua URL do serviço BizTalk do Azure.</span><span class="sxs-lookup"><span data-stu-id="e24bf-263"><strong>Common Name</strong>: Enter hello fully qualified domain name (FQDN) of your Azure BizTalk Service URL.</span></span> <span data-ttu-id="e24bf-264">Veja <a HREF="#CreateService">Criar um Serviço BizTalk</a> neste artigo.</span><span class="sxs-lookup"><span data-stu-id="e24bf-264">See <a HREF="#CreateService">Create a BizTalk Service</a> in this article.</span></span></li>
</ul>
<br/>
<span data-ttu-id="e24bf-265">Pode ser adicionado a um certificado novo ou diferente depois Olá BizTalk Service é criado.</span><span class="sxs-lookup"><span data-stu-id="e24bf-265">A new or different certificate can be added after hello BizTalk Service is created.</span></span>
</td>
</tr>
</table>
<!---Loc Comment: Please, check link [Create a BizTalk Service] since it is not redirecting tooany location.--->



## <a name="hybrid-connections"></a><span data-ttu-id="e24bf-266">Conexões Híbridas</span><span class="sxs-lookup"><span data-stu-id="e24bf-266">Hybrid Connections</span></span>
<span data-ttu-id="e24bf-267">Quando você cria um serviço de BizTalk do Azure, Olá **conexões híbridas** guia está disponível:</span><span class="sxs-lookup"><span data-stu-id="e24bf-267">When you create an Azure BizTalk Service, hello **Hybrid Connections** tab is available:</span></span>

![Guia de Conexões Híbridas][HybridConnectionTab]

<span data-ttu-id="e24bf-269">Conexões híbridas são usada tooconnect do Azure site ou serviço móvel do Azure tooany local recursos que usa uma porta TCP estática, como SQL Server, MySQL, APIs da Web de HTTP, os serviços móveis e a maioria dos serviços da Web personalizados.</span><span class="sxs-lookup"><span data-stu-id="e24bf-269">Hybrid Connections are used tooconnect an Azure website or Azure mobile service tooany on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, Mobile Services, and most custom Web Services.</span></span>  <span data-ttu-id="e24bf-270">Conexões híbridas e hello serviço de adaptador do BizTalk são diferentes.</span><span class="sxs-lookup"><span data-stu-id="e24bf-270">Hybrid Connections and hello BizTalk Adapter Service are different.</span></span> <span data-ttu-id="e24bf-271">Olá serviço de adaptador BizTalk é usado tooconnect Serviços BizTalk do Azure tooan no sistema local da linha de negócios (LOB).</span><span class="sxs-lookup"><span data-stu-id="e24bf-271">hello BizTalk Adapter Service is used tooconnect Azure BizTalk Services tooan on-premises Line of Business (LOB) system.</span></span>

 <span data-ttu-id="e24bf-272">Consulte [conexões híbridas](integration-hybrid-connection-overview.md) toolearn mais, incluindo a criação e gerenciamento de conexões híbridas.</span><span class="sxs-lookup"><span data-stu-id="e24bf-272">See [Hybrid Connections](integration-hybrid-connection-overview.md) toolearn more, including creating and managing Hybrid Connections.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e24bf-273">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e24bf-273">Next steps</span></span>
<span data-ttu-id="e24bf-274">Agora que um BizTalk Service foi criada, você se familiarizar com hello diferente [Serviços BizTalk: guias painel, monitorar e escala](biztalk-dashboard-monitor-scale-tabs.md).</span><span class="sxs-lookup"><span data-stu-id="e24bf-274">Now that a BizTalk Service is created, familiarize yourself with hello different [BizTalk Services: Dashboard, Monitor and Scale tabs](biztalk-dashboard-monitor-scale-tabs.md).</span></span> <span data-ttu-id="e24bf-275">Seu Serviço BizTalk está pronto para os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="e24bf-275">Your BizTalk Service is ready for your applications.</span></span> <span data-ttu-id="e24bf-276">toostart criação de aplicativos, vá muito[Serviços BizTalk do Azure](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span><span class="sxs-lookup"><span data-stu-id="e24bf-276">toostart creating applications, go too[Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span></span>

## <a name="see-also"></a><span data-ttu-id="e24bf-277">Consulte também</span><span class="sxs-lookup"><span data-stu-id="e24bf-277">See also</span></span>
* [<span data-ttu-id="e24bf-278">Serviços BizTalk: gráfico de edições</span><span class="sxs-lookup"><span data-stu-id="e24bf-278">BizTalk Services: Editions Chart</span></span>](biztalk-editions-feature-chart.md)<br/>
* [<span data-ttu-id="e24bf-279">Serviços BizTalk: gráfico de estado</span><span class="sxs-lookup"><span data-stu-id="e24bf-279">BizTalk Services: State Chart</span></span>](biztalk-service-state-chart.md)<br/>
* [<span data-ttu-id="e24bf-280">Serviços BizTalk: backup e restauração</span><span class="sxs-lookup"><span data-stu-id="e24bf-280">BizTalk Services: Backup and Restore</span></span>](biztalk-backup-restore.md)<br/>
* [<span data-ttu-id="e24bf-281">Serviços BizTalk: limitação</span><span class="sxs-lookup"><span data-stu-id="e24bf-281">BizTalk Services: Throttling</span></span>](biztalk-throttling-thresholds.md)<br/>
* [<span data-ttu-id="e24bf-282">Serviços BizTalk: nome e chave do emissor</span><span class="sxs-lookup"><span data-stu-id="e24bf-282">BizTalk Services: Issuer Name and Issuer Key</span></span>](biztalk-issuer-name-issuer-key.md)<br/>
* [<span data-ttu-id="e24bf-283">Como posso começar a usar Olá SDK dos Serviços BizTalk do Azure</span><span class="sxs-lookup"><span data-stu-id="e24bf-283">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="e24bf-284">Conexões híbridas</span><span class="sxs-lookup"><span data-stu-id="e24bf-284">Hybrid Connections</span></span>](integration-hybrid-connection-overview.md)

[NewBizTalkService]: ./media/biztalk-provision-services/WABS_NewBizTalkService.png
[NEWButton]: ./media/biztalk-provision-services/WABS_New.png
[ProgressComplete]: ./media/biztalk-provision-services/WABS_ProgressComplete.png
[ACSConnectInfo]: ./media/biztalk-provision-services/WABS_ACSConnectInformation.png
[QuickGlance]: ./media/biztalk-provision-services/WABS_QuickGlance.png
[ACSServiceIdentities]: ./media/biztalk-provision-services/WABS_ACSServiceIdentities.png
[HybridConnectionTab]: ./media/biztalk-provision-services/WABS_HybridConnectionTab.png
