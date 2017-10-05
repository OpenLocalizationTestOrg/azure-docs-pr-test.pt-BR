---
title: "Criar Serviços BizTalk do Azure no Portal do Azure | Microsoft Docs"
description: "Saiba como provisionar ou criar Serviços BizTalk no Portal do Azure; MABS, WABS"
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
ms.openlocfilehash: eca77b4a82eb67e1755717bb4429f8d450a64dc5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-biztalk-services-using-the-azure-portal"></a><span data-ttu-id="57f02-103">Criar Serviços BizTalk usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="57f02-103">Create BizTalk Services using the Azure portal</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]


> [!TIP]
> <span data-ttu-id="57f02-104">Para entrar no Portal do Azure, você precisa de uma conta e de uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="57f02-104">To sign in to the Azure portal, you need an Azure account and Azure subscription.</span></span> <span data-ttu-id="57f02-105">Se você não tiver uma conta, será possível criar uma conta de avaliação gratuita em questão de minutos.</span><span class="sxs-lookup"><span data-stu-id="57f02-105">If you don't have an account, you can create a free trial account within a few minutes.</span></span> <span data-ttu-id="57f02-106">Consulte [Avaliação gratuita do Azure](http://go.microsoft.com/fwlink/p/?LinkID=239738).</span><span class="sxs-lookup"><span data-stu-id="57f02-106">See [Azure Free Trial](http://go.microsoft.com/fwlink/p/?LinkID=239738).</span></span>


## <span data-ttu-id="57f02-107"><a name="CreateService"></a>Criar um Serviço do BizTalk</span><span class="sxs-lookup"><span data-stu-id="57f02-107"><a name="CreateService"></a>Create a BizTalk Service</span></span>
<span data-ttu-id="57f02-108">Dependendo da Edição que você escolher, será possível que não todas as configurações de Serviço do BizTalk estejam disponíveis.</span><span class="sxs-lookup"><span data-stu-id="57f02-108">Depending on the Edition you choose, not all BizTalk Service settings may be available.</span></span>

1. <span data-ttu-id="57f02-109">Entre no [Portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="57f02-109">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="57f02-110">Na parte inferior do painel de navegação, selecione **NOVO**:</span><span class="sxs-lookup"><span data-stu-id="57f02-110">In the bottom navigation pane, select **NEW**:</span></span>  
   <span data-ttu-id="57f02-111">![Selecionar o botão Novo][NEWButton]</span><span class="sxs-lookup"><span data-stu-id="57f02-111">![Select the New button][NEWButton]</span></span>
3. <span data-ttu-id="57f02-112">Selecione **SERVIÇOS DE APLICATIVOS** > **SERVIÇO BIZTALK** > **CRIAÇÃO PERSONALIZADA**:</span><span class="sxs-lookup"><span data-stu-id="57f02-112">Select **APP SERVICES** > **BIZTALK SERVICE** > **CUSTOM CREATE**:</span></span>  
   <span data-ttu-id="57f02-113">![Selecionar Serviço BizTalk e Criação Personalizada][NewBizTalkService]</span><span class="sxs-lookup"><span data-stu-id="57f02-113">![Select BizTalk Service and select Custom Create][NewBizTalkService]</span></span>
4. <span data-ttu-id="57f02-114">Insira as configurações do Serviço BizTalk:</span><span class="sxs-lookup"><span data-stu-id="57f02-114">Enter the BizTalk Service settings:</span></span>
   
    <table border="1">
    <tr>
    <td><span data-ttu-id="57f02-115"><strong>Nome do Serviço BizTalk</strong></span><span class="sxs-lookup"><span data-stu-id="57f02-115"><strong>BizTalk service name</strong></span></span></td>
    <td><span data-ttu-id="57f02-116">Você pode inserir qualquer nome, mas seja específico.</span><span class="sxs-lookup"><span data-stu-id="57f02-116">You can enter any name but be specific.</span></span> <span data-ttu-id="57f02-117">Alguns exemplos incluem:</span><span class="sxs-lookup"><span data-stu-id="57f02-117">Some examples include:</span></span><br/><br/><span data-ttu-id="57f02-118">
    <em>mycompany</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="57f02-118">
    <em>mycompany</em>.biztalk.windows.net</span></span><br/><span data-ttu-id="57f02-119">
    <em>mycompanymyapplication</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="57f02-119">
    <em>mycompanymyapplication</em>.biztalk.windows.net</span></span><br/><span data-ttu-id="57f02-120">
    <em>myapplication</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="57f02-120">
    <em>myapplication</em>.biztalk.windows.net</span></span><br/><br/><span data-ttu-id="57f02-121">".biztalk.windows.net" é adicionado automaticamente ao nome que você inserir.</span><span class="sxs-lookup"><span data-stu-id="57f02-121">".biztalk.windows.net" is automatically added to the name you enter.</span></span> <span data-ttu-id="57f02-122">Isso cria uma URL que é usada para acessar seu Serviço do BizTalk, como <strong>https://<em>meuaplicativo</em>.biztalk.windows.net</strong>.</span><span class="sxs-lookup"><span data-stu-id="57f02-122">This creates a URL that is used to access your BizTalk Service, like <strong>https://<em>myapplication</em>.biztalk.windows.net</strong>.</span></span>
    </td>
    </tr>
    <tr>
    <td><span data-ttu-id="57f02-123"><strong>Edição</strong></span><span class="sxs-lookup"><span data-stu-id="57f02-123"><strong>Edition</strong></span></span></td>
    <td><span data-ttu-id="57f02-124">Se você estiver em fase de teste/desenvolvimento, escolha <strong>Desenvolvedor</strong>.</span><span class="sxs-lookup"><span data-stu-id="57f02-124">If you are in the testing/development phase, choose <strong>Developer</strong>.</span></span> <span data-ttu-id="57f02-125">Se você estiver na fase de produção, use os <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302279">Serviços BizTalk: Gráfico de Edições</a> para determinar se <strong>Premium</strong>, <strong>Standard</strong> ou <strong>Básico</strong> é a escolha certa para seu cenário de negócios.</span><span class="sxs-lookup"><span data-stu-id="57f02-125">If you are in the production phase, use the <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302279">BizTalk Services: Editions Chart</a> to determine if <strong>Premium</strong>, <strong>Standard</strong>, or <strong>Basic</strong> is the correct choice for your business scenario.</span></span>
    </td>
    </tr>
    <tr>
    <td><span data-ttu-id="57f02-126"><strong>Região</strong></span><span class="sxs-lookup"><span data-stu-id="57f02-126"><strong>Region</strong></span></span></td>
    <td><span data-ttu-id="57f02-127">Selecione a região geográfica para hospedar seu Serviço BizTalk.</span><span class="sxs-lookup"><span data-stu-id="57f02-127">Select the geographic region to host your BizTalk Service.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="57f02-128"><strong>URL do Domínio</strong></span><span class="sxs-lookup"><span data-stu-id="57f02-128"><strong>Domain URL</strong></span></span></td>
    <td><span data-ttu-id="57f02-129"><strong>Opcional</strong>.</span><span class="sxs-lookup"><span data-stu-id="57f02-129"><strong>Optional</strong>.</span></span> <span data-ttu-id="57f02-130">Por padrão, a URL do domínio é <em>YourBizTalkServiceName</em>.biztalk.windows.net.</span><span class="sxs-lookup"><span data-stu-id="57f02-130">By default, the domain URL is <em>YourBizTalkServiceName</em>.biztalk.windows.net.</span></span> <span data-ttu-id="57f02-131">Um domínio personalizado também pode ser inserido.</span><span class="sxs-lookup"><span data-stu-id="57f02-131">A custom domain can also be entered.</span></span> <span data-ttu-id="57f02-132">Por exemplo, se seu domínio for <em>contoso</em>, insira:</span><span class="sxs-lookup"><span data-stu-id="57f02-132">For example, if your domain is <em>contoso</em>, you can enter:</span></span> <br/><br/><span data-ttu-id="57f02-133">
    <em>MyCompany</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="57f02-133">
    <em>MyCompany</em>.contoso.com</span></span><br/><span data-ttu-id="57f02-134">
    <em>MyCompanyMyApplication</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="57f02-134">
    <em>MyCompanyMyApplication</em>.contoso.com</span></span><br/><span data-ttu-id="57f02-135">
    <em>MyApplication</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="57f02-135">
    <em>MyApplication</em>.contoso.com</span></span><br/><span data-ttu-id="57f02-136">
    <em>YourBizTalkServiceName</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="57f02-136">
    <em>YourBizTalkServiceName</em>.contoso.com</span></span><br/>
    </td>
    </tr>
    </table>
<span data-ttu-id="57f02-137">Selecione a seta de AVANÇO.</span><span class="sxs-lookup"><span data-stu-id="57f02-137">Select the NEXT arrow.</span></span>
<span data-ttu-id="57f02-138">5.</span><span class="sxs-lookup"><span data-stu-id="57f02-138">5.</span></span> <span data-ttu-id="57f02-139">Inserir as configurações de banco de dados e de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="57f02-139">Enter the Storage and Database Settings:</span></span>  <table border="1">
    <tr>
    <td><span data-ttu-id="57f02-140"><strong>Conta de armazenamento de Monitoramento/Arquivamento</strong></span><span class="sxs-lookup"><span data-stu-id="57f02-140"><strong>Monitoring/Archiving storage account</strong></span></span></td>
    <td><span data-ttu-id="57f02-141">Selecione uma conta de armazenamento existente ou crie uma nova.</span><span class="sxs-lookup"><span data-stu-id="57f02-141">Select an existing storage account or create a new storage account.</span></span> <br/><br/><span data-ttu-id="57f02-142">Se você criar uma nova conta de Armazenamento, digite o <strong>Nome da Conta de Armazenamento</strong>.</span><span class="sxs-lookup"><span data-stu-id="57f02-142">If you create a new Storage account, enter the <strong>Storage Account Name</strong>.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="57f02-143"><strong>Acompanhamento de banco de dados</strong></span><span class="sxs-lookup"><span data-stu-id="57f02-143"><strong>Tracking database</strong></span></span></td>
    <td><span data-ttu-id="57f02-144">Se você usar um banco de dados SQL do Azure, não poderá ser usado por outro Serviço do BizTalk.</span><span class="sxs-lookup"><span data-stu-id="57f02-144">If you use an existing Azure SQL Database, it cannot be used by another BizTalk Service.</span></span> <span data-ttu-id="57f02-145">Você precisará do nome e da senha de logon inseridos na criação do Banco de Dados SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="57f02-145">You need the login name and password entered when that Azure SQL Database Server was created.</span></span><br/><br/><span data-ttu-id="57f02-146"><strong>DICA</strong> Crie o banco de dados de Acompanhamento e a conta de armazenamento de Monitoramento/Arquivamento na mesma região do Serviço BizTalk.</span><span class="sxs-lookup"><span data-stu-id="57f02-146"><strong>TIP</strong> Create the Tracking database and Monitoring/Archiving storage account in the same region as the BizTalk Service.</span></span></td>
    </tr>
    </table>
<span data-ttu-id="57f02-147">Selecione a seta de AVANÇO.</span><span class="sxs-lookup"><span data-stu-id="57f02-147">Select the NEXT arrow.</span></span>
<span data-ttu-id="57f02-148">6.</span><span class="sxs-lookup"><span data-stu-id="57f02-148">6.</span></span> <span data-ttu-id="57f02-149">Insira as configurações do banco de dados:</span><span class="sxs-lookup"><span data-stu-id="57f02-149">Enter the Database settings:</span></span>  <table border="1">
    <tr>
    <td><span data-ttu-id="57f02-150"><strong>Nome</strong></span><span class="sxs-lookup"><span data-stu-id="57f02-150"><strong>Name</strong></span></span></td>
    <td><span data-ttu-id="57f02-151">Disponível quando a opção <strong>Criar uma nova instância do Banco de Dados SQL</strong> é selecionada na tela anterior.</span><span class="sxs-lookup"><span data-stu-id="57f02-151">Available when <strong>Create a new SQL Database instance</strong> is selected in the previous screen.</span></span>
    <br/><br/>
<span data-ttu-id="57f02-152">Insira um nome do Banco de Dados SQL a ser usado pelo seu Serviço BizTalk.</span><span class="sxs-lookup"><span data-stu-id="57f02-152">Enter a SQL Database name to be used by your BizTalk Service.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="57f02-153"><strong>Servidor</strong></span><span class="sxs-lookup"><span data-stu-id="57f02-153"><strong>Server</strong></span></span></td>
    <td><span data-ttu-id="57f02-154">Disponível quando a opção <strong>Criar uma nova instância do Banco de Dados SQL</strong> é selecionada na tela anterior.</span><span class="sxs-lookup"><span data-stu-id="57f02-154">Available when <strong>Create a new SQL Database instance</strong> is selected in the previous screen.</span></span>
    <br/><br/>
<span data-ttu-id="57f02-155">Selecione um Servidor de Banco de Dados SQL ou crie um novo servidor de Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="57f02-155">Select an existing SQL Database Server or create a new SQL Database server.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="57f02-156"><strong>Nome de logon do servidor</strong></span><span class="sxs-lookup"><span data-stu-id="57f02-156"><strong>Server login name</strong></span></span></td>
    <td><span data-ttu-id="57f02-157">Digite o nome de usuário do logon.</span><span class="sxs-lookup"><span data-stu-id="57f02-157">Enter the login user name.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="57f02-158"><strong>Senha de logon do servidor</strong></span><span class="sxs-lookup"><span data-stu-id="57f02-158"><strong>Server login password</strong></span></span></td>
    <td><span data-ttu-id="57f02-159">Digite a senha do logon.</span><span class="sxs-lookup"><span data-stu-id="57f02-159">Enter the login password.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="57f02-160"><strong>Região</strong></span><span class="sxs-lookup"><span data-stu-id="57f02-160"><strong>Region</strong></span></span></td>
    <td><span data-ttu-id="57f02-161">Disponível quando a opção <strong>Criar uma nova instância do Banco de Dados SQL</strong> é selecionada.</span><span class="sxs-lookup"><span data-stu-id="57f02-161">Available when <strong>Create a new SQL Database instance</strong> is selected.</span></span> <span data-ttu-id="57f02-162">Selecione a região geográfica para hospedar seu Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="57f02-162">Select the geographic region to host your SQL Database.</span></span></td>
    </tr>
    </table>

<span data-ttu-id="57f02-163">Selecione a marca de seleção para concluir o assistente.</span><span class="sxs-lookup"><span data-stu-id="57f02-163">Select the check mark to complete the wizard.</span></span> <span data-ttu-id="57f02-164">O ícone de progresso aparece: </span><span class="sxs-lookup"><span data-stu-id="57f02-164">The progress icon appears:</span></span>  
![O ícone de progresso é exibido após a conclusão][ProgressComplete]

<span data-ttu-id="57f02-166">Ao concluir, o Serviço BizTalk do Azure será criado e estará pronto para seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="57f02-166">When complete, the Azure BizTalk Service is created and ready for your applications.</span></span> <span data-ttu-id="57f02-167">As configurações padrão são suficientes.</span><span class="sxs-lookup"><span data-stu-id="57f02-167">The default settings are sufficient.</span></span> <span data-ttu-id="57f02-168">Se você desejar alterar as configurações padrão, selecione **SERVIÇOS BIZTALK** no painel de navegação à esquerda e selecione o seu Serviço BizTalk.</span><span class="sxs-lookup"><span data-stu-id="57f02-168">If you want to change the default settings, select **BIZTALK SERVICES** in the left navigation pane, and then select your BizTalk Service.</span></span> <span data-ttu-id="57f02-169">Configurações adicionais são exibidas nas [guias Painel, Monitor e Escala.](biztalk-dashboard-monitor-scale-tabs.md) na parte superior.</span><span class="sxs-lookup"><span data-stu-id="57f02-169">Additional settings are displayed in the [Dashboard, Monitor, and Scale tabs](biztalk-dashboard-monitor-scale-tabs.md) at the top.</span></span>

<span data-ttu-id="57f02-170">Dependendo do estado do Serviço BizTalk, existem algumas operações que não podem ser concluídas.</span><span class="sxs-lookup"><span data-stu-id="57f02-170">Depending on the state of the BizTalk Service, there are some operations that cannot be completed.</span></span> <span data-ttu-id="57f02-171">Para obter uma lista dessas operações, consulte [Gráfico de estado do serviço BizTalk](biztalk-service-state-chart.md).</span><span class="sxs-lookup"><span data-stu-id="57f02-171">For a list of these operations, go to [BizTalk Services State Chart](biztalk-service-state-chart.md).</span></span>

## <a name="post-provisioning-steps"></a><span data-ttu-id="57f02-172">Etapas pós-provisionamento</span><span class="sxs-lookup"><span data-stu-id="57f02-172">Post-provisioning steps</span></span>
* [<span data-ttu-id="57f02-173">Instalar o certificado em um computador local</span><span class="sxs-lookup"><span data-stu-id="57f02-173">Install the certificate on a local computer</span></span>](#InstallCert)
* [<span data-ttu-id="57f02-174">Adicionar um certificado pronto para produção</span><span class="sxs-lookup"><span data-stu-id="57f02-174">Add a production-ready certificate</span></span>](#AddCert)
* [<span data-ttu-id="57f02-175">Obter o namespace do Controle de Acesso</span><span class="sxs-lookup"><span data-stu-id="57f02-175">Get the Access Control namespace</span></span>](#ACS)

#### <span data-ttu-id="57f02-176"><a name="InstallCert"></a>Instalar o certificado em um computador local</span><span class="sxs-lookup"><span data-stu-id="57f02-176"><a name="InstallCert"></a>Install the certificate on a local computer</span></span>
<span data-ttu-id="57f02-177">Como parte do provisionamento do Serviço do BizTalk, um certificado autoassinado é criado e associado com a assinatura do seu serviço do BizTalk.</span><span class="sxs-lookup"><span data-stu-id="57f02-177">As part of BizTalk Service provisioning, a self-signed certificate is created and associated with your BizTalk Service subscription.</span></span> <span data-ttu-id="57f02-178">Você deve baixar este certificado e instalá-lo em computadores de onde você implemente os aplicativos do Serviço do BizTalk ou envie mensagens para um ponto de extremidade do Serviço do BizTalk.</span><span class="sxs-lookup"><span data-stu-id="57f02-178">You must download this certificate and install it on computers from where you either deploy BizTalk Service applications or send messages to a BizTalk Service endpoint.</span></span>

1. <span data-ttu-id="57f02-179">Entre no [Portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="57f02-179">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="57f02-180">Clique em **SERVIÇOS BIZTALK** no painel de navegação à esquerda e selecione a assinatura do seu Serviço BizTalk.</span><span class="sxs-lookup"><span data-stu-id="57f02-180">Select **BIZTALK SERVICES** in the left navigation pane, and then select your BizTalk Service subscription.</span></span>
3. <span data-ttu-id="57f02-181">Selecione a guia **Painel** .</span><span class="sxs-lookup"><span data-stu-id="57f02-181">Select the **Dashboard** tab.</span></span>
4. <span data-ttu-id="57f02-182">Selecione **Baixar Certificado SSL**:</span><span class="sxs-lookup"><span data-stu-id="57f02-182">Select **Download SSL Certificate**:</span></span>  
   <span data-ttu-id="57f02-183">![Modificar certificado SSL][QuickGlance]</span><span class="sxs-lookup"><span data-stu-id="57f02-183">![Modify SSL Certificate][QuickGlance]</span></span>
5. <span data-ttu-id="57f02-184">Clique duas vezes no certificado e execute-o com o assistente para instalar o certificado.</span><span class="sxs-lookup"><span data-stu-id="57f02-184">Double-click the certificate and run through the wizard to install the certificate.</span></span> <span data-ttu-id="57f02-185">Certifique-se de instalar o certificado no armazenamento **Autoridades de certificação de raiz confiáveis** .</span><span class="sxs-lookup"><span data-stu-id="57f02-185">Make sure you install the certificate under the **Trusted Root Certificate Authorities** store.</span></span>

#### <span data-ttu-id="57f02-186"><a name="AddCert"></a>Adicionar um certificado pronto para produção</span><span class="sxs-lookup"><span data-stu-id="57f02-186"><a name="AddCert"></a>Add a production-ready certificate</span></span>
<span data-ttu-id="57f02-187">O certificado autoassinado criado automaticamente durante a criação dos Serviços BizTalk devem ser usados apenas em ambientes de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="57f02-187">The self-signed certificate that is automatically created when creating BizTalk Services is intended for use in development environments only.</span></span> <span data-ttu-id="57f02-188">Para cenários de produção, substitua-o por um certificado pronto para produção.</span><span class="sxs-lookup"><span data-stu-id="57f02-188">For production scenarios, replace it with a production-ready certificate.</span></span>

1. <span data-ttu-id="57f02-189">Na guia **Painel**, selecione **Atualizar Certificado SSL**.</span><span class="sxs-lookup"><span data-stu-id="57f02-189">On the **Dashboard** tab, select **Update SSL Certificate**.</span></span>
2. <span data-ttu-id="57f02-190">Procure o certificado SSL privado (*CertificateName*.pfx) que inclui o nome do seu Serviço do BizTalk, insira a senha e clique na caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="57f02-190">Browse to your private SSL certificate (*CertificateName*.pfx) that includes your BizTalk Service name, enter the password, and then click the check mark.</span></span>

#### <span data-ttu-id="57f02-191"><a name="ACS"></a>Obter o namespace do Controle de Acesso</span><span class="sxs-lookup"><span data-stu-id="57f02-191"><a name="ACS"></a>Get the Access Control namespace</span></span>
1. <span data-ttu-id="57f02-192">Entre no [Portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="57f02-192">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="57f02-193">Selecione **SERVIÇOS BIZTALK** no painel de navegação à esquerda e selecione o seu Serviço BizTalk.</span><span class="sxs-lookup"><span data-stu-id="57f02-193">Select **BIZTALK SERVICES** in the left navigation pane, and then select your BizTalk Service.</span></span>
3. <span data-ttu-id="57f02-194">Na barra de tarefas, selecione **Informações da Conexão**:</span><span class="sxs-lookup"><span data-stu-id="57f02-194">In the task bar, select **Connection Information**:</span></span>  
   <span data-ttu-id="57f02-195">![Selecionar Informações de conexão][ACSConnectInfo]</span><span class="sxs-lookup"><span data-stu-id="57f02-195">![Select Connection Information][ACSConnectInfo]</span></span>
4. <span data-ttu-id="57f02-196">Copiar os valores de Controle de Acesso.</span><span class="sxs-lookup"><span data-stu-id="57f02-196">Copy the Access Control values.</span></span>

<span data-ttu-id="57f02-197">Ao implantar um projeto do Serviço BizTalk no Visual Studio, você insere esse namespace do Controle de Acesso.</span><span class="sxs-lookup"><span data-stu-id="57f02-197">When you deploy a BizTalk Service project from Visual Studio, you enter this Access Control namespace.</span></span> <span data-ttu-id="57f02-198">O namespace do Controle de Acesso é criado automaticamente para seu Serviço BizTalk.</span><span class="sxs-lookup"><span data-stu-id="57f02-198">The Access Control namespace is automatically created for your BizTalk Service.</span></span>

<span data-ttu-id="57f02-199">Os valores de Controle de acesso podem ser usados com qualquer aplicativo.</span><span class="sxs-lookup"><span data-stu-id="57f02-199">The Access Control values can be used with any application.</span></span> <span data-ttu-id="57f02-200">Quando os Serviços do BizTalk do Microsoft Azure estiverem criados, esse namespace do Controle de Acesso controla a autenticação com sua implantação do Serviço BizTalk.</span><span class="sxs-lookup"><span data-stu-id="57f02-200">When Azure BizTalk Services is created, this Access Control namespace controls the authentication with your BizTalk Service deployment.</span></span> <span data-ttu-id="57f02-201">Se você desejar alterar a assinatura ou gerenciar o namespace, selecione **ACTIVE DIRECTORY** no painel de navegação à esquerda e selecione seu namespace.</span><span class="sxs-lookup"><span data-stu-id="57f02-201">If you want to change the subscription or manage the namespace, select **ACTIVE DIRECTORY** in the left navigation pane and then select your namespace.</span></span> <span data-ttu-id="57f02-202">A barra de tarefas lista suas opções.</span><span class="sxs-lookup"><span data-stu-id="57f02-202">The task bar lists your options.</span></span>

<span data-ttu-id="57f02-203">Um clique em **Gerenciar** abre o Portal de Gerenciamento do Controle de Acesso.</span><span class="sxs-lookup"><span data-stu-id="57f02-203">Clicking **Manage** opens the Access Control Management Portal.</span></span> <span data-ttu-id="57f02-204">No Portal de Gerenciamento do Controle de Acesso, o Serviço BizTalk usa **Identidades de serviço**:</span><span class="sxs-lookup"><span data-stu-id="57f02-204">In the Access Control Management Portal, the BizTalk Service uses **Service identities**:</span></span>  
<span data-ttu-id="57f02-205">![Identidades do serviço ACS no Portal de Gerenciamento do Controle de Acesso][ACSServiceIdentities]</span><span class="sxs-lookup"><span data-stu-id="57f02-205">![ACS Service Identities in the Access Control Management Portal][ACSServiceIdentities]</span></span>

<span data-ttu-id="57f02-206">A identidade do serviço do Controle de Acesso é um conjunto de credenciais que permitem que aplicativos ou clientes façam autenticação diretamente com o Controle de Acesso e recebam um token.</span><span class="sxs-lookup"><span data-stu-id="57f02-206">The Access Control service identity is a set of credentials that allow applications or clients to authenticate directly with Access Control and receive a token.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="57f02-207">O Serviço BizTalk usa **Proprietário** para a identidade do serviço padrão e o valor da **Senha**.</span><span class="sxs-lookup"><span data-stu-id="57f02-207">The BizTalk Service uses **Owner** for the default service identity and the **Password** value.</span></span> <span data-ttu-id="57f02-208">Se você usar o valor de Chave Simétrica em vez de o valor de Senha, poderá ocorrer o erro a seguir.</span><span class="sxs-lookup"><span data-stu-id="57f02-208">If you use the Symmetric Key value instead of the Password value, the following error may occur.</span></span><br/><br/><span data-ttu-id="57f02-209">*Não foi possível conectar à conta do Serviço de Gerenciamento do Controle de Acesso com as credenciais especificadas*</span><span class="sxs-lookup"><span data-stu-id="57f02-209">*Could not connect to the Access Control Management Service account with the specified credentials*</span></span>
> 
> 

<span data-ttu-id="57f02-210">[Gerenciando o namespace de seu ACS](https://msdn.microsoft.com/library/azure/hh674478.aspx) lista algumas diretrizes e recomendações.</span><span class="sxs-lookup"><span data-stu-id="57f02-210">[Managing Your ACS Namespace](https://msdn.microsoft.com/library/azure/hh674478.aspx) lists some guidelines and recommendations.</span></span>

## <a name="requirements-explained"></a><span data-ttu-id="57f02-211">Requisitos explicados</span><span class="sxs-lookup"><span data-stu-id="57f02-211">Requirements explained</span></span>
<span data-ttu-id="57f02-212">Estes requisitos não se aplicam à edição gratuita.</span><span class="sxs-lookup"><span data-stu-id="57f02-212">These requirements do not apply to the Free Edition.</span></span>

<table border="1">
<tr bgcolor="FAF9F9">
        <td><span data-ttu-id="57f02-213"><strong>O que você precisa</strong></span><span class="sxs-lookup"><span data-stu-id="57f02-213"><strong>What you need</strong></span></span></td>
        <td><span data-ttu-id="57f02-214"><strong>Por que você precisa disto</strong></span><span class="sxs-lookup"><span data-stu-id="57f02-214"><strong>Why you need it</strong></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="57f02-215">Assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="57f02-215">Azure subscription</span></span></td>
<td><span data-ttu-id="57f02-216">A assinatura determina quem pode entrar no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="57f02-216">The subscription determines who can sign in to the Azure portal.</span></span> <span data-ttu-id="57f02-217">O Titular da conta cria a assinatura em <a HREF="https://account.windowsazure.com/Subscriptions">Assinaturas do Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="57f02-217">The Account holder creates the subscription at <a HREF="https://account.windowsazure.com/Subscriptions"> Azure Subscriptions</a>.</span></span>
<br/><br/>
<span data-ttu-id="57f02-218">A conta do Azure pode ter várias assinaturas e pode ser gerenciada por qualquer pessoa que tenha permissão.</span><span class="sxs-lookup"><span data-stu-id="57f02-218">The Azure account can have multiple subscriptions and can be managed by anyone who is permitted.</span></span> <span data-ttu-id="57f02-219">Por exemplo, o titular da sua conta do Azure cria uma assinatura chamada <em>BizTalkServiceSubscription</em> e dá acesso a essa assinatura aos Administradores do BizTalk em sua empresa (por exemplo, ContosoBTSAdmins@live.com).</span><span class="sxs-lookup"><span data-stu-id="57f02-219">For example, your Azure account holder creates a subscription named <em>BizTalkServiceSubscription</em> and gives the BizTalk Administrators within your company (for example, ContosoBTSAdmins@live.com) access to this subscription.</span></span> <span data-ttu-id="57f02-220">Nesse cenário, os Administradores do BizTalk entram no Portal do Azure e têm acesso total aos serviços hospedados na assinatura, inclusive os Serviços BizTalk do Azure.</span><span class="sxs-lookup"><span data-stu-id="57f02-220">In this scenario, the BizTalk Administrators sign in to the Azure portal and have full Administrator rights to all the hosted services in the subscription, including Azure BizTalk Services.</span></span> <span data-ttu-id="57f02-221">Os administradores do BizTalk não são os titulares da conta do Azure e, portanto, não têm acesso às informações de cobrança.</span><span class="sxs-lookup"><span data-stu-id="57f02-221">The BizTalk Administrators are not the Azure account holders and therefore don't have access to any billing information.</span></span>
<br/><br/><span data-ttu-id="57f02-222">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=267577">Gerenciar assinaturas e contas de armazenamento no Portal do Azure</a> fornece mais informações.</span><span class="sxs-lookup"><span data-stu-id="57f02-222">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=267577"> Manage Subscriptions and Storage Accounts in the Azure portal</a> provides more information.</span></span>
</td>
</tr>
<tr>
<td><span data-ttu-id="57f02-223">Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="57f02-223">Azure SQL Database</span></span></td>
<td><span data-ttu-id="57f02-224">Armazena as tabelas, as exibições e os procedimentos armazenados usados pelo Serviço BizTalk do Azure, incluindo o Rastreamento de dados</span><span class="sxs-lookup"><span data-stu-id="57f02-224">Stores the tables, views, and stored procedures used by the BizTalk Service, including the Tracking data.</span></span>
<br/><br/>
<span data-ttu-id="57f02-225">Ao criar um Serviço BizTalk, você pode usar um SQL Server do Azure ou um Banco de Dados SQL do Azure ou criar automaticamente um novo servidor ou banco de dados.</span><span class="sxs-lookup"><span data-stu-id="57f02-225">When you create a BizTalk Service, you can use an existing Azure SQL Server, Azure SQL Database, or automatically create a new Server or Database.</span></span>
<br/><br/>
<span data-ttu-id="57f02-226">A escala do Banco de Dados SQL é configurada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="57f02-226">The SQL Database scale is automatically configured.</span></span> <span data-ttu-id="57f02-227">Tipicamente a escala padrão é suficiente para um Serviço BizTalk.</span><span class="sxs-lookup"><span data-stu-id="57f02-227">Typically, the default scale is sufficient for a BizTalk Service.</span></span> <span data-ttu-id="57f02-228">Alterar a escala afeta ao preço.</span><span class="sxs-lookup"><span data-stu-id="57f02-228">Changing the scale impacts pricing.</span></span> <span data-ttu-id="57f02-229">Confira <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=234930">Contas e faturamento no banco de dados SQL do Azure</a>
</span><span class="sxs-lookup"><span data-stu-id="57f02-229">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=234930"> Accounts and Billing in Azure SQL Database</a>
</span></span><br/><br/><span data-ttu-id="57f02-230">
<strong>Observações</strong>
</span><span class="sxs-lookup"><span data-stu-id="57f02-230">
<strong>Notes</strong>
</span></span><br/>
<ul>
<li> <span data-ttu-id="57f02-231">Quando você criar um novo SQL Server e Banco de Dados do Azure, os Serviços do Azure são habilitados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="57f02-231">When you create a new Azure SQL Server and Database, Azure Services is automatically enabled.</span></span> <span data-ttu-id="57f02-232">O Serviço do BizTalk requer que os Serviços do Azure sejam habilitados.</span><span class="sxs-lookup"><span data-stu-id="57f02-232">The BizTalk Service requires Azure Services be enabled.</span></span></li>
<li><span data-ttu-id="57f02-233">Se você criar um novo Banco de Dados SQL do Azure em um SQL Server do Azure existente, as regras do firewall do servidor não serão alterados.</span><span class="sxs-lookup"><span data-stu-id="57f02-233">If you create a new Azure SQL Database on an existing Azure SQL Server, the firewall rules of the Server are not changed.</span></span> <span data-ttu-id="57f02-234">Como resultado, é possível que outros Serviços do Azure não tenham permissão de acesso aos bancos de dados do servidor.</span><span class="sxs-lookup"><span data-stu-id="57f02-234">As a result, it's possible other Azure Services are not allowed access to the Server's databases.</span></span></li>
</ul>
</td>
</tr>
<tr>
<td><span data-ttu-id="57f02-235">Namespace do Controle de Acesso do Azure</span><span class="sxs-lookup"><span data-stu-id="57f02-235">Azure Access Control namespace</span></span></td>
<td><span data-ttu-id="57f02-236">Autenticados com os Serviços do BizTalk do Azure.</span><span class="sxs-lookup"><span data-stu-id="57f02-236">Authenticates with Azure BizTalk Services.</span></span> <span data-ttu-id="57f02-237">Ao implantar um projeto do Serviço BizTalk no Visual Studio, você insere esse namespace do Controle de Acesso.</span><span class="sxs-lookup"><span data-stu-id="57f02-237">When you deploy a BizTalk Service project from Visual Studio, you enter this Access Control namespace.</span></span> <span data-ttu-id="57f02-238">Quando você cria um Serviço BizTalk, o namespace de Controle de Acesso é criado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="57f02-238">When you create a BizTalk Service, the Access Control namespace is automatically created.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="57f02-239">Conta de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="57f02-239">Azure Storage account</span></span></td>
<td><span data-ttu-id="57f02-240">Dá acesso às tabelas, aos blobs e às filas usadas pelos Serviços do BizTalk para fazer o seguinte:</span><span class="sxs-lookup"><span data-stu-id="57f02-240">Gives access to tables, blobs, and queues used by your BizTalk Service to save the following:</span></span>

<ul>
<li><span data-ttu-id="57f02-241">Arquivos de log que monitoram o Serviço do BizTalk.</span><span class="sxs-lookup"><span data-stu-id="57f02-241">Log files that monitor the BizTalk Service.</span></span> <span data-ttu-id="57f02-242">A saída do monitoramento também é exibida na guia **Monitoramento** no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="57f02-242">The monitoring output is also displayed in the **Monitoring** tab in the Azure portal.</span></span></li>
<li><span data-ttu-id="57f02-243">Ao criar um contrato X12 ou AS2 entre parceiros, você pode habilitar o recurso de Arquivamento para armazenar propriedades de mensagens.</span><span class="sxs-lookup"><span data-stu-id="57f02-243">When creating an X12 or AS2 agreement between partners, you can enable the Archiving feature to store message properties.</span></span> <span data-ttu-id="57f02-244">Esses dados são salvos na conta de Armazenamento.</span><span class="sxs-lookup"><span data-stu-id="57f02-244">This data is saved in the Storage account.</span></span></li>
</ul>
<br/>
<span data-ttu-id="57f02-245">Ao criar um Serviço BizTalk, você pode usar uma conta de Armazenamento existente ou criar automaticamente uma nova conta de Armazenamento.</span><span class="sxs-lookup"><span data-stu-id="57f02-245">When you create a BizTalk Service, you can use an existing Storage account or automatically create a new Storage account.</span></span>
<br/><br/>
<span data-ttu-id="57f02-246">As configurações de Armazenamento padrão são suficientes para um Serviço BizTalk.</span><span class="sxs-lookup"><span data-stu-id="57f02-246">The default Storage settings are sufficient for a BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="57f02-247">Quando você cria uma Conta de Armazenamento, uma chave primária e uma chave secundária são criadas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="57f02-247">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="57f02-248">Essas chaves controlam o acesso à sua conta de Armazenamento.</span><span class="sxs-lookup"><span data-stu-id="57f02-248">These Keys control access to your Storage account.</span></span> <span data-ttu-id="57f02-249">O Serviço BizTalk usa automaticamente a chave primária.</span><span class="sxs-lookup"><span data-stu-id="57f02-249">The BizTalk Service automatically uses the Primary Key.</span></span>
<br/><br/>
<span data-ttu-id="57f02-250">Consulte <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285671">Armazenamento</a> para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="57f02-250">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285671"> Storage</a> for more information.</span></span>
</td>
</tr>

<tr>
<td><span data-ttu-id="57f02-251">Certificado SSL privado</span><span class="sxs-lookup"><span data-stu-id="57f02-251">SSL private certificate</span></span></td>
<td>
<span data-ttu-id="57f02-252">Quando um Serviço do BizTalk do Azure for criado, uma URL HTTPS que inclui o nome do seu Serviço do BizTalk também é criado.</span><span class="sxs-lookup"><span data-stu-id="57f02-252">When an Azure BizTalk Service is created, an HTTPS URL that includes your BizTalk Service name is also created.</span></span> <span data-ttu-id="57f02-253">Esta URL é configurada automaticamente para usar um certificado autoassinado apenas de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="57f02-253">This URL is automatically configured to use a self-signed development-only certificate.</span></span> <span data-ttu-id="57f02-254">Para produção, você necessita um certificado SSL privado.</span><span class="sxs-lookup"><span data-stu-id="57f02-254">For production, you need a private SSL certificate.</span></span>
<br/><br/><span data-ttu-id="57f02-255">
<strong>Informações importantes sobre o Certificado SSL</strong>

</span><span class="sxs-lookup"><span data-stu-id="57f02-255">
<strong>Important SSL Certificate Information</strong>

</span></span><ul>
<li><span data-ttu-id="57f02-256">A data de expiração do certificado deve ser anterior a cinco anos.</span><span class="sxs-lookup"><span data-stu-id="57f02-256">The certificate expiration date must be less than 5 years.</span></span></li>
<li><span data-ttu-id="57f02-257">Todos os certificados privados exigem uma senha.</span><span class="sxs-lookup"><span data-stu-id="57f02-257">All private certificates require a password.</span></span> <span data-ttu-id="57f02-258">Saiba essa senha e, como uma prática recomendada, compartilhe essa senha com seus administradores.</span><span class="sxs-lookup"><span data-stu-id="57f02-258">Know this password and as a best practice, share this password with your administrators.</span></span></li>
<li><span data-ttu-id="57f02-259">Os certificados autoassinados são usados em um ambientes de desenvolvimento/teste.</span><span class="sxs-lookup"><span data-stu-id="57f02-259">Self-signed certificates are used in a test/development environment.</span></span> <span data-ttu-id="57f02-260">Ao usar certificados autoassinados, importe o certificado para o armazenamento de certificados pessoais e o armazenamento de certificados de Autoridades de Certificação Raiz Confiáveis.</span><span class="sxs-lookup"><span data-stu-id="57f02-260">When using self-signed certificates, import the certificate to your Personal certificate store and the Trusted Root Certification Authorities certificate store.</span></span></li>
</ul>
<br/><span data-ttu-id="57f02-261">Ao enviar a solicitação de certificado de produção à autoridade de certificação, forneça as seguintes propriedades de certificado:</span><span class="sxs-lookup"><span data-stu-id="57f02-261">When sending the production certificate request to your certification authority, give the following certificate properties:</span></span>
<br/>

<ul>
<li><span data-ttu-id="57f02-262"><strong>Uso avançado de chave</strong>: no mínimo, os Serviços BizTalk do Azure exigem a Autenticação de Servidor.</span><span class="sxs-lookup"><span data-stu-id="57f02-262"><strong>Enhanced Key Usage</strong>: At a minimum, Azure BizTalk Services requires Server Authentication.</span></span></li>
<li><span data-ttu-id="57f02-263"><strong>Nome comum</strong>: insira o nome de domínio totalmente qualificado (FQDN) da sua URL de Serviço do BizTalk do Azure.</span><span class="sxs-lookup"><span data-stu-id="57f02-263"><strong>Common Name</strong>: Enter the fully qualified domain name (FQDN) of your Azure BizTalk Service URL.</span></span> <span data-ttu-id="57f02-264">Veja <a HREF="#CreateService">Criar um Serviço BizTalk</a> neste artigo.</span><span class="sxs-lookup"><span data-stu-id="57f02-264">See <a HREF="#CreateService">Create a BizTalk Service</a> in this article.</span></span></li>
</ul>
<br/>
<span data-ttu-id="57f02-265">Um certificado novo ou diferente pode ser adicionado após o Serviço BizTalk ser criado.</span><span class="sxs-lookup"><span data-stu-id="57f02-265">A new or different certificate can be added after the BizTalk Service is created.</span></span>
</td>
</tr>
</table>
<!---Loc Comment: Please, check link [Create a BizTalk Service] since it is not redirecting to any location.--->



## <a name="hybrid-connections"></a><span data-ttu-id="57f02-266">Conexões Híbridas</span><span class="sxs-lookup"><span data-stu-id="57f02-266">Hybrid Connections</span></span>
<span data-ttu-id="57f02-267">Quando você cria um Serviço do BizTalk do Azure, a guia **Conexões híbridas** está disponível:</span><span class="sxs-lookup"><span data-stu-id="57f02-267">When you create an Azure BizTalk Service, the **Hybrid Connections** tab is available:</span></span>

![Guia de Conexões Híbridas][HybridConnectionTab]

<span data-ttu-id="57f02-269">As Conexões Híbridas são usadas para conectar um site do Azure ou um serviço móvel do Azure a um recurso local que utilize uma porta TCP estática, como SQL Server, MySQL, APIs da web HTTP, e os serviços Web mais personalizados.</span><span class="sxs-lookup"><span data-stu-id="57f02-269">Hybrid Connections are used to connect an Azure website or Azure mobile service to any on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, Mobile Services, and most custom Web Services.</span></span>  <span data-ttu-id="57f02-270">As Conexões híbridas e o Serviço do adaptador do BizTalk são diferentes.</span><span class="sxs-lookup"><span data-stu-id="57f02-270">Hybrid Connections and the BizTalk Adapter Service are different.</span></span> <span data-ttu-id="57f02-271">O Serviço do Adaptador do BizTalk é usado para conectar os Serviços do BizTalk do Azure a um sistema de Linha de Negócios (LOB) local.</span><span class="sxs-lookup"><span data-stu-id="57f02-271">The BizTalk Adapter Service is used to connect Azure BizTalk Services to an on-premises Line of Business (LOB) system.</span></span>

 <span data-ttu-id="57f02-272">Consulte [Conexões híbridas](integration-hybrid-connection-overview.md) para saber mais, incluindo a criação e gerenciamento de Conexões híbridos.</span><span class="sxs-lookup"><span data-stu-id="57f02-272">See [Hybrid Connections](integration-hybrid-connection-overview.md) to learn more, including creating and managing Hybrid Connections.</span></span>

## <a name="next-steps"></a><span data-ttu-id="57f02-273">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="57f02-273">Next steps</span></span>
<span data-ttu-id="57f02-274">Agora que o Serviço BizTalk foi criado, familiarize-se com os diferentes [Serviços BizTalk: guias Painel, Monitor e Escala](biztalk-dashboard-monitor-scale-tabs.md).</span><span class="sxs-lookup"><span data-stu-id="57f02-274">Now that a BizTalk Service is created, familiarize yourself with the different [BizTalk Services: Dashboard, Monitor and Scale tabs](biztalk-dashboard-monitor-scale-tabs.md).</span></span> <span data-ttu-id="57f02-275">Seu Serviço BizTalk está pronto para os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="57f02-275">Your BizTalk Service is ready for your applications.</span></span> <span data-ttu-id="57f02-276">Para começar a criar aplicativos, visite [Serviços BizTalk do Azure (a página pode estar em inglês)](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span><span class="sxs-lookup"><span data-stu-id="57f02-276">To start creating applications, go to [Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span></span>

## <a name="see-also"></a><span data-ttu-id="57f02-277">Consulte também</span><span class="sxs-lookup"><span data-stu-id="57f02-277">See also</span></span>
* [<span data-ttu-id="57f02-278">Serviços BizTalk: gráfico de edições</span><span class="sxs-lookup"><span data-stu-id="57f02-278">BizTalk Services: Editions Chart</span></span>](biztalk-editions-feature-chart.md)<br/>
* [<span data-ttu-id="57f02-279">Serviços BizTalk: gráfico de estado</span><span class="sxs-lookup"><span data-stu-id="57f02-279">BizTalk Services: State Chart</span></span>](biztalk-service-state-chart.md)<br/>
* [<span data-ttu-id="57f02-280">Serviços BizTalk: backup e restauração</span><span class="sxs-lookup"><span data-stu-id="57f02-280">BizTalk Services: Backup and Restore</span></span>](biztalk-backup-restore.md)<br/>
* [<span data-ttu-id="57f02-281">Serviços BizTalk: limitação</span><span class="sxs-lookup"><span data-stu-id="57f02-281">BizTalk Services: Throttling</span></span>](biztalk-throttling-thresholds.md)<br/>
* [<span data-ttu-id="57f02-282">Serviços BizTalk: nome e chave do emissor</span><span class="sxs-lookup"><span data-stu-id="57f02-282">BizTalk Services: Issuer Name and Issuer Key</span></span>](biztalk-issuer-name-issuer-key.md)<br/>
* [<span data-ttu-id="57f02-283">Como começar a usar o SDK dos Serviços BizTalk do Azure</span><span class="sxs-lookup"><span data-stu-id="57f02-283">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="57f02-284">Conexões Híbridas</span><span class="sxs-lookup"><span data-stu-id="57f02-284">Hybrid Connections</span></span>](integration-hybrid-connection-overview.md)

[NewBizTalkService]: ./media/biztalk-provision-services/WABS_NewBizTalkService.png
[NEWButton]: ./media/biztalk-provision-services/WABS_New.png
[ProgressComplete]: ./media/biztalk-provision-services/WABS_ProgressComplete.png
[ACSConnectInfo]: ./media/biztalk-provision-services/WABS_ACSConnectInformation.png
[QuickGlance]: ./media/biztalk-provision-services/WABS_QuickGlance.png
[ACSServiceIdentities]: ./media/biztalk-provision-services/WABS_ACSServiceIdentities.png
[HybridConnectionTab]: ./media/biztalk-provision-services/WABS_HybridConnectionTab.png
