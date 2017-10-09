---
title: 'Always Encrypted: Banco de Dados SQL - Azure Key Vault | Microsoft Docs'
description: "Este artigo mostra como os dados confidenciais no banco de dados SQL com o uso de criptografia de dados toosecure Olá Assistente do sempre criptografado no SQL Server Management Studio. Ele também inclui instruções que lhe mostrará como toostore cada chave de criptografia no cofre de chaves do Azure."
keywords: criptografia de dados, chave de criptografia, criptografia de nuvem
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: cgronlun
ms.assetid: 6ca16644-5969-497b-a413-d28c3b835c9b
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: sstein
ms.openlocfilehash: 8226bfef584e979643f5bb0747d4df16569f8204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="always-encrypted-protect-sensitive-data-in-sql-database-and-store-your-encryption-keys-in-azure-key-vault"></a><span data-ttu-id="95ec3-105">Always Encrypted: proteger dados confidenciais no Banco de Dados SQL e armazenar suas chaves de criptografia no Cofre de Chaves do Azure</span><span class="sxs-lookup"><span data-stu-id="95ec3-105">Always Encrypted: Protect sensitive data in SQL Database and store your encryption keys in Azure Key Vault</span></span>

<span data-ttu-id="95ec3-106">Este artigo mostra como os dados confidenciais em um SQL toosecure banco de dados com a criptografia de dados usando Olá [Assistente do Always Encrypted](https://msdn.microsoft.com/library/mt459280.aspx) na [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span><span class="sxs-lookup"><span data-stu-id="95ec3-106">This article shows you how toosecure sensitive data in a SQL database with data encryption using hello [Always Encrypted Wizard](https://msdn.microsoft.com/library/mt459280.aspx) in [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span></span> <span data-ttu-id="95ec3-107">Ele também inclui instruções que lhe mostrará como toostore cada chave de criptografia no cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="95ec3-107">It also includes instructions that will show you how toostore each encryption key in Azure Key Vault.</span></span>

<span data-ttu-id="95ec3-108">Sempre criptografado é uma nova tecnologia de criptografia de dados no banco de dados do SQL Azure e SQL Server que ajuda a proteger dados confidenciais em repouso no servidor de saudação, durante a movimentação entre cliente e servidor e, enquanto dados saudação estão em uso.</span><span class="sxs-lookup"><span data-stu-id="95ec3-108">Always Encrypted is a new data encryption technology in Azure SQL Database and SQL Server that helps protect sensitive data at rest on hello server, during movement between client and server, and while hello data is in use.</span></span> <span data-ttu-id="95ec3-109">Sempre criptografado garante que os dados confidenciais nunca seja exibida como texto sem formatação no sistema de banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="95ec3-109">Always Encrypted ensures that sensitive data never appears as plaintext inside hello database system.</span></span> <span data-ttu-id="95ec3-110">Depois de configurar a criptografia de dados, somente os aplicativos cliente ou servidores de aplicativos que têm acesso toohello chaves podem acessar dados de texto sem formatação.</span><span class="sxs-lookup"><span data-stu-id="95ec3-110">After you configure data encryption, only client applications or app servers that have access toohello keys can access plaintext data.</span></span> <span data-ttu-id="95ec3-111">Para obter informações detalhadas, consulte [Always Encrypted (Mecanismo do Banco de Dados)](https://msdn.microsoft.com/library/mt163865.aspx).</span><span class="sxs-lookup"><span data-stu-id="95ec3-111">For detailed information, see [Always Encrypted (Database Engine)](https://msdn.microsoft.com/library/mt163865.aspx).</span></span>

<span data-ttu-id="95ec3-112">Depois de configurar Olá toouse de banco de dados sempre criptografado, você criará um aplicativo cliente em c# com Visual Studio toowork com dados criptografado de saudação.</span><span class="sxs-lookup"><span data-stu-id="95ec3-112">After you configure hello database toouse Always Encrypted, you will create a client application in C# with Visual Studio toowork with hello encrypted data.</span></span>

<span data-ttu-id="95ec3-113">Siga as etapas de saudação neste artigo e saiba como tooset o sempre criptografado para um banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="95ec3-113">Follow hello steps in this article and learn how tooset up Always Encrypted for an Azure SQL database.</span></span> <span data-ttu-id="95ec3-114">Neste artigo, você aprenderá como Olá tooperform seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="95ec3-114">In this article you will learn how tooperform hello following tasks:</span></span>

* <span data-ttu-id="95ec3-115">Assistente de sempre criptografado Olá Use no SSMS toocreate [chaves Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span><span class="sxs-lookup"><span data-stu-id="95ec3-115">Use hello Always Encrypted wizard in SSMS toocreate [Always Encrypted keys](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span></span>
  * <span data-ttu-id="95ec3-116">Crie uma [CMK (Chave Mestra da Coluna)](https://msdn.microsoft.com/library/mt146393.aspx).</span><span class="sxs-lookup"><span data-stu-id="95ec3-116">Create a [column master key (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).</span></span>
  * <span data-ttu-id="95ec3-117">Crie uma [CEK (Chave de Criptografia da Coluna)](https://msdn.microsoft.com/library/mt146372.aspx).</span><span class="sxs-lookup"><span data-stu-id="95ec3-117">Create a [column encryption key (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).</span></span>
* <span data-ttu-id="95ec3-118">Criar uma tabela de banco de dados e criptografar colunas.</span><span class="sxs-lookup"><span data-stu-id="95ec3-118">Create a database table and encrypt columns.</span></span>
* <span data-ttu-id="95ec3-119">Crie um aplicativo que insere, seleciona e exibe dados de colunas Olá criptografado.</span><span class="sxs-lookup"><span data-stu-id="95ec3-119">Create an application that inserts, selects, and displays data from hello encrypted columns.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="95ec3-120">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="95ec3-120">Prerequisites</span></span>
<span data-ttu-id="95ec3-121">Para este tutorial, será necessário:</span><span class="sxs-lookup"><span data-stu-id="95ec3-121">For this tutorial, you'll need:</span></span>

* <span data-ttu-id="95ec3-122">Uma conta e uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="95ec3-122">An Azure account and subscription.</span></span> <span data-ttu-id="95ec3-123">Se não tiver uma, inscreva-se em uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="95ec3-123">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="95ec3-124">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) versão 13.0.700.242 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="95ec3-124">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) version 13.0.700.242 or later.</span></span>
* <span data-ttu-id="95ec3-125">[.NET framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) ou posterior (no computador do cliente de saudação).</span><span class="sxs-lookup"><span data-stu-id="95ec3-125">[.NET Framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) or later (on hello client computer).</span></span>
* <span data-ttu-id="95ec3-126">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="95ec3-126">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span></span>
* <span data-ttu-id="95ec3-127">[Azure PowerShell](/powershell/azure/overview), versão 1.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="95ec3-127">[Azure PowerShell](/powershell/azure/overview), version  1.0 or later.</span></span> <span data-ttu-id="95ec3-128">Tipo **(Get-Module azure - ListAvailable). Versão** toosee qual versão do PowerShell que você está executando.</span><span class="sxs-lookup"><span data-stu-id="95ec3-128">Type **(Get-Module azure -ListAvailable).Version** toosee what version of PowerShell you are running.</span></span>

## <a name="enable-your-client-application-tooaccess-hello-sql-database-service"></a><span data-ttu-id="95ec3-129">Habilitar o serviço de banco de dados SQL de saudação do cliente aplicativo tooaccess</span><span class="sxs-lookup"><span data-stu-id="95ec3-129">Enable your client application tooaccess hello SQL Database service</span></span>
<span data-ttu-id="95ec3-130">Você deve habilitar seu serviço de banco de dados do SQL cliente aplicativo tooaccess Olá Configurando a autenticação necessária hello e hello aquisição *ClientId* e *segredo* que você precisará tooauthenticate seu aplicativo no hello código a seguir.</span><span class="sxs-lookup"><span data-stu-id="95ec3-130">You must enable your client application tooaccess hello SQL Database service by setting up hello required authentication and acquiring hello *ClientId* and *Secret* that you will need tooauthenticate your application in hello following code.</span></span>

1. <span data-ttu-id="95ec3-131">Olá abrir [portal clássico do Azure](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="95ec3-131">Open hello [Azure classic portal](http://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="95ec3-132">Selecione **do Active Directory** e clique em instância do Active Directory Olá que seu aplicativo usará.</span><span class="sxs-lookup"><span data-stu-id="95ec3-132">Select **Active Directory** and click hello Active Directory instance that your application will use.</span></span>
3. <span data-ttu-id="95ec3-133">Clique em **Aplicativos** e, em seguida, clique em **ADICIONAR**.</span><span class="sxs-lookup"><span data-stu-id="95ec3-133">Click **Applications**, and then click **ADD**.</span></span>
4. <span data-ttu-id="95ec3-134">Digite um nome para seu aplicativo (por exemplo: *myClientApp*), selecione **aplicativo WEB**e clique em Olá seta toocontinue.</span><span class="sxs-lookup"><span data-stu-id="95ec3-134">Type a name for your application (for example: *myClientApp*), select **WEB APPLICATION**, and click hello arrow toocontinue.</span></span>
5. <span data-ttu-id="95ec3-135">Para Olá **URL de logon** e **URI da ID do aplicativo** você pode digitar uma URL válida (por exemplo, *http://myClientApp*) e continuar.</span><span class="sxs-lookup"><span data-stu-id="95ec3-135">For hello **SIGN-ON URL** and **APP ID URI** you can type a valid URL (for example, *http://myClientApp*) and continue.</span></span>
6. <span data-ttu-id="95ec3-136">Clique em **CONFIGURAR**.</span><span class="sxs-lookup"><span data-stu-id="95ec3-136">Click **CONFIGURE**.</span></span>
7. <span data-ttu-id="95ec3-137">Copie a **ID DO CLIENTE**.</span><span class="sxs-lookup"><span data-stu-id="95ec3-137">Copy your **CLIENT ID**.</span></span> <span data-ttu-id="95ec3-138">(Posteriormente você precisará desse valor no código)</span><span class="sxs-lookup"><span data-stu-id="95ec3-138">(You will need this value in your code later.)</span></span>
8. <span data-ttu-id="95ec3-139">Em Olá **chaves** seção, selecione **1 ano** de saudação **selecionar duração** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="95ec3-139">In hello **keys** section, select **1 year** from hello  **Select duration** drop-down list.</span></span> <span data-ttu-id="95ec3-140">(Você copiará chave Olá depois de salvar a etapa 13.)</span><span class="sxs-lookup"><span data-stu-id="95ec3-140">(You will copy hello key after you save in step 13.)</span></span>
9. <span data-ttu-id="95ec3-141">Role para baixo e clique em **Adicionar aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="95ec3-141">Scroll down and click **Add application**.</span></span>
10. <span data-ttu-id="95ec3-142">Deixe **Mostrar** definido muito**Microsoft Apps** e selecione **API de gerenciamento de serviços do Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="95ec3-142">Leave **SHOW** set too**Microsoft Apps** and select **Microsoft Azure Service Management API**.</span></span> <span data-ttu-id="95ec3-143">Clique em Olá toocontinue de marca de seleção.</span><span class="sxs-lookup"><span data-stu-id="95ec3-143">Click hello checkmark toocontinue.</span></span>
11. <span data-ttu-id="95ec3-144">Selecione **acessar o gerenciamento de serviços do Azure...**  de saudação **permissões delegadas** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="95ec3-144">Select **Access Azure Service Management...** from hello **Delegated Permissions** drop-down list.</span></span>
12. <span data-ttu-id="95ec3-145">Clique em **SALVAR**.</span><span class="sxs-lookup"><span data-stu-id="95ec3-145">Click **SAVE**.</span></span>
13. <span data-ttu-id="95ec3-146">Após Olá salvar for concluída, copie o valor da chave Olá no hello **chaves** seção.</span><span class="sxs-lookup"><span data-stu-id="95ec3-146">After hello save finishes, copy hello key value in hello **keys** section.</span></span> <span data-ttu-id="95ec3-147">(Posteriormente você precisará desse valor no código)</span><span class="sxs-lookup"><span data-stu-id="95ec3-147">(You will need this value in your code later.)</span></span>

## <a name="create-a-key-vault-toostore-your-keys"></a><span data-ttu-id="95ec3-148">Criar um cofre de chaves toostore suas chaves</span><span class="sxs-lookup"><span data-stu-id="95ec3-148">Create a key vault toostore your keys</span></span>
<span data-ttu-id="95ec3-149">Agora que o aplicativo cliente está configurado e você tem a ID do cliente, é hora toocreate um cofre de chaves e configurar sua política de acesso para que você e seu aplicativo podem acessar os segredos do cofre da saudação (chaves Always Encrypted Olá).</span><span class="sxs-lookup"><span data-stu-id="95ec3-149">Now that your client app is configured and you have your client ID, it's time toocreate a key vault and configure its access policy so you and your application can access hello vault's secrets (hello Always Encrypted keys).</span></span> <span data-ttu-id="95ec3-150">Olá *criar*, *obter*, *lista*, *sinal*, *verificar*, *wrapKey*, e *unwrapKey* permissões são necessárias para criar uma nova chave mestra de coluna e para configurar a criptografia com o SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="95ec3-150">hello *create*, *get*, *list*, *sign*, *verify*, *wrapKey*, and *unwrapKey* permissions are required for creating a new column master key and for setting up encryption with SQL Server Management Studio.</span></span>

<span data-ttu-id="95ec3-151">Você pode criar rapidamente um cofre de chaves executando Olá script a seguir.</span><span class="sxs-lookup"><span data-stu-id="95ec3-151">You can quickly create a key vault by running hello following script.</span></span> <span data-ttu-id="95ec3-152">Para obter uma explicação detalhada sobre esses cmdlets e obter mais informações sobre como criar e configurar um cofre de chaves, veja [Introdução ao Cofre de Chaves do Azure](../key-vault/key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="95ec3-152">For a detailed explanation of these cmdlets and more information about creating and configuring a key vault, see [Get started with Azure Key Vault](../key-vault/key-vault-get-started.md).</span></span>

    $subscriptionName = '<your Azure subscription name>'
    $userPrincipalName = '<username@domain.com>'
    $clientId = '<client ID that you copied in step 7 above>'
    $resourceGroupName = '<resource group name>'
    $location = '<datacenter location>'
    $vaultName = 'AeKeyVault'


    Login-AzureRmAccount
    $subscriptionId = (Get-AzureRmSubscription -SubscriptionName $subscriptionName).Id
    Set-AzureRmContext -SubscriptionId $subscriptionId

    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
    New-AzureRmKeyVault -VaultName $vaultName -ResourceGroupName $resourceGroupName -Location $location

    Set-AzureRmKeyVaultAccessPolicy -VaultName $vaultName -ResourceGroupName $resourceGroupName -PermissionsToKeys create,get,wrapKey,unwrapKey,sign,verify,list -UserPrincipalName $userPrincipalName
    Set-AzureRmKeyVaultAccessPolicy  -VaultName $vaultName  -ResourceGroupName $resourceGroupName -ServicePrincipalName $clientId -PermissionsToKeys get,wrapKey,unwrapKey,sign,verify,list




## <a name="create-a-blank-sql-database"></a><span data-ttu-id="95ec3-153">Criar um banco de dados SQL em branco</span><span class="sxs-lookup"><span data-stu-id="95ec3-153">Create a blank SQL database</span></span>
1. <span data-ttu-id="95ec3-154">Entrar toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="95ec3-154">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="95ec3-155">Vá muito**novo** > **dados + armazenamento** > **banco de dados SQL**.</span><span class="sxs-lookup"><span data-stu-id="95ec3-155">Go too**New** > **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="95ec3-156">Crie um banco de dados **Em branco** chamado **Clínica** em um servidor novo ou existente.</span><span class="sxs-lookup"><span data-stu-id="95ec3-156">Create a **Blank** database named **Clinic** on a new or existing server.</span></span> <span data-ttu-id="95ec3-157">Para obter instruções detalhadas sobre como toocreate um banco de dados Olá portal do Azure, consulte [seu primeiro banco de dados do SQL Azure](sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="95ec3-157">For detailed directions about how toocreate a database in hello Azure portal, see [Your first Azure SQL database](sql-database-get-started-portal.md).</span></span>
   
    ![Criar um banco de dados vazio](./media/sql-database-always-encrypted-azure-key-vault/create-database.png)

<span data-ttu-id="95ec3-159">Você será necessário Olá cadeia de caracteres de conexão mais tarde no tutorial Olá, assim depois de criar o banco de dados Olá, procurar toohello nova clínica banco de dados e copiar Olá conexão cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="95ec3-159">You will need hello connection string later in hello tutorial, so after you create hello database, browse toohello new  Clinic database and copy hello connection string.</span></span> <span data-ttu-id="95ec3-160">Você pode obter a cadeia de caracteres de conexão Olá a qualquer momento, mas é fácil toocopy no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="95ec3-160">You can get hello connection string at any time, but it's easy toocopy it in hello Azure portal.</span></span>

1. <span data-ttu-id="95ec3-161">Vá muito**bancos de dados SQL** > **clínica** > **Mostrar cadeias de conexão de banco de dados**.</span><span class="sxs-lookup"><span data-stu-id="95ec3-161">Go too**SQL databases** > **Clinic** > **Show database connection strings**.</span></span>
2. <span data-ttu-id="95ec3-162">Copie a cadeia de caracteres de conexão de saudação para **ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="95ec3-162">Copy hello connection string for **ADO.NET**.</span></span>
   
    ![Copie a cadeia de caracteres de conexão Olá](./media/sql-database-always-encrypted-azure-key-vault/connection-strings.png)

## <a name="connect-toohello-database-with-ssms"></a><span data-ttu-id="95ec3-164">Conectar-se o banco de dados toohello com SSMS</span><span class="sxs-lookup"><span data-stu-id="95ec3-164">Connect toohello database with SSMS</span></span>
<span data-ttu-id="95ec3-165">Abra o SSMS e conecte o servidor de toohello com o banco de dados do hello clínica.</span><span class="sxs-lookup"><span data-stu-id="95ec3-165">Open SSMS and connect toohello server with hello Clinic database.</span></span>

1. <span data-ttu-id="95ec3-166">Abra o SSMS.</span><span class="sxs-lookup"><span data-stu-id="95ec3-166">Open SSMS.</span></span> <span data-ttu-id="95ec3-167">(Ir muito**conectar** > **mecanismo de banco de dados** tooopen Olá **conectar tooServer** janela se ele não estiver aberto.)</span><span class="sxs-lookup"><span data-stu-id="95ec3-167">(Go too**Connect** > **Database Engine** tooopen hello **Connect tooServer** window if it isn't open.)</span></span>
2. <span data-ttu-id="95ec3-168">Insira o nome do servidor e credenciais.</span><span class="sxs-lookup"><span data-stu-id="95ec3-168">Enter your server name and credentials.</span></span> <span data-ttu-id="95ec3-169">nome do servidor de saudação pode ser encontrada na folha de banco de dados SQL hello e na cadeia de caracteres de conexão Olá copiados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="95ec3-169">hello server name can be found on hello SQL database blade and in hello connection string you copied earlier.</span></span> <span data-ttu-id="95ec3-170">Nome de servidor completo do tipo hello, incluindo *t*.</span><span class="sxs-lookup"><span data-stu-id="95ec3-170">Type hello complete server name, including *database.windows.net*.</span></span>
   
    ![Copie a cadeia de caracteres de conexão Olá](./media/sql-database-always-encrypted-azure-key-vault/ssms-connect.png)

<span data-ttu-id="95ec3-172">Se hello **nova regra de Firewall** abre a janela, entrar tooAzure e permitem SSMS criar uma nova regra de firewall para você.</span><span class="sxs-lookup"><span data-stu-id="95ec3-172">If hello **New Firewall Rule** window opens, sign in tooAzure and let SSMS create a new firewall rule for you.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="95ec3-173">Criar uma tabela</span><span class="sxs-lookup"><span data-stu-id="95ec3-173">Create a table</span></span>
<span data-ttu-id="95ec3-174">Nesta seção, você criará um dados dos pacientes toohold da tabela.</span><span class="sxs-lookup"><span data-stu-id="95ec3-174">In this section, you will create a table toohold patient data.</span></span> <span data-ttu-id="95ec3-175">Ele não é inicialmente criptografado - você irá configurar a criptografia na próxima seção, Olá.</span><span class="sxs-lookup"><span data-stu-id="95ec3-175">It's not initially encrypted--you will configure encryption in hello next section.</span></span>

1. <span data-ttu-id="95ec3-176">Expanda **Bancos de Dados**.</span><span class="sxs-lookup"><span data-stu-id="95ec3-176">Expand **Databases**.</span></span>
2. <span data-ttu-id="95ec3-177">Saudação de atalho **clínica** de banco de dados e clique em **nova consulta**.</span><span class="sxs-lookup"><span data-stu-id="95ec3-177">Right-click hello **Clinic** database and click **New Query**.</span></span>
3. <span data-ttu-id="95ec3-178">Saudação de colar Transact-SQL (T-SQL) a seguir na nova janela de consulta hello e **Execute** -lo.</span><span class="sxs-lookup"><span data-stu-id="95ec3-178">Paste hello following Transact-SQL (T-SQL) into hello new query window and **Execute** it.</span></span>

        CREATE TABLE [dbo].[Patients](
         [PatientId] [int] IDENTITY(1,1),
         [SSN] [char](11) NOT NULL,
         [FirstName] [nvarchar](50) NULL,
         [LastName] [nvarchar](50) NULL,
         [MiddleName] [nvarchar](50) NULL,
         [StreetAddress] [nvarchar](50) NULL,
         [City] [nvarchar](50) NULL,
         [ZipCode] [char](5) NULL,
         [State] [char](2) NULL,
         [BirthDate] [date] NOT NULL
         PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY] );
         GO


## <a name="encrypt-columns-configure-always-encrypted"></a><span data-ttu-id="95ec3-179">Criptografar colunas (configurar o Always Encrypted)</span><span class="sxs-lookup"><span data-stu-id="95ec3-179">Encrypt columns (configure Always Encrypted)</span></span>
<span data-ttu-id="95ec3-180">SSMS fornece um assistente que ajuda você a configurar facilmente sempre criptografado por configuração Olá chave mestra da coluna, chave de criptografia de coluna e colunas criptografadas para você.</span><span class="sxs-lookup"><span data-stu-id="95ec3-180">SSMS provides a wizard that helps you easily configure Always Encrypted by setting up hello column master key, column encryption key, and encrypted columns for you.</span></span>

1. <span data-ttu-id="95ec3-181">Expandaa **Bancos de Dados** > **Clínica** > **Tabelas**.</span><span class="sxs-lookup"><span data-stu-id="95ec3-181">Expand **Databases** > **Clinic** > **Tables**.</span></span>
2. <span data-ttu-id="95ec3-182">Atalho Olá **pacientes** de tabela e selecione **criptografar colunas** Assistente de sempre criptografado Olá tooopen:</span><span class="sxs-lookup"><span data-stu-id="95ec3-182">Right-click hello **Patients** table and select **Encrypt Columns** tooopen hello Always Encrypted wizard:</span></span>
   
    ![Criptografar Colunas](./media/sql-database-always-encrypted-azure-key-vault/encrypt-columns.png)

<span data-ttu-id="95ec3-184">Assistente de sempre criptografado Hello inclui Olá seções a seguir: **seleção de coluna**, **configuração da chave mestra**, **validação**, e **resumo** .</span><span class="sxs-lookup"><span data-stu-id="95ec3-184">hello Always Encrypted wizard includes hello following sections: **Column Selection**, **Master Key Configuration**, **Validation**, and **Summary**.</span></span>

### <a name="column-selection"></a><span data-ttu-id="95ec3-185">Seleção de coluna</span><span class="sxs-lookup"><span data-stu-id="95ec3-185">Column Selection</span></span>
<span data-ttu-id="95ec3-186">Clique em **próximo** em Olá **Introdução** Olá de tooopen página **seleção de coluna** página.</span><span class="sxs-lookup"><span data-stu-id="95ec3-186">Click **Next** on hello **Introduction** page tooopen hello **Column Selection** page.</span></span> <span data-ttu-id="95ec3-187">Nessa página, você seleciona as colunas que você deseja tooencrypt, [Olá tipo de criptografia e qual chave de criptografia de coluna (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse.</span><span class="sxs-lookup"><span data-stu-id="95ec3-187">On this page, you will select which columns you want tooencrypt, [hello type of encryption, and what column encryption key (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse.</span></span>

<span data-ttu-id="95ec3-188">Criptografe as informações de **SSN** e **BirthDate** de cada paciente.</span><span class="sxs-lookup"><span data-stu-id="95ec3-188">Encrypt **SSN** and **BirthDate** information for each patient.</span></span> <span data-ttu-id="95ec3-189">coluna de SSN Olá usará criptografia determinística, que dá suporte a pesquisas de igualdade, junções e group by.</span><span class="sxs-lookup"><span data-stu-id="95ec3-189">hello SSN column will use deterministic encryption, which supports equality lookups, joins, and group by.</span></span> <span data-ttu-id="95ec3-190">coluna de data de nascimento Olá usará criptografia aleatória, que não oferece suporte a operações.</span><span class="sxs-lookup"><span data-stu-id="95ec3-190">hello BirthDate column will use randomized encryption, which does not support operations.</span></span>

<span data-ttu-id="95ec3-191">Saudação de conjunto **tipo de criptografia** coluna Olá SSN muito**determinística** e Olá coluna BirthDate muito**aleatória**.</span><span class="sxs-lookup"><span data-stu-id="95ec3-191">Set hello **Encryption Type** for hello SSN column too**Deterministic** and hello BirthDate column too**Randomized**.</span></span> <span data-ttu-id="95ec3-192">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="95ec3-192">Click **Next**.</span></span>

![Criptografar Colunas](./media/sql-database-always-encrypted-azure-key-vault/column-selection.png)

### <a name="master-key-configuration"></a><span data-ttu-id="95ec3-194">Configuração da Chave Mestra</span><span class="sxs-lookup"><span data-stu-id="95ec3-194">Master Key Configuration</span></span>
<span data-ttu-id="95ec3-195">Olá **configuração da chave mestra** página é onde você configurar a CMK e provedor de repositório de chaves hello selecione onde hello CMK será armazenado.</span><span class="sxs-lookup"><span data-stu-id="95ec3-195">hello **Master Key Configuration** page is where you set up your CMK and select hello key store provider where hello CMK will be stored.</span></span> <span data-ttu-id="95ec3-196">No momento, você pode armazenar uma CMK no repositório de certificados do Windows hello, o Cofre de chaves do Azure ou um módulo de segurança de hardware (HSM).</span><span class="sxs-lookup"><span data-stu-id="95ec3-196">Currently, you can store a CMK in hello Windows certificate store, Azure Key Vault, or a hardware security module (HSM).</span></span>

<span data-ttu-id="95ec3-197">Este tutorial mostra como toostore as chaves no cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="95ec3-197">This tutorial shows how toostore your keys in Azure Key Vault.</span></span>

1. <span data-ttu-id="95ec3-198">Selecione **Cofre de Chaves do Azure**.</span><span class="sxs-lookup"><span data-stu-id="95ec3-198">Select **Azure Key Vault**.</span></span>
2. <span data-ttu-id="95ec3-199">Selecione o Cofre de chave desejado Olá da lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="95ec3-199">Select hello desired key vault from hello drop-down list.</span></span>
3. <span data-ttu-id="95ec3-200">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="95ec3-200">Click **Next**.</span></span>

![Configuração da Chave Mestra](./media/sql-database-always-encrypted-azure-key-vault/master-key-configuration.png)

### <a name="validation"></a><span data-ttu-id="95ec3-202">Validação</span><span class="sxs-lookup"><span data-stu-id="95ec3-202">Validation</span></span>
<span data-ttu-id="95ec3-203">Você pode criptografar colunas Olá agora ou salvar um toorun de script do PowerShell mais tarde.</span><span class="sxs-lookup"><span data-stu-id="95ec3-203">You can encrypt hello columns now or save a PowerShell script toorun later.</span></span> <span data-ttu-id="95ec3-204">Para este tutorial, selecione **continuar toofinish agora** e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="95ec3-204">For this tutorial, select **Proceed toofinish now** and click **Next**.</span></span>

### <a name="summary"></a><span data-ttu-id="95ec3-205">Resumo</span><span class="sxs-lookup"><span data-stu-id="95ec3-205">Summary</span></span>
<span data-ttu-id="95ec3-206">Verifique se as configurações de saudação estão corretas e clique em **concluir** toocomplete o programa de instalação de saudação do sempre criptografado.</span><span class="sxs-lookup"><span data-stu-id="95ec3-206">Verify that hello settings are all correct and click **Finish** toocomplete hello setup for Always Encrypted.</span></span>

![Resumo](./media/sql-database-always-encrypted-azure-key-vault/summary.png)

### <a name="verify-hello-wizards-actions"></a><span data-ttu-id="95ec3-208">Verifique se ações do assistente Olá</span><span class="sxs-lookup"><span data-stu-id="95ec3-208">Verify hello wizard's actions</span></span>
<span data-ttu-id="95ec3-209">Concluído o Assistente de saudação, seu banco de dados está configurado para sempre criptografado.</span><span class="sxs-lookup"><span data-stu-id="95ec3-209">After hello wizard is finished, your database is set up for Always Encrypted.</span></span> <span data-ttu-id="95ec3-210">Olá Olá de assistente executado ações a seguir:</span><span class="sxs-lookup"><span data-stu-id="95ec3-210">hello wizard performed hello following actions:</span></span>

* <span data-ttu-id="95ec3-211">Criação de uma chave mestra de coluna e armazenamento no Cofre de Chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="95ec3-211">Created a column master key and stored it in Azure Key Vault.</span></span>
* <span data-ttu-id="95ec3-212">Criação de uma chave de criptografia de coluna e armazenamento no Cofre de Chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="95ec3-212">Created a column encryption key and stored it in Azure Key Vault.</span></span>
* <span data-ttu-id="95ec3-213">Saudação configurado selecionado colunas para criptografia.</span><span class="sxs-lookup"><span data-stu-id="95ec3-213">Configured hello selected columns for encryption.</span></span> <span data-ttu-id="95ec3-214">tabela de pacientes Olá atualmente não tem dados, mas os dados existentes nas colunas de saudação selecionada agora são criptografados.</span><span class="sxs-lookup"><span data-stu-id="95ec3-214">hello Patients table currently has no data, but any existing data in hello selected columns is now encrypted.</span></span>

<span data-ttu-id="95ec3-215">Verificar a criação de saudação de chaves Olá no SSMS expandindo **clínica** > **segurança** > **chaves Always Encrypted**.</span><span class="sxs-lookup"><span data-stu-id="95ec3-215">You can verify hello creation of hello keys in SSMS by expanding **Clinic** > **Security** > **Always Encrypted Keys**.</span></span>

## <a name="create-a-client-application-that-works-with-hello-encrypted-data"></a><span data-ttu-id="95ec3-216">Criar um aplicativo cliente que funciona com dados saudação criptografado</span><span class="sxs-lookup"><span data-stu-id="95ec3-216">Create a client application that works with hello encrypted data</span></span>
<span data-ttu-id="95ec3-217">Agora que sempre criptografado estiver configurado, você pode criar um aplicativo que realiza *insere* e *seleciona* em Olá colunas criptografadas.</span><span class="sxs-lookup"><span data-stu-id="95ec3-217">Now that Always Encrypted is set up, you can build an application that performs *inserts* and *selects* on hello encrypted columns.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="95ec3-218">O aplicativo deve usar [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) objetos ao passar o servidor de toohello de dados de texto sem formatação com colunas sempre criptografadas.</span><span class="sxs-lookup"><span data-stu-id="95ec3-218">Your application must use [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) objects when passing plaintext data toohello server with Always Encrypted columns.</span></span> <span data-ttu-id="95ec3-219">A passagem de valores literais sem usar objetos SqlParameter resultará em uma exceção.</span><span class="sxs-lookup"><span data-stu-id="95ec3-219">Passing literal values without using SqlParameter objects will result in an exception.</span></span>
> 
> 

1. <span data-ttu-id="95ec3-220">Abra o Visual Studio e crie um novo **Aplicativo de Console** do C# (Visual Studio 2015 e anterior) ou **Aplicativo de Console (.NET Framework)** (Visual Studio 2017 e posterior).</span><span class="sxs-lookup"><span data-stu-id="95ec3-220">Open Visual Studio and create a new C# **Console Application** (Visual Studio 2015 and earlier) or **Console App (.NET Framework)** (Visual Studio 2017 and later).</span></span> <span data-ttu-id="95ec3-221">Verifique se seu projeto está definido muito**do .NET Framework 4.6** ou posterior.</span><span class="sxs-lookup"><span data-stu-id="95ec3-221">Make sure your project is set too**.NET Framework 4.6** or later.</span></span>
2. <span data-ttu-id="95ec3-222">Projeto de saudação do nome **AlwaysEncryptedConsoleAKVApp** e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="95ec3-222">Name hello project **AlwaysEncryptedConsoleAKVApp** and click **OK**.</span></span>
3. <span data-ttu-id="95ec3-223">Instalar Olá seguintes pacotes do NuGet indo muito**ferramentas** > **NuGet Package Manager** > **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="95ec3-223">Install hello following NuGet packages by going too**Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>

<span data-ttu-id="95ec3-224">Execute estas duas linhas de código em Olá Package Manager Console.</span><span class="sxs-lookup"><span data-stu-id="95ec3-224">Run these two lines of code in hello Package Manager Console.</span></span>

    Install-Package Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory



## <a name="modify-your-connection-string-tooenable-always-encrypted"></a><span data-ttu-id="95ec3-225">Modificar sua tooenable de cadeia de caracteres de conexão sempre criptografado</span><span class="sxs-lookup"><span data-stu-id="95ec3-225">Modify your connection string tooenable Always Encrypted</span></span>
<span data-ttu-id="95ec3-226">Esta seção explica como tooenable sempre criptografados em sua cadeia de conexão do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="95ec3-226">This section  explains how tooenable Always Encrypted in your database connection string.</span></span>

<span data-ttu-id="95ec3-227">tooenable sempre criptografado, você precisa Olá tooadd **Column Encryption Setting** conexão de tooyour de palavra-chave da cadeia de caracteres e defini-lo muito**habilitado**.</span><span class="sxs-lookup"><span data-stu-id="95ec3-227">tooenable Always Encrypted, you need tooadd hello **Column Encryption Setting** keyword tooyour connection string and set it too**Enabled**.</span></span>

<span data-ttu-id="95ec3-228">Você pode definir isso diretamente na cadeia de caracteres de conexão hello, ou pode defini-lo usando [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span><span class="sxs-lookup"><span data-stu-id="95ec3-228">You can set this directly in hello connection string, or you can set it by using [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span></span> <span data-ttu-id="95ec3-229">aplicativo de exemplo Hello em Olá próxima seção mostra como toouse **SqlConnectionStringBuilder**.</span><span class="sxs-lookup"><span data-stu-id="95ec3-229">hello sample application in hello next section shows how toouse **SqlConnectionStringBuilder**.</span></span>

### <a name="enable-always-encrypted-in-hello-connection-string"></a><span data-ttu-id="95ec3-230">Habilitar o sempre criptografado na cadeia de caracteres de conexão Olá</span><span class="sxs-lookup"><span data-stu-id="95ec3-230">Enable Always Encrypted in hello connection string</span></span>
<span data-ttu-id="95ec3-231">Adicione Olá cadeia de caracteres de conexão de tooyour palavra-chave a seguir.</span><span class="sxs-lookup"><span data-stu-id="95ec3-231">Add hello following keyword tooyour connection string.</span></span>

    Column Encryption Setting=Enabled


### <a name="enable-always-encrypted-with-sqlconnectionstringbuilder"></a><span data-ttu-id="95ec3-232">Habilitar o Always Encrypted com SqlConnectionStringBuilder</span><span class="sxs-lookup"><span data-stu-id="95ec3-232">Enable Always Encrypted with SqlConnectionStringBuilder</span></span>
<span data-ttu-id="95ec3-233">Olá mostrado no código a seguir como tooenable sempre criptografado, definindo [Columnencryptionsetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) muito[habilitado](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span><span class="sxs-lookup"><span data-stu-id="95ec3-233">hello following code shows how tooenable Always Encrypted by setting [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) too[Enabled](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span></span>

    // Instantiate a SqlConnectionStringBuilder.
    SqlConnectionStringBuilder connStringBuilder =
       new SqlConnectionStringBuilder("replace with your connection string");

    // Enable Always Encrypted.
    connStringBuilder.ColumnEncryptionSetting =
       SqlConnectionColumnEncryptionSetting.Enabled;

## <a name="register-hello-azure-key-vault-provider"></a><span data-ttu-id="95ec3-234">Registrar provedor do Azure Key Vault Olá</span><span class="sxs-lookup"><span data-stu-id="95ec3-234">Register hello Azure Key Vault provider</span></span>
<span data-ttu-id="95ec3-235">Olá código a seguir mostra como tooregister Olá provedor de Cofre de chaves do Azure com o driver do ADO.NET hello.</span><span class="sxs-lookup"><span data-stu-id="95ec3-235">hello following code shows how tooregister hello Azure Key Vault provider with hello ADO.NET driver.</span></span>

    private static ClientCredential _clientCredential;

    static void InitializeAzureKeyVaultProvider()
    {
       _clientCredential = new ClientCredential(clientId, clientSecret);

       SqlColumnEncryptionAzureKeyVaultProvider azureKeyVaultProvider =
          new SqlColumnEncryptionAzureKeyVaultProvider(GetToken);

       Dictionary<string, SqlColumnEncryptionKeyStoreProvider> providers =
          new Dictionary<string, SqlColumnEncryptionKeyStoreProvider>();

       providers.Add(SqlColumnEncryptionAzureKeyVaultProvider.ProviderName, azureKeyVaultProvider);
       SqlConnection.RegisterColumnEncryptionKeyStoreProviders(providers);
    }



## <a name="always-encrypted-sample-console-application"></a><span data-ttu-id="95ec3-236">Aplicativo de console de exemplo do Always Encrypted</span><span class="sxs-lookup"><span data-stu-id="95ec3-236">Always Encrypted sample console application</span></span>
<span data-ttu-id="95ec3-237">Este exemplo demonstra como:</span><span class="sxs-lookup"><span data-stu-id="95ec3-237">This sample demonstrates how to:</span></span>

* <span data-ttu-id="95ec3-238">Modifique seu tooenable de cadeia de caracteres de conexão sempre criptografado.</span><span class="sxs-lookup"><span data-stu-id="95ec3-238">Modify your connection string tooenable Always Encrypted.</span></span>
* <span data-ttu-id="95ec3-239">Registre o Cofre de chaves do Azure como Olá provedor de repositório de chaves do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="95ec3-239">Register Azure Key Vault as hello application's key store provider.</span></span>  
* <span data-ttu-id="95ec3-240">Inserir dados nas colunas de saudação criptografada.</span><span class="sxs-lookup"><span data-stu-id="95ec3-240">Insert data into hello encrypted columns.</span></span>
* <span data-ttu-id="95ec3-241">Selecionar um registro por filtragem para um valor específico em uma coluna criptografada.</span><span class="sxs-lookup"><span data-stu-id="95ec3-241">Select a record by filtering for a specific value in an encrypted column.</span></span>

<span data-ttu-id="95ec3-242">Substitua o conteúdo de saudação do **Program.cs** com hello código a seguir.</span><span class="sxs-lookup"><span data-stu-id="95ec3-242">Replace hello contents of **Program.cs** with hello following code.</span></span> <span data-ttu-id="95ec3-243">Substitua a cadeia de caracteres de conexão de saudação para a variável de connectionString global Olá na linha de saudação que precede diretamente o método Main de saudação com a cadeia de conexão válida do hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="95ec3-243">Replace hello connection string for hello global connectionString variable in hello line that directly precedes hello Main method with your valid connection string from hello Azure portal.</span></span> <span data-ttu-id="95ec3-244">Essa é Olá alteração só é necessário toomake toothis código.</span><span class="sxs-lookup"><span data-stu-id="95ec3-244">This is hello only change you need toomake toothis code.</span></span>

<span data-ttu-id="95ec3-245">Execute Olá aplicativo toosee sempre criptografado em ação.</span><span class="sxs-lookup"><span data-stu-id="95ec3-245">Run hello app toosee Always Encrypted in action.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Data;
    using System.Data.SqlClient;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider;

    namespace AlwaysEncryptedConsoleAKVApp
    {
    class Program
    {
        // Update this line with your Clinic database connection string from hello Azure portal.
        static string connectionString = @"<connection string from hello portal>";
        static string clientId = @"<client id from step 7 above>";
        static string clientSecret = "<key from step 13 above>";


        static void Main(string[] args)
        {
            InitializeAzureKeyVaultProvider();

            Console.WriteLine("Signed in as: " + _clientCredential.ClientId);

            Console.WriteLine("Original connection string copied from hello Azure portal:");
            Console.WriteLine(connectionString);

            // Create a SqlConnectionStringBuilder.
            SqlConnectionStringBuilder connStringBuilder =
                new SqlConnectionStringBuilder(connectionString);

            // Enable Always Encrypted for hello connection.
            // This is hello only change specific tooAlways Encrypted
            connStringBuilder.ColumnEncryptionSetting =
                SqlConnectionColumnEncryptionSetting.Enabled;

            Console.WriteLine(Environment.NewLine + "Updated connection string with Always Encrypted enabled:");
            Console.WriteLine(connStringBuilder.ConnectionString);

            // Update hello connection string with a password supplied at runtime.
            Console.WriteLine(Environment.NewLine + "Enter server password:");
            connStringBuilder.Password = Console.ReadLine();


            // Assign hello updated connection string tooour global variable.
            connectionString = connStringBuilder.ConnectionString;


            // Delete all records toorestart this demo app.
            ResetPatientsTable();

            // Add sample data toohello Patients table.
            Console.Write(Environment.NewLine + "Adding sample patient data toohello database...");

            InsertPatient(new Patient()
            {
                SSN = "999-99-0001",
                FirstName = "Orlando",
                LastName = "Gee",
                BirthDate = DateTime.Parse("01/04/1964")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0002",
                FirstName = "Keith",
                LastName = "Harris",
                BirthDate = DateTime.Parse("06/20/1977")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0003",
                FirstName = "Donna",
                LastName = "Carreras",
                BirthDate = DateTime.Parse("02/09/1973")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0004",
                FirstName = "Janet",
                LastName = "Gates",
                BirthDate = DateTime.Parse("08/31/1985")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0005",
                FirstName = "Lucy",
                LastName = "Harrington",
                BirthDate = DateTime.Parse("05/06/1993")
            });


            // Fetch and display all patients.
            Console.WriteLine(Environment.NewLine + "All hello records currently in hello Patients table:");

            foreach (Patient patient in SelectAllPatients())
            {
                Console.WriteLine(patient.FirstName + " " + patient.LastName + "\tSSN: " + patient.SSN + "\tBirthdate: " + patient.BirthDate);
            }

            // Get patients by SSN.
            Console.WriteLine(Environment.NewLine + "Now lets locate records by searching hello encrypted SSN column.");

            string ssn;

            // This very simple validation only checks that hello user entered 11 characters.
            // In production be sure toocheck all user input and use hello best validation for your specific application.
            do
            {
                Console.WriteLine("Please enter a valid SSN (ex. 999-99-0003):");
                ssn = Console.ReadLine();
            } while (ssn.Length != 11);

            // hello example allows duplicate SSN entries so we will return all records
            // that match hello provided value and store hello results in selectedPatients.
            Patient selectedPatient = SelectPatientBySSN(ssn);

            // Check if any records were returned and display our query results.
            if (selectedPatient != null)
            {
                Console.WriteLine("Patient found with SSN = " + ssn);
                Console.WriteLine(selectedPatient.FirstName + " " + selectedPatient.LastName + "\tSSN: "
                    + selectedPatient.SSN + "\tBirthdate: " + selectedPatient.BirthDate);
            }
            else
            {
                Console.WriteLine("No patients found with SSN = " + ssn);
            }

            Console.WriteLine("Press Enter tooexit...");
            Console.ReadLine();
        }


        private static ClientCredential _clientCredential;

        static void InitializeAzureKeyVaultProvider()
        {

            _clientCredential = new ClientCredential(clientId, clientSecret);

            SqlColumnEncryptionAzureKeyVaultProvider azureKeyVaultProvider =
              new SqlColumnEncryptionAzureKeyVaultProvider(GetToken);

            Dictionary<string, SqlColumnEncryptionKeyStoreProvider> providers =
              new Dictionary<string, SqlColumnEncryptionKeyStoreProvider>();

            providers.Add(SqlColumnEncryptionAzureKeyVaultProvider.ProviderName, azureKeyVaultProvider);
            SqlConnection.RegisterColumnEncryptionKeyStoreProviders(providers);
        }

        public async static Task<string> GetToken(string authority, string resource, string scope)
        {
            var authContext = new AuthenticationContext(authority);
            AuthenticationResult result = await authContext.AcquireTokenAsync(resource, _clientCredential);

            if (result == null)
                throw new InvalidOperationException("Failed tooobtain hello access token");
            return result.AccessToken;
        }

        static int InsertPatient(Patient newPatient)
        {
            int returnValue = 0;

            string sqlCmdText = @"INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate])
     VALUES (@SSN, @FirstName, @LastName, @BirthDate);";

            SqlCommand sqlCmd = new SqlCommand(sqlCmdText);


            SqlParameter paramSSN = new SqlParameter(@"@SSN", newPatient.SSN);
            paramSSN.DbType = DbType.AnsiStringFixedLength;
            paramSSN.Direction = ParameterDirection.Input;
            paramSSN.Size = 11;

            SqlParameter paramFirstName = new SqlParameter(@"@FirstName", newPatient.FirstName);
            paramFirstName.DbType = DbType.String;
            paramFirstName.Direction = ParameterDirection.Input;

            SqlParameter paramLastName = new SqlParameter(@"@LastName", newPatient.LastName);
            paramLastName.DbType = DbType.String;
            paramLastName.Direction = ParameterDirection.Input;

            SqlParameter paramBirthDate = new SqlParameter(@"@BirthDate", newPatient.BirthDate);
            paramBirthDate.SqlDbType = SqlDbType.Date;
            paramBirthDate.Direction = ParameterDirection.Input;

            sqlCmd.Parameters.Add(paramSSN);
            sqlCmd.Parameters.Add(paramFirstName);
            sqlCmd.Parameters.Add(paramLastName);
            sqlCmd.Parameters.Add(paramBirthDate);

            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    sqlCmd.ExecuteNonQuery();
                }
                catch (Exception ex)
                {
                    returnValue = 1;
                    Console.WriteLine("hello following error was encountered: ");
                    Console.WriteLine(ex.Message);
                    Console.WriteLine(Environment.NewLine + "Press Enter key tooexit");
                    Console.ReadLine();
                    Environment.Exit(0);
                }
            }
            return returnValue;
        }


        static List<Patient> SelectAllPatients()
        {
            List<Patient> patients = new List<Patient>();


            SqlCommand sqlCmd = new SqlCommand(
              "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients]",
                new SqlConnection(connectionString));


            using (sqlCmd.Connection = new SqlConnection(connectionString))

            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    SqlDataReader reader = sqlCmd.ExecuteReader();

                    if (reader.HasRows)
                    {
                        while (reader.Read())
                        {
                            patients.Add(new Patient()
                            {
                                SSN = reader[0].ToString(),
                                FirstName = reader[1].ToString(),
                                LastName = reader["LastName"].ToString(),
                                BirthDate = (DateTime)reader["BirthDate"]
                            });
                        }
                    }
                }
                catch (Exception ex)
                {
                    throw;
                }
            }

            return patients;
        }


        static Patient SelectPatientBySSN(string ssn)
        {
            Patient patient = new Patient();

            SqlCommand sqlCmd = new SqlCommand(
                "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [SSN]=@SSN",
                new SqlConnection(connectionString));

            SqlParameter paramSSN = new SqlParameter(@"@SSN", ssn);
            paramSSN.DbType = DbType.AnsiStringFixedLength;
            paramSSN.Direction = ParameterDirection.Input;
            paramSSN.Size = 11;

            sqlCmd.Parameters.Add(paramSSN);


            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    SqlDataReader reader = sqlCmd.ExecuteReader();

                    if (reader.HasRows)
                    {
                        while (reader.Read())
                        {
                            patient = new Patient()
                            {
                                SSN = reader[0].ToString(),
                                FirstName = reader[1].ToString(),
                                LastName = reader["LastName"].ToString(),
                                BirthDate = (DateTime)reader["BirthDate"]
                            };
                        }
                    }
                    else
                    {
                        patient = null;
                    }
                }
                catch (Exception ex)
                {
                    throw;
                }
            }
            return patient;
        }


        // This method simply deletes all records in hello Patients table tooreset our demo.
        static int ResetPatientsTable()
        {
            int returnValue = 0;

            SqlCommand sqlCmd = new SqlCommand("DELETE FROM Patients");
            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    sqlCmd.ExecuteNonQuery();

                }
                catch (Exception ex)
                {
                    returnValue = 1;
                }
            }
            return returnValue;
        }
    }

    class Patient
    {
        public string SSN { get; set; }
        public string FirstName { get; set; }
        public string LastName { get; set; }
        public DateTime BirthDate { get; set; }
    }
    }



## <a name="verify-that-hello-data-is-encrypted"></a><span data-ttu-id="95ec3-246">Verificar se os dados de saudação foi criptografados</span><span class="sxs-lookup"><span data-stu-id="95ec3-246">Verify that hello data is encrypted</span></span>
<span data-ttu-id="95ec3-247">Você pode verificar rapidamente que dados reais de saudação no servidor de saudação são criptografados consultando dados de pacientes saudação com o SSMS (usando sua conexão atual onde **Column Encryption Setting** ainda não foi habilitado).</span><span class="sxs-lookup"><span data-stu-id="95ec3-247">You can quickly check that hello actual data on hello server is encrypted by querying hello Patients data with SSMS (using your current connection where **Column Encryption Setting** is not yet enabled).</span></span>

<span data-ttu-id="95ec3-248">Execute Olá consulta a seguir no banco de dados de clínica hello.</span><span class="sxs-lookup"><span data-stu-id="95ec3-248">Run hello following query on hello Clinic database.</span></span>

    SELECT FirstName, LastName, SSN, BirthDate FROM Patients;

<span data-ttu-id="95ec3-249">Você pode ver que colunas Olá criptografado não contêm nenhum dado de texto sem formatação.</span><span class="sxs-lookup"><span data-stu-id="95ec3-249">You can see that hello encrypted columns do not contain any plaintext data.</span></span>

   ![Novo aplicativo de console](./media/sql-database-always-encrypted-azure-key-vault/ssms-encrypted.png)

<span data-ttu-id="95ec3-251">toouse SSMS tooaccess Olá dados de texto sem formatação, você pode adicionar Olá *Column Encryption Setting = habilitado* conexão de toohello do parâmetro.</span><span class="sxs-lookup"><span data-stu-id="95ec3-251">toouse SSMS tooaccess hello plaintext data, you can add hello *Column Encryption Setting=enabled* parameter toohello connection.</span></span>

1. <span data-ttu-id="95ec3-252">No SSMS, clique com o botão direito do mouse em seu servidor no **Pesquisador de Objetos** e escolha **Desconectar**.</span><span class="sxs-lookup"><span data-stu-id="95ec3-252">In SSMS, right-click your server in **Object Explorer** and choose **Disconnect**.</span></span>
2. <span data-ttu-id="95ec3-253">Clique em **conectar** > **mecanismo de banco de dados** tooopen Olá **conectar tooServer** janela e clique em **opções**.</span><span class="sxs-lookup"><span data-stu-id="95ec3-253">Click **Connect** > **Database Engine** tooopen hello **Connect tooServer** window and click **Options**.</span></span>
3. <span data-ttu-id="95ec3-254">Clique em **Parâmetros Adicionais de Conexão** e digite **Column Encryption Setting=enabled**.</span><span class="sxs-lookup"><span data-stu-id="95ec3-254">Click **Additional Connection Parameters** and type **Column Encryption Setting=enabled**.</span></span>
   
    ![Novo aplicativo de console](./media/sql-database-always-encrypted-azure-key-vault/ssms-connection-parameter.png)
4. <span data-ttu-id="95ec3-256">Execute Olá consulta a seguir no banco de dados de clínica hello.</span><span class="sxs-lookup"><span data-stu-id="95ec3-256">Run hello following query on hello Clinic database.</span></span>
   
        SELECT FirstName, LastName, SSN, BirthDate FROM Patients;
   
     <span data-ttu-id="95ec3-257">Agora você pode ver os dados de texto sem formatação de saudação em colunas criptografada de saudação.</span><span class="sxs-lookup"><span data-stu-id="95ec3-257">You can now see hello plaintext data in hello encrypted columns.</span></span>

    ![Novo aplicativo de console](./media/sql-database-always-encrypted-azure-key-vault/ssms-plaintext.png)


## <a name="next-steps"></a><span data-ttu-id="95ec3-259">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="95ec3-259">Next steps</span></span>
<span data-ttu-id="95ec3-260">Depois de criar um banco de dados que usa o sempre criptografado, você poderá desejar a seguir Olá toodo:</span><span class="sxs-lookup"><span data-stu-id="95ec3-260">After you create a database that uses Always Encrypted, you may want toodo hello following:</span></span>

* <span data-ttu-id="95ec3-261">[Girar e limpar suas chaves](https://msdn.microsoft.com/library/mt607048.aspx).</span><span class="sxs-lookup"><span data-stu-id="95ec3-261">[Rotate and clean up your keys](https://msdn.microsoft.com/library/mt607048.aspx).</span></span>
* <span data-ttu-id="95ec3-262">[Migrar dados que já foram criptografados com o Always Encrypted](https://msdn.microsoft.com/library/mt621539.aspx).</span><span class="sxs-lookup"><span data-stu-id="95ec3-262">[Migrate data that is already encrypted with Always Encrypted](https://msdn.microsoft.com/library/mt621539.aspx).</span></span>

## <a name="related-information"></a><span data-ttu-id="95ec3-263">Informações relacionadas</span><span class="sxs-lookup"><span data-stu-id="95ec3-263">Related information</span></span>
* [<span data-ttu-id="95ec3-264">Always Encrypted (Desenvolvimento Cliente)</span><span class="sxs-lookup"><span data-stu-id="95ec3-264">Always Encrypted (client development)</span></span>](https://msdn.microsoft.com/library/mt147923.aspx)
* [<span data-ttu-id="95ec3-265">Transparent Data Encryption</span><span class="sxs-lookup"><span data-stu-id="95ec3-265">Transparent data encryption</span></span>](https://msdn.microsoft.com/library/bb934049.aspx)
* [<span data-ttu-id="95ec3-266">Criptografia do SQL Server</span><span class="sxs-lookup"><span data-stu-id="95ec3-266">SQL Server encryption</span></span>](https://msdn.microsoft.com/library/bb510663.aspx)
* [<span data-ttu-id="95ec3-267">Assistente do Always Encrypted</span><span class="sxs-lookup"><span data-stu-id="95ec3-267">Always Encrypted wizard</span></span>](https://msdn.microsoft.com/library/mt459280.aspx)
* [<span data-ttu-id="95ec3-268">Blog do Always Encrypted</span><span class="sxs-lookup"><span data-stu-id="95ec3-268">Always Encrypted blog</span></span>](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

