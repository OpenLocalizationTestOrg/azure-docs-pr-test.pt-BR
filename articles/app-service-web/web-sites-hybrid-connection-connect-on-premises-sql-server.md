---
title: "aaaConnect tooon local SQL Server de um aplicativo web no serviço de aplicativo do Azure usando conexões híbridas"
description: Criar um aplicativo web no Microsoft Azure e conecte-o banco de dados do SQL Server tooan no local
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: 2b4e0539-1a0b-4aa1-8a69-b4b053c3b2e5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2016
ms.author: cephalin
ms.openlocfilehash: 2e8f8f7e0b9733cfb0433697615faba4358c6023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooon-premises-sql-server-from-a-web-app-in-azure-app-service-using-hybrid-connections"></a><span data-ttu-id="873a6-103">Conecte-se o SQL Server local tooon de um aplicativo web no serviço de aplicativo do Azure usando conexões híbridas</span><span class="sxs-lookup"><span data-stu-id="873a6-103">Connect tooon-premises SQL Server from a web app in Azure App Service using Hybrid Connections</span></span>
<span data-ttu-id="873a6-104">Conexões híbridas podem se conectar [do serviço de aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) recursos de tooon locais de aplicativos Web que usam uma porta TCP estática.</span><span class="sxs-lookup"><span data-stu-id="873a6-104">Hybrid Connections can connect [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps tooon-premises resources that use a static TCP port.</span></span> <span data-ttu-id="873a6-105">Os recursos com suporte incluem Microsoft SQL Server, MySQL, APIs Web HTTP, Serviço de Aplicativo e os serviços Web mais personalizados.</span><span class="sxs-lookup"><span data-stu-id="873a6-105">Supported resources include Microsoft SQL Server, MySQL, HTTP Web APIs, App Service, and most custom Web Services.</span></span>

<span data-ttu-id="873a6-106">Neste tutorial, você aprenderá como toocreate um aplicativo de serviço web app Olá [Portal do Azure](http://go.microsoft.com/fwlink/?LinkId=529715), conectar Olá web aplicativo tooyour local no local do SQL Server banco de dados usando o novo recurso de Conexão híbrida hello, criar um simples ASP.NET aplicativo que usar conexão de híbrida hello e implantar Olá aplicativo toohello aplicativo do serviço de aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="873a6-106">In this tutorial, you will learn how toocreate an App Service web app in hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715), connect hello web app tooyour local on-premises SQL Server database using hello new Hybrid Connection feature, create a simple ASP.NET application that will use hello hybrid connection, and deploy hello application toohello App Service web app.</span></span> <span data-ttu-id="873a6-107">Olá concluída web app no Azure armazena as credenciais do usuário em um banco de dados de associação que é local.</span><span class="sxs-lookup"><span data-stu-id="873a6-107">hello completed web app on Azure stores user credentials in a membership database that is on-premises.</span></span> <span data-ttu-id="873a6-108">tutorial de saudação não assume nenhuma experiência anterior com o Azure ou o ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="873a6-108">hello tutorial assumes no prior experience using Azure or ASP.NET.</span></span>

> [!NOTE]
> <span data-ttu-id="873a6-109">Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="873a6-109">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="873a6-110">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="873a6-110">No credit cards required; no commitments.</span></span>
> 
> <span data-ttu-id="873a6-111">parte de aplicativos Web de saudação do recurso de conexões híbridas hello está disponível apenas no hello [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="873a6-111">hello Web Apps portion of hello Hybrid Connections feature is available only in hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="873a6-112">toocreate uma conexão nos serviços do BizTalk, consulte [conexões híbridas](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span><span class="sxs-lookup"><span data-stu-id="873a6-112">toocreate a connection in BizTalk Services, see [Hybrid Connections](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span></span>  
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="873a6-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="873a6-113">Prerequisites</span></span>
<span data-ttu-id="873a6-114">toocomplete neste tutorial, você precisará Olá produtos a seguir.</span><span class="sxs-lookup"><span data-stu-id="873a6-114">toocomplete this tutorial, you'll need hello following products.</span></span> <span data-ttu-id="873a6-115">Todos estão disponíveis em versões gratuitas, portanto, é possível começar a desenvolver para o Azure de maneira totalmente gratuita.</span><span class="sxs-lookup"><span data-stu-id="873a6-115">All are available in free versions, so you can start developing for Azure entirely for free.</span></span>

* <span data-ttu-id="873a6-116">**Assinatura do Azure** - para uma assinatura gratuita, consulte [Avaliação Gratuita do Azure](/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="873a6-116">**Azure subscription** - For a free subscription, see [Azure Free Trial](/pricing/free-trial/).</span></span>
* <span data-ttu-id="873a6-117">**Visual Studio 2013** -toodownload uma versão de avaliação gratuita do Visual Studio 2013, consulte [Downloads do Visual Studio](http://www.visualstudio.com/downloads/download-visual-studio-vs).</span><span class="sxs-lookup"><span data-stu-id="873a6-117">**Visual Studio 2013** - toodownload a free trial version of Visual Studio 2013, see [Visual Studio Downloads](http://www.visualstudio.com/downloads/download-visual-studio-vs).</span></span> <span data-ttu-id="873a6-118">Instale isso antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="873a6-118">Install this before continuing.</span></span>
* <span data-ttu-id="873a6-119">**Microsoft .NET Framework 3.5 Service Pack 1** – Se o seu sistema operacional for Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7 ou Windows Server 2008 R2, você pode habilitar esse item em Painel de Controle > Programas e Recursos > Ativar ou desativar recursos do Windows.</span><span class="sxs-lookup"><span data-stu-id="873a6-119">**Microsoft .NET Framework 3.5 Service Pack 1** - If your operating system is Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7, or Windows Server 2008 R2, you can enable this in Control Panel > Programs and Features > Turn Windows features on or off.</span></span> <span data-ttu-id="873a6-120">Caso contrário, você pode baixá-lo do hello [Microsoft Download Center](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22).</span><span class="sxs-lookup"><span data-stu-id="873a6-120">Otherwise, you can download it from hello [Microsoft Download Center](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22).</span></span>
* <span data-ttu-id="873a6-121">**SQL Server 2014 Express com ferramentas** -baixar o Microsoft SQL Server Express gratuitamente em Olá [página de banco de dados do Microsoft Web Platform](http://www.microsoft.com/web/platform/database.aspx).</span><span class="sxs-lookup"><span data-stu-id="873a6-121">**SQL Server 2014 Express with Tools** - download Microsoft SQL Server Express for free at hello [Microsoft Web Platform Database page](http://www.microsoft.com/web/platform/database.aspx).</span></span> <span data-ttu-id="873a6-122">Escolha Olá **Express** (não LocalDB) versão.</span><span class="sxs-lookup"><span data-stu-id="873a6-122">Choose hello **Express** (not LocalDB) version.</span></span> <span data-ttu-id="873a6-123">Olá **Express with Tools** versão inclui o SQL Server Management Studio, você usará neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="873a6-123">hello **Express with Tools** version includes SQL Server Management Studio, which you will use in this tutorial.</span></span>
* <span data-ttu-id="873a6-124">**SQL Server Management Studio Express** - isso é incluído com o SQL Server 2014 Express de saudação com download de ferramentas mencionado acima, mas se você precisar tooinstall-lo separadamente, você pode baixar e instalá-lo de saudação [SQL Server Express página de download](http://www.microsoft.com/web/platform/database.aspx).</span><span class="sxs-lookup"><span data-stu-id="873a6-124">**SQL Server Management Studio Express** - This is included with hello SQL Server 2014 Express with Tools download mentioned above, but if you need tooinstall it separately, you can download and install it from hello [SQL Server Express download page](http://www.microsoft.com/web/platform/database.aspx).</span></span>

<span data-ttu-id="873a6-125">tutorial de saudação pressupõe que você tenha uma assinatura do Azure, que você tenha instalado o Visual Studio 2013, e que você tenha instalado ou habilitado do .NET Framework 3.5.</span><span class="sxs-lookup"><span data-stu-id="873a6-125">hello tutorial assumes that you have an Azure subscription, that you have installed Visual Studio 2013, and that you have installed or enabled .NET Framework 3.5.</span></span> <span data-ttu-id="873a6-126">tutorial de saudação mostra como tooinstall SQL Server 2014 Express em uma configuração que funciona bem com hello Azure híbrido conexões recurso (uma instância padrão com uma porta TCP estática).</span><span class="sxs-lookup"><span data-stu-id="873a6-126">hello tutorial shows you how tooinstall SQL Server 2014 Express in a configuration that works well with hello Azure Hybrid Connections feature (a default instance with a static TCP port).</span></span> <span data-ttu-id="873a6-127">Antes de iniciar o tutorial hello, baixe o SQL Server 2014 Express com ferramentas de local de saudação mencionado acima, se você não tiver o SQL Server instalado.</span><span class="sxs-lookup"><span data-stu-id="873a6-127">Before starting hello tutorial, download SQL Server 2014 Express with Tools from hello location mentioned above if you do not have SQL Server installed.</span></span>

### <a name="notes"></a><span data-ttu-id="873a6-128">Observações</span><span class="sxs-lookup"><span data-stu-id="873a6-128">Notes</span></span>
<span data-ttu-id="873a6-129">toouse um SQL Server no local ou no banco de dados do SQL Server Express com uma conexão híbrida, TCP/IP precisa toobe habilitado em uma porta estática.</span><span class="sxs-lookup"><span data-stu-id="873a6-129">toouse an on-premises SQL Server or SQL Server Express database with a hybrid connection, TCP/IP needs toobe enabled on a static port.</span></span> <span data-ttu-id="873a6-130">As instâncias padrão no SQL Server usam a porta estática 1433, ao passo que instâncias nomeadas não.</span><span class="sxs-lookup"><span data-stu-id="873a6-130">Default instances on SQL Server use static port 1433, whereas named instances do not.</span></span>

<span data-ttu-id="873a6-131">computador Olá no qual você instala o agente de Gerenciador de Conexão híbrida local hello:</span><span class="sxs-lookup"><span data-stu-id="873a6-131">hello computer on which you install hello on-premises Hybrid Connection Manager agent:</span></span>

* <span data-ttu-id="873a6-132">Deve ter conectividade de saída tooAzure sobre:</span><span class="sxs-lookup"><span data-stu-id="873a6-132">Must have outbound connectivity tooAzure over:</span></span>

| <span data-ttu-id="873a6-133">Porta</span><span class="sxs-lookup"><span data-stu-id="873a6-133">Port</span></span> | <span data-ttu-id="873a6-134">Porque</span><span class="sxs-lookup"><span data-stu-id="873a6-134">Why</span></span> |
| --- | --- |
| <span data-ttu-id="873a6-135">80</span><span class="sxs-lookup"><span data-stu-id="873a6-135">80</span></span> |<span data-ttu-id="873a6-136">**Necessária** para porta HTTP para validação de certificado e, opcionalmente, para conectividade de dados.</span><span class="sxs-lookup"><span data-stu-id="873a6-136">**Required** for HTTP port for certificate validation and optionally for data connectivity.</span></span> |
| <span data-ttu-id="873a6-137">443</span><span class="sxs-lookup"><span data-stu-id="873a6-137">443</span></span> |<span data-ttu-id="873a6-138">**Opcional** para conectividade de dados.</span><span class="sxs-lookup"><span data-stu-id="873a6-138">**Optional** for data connectivity.</span></span> <span data-ttu-id="873a6-139">Se a conectividade de saída too443 não estiver disponível, a porta TCP 80 é usada.</span><span class="sxs-lookup"><span data-stu-id="873a6-139">If outbound connectivity too443 is unavailable, TCP port 80 is used.</span></span> |
| <span data-ttu-id="873a6-140">5671 e 9352</span><span class="sxs-lookup"><span data-stu-id="873a6-140">5671 and 9352</span></span> |<span data-ttu-id="873a6-141">**Recomendada** , mas opcional para conectividade de dados.</span><span class="sxs-lookup"><span data-stu-id="873a6-141">**Recommended** but Optional for data connectivity.</span></span> <span data-ttu-id="873a6-142">Observe que esse modo costuma produzir uma taxa de transferência maior.</span><span class="sxs-lookup"><span data-stu-id="873a6-142">Note this mode usually yields higher throughput.</span></span> <span data-ttu-id="873a6-143">Se portas de toothese de conectividade de saída não estiver disponível, a porta TCP 443 será usada.</span><span class="sxs-lookup"><span data-stu-id="873a6-143">If outbound connectivity toothese ports is unavailable, TCP port 443 is used.</span></span> |

* <span data-ttu-id="873a6-144">Deve ser capaz de tooreach Olá *hostname*:*portnumber* do recurso local.</span><span class="sxs-lookup"><span data-stu-id="873a6-144">Must be able tooreach hello *hostname*:*portnumber* of your on-premises resource.</span></span>

<span data-ttu-id="873a6-145">Olá etapas neste artigo presumem que você está usando o navegador de saudação do computador Olá que hospedará o agente de conexão híbrida do hello local.</span><span class="sxs-lookup"><span data-stu-id="873a6-145">hello steps in this article assume that you are using hello browser from hello computer that will host hello on-premises hybrid connection agent.</span></span>

<span data-ttu-id="873a6-146">Se você já tiver o SQL Server instalado em uma configuração e em um ambiente que atenda às condições de saudação descritas acima, você pode ignorá-la e começar com [criar um banco de dados do SQL Server local](#CreateSQLDB).</span><span class="sxs-lookup"><span data-stu-id="873a6-146">If you already have SQL Server installed in a configuration and in an environment that meets hello conditions described above, you can skip ahead and start with [Create a SQL Server database on-premises](#CreateSQLDB).</span></span>

<a name="InstallSQL"></a>

## <a name="a-install-sql-server-express-enable-tcpip-and-create-a-sql-server-database-on-premises"></a><span data-ttu-id="873a6-147">R.</span><span class="sxs-lookup"><span data-stu-id="873a6-147">A.</span></span> <span data-ttu-id="873a6-148">Instalar o SQL Server Express, habilitar TCP/IP e criar um banco de dados SQL Server local</span><span class="sxs-lookup"><span data-stu-id="873a6-148">Install SQL Server Express, enable TCP/IP, and create a SQL Server database on-premises</span></span>
<span data-ttu-id="873a6-149">Esta seção mostra como tooinstall SQL Server Express, habilite o TCP/IP e criar um banco de dados para que seu aplicativo web trabalhará com hello Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="873a6-149">This section shows you how tooinstall SQL Server Express, enable TCP/IP, and create a database so that your web application will work with hello Azure Portal.</span></span>

### <a name="install-sql-server-express"></a><span data-ttu-id="873a6-150">Instalar SQL Server Express</span><span class="sxs-lookup"><span data-stu-id="873a6-150">Install SQL Server Express</span></span>
1. <span data-ttu-id="873a6-151">tooinstall SQL Server Express, execute Olá **SQLEXPRWT_x64_ENU.exe** ou **SQLEXPR_x86_ENU.exe** arquivo que você baixou.</span><span class="sxs-lookup"><span data-stu-id="873a6-151">tooinstall SQL Server Express, run hello **SQLEXPRWT_x64_ENU.exe** or **SQLEXPR_x86_ENU.exe** file that you downloaded.</span></span> <span data-ttu-id="873a6-152">Olá Central de instalação do SQL Server Assistente é exibido.</span><span class="sxs-lookup"><span data-stu-id="873a6-152">hello SQL Server Installation Center wizard appears.</span></span>
   
    ![Instalar SQL Server][SQLServerInstall]
2. <span data-ttu-id="873a6-154">Escolha **instalação autônoma do novo SQL Server ou adicionar recursos tooan existente instalação**.</span><span class="sxs-lookup"><span data-stu-id="873a6-154">Choose **New SQL Server stand-alone installation or add features tooan existing installation**.</span></span> <span data-ttu-id="873a6-155">Siga as instruções do hello, aceitando as opções padrão hello e configurações, até chegar toohello **configuração da instância** página.</span><span class="sxs-lookup"><span data-stu-id="873a6-155">Follow hello instructions, accepting hello default choices and settings, until you get toohello **Instance Configuration** page.</span></span>
3. <span data-ttu-id="873a6-156">Em Olá **configuração da instância** escolha **instância padrão**.</span><span class="sxs-lookup"><span data-stu-id="873a6-156">On hello **Instance Configuration** page, choose **Default instance**.</span></span>
   
    ![Selecione Instância padrão][ChooseDefaultInstance]
   
    <span data-ttu-id="873a6-158">Por padrão, instância padrão de saudação do SQL Server escuta para solicitações de clientes do SQL Server na porta estática 1433, que é o hello recurso exige que as conexões híbridas.</span><span class="sxs-lookup"><span data-stu-id="873a6-158">By default, hello default instance of SQL Server listens for requests from SQL Server clients on static port 1433, which is what hello Hybrid Connections feature requires.</span></span> <span data-ttu-id="873a6-159">Instâncias nomeadas utilizam portas dinâmicas e UDP, que não têm suporte em Conexões Híbridas.</span><span class="sxs-lookup"><span data-stu-id="873a6-159">Named instances use dynamic ports and UDP, which are not supported by Hybrid Connections.</span></span>
4. <span data-ttu-id="873a6-160">Aceite os padrões Olá Olá **configuração do servidor** página.</span><span class="sxs-lookup"><span data-stu-id="873a6-160">Accept hello defaults on hello **Server Configuration** page.</span></span>
5. <span data-ttu-id="873a6-161">Em Olá **configuração do mecanismo de banco de dados** página em **modo de autenticação**, escolha **modo misto (autenticação do SQL Server e autenticação do Windows)**e fornecer uma senha.</span><span class="sxs-lookup"><span data-stu-id="873a6-161">On hello **Database Engine Configuration** page, under **Authentication Mode**, choose **Mixed Mode (SQL Server authentication and Windows authentication)**, and provide a password.</span></span>
   
    ![Selecione Modo Misto][ChooseMixedMode]
   
    <span data-ttu-id="873a6-163">Neste tutorial, você irá utilizar autenticação de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="873a6-163">In this tutorial, you will be using SQL Server authentication.</span></span> <span data-ttu-id="873a6-164">Ser senha de saudação tooremember-se de que você fornecer, pois você precisará dele mais tarde.</span><span class="sxs-lookup"><span data-stu-id="873a6-164">Be sure tooremember hello password that you provide, because you will need it later.</span></span>
6. <span data-ttu-id="873a6-165">Percorra o restante da saudação da instalação de Olá Olá Assistente toocomplete.</span><span class="sxs-lookup"><span data-stu-id="873a6-165">Step through hello rest of hello wizard toocomplete hello installation.</span></span>

### <a name="enable-tcpip"></a><span data-ttu-id="873a6-166">Habilitar TCP/IP</span><span class="sxs-lookup"><span data-stu-id="873a6-166">Enable TCP/IP</span></span>
<span data-ttu-id="873a6-167">tooenable TCP/IP, você usará a SQL Server Configuration Manager, que foi instalado quando você instalou o SQL Server Express.</span><span class="sxs-lookup"><span data-stu-id="873a6-167">tooenable TCP/IP, you will use SQL Server Configuration Manager, which was installed when you installed SQL Server Express.</span></span> <span data-ttu-id="873a6-168">Siga as etapas de saudação em [habilitar o protocolo de rede TCP/IP para o SQL Server](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="873a6-168">Follow hello steps in [Enable TCP/IP Network Protocol for SQL Server](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) before continuing.</span></span>

<a name="CreateSQLDB"></a>

### <a name="create-a-sql-server-database-on-premises"></a><span data-ttu-id="873a6-169">Criar um banco de dados SQL Server local</span><span class="sxs-lookup"><span data-stu-id="873a6-169">Create a SQL Server database on-premises</span></span>
<span data-ttu-id="873a6-170">Seu aplicativo Web do Visual Studio exige um banco de dados de associação que possa ser acessado pelo Azure.</span><span class="sxs-lookup"><span data-stu-id="873a6-170">Your Visual Studio web application requires a membership database that can be accessed by Azure.</span></span> <span data-ttu-id="873a6-171">Isso exige um SQL Server ou SQL Server Express banco de dados (não Olá LocalDB que Olá MVC modelo usa por padrão), portanto, você vai criar banco de dados de associação de saudação lado.</span><span class="sxs-lookup"><span data-stu-id="873a6-171">This requires a SQL Server or SQL Server Express database (not hello LocalDB database that hello MVC template uses by default), so you'll create hello membership database next.</span></span>

1. <span data-ttu-id="873a6-172">No SQL Server Management Studio, conecte-se toohello recém-instalada do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="873a6-172">In SQL Server Management Studio, connect toohello SQL Server you just installed.</span></span> <span data-ttu-id="873a6-173">(Se hello **conectar tooServer** caixa de diálogo não for exibido automaticamente, navegue muito**Pesquisador de objetos** no painel esquerdo do hello, clique em **conectar**e, em seguida, clique em **Mecanismo de banco de dados**.) ![Conecte-se tooServer][SSMSConnectToServer]</span><span class="sxs-lookup"><span data-stu-id="873a6-173">(If hello **Connect tooServer** dialog does not appear automatically, navigate too**Object Explorer** in hello left pane, click **Connect**, and then click **Database Engine**.) ![Connect tooServer][SSMSConnectToServer]</span></span>
   
    <span data-ttu-id="873a6-174">Para **Tipo de servidor**, selecione **Mecanismo de Banco de Dados**.</span><span class="sxs-lookup"><span data-stu-id="873a6-174">For **Server type**, choose **Database Engine**.</span></span> <span data-ttu-id="873a6-175">Para **nome do servidor**, você pode usar **localhost** ou nome de saudação do computador de saudação que você está usando.</span><span class="sxs-lookup"><span data-stu-id="873a6-175">For **Server name**, you can use **localhost** or hello name of hello computer that you are using.</span></span> <span data-ttu-id="873a6-176">Escolha **autenticação do SQL Server**e, em seguida, faça logon com nome de usuário do hello sa e a senha de saudação que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="873a6-176">Choose **SQL Server authentication**, and then log in with hello sa user name and hello password that you created earlier.</span></span>
2. <span data-ttu-id="873a6-177">toocreate um novo banco de dados usando o SQL Server Management Studio, clique com botão direito **bancos de dados** no Pesquisador de objetos e, em seguida, clique em **novo banco de dados**.</span><span class="sxs-lookup"><span data-stu-id="873a6-177">toocreate a new database by using SQL Server Management Studio, right-click **Databases** in Object Explorer, and then click **New Database**.</span></span>
   
    ![Criar novo banco de dados][SSMScreateNewDB]
3. <span data-ttu-id="873a6-179">Em Olá **novo banco de dados** caixa de diálogo, digite MembershipDB para o nome do banco de dados de saudação e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="873a6-179">In hello **New Database** dialog, enter MembershipDB for hello database name, and then click **OK**.</span></span>
   
    ![Fornecer nome de banco de dados][SSMSprovideDBname]
   
    <span data-ttu-id="873a6-181">Observe que você não faça qualquer banco de dados de toohello alterações neste momento.</span><span class="sxs-lookup"><span data-stu-id="873a6-181">Note that you do not make any changes toohello database at this point.</span></span> <span data-ttu-id="873a6-182">informações de associação de saudação serão adicionadas automaticamente mais tarde pelo aplicativo web quando você executá-lo.</span><span class="sxs-lookup"><span data-stu-id="873a6-182">hello membership information will be added automatically later by your web application when you run it.</span></span>
4. <span data-ttu-id="873a6-183">No Pesquisador de objetos, se você expandir **bancos de dados**, você verá esse banco de dados de associação de saudação foi criado.</span><span class="sxs-lookup"><span data-stu-id="873a6-183">In Object Explorer, if you expand **Databases**, you will see that hello membership database has been created.</span></span>
   
    ![MembershipDB criado][SSMSMembershipDBCreated]

<a name="CreateSite"></a>

## <a name="b-create-a-web-app-in-hello-azure-portal"></a><span data-ttu-id="873a6-185">B.</span><span class="sxs-lookup"><span data-stu-id="873a6-185">B.</span></span> <span data-ttu-id="873a6-186">Criar um aplicativo web no hello Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="873a6-186">Create a web app in hello Azure Portal</span></span>
> [!NOTE]
> <span data-ttu-id="873a6-187">Se você já tiver criado um aplicativo web no hello Portal do Azure que você deseja toouse para este tutorial, você poderá pular muito[criar uma Conexão híbrida e um BizTalk Service](#CreateHC) e continuar a partir daí.</span><span class="sxs-lookup"><span data-stu-id="873a6-187">If you have already created a web app in hello Azure Portal that you want toouse for this tutorial, you can skip ahead too[Create a Hybrid Connection and a BizTalk Service](#CreateHC) and continue from there.</span></span>
> 
> 

1. <span data-ttu-id="873a6-188">Em Olá [Portal do Azure](https://portal.azure.com), clique em **novo** > **Web + móvel** > **aplicativo Web**.</span><span class="sxs-lookup"><span data-stu-id="873a6-188">In hello [Azure Portal](https://portal.azure.com), click **New** > **Web + Mobile** > **Web app**.</span></span>
   
    ![Novo botão][New]
2. <span data-ttu-id="873a6-190">Configure o aplicativo Web e, em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="873a6-190">Configure your web app, and then click **Create**.</span></span>
   
    ![Nome do site][WebsiteCreationBlade]
3. <span data-ttu-id="873a6-192">Após alguns instantes, Olá web app é criado e aparece de folha do aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="873a6-192">After a few moments, hello web app is created and its web app blade appears.</span></span> <span data-ttu-id="873a6-193">folha de saudação é um painel rolável verticalmente que permite que você gerencie o seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="873a6-193">hello blade is a vertically scrollable dashboard that lets you manage your web app.</span></span>
   
    ![Website executando][WebSiteRunningBlade]
   
    <span data-ttu-id="873a6-195">tooverify Olá web aplicativo estiver ativo, você pode clicar em Olá **procurar** página padrão do ícone toodisplay hello.</span><span class="sxs-lookup"><span data-stu-id="873a6-195">tooverify hello web app is live, you can click hello **Browse** icon toodisplay hello default page.</span></span>

<span data-ttu-id="873a6-196">Em seguida, você criará uma conexão híbrida e um serviço BizTalk para o aplicativo web de saudação.</span><span class="sxs-lookup"><span data-stu-id="873a6-196">Next, you will create a hybrid connection and a BizTalk service for hello web app.</span></span>

<a name="CreateHC"></a>

## <a name="c-create-a-hybrid-connection-and-a-biztalk-service"></a><span data-ttu-id="873a6-197">C.</span><span class="sxs-lookup"><span data-stu-id="873a6-197">C.</span></span> <span data-ttu-id="873a6-198">Criar uma Conexão Híbrida e um Serviço do BizTalk</span><span class="sxs-lookup"><span data-stu-id="873a6-198">Create a Hybrid Connection and a BizTalk Service</span></span>
1. <span data-ttu-id="873a6-199">No Portal do hello, vá toosettings novamente e clique em **rede** > **configurar seus pontos de extremidade de conexão híbrida**.</span><span class="sxs-lookup"><span data-stu-id="873a6-199">Back in hello Portal, go toosettings and click **Networking** > **Configure your hybrid connection endpoints**.</span></span>
   
    ![Conexões Híbridas][CreateHCHCIcon]
2. <span data-ttu-id="873a6-201">Na folha de conexões do hello híbrida, clique em **adicionar** > **nova conexão de híbrida**.</span><span class="sxs-lookup"><span data-stu-id="873a6-201">On hello Hybrid connections blade, click **Add** > **New hybrid connection**.</span></span>
3. <span data-ttu-id="873a6-202">Em Olá **criar conexão híbrida** folha:</span><span class="sxs-lookup"><span data-stu-id="873a6-202">On hello **Create hybrid connection** blade:</span></span>
   
   * <span data-ttu-id="873a6-203">Para **nome**, forneça um nome para a conexão de saudação.</span><span class="sxs-lookup"><span data-stu-id="873a6-203">For **Name**, provide a name for hello connection.</span></span>
   * <span data-ttu-id="873a6-204">Para **Hostname**, digite nome do computador de saudação do computador host do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="873a6-204">For **Hostname**, enter hello computer name of your SQL Server host computer.</span></span>
   * <span data-ttu-id="873a6-205">Para **porta**, digite 1433 (porta de saudação padrão para o SQL Server).</span><span class="sxs-lookup"><span data-stu-id="873a6-205">For **Port**, enter 1433 (hello default port for SQL Server).</span></span>
   * <span data-ttu-id="873a6-206">Clique em **BizTalk Service** > **novo serviço BizTalk** e insira um nome para o serviço BizTalk da saudação.</span><span class="sxs-lookup"><span data-stu-id="873a6-206">Click **BizTalk Service** > **New BizTalk Service** and enter a name for hello BizTalk service.</span></span>
     
     ![Criar uma Conexão Híbrida][TwinCreateHCBlades]
4. <span data-ttu-id="873a6-208">Clique em **OK** duas vezes.</span><span class="sxs-lookup"><span data-stu-id="873a6-208">Click **OK** twice.</span></span>
   
    <span data-ttu-id="873a6-209">Quando Olá processo for concluído, hello **notificações** área pisca uma verde **êxito** e hello **conexão híbrida** folha mostrará a nova conexão de híbrida Olá com Olá status como **não conectado**.</span><span class="sxs-lookup"><span data-stu-id="873a6-209">When hello process completes, hello **Notifications** area will flash a green **SUCCESS** and hello **Hybrid connection** blade will show hello new hybrid connection with hello status as **Not connected**.</span></span>
   
    ![Uma conexão híbrida criada][CreateHCOneConnectionCreated]

<span data-ttu-id="873a6-211">Neste ponto, você concluiu uma parte importante da infraestrutura de conexão Olá nuvem híbrida.</span><span class="sxs-lookup"><span data-stu-id="873a6-211">At this point, you have completed an important part of hello cloud hybrid connection infrastructure.</span></span> <span data-ttu-id="873a6-212">Em seguida, você criará uma parte local correspondente.</span><span class="sxs-lookup"><span data-stu-id="873a6-212">Next, you will create a corresponding on-premises piece.</span></span>

<a name="InstallHCM"></a>

## <a name="d-install-hello-on-premises-hybrid-connection-manager-toocomplete-hello-connection"></a><span data-ttu-id="873a6-213">D.</span><span class="sxs-lookup"><span data-stu-id="873a6-213">D.</span></span> <span data-ttu-id="873a6-214">Instalar Olá conexão do Gerenciador de Conexão híbrida toocomplete Olá local</span><span class="sxs-lookup"><span data-stu-id="873a6-214">Install hello on-premises Hybrid Connection Manager toocomplete hello connection</span></span>
[!INCLUDE [app-service-hybrid-connections-manager-install](../../includes/app-service-hybrid-connections-manager-install.md)]

<span data-ttu-id="873a6-215">Essa infra-estrutura de conexão híbrida Olá é concluída, você criará um aplicativo web que utiliza.</span><span class="sxs-lookup"><span data-stu-id="873a6-215">Now that hello hybrid connection infrastructure is complete, you will create a web application that uses it.</span></span>

<a name="CreateASPNET"></a>

## <a name="e-create-a-basic-aspnet-web-project-edit-hello-database-connection-string-and-run-hello-project-locally"></a><span data-ttu-id="873a6-216">E.</span><span class="sxs-lookup"><span data-stu-id="873a6-216">E.</span></span> <span data-ttu-id="873a6-217">Criar um projeto de web do ASP.NET básico, editar cadeia de conexão de banco de dados de saudação e executar o projeto Olá localmente</span><span class="sxs-lookup"><span data-stu-id="873a6-217">Create a basic ASP.NET web project, edit hello database connection string, and run hello project locally</span></span>
### <a name="create-a-basic-aspnet-project"></a><span data-ttu-id="873a6-218">Criar um projeto ASP.NET básico</span><span class="sxs-lookup"><span data-stu-id="873a6-218">Create a basic ASP.NET project</span></span>
1. <span data-ttu-id="873a6-219">No Visual Studio, no hello **arquivo** menu, crie um novo projeto:</span><span class="sxs-lookup"><span data-stu-id="873a6-219">In Visual Studio, on hello **File** menu, create a new Project:</span></span>
   
    ![Novo projeto de Visual Studio][HCVSNewProject]
2. <span data-ttu-id="873a6-221">Em Olá **modelos** seção Olá **novo projeto** caixa de diálogo, selecione **Web** e escolha **aplicativo Web ASP.NET**e, em seguida, clique em  **Okey**.</span><span class="sxs-lookup"><span data-stu-id="873a6-221">In hello **Templates** section of hello **New Project** dialog, select **Web** and choose **ASP.NET Web Application**, and then click **OK**.</span></span>
   
    ![Selecione Aplicativo Web ASP.NET][HCVSChooseASPNET]
3. <span data-ttu-id="873a6-223">Em Olá **novo projeto ASP.NET** caixa de diálogo, escolha **MVC**e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="873a6-223">In hello **New ASP.NET Project** dialog, choose **MVC**, and then click **OK**.</span></span>
   
    ![Selecione MVC][HCVSChooseMVC]
4. <span data-ttu-id="873a6-225">Quando Olá projeto foi criado, Olá aplicativo Leiame página será exibida.</span><span class="sxs-lookup"><span data-stu-id="873a6-225">When hello project has been created, hello application readme page appears.</span></span> <span data-ttu-id="873a6-226">Não execute Olá web projeto ainda.</span><span class="sxs-lookup"><span data-stu-id="873a6-226">Do not run hello web project yet.</span></span>
   
    ![Página Leia-me][HCVSReadmePage]

### <a name="edit-hello-database-connection-string-for-hello-application"></a><span data-ttu-id="873a6-228">Editar cadeia de conexão de banco de dados Olá para o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="873a6-228">Edit hello database connection string for hello application</span></span>
<span data-ttu-id="873a6-229">Nesta etapa, você editar cadeia de caracteres de conexão de saudação que informa ao seu aplicativo onde toofind seu local do SQL Server Express banco de dados.</span><span class="sxs-lookup"><span data-stu-id="873a6-229">In this step, you edit hello connection string that tells your application where toofind your local SQL Server Express database.</span></span> <span data-ttu-id="873a6-230">cadeia de caracteres de conexão Hello está no arquivo de Web. config do aplicativo hello, que contém informações de configuração para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="873a6-230">hello connection string is in hello application's Web.config file, which contains configuration information for hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="873a6-231">tooensure que seu aplicativo usa o banco de dados de saudação que você criou no SQL Server Express e não hello um padrão do Visual Studio LocalDB, é importante que você concluir esta etapa antes de executar seu projeto.</span><span class="sxs-lookup"><span data-stu-id="873a6-231">tooensure that your application uses hello database that you created in SQL Server Express, and not hello one in Visual Studio's default LocalDB, it is important that you complete this step before running your project.</span></span>
> 
> 

1. <span data-ttu-id="873a6-232">No Solution Explorer, clique duas vezes no arquivo Web. config de saudação.</span><span class="sxs-lookup"><span data-stu-id="873a6-232">In Solution Explorer, double-click hello Web.config file.</span></span>
   
    ![Web.config][HCVSChooseWebConfig]
2. <span data-ttu-id="873a6-234">Editar saudação **connectionStrings** seção toopoint toohello banco de dados SQL em seu computador local, o que segue a sintaxe da saudação em Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="873a6-234">Edit hello **connectionStrings** section toopoint toohello SQL Server database on your local machine, following hello syntax in hello following example:</span></span>
   
    ![Cadeia de conexão][HCVSConnectionString]
   
    <span data-ttu-id="873a6-236">Ao compor a cadeia de caracteres de conexão Olá, lembre-se no seguinte de saudação mente:</span><span class="sxs-lookup"><span data-stu-id="873a6-236">When composing hello connection string, keep in mind hello following:</span></span>
   
   * <span data-ttu-id="873a6-237">Se você estiver se conectando tooa chamado instância em vez de uma instância padrão (por exemplo, YourServer\SQLEXPRESS), você deve configurar as portas de estático toouse do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="873a6-237">If you are connecting tooa named instance instead of a default instance (for example, YourServer\SQLEXPRESS), you must configure your SQL Server toouse static ports.</span></span> <span data-ttu-id="873a6-238">Para obter informações sobre como configurar portas estáticas, consulte [como tooconfigure toolisten de SQL Server em uma porta específica](http://support.microsoft.com/kb/823938).</span><span class="sxs-lookup"><span data-stu-id="873a6-238">For information on configuring static ports, see [How tooconfigure SQL Server toolisten on a specific port](http://support.microsoft.com/kb/823938).</span></span> <span data-ttu-id="873a6-239">Por padrão, instâncias nomeadas utilizam UDP e portas dinâmicas, que não têm suporte em Conexões Híbridas.</span><span class="sxs-lookup"><span data-stu-id="873a6-239">By default, named instances use UDP and dynamic ports, which are not supported by Hybrid Connections.</span></span>
   * <span data-ttu-id="873a6-240">É recomendável que você especifique Olá porta (1433 por padrão, conforme mostrado no exemplo hello) na cadeia de caracteres de conexão Olá para que você pode ter certeza de que o SQL Server local tem TCP habilitado e está usando a porta correta hello.</span><span class="sxs-lookup"><span data-stu-id="873a6-240">It is recommended that you specify hello port (1433 by default, as shown in hello example) on hello connection string so that you can be sure that your local SQL Server has TCP enabled and is using hello correct port.</span></span>
   * <span data-ttu-id="873a6-241">Lembre-se de toouse tooconnect de autenticação do SQL Server, especificando Olá ID de usuário e senha na cadeia de caracteres de conexão.</span><span class="sxs-lookup"><span data-stu-id="873a6-241">Remember toouse SQL Server Authentication tooconnect, specifying hello user ID and password in your connection string.</span></span>
3. <span data-ttu-id="873a6-242">Clique em **salvar** no arquivo Web. config do Visual Studio toosave hello.</span><span class="sxs-lookup"><span data-stu-id="873a6-242">Click **Save** in Visual Studio toosave hello Web.config file.</span></span>

### <a name="run-hello-project-locally-and-register-a-new-user"></a><span data-ttu-id="873a6-243">Execute o projeto de saudação localmente e registrar um novo usuário</span><span class="sxs-lookup"><span data-stu-id="873a6-243">Run hello project locally and register a new user</span></span>
1. <span data-ttu-id="873a6-244">Agora, execute o novo projeto web localmente clicando o botão Olá em depuração.</span><span class="sxs-lookup"><span data-stu-id="873a6-244">Now, run your new web project locally by clicking hello browse button under Debug.</span></span> <span data-ttu-id="873a6-245">Este exemplo usa o Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="873a6-245">This example uses Internet Explorer.</span></span>
   
    ![Executar projeto][HCVSRunProject]
2. <span data-ttu-id="873a6-247">Superior direito da página de web padrão Olá Olá, escolha **registrar** tooregister uma nova conta:</span><span class="sxs-lookup"><span data-stu-id="873a6-247">On hello upper right of hello default web page, choose **Register** tooregister a new account:</span></span>
   
    ![Registrar uma nova conta][HCVSRegisterLocally]
3. <span data-ttu-id="873a6-249">Digite um nome de usuário e uma senha:</span><span class="sxs-lookup"><span data-stu-id="873a6-249">Enter a user name and password:</span></span>
   
    ![Digite nome de usuário e senha][HCVSCreateNewAccount]
   
    <span data-ttu-id="873a6-251">Isso cria automaticamente um banco de dados no SQL Server local que contém informações de associação de saudação para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="873a6-251">This automatically creates a database on your local SQL Server that holds hello membership information for your application.</span></span> <span data-ttu-id="873a6-252">Uma das tabelas de saudação (**dbo. AspNetUsers**) mantém web credenciais de usuário do aplicativo como Olá aqueles que você acabou de digitar.</span><span class="sxs-lookup"><span data-stu-id="873a6-252">One of hello tables (**dbo.AspNetUsers**) holds web app user credentials like hello ones that you just entered.</span></span> <span data-ttu-id="873a6-253">Você verá essa tabela mais tarde no tutorial de saudação.</span><span class="sxs-lookup"><span data-stu-id="873a6-253">You will see this table later in hello tutorial.</span></span>
4. <span data-ttu-id="873a6-254">Feche a janela do navegador de saudação da página de web saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="873a6-254">Close hello browser window of hello default web page.</span></span> <span data-ttu-id="873a6-255">Isso impede que o aplicativo hello no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="873a6-255">This stops hello application in Visual Studio.</span></span>

<span data-ttu-id="873a6-256">Você agora está pronto para Olá próxima etapa, que é toopublish Olá aplicativo tooAzure e testá-lo.</span><span class="sxs-lookup"><span data-stu-id="873a6-256">You are now ready for hello next step, which is toopublish hello application tooAzure and test it.</span></span>

<a name="PubNTest"></a>

## <a name="f-publish-hello-web-application-tooazure-and-test-it"></a><span data-ttu-id="873a6-257">F.</span><span class="sxs-lookup"><span data-stu-id="873a6-257">F.</span></span> <span data-ttu-id="873a6-258">Publicar Olá web aplicativo tooAzure e testá-lo</span><span class="sxs-lookup"><span data-stu-id="873a6-258">Publish hello web application tooAzure and test it</span></span>
<span data-ttu-id="873a6-259">Agora, você publicar seu aplicativo tooyour aplicativo do serviço de aplicativo web e testá-lo toosee como conexão híbrida de saudação configurados anteriormente está sendo usado tooconnect seu banco de dados do toohello de aplicativo da web em seu computador local.</span><span class="sxs-lookup"><span data-stu-id="873a6-259">Now, you'll publish your application tooyour App Service web app and then test it toosee how hello hybrid connection you configured earlier is being used tooconnect your web app toohello database on your local machine.</span></span>

### <a name="publish-hello-web-application"></a><span data-ttu-id="873a6-260">Publicar o aplicativo da web hello</span><span class="sxs-lookup"><span data-stu-id="873a6-260">Publish hello web application</span></span>
1. <span data-ttu-id="873a6-261">Você pode baixar o perfil de publicação para Olá aplicativo do serviço de aplicativo web de saudação Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="873a6-261">You can download your publishing profile for hello App Service web app in hello Azure Portal.</span></span> <span data-ttu-id="873a6-262">Na folha de saudação para seu aplicativo web, clique em **obter perfil de publicação**e, em seguida, salve o computador de tooyour arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="873a6-262">On hello blade for your web app, click **Get publish profile**, and then save hello file tooyour computer.</span></span>
   
    ![Baixar perfil de publicação][PortalDownloadPublishProfile]
   
    <span data-ttu-id="873a6-264">Em seguida, você importará esse arquivo em seu aplicativo Web do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="873a6-264">Next, you will import this file into your Visual Studio web application.</span></span>
2. <span data-ttu-id="873a6-265">No Visual Studio, clique em nome do projeto Olá no Gerenciador de soluções e selecione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="873a6-265">In Visual Studio, right-click hello project name in Solution Explorer and select **Publish**.</span></span>
   
    ![Selecionar Publicar][HCVSRightClickProjectSelectPublish]
3. <span data-ttu-id="873a6-267">Em Olá **Publicar Web** caixa de diálogo, no hello **perfil** guia, escolha **importação**.</span><span class="sxs-lookup"><span data-stu-id="873a6-267">In hello **Publish Web** dialog, on hello **Profile** tab, choose **Import**.</span></span>
   
    ![Importar][HCVSPublishWebDialogImport]
4. <span data-ttu-id="873a6-269">Procurar tooyour baixado o perfil de publicação, selecioná-lo e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="873a6-269">Browse tooyour downloaded publishing profile, select it, and then click **OK**.</span></span>
   
    ![Procurar tooprofile][HCVSBrowseToImportPubProfile]
5. <span data-ttu-id="873a6-271">As informações de publicação são importadas e exibe no hello **Conexão** guia da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="873a6-271">Your publishing information is imported and displays on hello **Connection** tab of hello dialog.</span></span>
   
    ![Clicar em Publicar][HCVSClickPublish]
   
    <span data-ttu-id="873a6-273">Clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="873a6-273">Click **Publish**.</span></span>
   
    <span data-ttu-id="873a6-274">Quando a publicação for concluído, o navegador iniciará e mostrar seu aplicativo ASP.NET já conhecido - exceto que agora ele está ativo no hello nuvem do Azure!</span><span class="sxs-lookup"><span data-stu-id="873a6-274">When publishing completes, your browser will launch and show your now familiar ASP.NET application -- except that now it is live in hello Azure cloud!</span></span>

<span data-ttu-id="873a6-275">Em seguida, você usará o toosee de aplicativo da web dinâmico sua Conexão híbrida na ação.</span><span class="sxs-lookup"><span data-stu-id="873a6-275">Next, you will use your live web application toosee its Hybrid Connection in action.</span></span>

### <a name="test-hello-completed-web-application-on-azure"></a><span data-ttu-id="873a6-276">Saudação de teste concluído o aplicativo web no Azure</span><span class="sxs-lookup"><span data-stu-id="873a6-276">Test hello completed web application on Azure</span></span>
1. <span data-ttu-id="873a6-277">Na parte superior de saudação à direita da página da web no Azure, escolha **login**.</span><span class="sxs-lookup"><span data-stu-id="873a6-277">On hello top right of your web page on Azure, choose **Log in**.</span></span>
   
    ![Logon Para Teste][HCTestLogIn]
2. <span data-ttu-id="873a6-279">Seu serviço de aplicativo web aplicativo agora está conectado banco de dados de associação do aplicativo da web tooyour em seu computador local.</span><span class="sxs-lookup"><span data-stu-id="873a6-279">Your App Service web app is now connected tooyour web application's membership database on your local machine.</span></span> <span data-ttu-id="873a6-280">tooverify isso, faça logon com hello mesmas credenciais que você inseriu no local de saudação do banco de dados anterior.</span><span class="sxs-lookup"><span data-stu-id="873a6-280">tooverify this, log in with hello same credentials that you entered in hello local database earlier.</span></span>
   
    ![Olá saudação][HCTestHelloContoso]
3. <span data-ttu-id="873a6-282">toofurther testar sua conexão híbrida novo, sair de seu aplicativo web do Azure e registrar-se como outro usuário.</span><span class="sxs-lookup"><span data-stu-id="873a6-282">toofurther test your new hybrid connection, log off of your Azure web application and register as another user.</span></span> <span data-ttu-id="873a6-283">Forneça nome de usuário e senha novos e depois clique em **Registrar**.</span><span class="sxs-lookup"><span data-stu-id="873a6-283">Provide a new user name and password, and then click **Register**.</span></span>
   
    ![Testar registro de um outro usuário][HCTestRegisterRelecloud]
4. <span data-ttu-id="873a6-285">tooverify que as credenciais de saudação do novo usuário foram armazenadas no banco de dados local por meio de sua conexão híbrida, abra o SQL Management Studio no computador local.</span><span class="sxs-lookup"><span data-stu-id="873a6-285">tooverify that hello new user's credentials have been stored in your local database through your hybrid connection, open SQL Management Studio on your local computer.</span></span> <span data-ttu-id="873a6-286">No Pesquisador de objetos, expanda Olá **MembershipDB** banco de dados e, em seguida, expanda **tabelas**.</span><span class="sxs-lookup"><span data-stu-id="873a6-286">In Object Explorer, expand hello **MembershipDB** database, and then expand **Tables**.</span></span> <span data-ttu-id="873a6-287">Saudação de atalho **dbo. AspNetUsers** associação de tabela e escolha **selecionar 1000 linhas superiores** tooview resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="873a6-287">Right-click hello **dbo.AspNetUsers** membership table and choose **Select Top 1000 Rows** tooview hello results.</span></span>
   
    ![Exibir resultados da saudação][HCTestSSMSTree]
5. <span data-ttu-id="873a6-289">A tabela de associação local agora mostra ambas as contas - Olá que foi criada localmente e Olá que você criou no hello nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="873a6-289">Your local membership table now shows both accounts - hello one that you created locally, and hello one that you created in hello Azure cloud.</span></span> <span data-ttu-id="873a6-290">Olá que você criou na nuvem Olá foi salvo tooyour banco de dados no local por meio do recurso de Conexão híbrida do Azure.</span><span class="sxs-lookup"><span data-stu-id="873a6-290">hello one that you created in hello cloud has been saved tooyour on-premises database through Azure's Hybrid Connection feature.</span></span>
   
    ![Usuários registrados em banco de dados local][HCTestShowMemberDb]

<span data-ttu-id="873a6-292">Agora você criou e implantou um aplicativo web ASP.NET que usa uma conexão híbrida entre um aplicativo web no hello nuvem do Azure e um banco de dados do SQL Server local.</span><span class="sxs-lookup"><span data-stu-id="873a6-292">You have now created and deployed an ASP.NET web application that uses a hybrid connection between a web app in hello Azure cloud and an on-premises SQL Server database.</span></span> <span data-ttu-id="873a6-293">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="873a6-293">Congratulations!</span></span>

## <a name="see-also"></a><span data-ttu-id="873a6-294">Consulte também</span><span class="sxs-lookup"><span data-stu-id="873a6-294">See Also</span></span>
[<span data-ttu-id="873a6-295">Visão geral de Conexões Híbridas</span><span class="sxs-lookup"><span data-stu-id="873a6-295">Hybrid Connections overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[<span data-ttu-id="873a6-296">Josh Twist apresenta conexões híbridas (vídeo no Channel 9)</span><span class="sxs-lookup"><span data-stu-id="873a6-296">Josh Twist introduces hybrid connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[<span data-ttu-id="873a6-297">Visão geral de Conexões Híbridas</span><span class="sxs-lookup"><span data-stu-id="873a6-297">Hybrid Connections overview</span></span>](/services/biztalk-services/)

[<span data-ttu-id="873a6-298">Serviços BizTalk: guias Painel, Monitor, Escala, Configurar e Conexão Híbrida</span><span class="sxs-lookup"><span data-stu-id="873a6-298">BizTalk Services: Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[<span data-ttu-id="873a6-299">Criando uma nuvem híbrida no mundo real com portabilidade perfeita com aplicativo (vídeo no Channel 9)</span><span class="sxs-lookup"><span data-stu-id="873a6-299">Building a Real-World Hybrid Cloud with Seamless Application Portability (Channel 9 video)</span></span>](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[<span data-ttu-id="873a6-300">Acessar os recursos locais usando conexões híbridas no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="873a6-300">Access on-premises resources using hybrid connections in Azure App Service</span></span>](web-sites-hybrid-connection-get-started.md)

[<span data-ttu-id="873a6-301">Visão geral de Identidade ASP.NET</span><span class="sxs-lookup"><span data-stu-id="873a6-301">ASP.NET Identity Overview</span></span>](http://www.asp.net/identity)

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

<!-- IMAGES -->
[SQLServerInstall]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A01SQLServerInstall.png
[ChooseDefaultInstance]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A02ChooseDefaultInstance.png
[ChooseMixedMode]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A03ChooseMixedMode.png
[SSMSConnectToServer]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A04SSMSConnectToServer.png
[SSMScreateNewDB]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A05SSMScreateNewDBlh.png
[SSMSprovideDBname]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A06SSMSprovideDBname.png
[SSMSMembershipDBCreated]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A07SSMSMembershipDBCreated.png
[New]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B01New.png
[NewWebsite]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B02NewWebsite.png
[WebsiteCreationBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B03WebsiteCreationBlade.png
[WebSiteRunningBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B04WebSiteRunningBlade.png
[Browse]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B05Browse.png
[DefaultWebSitePage]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B06DefaultWebSitePage.png
[CreateHCHCIcon]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C01CreateHCHCIcon.png
[CreateHCAddHC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C02CreateHCAddHC.png
[TwinCreateHCBlades]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C03TwinCreateHCBlades.png
[CreateHCCreateBTS]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C04CreateHCCreateBTS.png
[CreateBTScomplete]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C05CreateBTScomplete.png
[CreateHCSuccessNotification]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C06CreateHCSuccessNotification.png
[CreateHCOneConnectionCreated]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C07CreateHCOneConnectionCreated.png
[HCIcon]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D01HCIcon.png
[NotConnected]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D02NotConnected.png
[NotConnectedBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D03NotConnectedBlade.png
[ClickListenerSetup]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D04ClickListenerSetup.png
[ClickToInstallHCM]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D05ClickToInstallHCM.png
[ApplicationRunWarning]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D06ApplicationRunWarning.png
[UAC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D07UAC.png
[HCMInstalling]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D08HCMInstalling.png
[HCMInstallComplete]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D09HCMInstallComplete.png
[HCStatusConnected]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D10HCStatusConnected.png
[HCVSNewProject]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E01HCVSNewProject.png
[HCVSChooseASPNET]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E02HCVSChooseASPNET.png
[HCVSChooseMVC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E03HCVSChooseMVC.png
[HCVSReadmePage]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E04HCVSReadmePage.png
[HCVSChooseWebConfig]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E05HCVSChooseWebConfig.png
[HCVSConnectionString]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E06HCVSConnectionString.png
[HCVSRunProject]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E06HCVSRunProject.png
[HCVSRegisterLocally]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E07HCVSRegisterLocally.png
[HCVSCreateNewAccount]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E08HCVSCreateNewAccount.png
[PortalDownloadPublishProfile]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F01PortalDownloadPublishProfile.png
[HCVSPublishProfileInDownloadsFolder]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F02HCVSPublishProfileInDownloadsFolder.png
[HCVSRightClickProjectSelectPublish]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F03HCVSRightClickProjectSelectPublish.png
[HCVSPublishWebDialogImport]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F04HCVSPublishWebDialogImport.png
[HCVSBrowseToImportPubProfile]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F05HCVSBrowseToImportPubProfile.png
[HCVSClickPublish]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F06HCVSClickPublish.png
[HCTestLogIn]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F07HCTestLogIn.png
[HCTestHelloContoso]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F08HCTestHelloContoso.png
[HCTestRegisterRelecloud]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F09HCTestRegisterRelecloud.png
[HCTestSSMSTree]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F10HCTestSSMSTree.png
[HCTestShowMemberDb]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F11HCTestShowMemberDb.png
