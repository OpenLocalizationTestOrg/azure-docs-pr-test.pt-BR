---
title: 'Always Encrypted: Banco de Dados SQL do Azure - armazenamento de certificados do Windows | Microsoft Docs'
description: "Este artigo mostra como proteger os dados confidenciais no banco de dados SQL com a criptografia de banco de dados usando o Assistente Always Encrypted no SQL Server Management Studio (SSMS). Ele mostra como armazenar suas chaves de criptografia no repositório de certificados do Windows."
keywords: criptografar dados, criptografia do sql, criptografia de banco de dados, dados confidenciais, sempre criptografados
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: cgronlun
ms.assetid: ce7e052e-8bf6-4d7c-9204-4c6f4afeba4b
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/02/2017
ms.author: sstein
ms.openlocfilehash: d1fdfc4f739e65ff532b159eefaffe1622ad0963
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="always-encrypted-protect-sensitive-data-in-sql-database-and-store-your-encryption-keys-in-the-windows-certificate-store"></a><span data-ttu-id="ec303-105">Always Encrypted: proteger dados confidenciais no Banco de Dados SQL e armazenar suas chaves de criptografia no repositório de certificados do Windows</span><span class="sxs-lookup"><span data-stu-id="ec303-105">Always Encrypted: Protect sensitive data in SQL Database and store your encryption keys in the Windows certificate store</span></span>

<span data-ttu-id="ec303-106">Este artigo mostra como proteger os dados confidenciais no banco de dados SQL com a criptografia de banco de dados usando o [Assistente Always Encrypted](https://msdn.microsoft.com/library/mt459280.aspx) no [SSMS (SQL Server Management Studio](https://msdn.microsoft.com/library/hh213248.aspx).</span><span class="sxs-lookup"><span data-stu-id="ec303-106">This article shows you how to secure sensitive data in a SQL database with database encryption by using the [Always Encrypted Wizard](https://msdn.microsoft.com/library/mt459280.aspx) in [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span></span> <span data-ttu-id="ec303-107">Ele mostra como armazenar suas chaves de criptografia no repositório de certificados do Windows.</span><span class="sxs-lookup"><span data-stu-id="ec303-107">It also shows you how to store your encryption keys in the Windows certificate store.</span></span>

<span data-ttu-id="ec303-108">O Always Encrypted é uma nova tecnologia de criptografia de dados no Banco de Dados SQL do Azure e no SQL Server que ajuda a proteger dados confidenciais em repouso no servidor, durante a movimentação entre o cliente e o servidor e enquanto os dados estão em uso, garantindo que os dados confidenciais nunca apareçam como texto não criptografado dentro do sistema de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="ec303-108">Always Encrypted is a new data encryption technology in Azure SQL Database and SQL Server that helps protect sensitive data at rest on the server, during movement between client and server, and while the data is in use, ensuring that sensitive data never appears as plaintext inside the database system.</span></span> <span data-ttu-id="ec303-109">Depois de criptografar dados, somente aplicativos cliente ou servidores de aplicativos que têm acesso às chaves podem acessar dados de texto não criptografado.</span><span class="sxs-lookup"><span data-stu-id="ec303-109">After you encrypt data, only client applications or app servers that have access to the keys can access plaintext data.</span></span> <span data-ttu-id="ec303-110">Para obter informações detalhadas, consulte [Always Encrypted (Mecanismo do Banco de Dados)](https://msdn.microsoft.com/library/mt163865.aspx).</span><span class="sxs-lookup"><span data-stu-id="ec303-110">For detailed information, see [Always Encrypted (Database Engine)](https://msdn.microsoft.com/library/mt163865.aspx).</span></span>

<span data-ttu-id="ec303-111">Depois de configurar o banco de dados para usar o Always Encrypted, você criará um aplicativo cliente em C# com o Visual Studio para trabalhar com os dados criptografados.</span><span class="sxs-lookup"><span data-stu-id="ec303-111">After configuring the database to use Always Encrypted, you will create a client application in C# with Visual Studio to work with the encrypted data.</span></span>

<span data-ttu-id="ec303-112">Siga as etapas neste artigo para saber como configurar o Always Encrypted para um banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="ec303-112">Follow the steps in this article to learn how to set up Always Encrypted for an Azure SQL database.</span></span> <span data-ttu-id="ec303-113">Neste artigo, você aprenderá como realizar as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="ec303-113">In this article, you will learn how to perform the following tasks:</span></span>

* <span data-ttu-id="ec303-114">Usar o assistente Always Encrypted no SSMS para criar [Chaves Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span><span class="sxs-lookup"><span data-stu-id="ec303-114">Use the Always Encrypted wizard in SSMS to create [Always Encrypted Keys](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span></span>
  * <span data-ttu-id="ec303-115">Crie uma [CMK (Chave Mestra da Coluna)](https://msdn.microsoft.com/library/mt146393.aspx).</span><span class="sxs-lookup"><span data-stu-id="ec303-115">Create a [Column Master Key (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).</span></span>
  * <span data-ttu-id="ec303-116">Crie uma [CEK (Chave de Criptografia da Coluna)](https://msdn.microsoft.com/library/mt146372.aspx).</span><span class="sxs-lookup"><span data-stu-id="ec303-116">Create a [Column Encryption Key (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).</span></span>
* <span data-ttu-id="ec303-117">Criar uma tabela de banco de dados e criptografar colunas.</span><span class="sxs-lookup"><span data-stu-id="ec303-117">Create a database table and encrypt columns.</span></span>
* <span data-ttu-id="ec303-118">Crie um aplicativo que insira, selecione e exiba os dados das colunas criptografadas.</span><span class="sxs-lookup"><span data-stu-id="ec303-118">Create an application that inserts, selects, and displays data from the encrypted columns.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ec303-119">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ec303-119">Prerequisites</span></span>
<span data-ttu-id="ec303-120">Para este tutorial, será necessário:</span><span class="sxs-lookup"><span data-stu-id="ec303-120">For this tutorial, you'll need:</span></span>

* <span data-ttu-id="ec303-121">Uma conta e uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="ec303-121">An Azure account and subscription.</span></span> <span data-ttu-id="ec303-122">Se não tiver uma, inscreva-se em uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ec303-122">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="ec303-123">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) versão 13.0.700.242 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="ec303-123">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) version 13.0.700.242 or later.</span></span>
* <span data-ttu-id="ec303-124">[.NET Framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) ou posterior (no computador cliente).</span><span class="sxs-lookup"><span data-stu-id="ec303-124">[.NET Framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) or later (on the client computer).</span></span>
* <span data-ttu-id="ec303-125">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="ec303-125">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span></span>

## <a name="create-a-blank-sql-database"></a><span data-ttu-id="ec303-126">Criar um banco de dados SQL em branco</span><span class="sxs-lookup"><span data-stu-id="ec303-126">Create a blank SQL database</span></span>
1. <span data-ttu-id="ec303-127">Entre no [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ec303-127">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="ec303-128">Clique em **Novo** > **Dados + Armazenamento** > **Banco de Dados SQL**.</span><span class="sxs-lookup"><span data-stu-id="ec303-128">Click **New** > **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="ec303-129">Crie um banco de dados **Em branco** chamado **Clínica** em um servidor novo ou existente.</span><span class="sxs-lookup"><span data-stu-id="ec303-129">Create a **Blank** database named **Clinic** on a new or existing server.</span></span> <span data-ttu-id="ec303-130">Para obter instruções detalhadas sobre como criar um banco de dados no Portal do Azure, consulte [Seu primeiro Banco de Dados SQL do Azure](sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ec303-130">For detailed instructions about creating a database in the Azure portal, see [Your first Azure SQL database](sql-database-get-started-portal.md).</span></span>
   
    ![Criar um banco de dados vazio](./media/sql-database-always-encrypted/create-database.png)

<span data-ttu-id="ec303-132">Você precisará da cadeia de conexão posteriormente neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="ec303-132">You will need the connection string later in the tutorial.</span></span> <span data-ttu-id="ec303-133">Depois que o banco de dados for criado, vá para o novo banco de dados Clínica e copie a cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="ec303-133">After the database is created, go to the new Clinic database and copy the connection string.</span></span> <span data-ttu-id="ec303-134">Você pode obter a cadeia de conexão a qualquer momento, mas é fácil para copiá-la quando estiver no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ec303-134">You can get the connection string at any time, but it's easy to copy it when you're in the Azure portal.</span></span>

1. <span data-ttu-id="ec303-135">Clique em **Bancos de dados SQL** > **Clínica** > **Mostrar cadeias de conexão do banco de dados**.</span><span class="sxs-lookup"><span data-stu-id="ec303-135">Click **SQL databases** > **Clinic** > **Show database connection strings**.</span></span>
2. <span data-ttu-id="ec303-136">Copie a cadeia de conexão para **ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="ec303-136">Copy the connection string for **ADO.NET**.</span></span>
   
    ![Copiar a cadeia de conexão](./media/sql-database-always-encrypted/connection-strings.png)

## <a name="connect-to-the-database-with-ssms"></a><span data-ttu-id="ec303-138">Conectar-se ao banco de dados com o SSMS</span><span class="sxs-lookup"><span data-stu-id="ec303-138">Connect to the database with SSMS</span></span>
<span data-ttu-id="ec303-139">Abra o SSMS e conecte-se ao servidor com o banco de dados Clínica.</span><span class="sxs-lookup"><span data-stu-id="ec303-139">Open SSMS and connect to the server with the Clinic database.</span></span>

1. <span data-ttu-id="ec303-140">Abra o SSMS.</span><span class="sxs-lookup"><span data-stu-id="ec303-140">Open SSMS.</span></span> <span data-ttu-id="ec303-141">(Clique em **Conectar** > **Mecanismo de Banco de Dados** para abrir a janela **Conectar ao Servidor**, caso não esteja aberta).</span><span class="sxs-lookup"><span data-stu-id="ec303-141">(Click **Connect** > **Database Engine** to open the **Connect to Server** window if it is not open).</span></span>
2. <span data-ttu-id="ec303-142">Insira o nome do servidor e credenciais.</span><span class="sxs-lookup"><span data-stu-id="ec303-142">Enter your server name and credentials.</span></span> <span data-ttu-id="ec303-143">O nome do servidor pode ser encontrado na folha do banco de dados SQL e na cadeia de conexão que você copiou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ec303-143">The server name can be found on the SQL database blade and in the connection string you copied earlier.</span></span> <span data-ttu-id="ec303-144">Digite o nome completo do servidor, incluindo *database.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="ec303-144">Type the complete server name including *database.windows.net*.</span></span>
   
    ![Copiar a cadeia de conexão](./media/sql-database-always-encrypted/ssms-connect.png)

<span data-ttu-id="ec303-146">Se a janela **Nova Regra de Firewall** for aberta, entre no Azure e deixe o SSMS criar uma nova regra de firewall para você.</span><span class="sxs-lookup"><span data-stu-id="ec303-146">If the **New Firewall Rule** window opens, sign in to Azure and let SSMS create a new firewall rule for you.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="ec303-147">Criar uma tabela</span><span class="sxs-lookup"><span data-stu-id="ec303-147">Create a table</span></span>
<span data-ttu-id="ec303-148">Nesta seção, você criará uma tabela para armazenar os dados dos pacientes.</span><span class="sxs-lookup"><span data-stu-id="ec303-148">In this section, you will create a table to hold patient data.</span></span> <span data-ttu-id="ec303-149">Inicialmente, essa será uma tabela normal; você vai configurar a criptografia na próxima seção.</span><span class="sxs-lookup"><span data-stu-id="ec303-149">This will be a normal table initially--you will configure encryption in the next section.</span></span>

1. <span data-ttu-id="ec303-150">Expanda **Bancos de Dados**.</span><span class="sxs-lookup"><span data-stu-id="ec303-150">Expand **Databases**.</span></span>
2. <span data-ttu-id="ec303-151">Clique com o botão direito do mouse no banco de dados **Clínica** e clique em **Nova Consulta**.</span><span class="sxs-lookup"><span data-stu-id="ec303-151">Right-click the **Clinic** database and click **New Query**.</span></span>
3. <span data-ttu-id="ec303-152">Cole o T-SQL (Transact-SQL) a seguir na janela de nova consulta e o **execute** .</span><span class="sxs-lookup"><span data-stu-id="ec303-152">Paste the following Transact-SQL (T-SQL) into the new query window and **Execute** it.</span></span>

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


## <a name="encrypt-columns-configure-always-encrypted"></a><span data-ttu-id="ec303-153">Criptografar colunas (configurar o Always Encrypted)</span><span class="sxs-lookup"><span data-stu-id="ec303-153">Encrypt columns (configure Always Encrypted)</span></span>
<span data-ttu-id="ec303-154">O SSMS fornece um assistente para configurar facilmente o Always Encrypted definindo as colunas criptografadas, CMK e CEK para você.</span><span class="sxs-lookup"><span data-stu-id="ec303-154">SSMS provides a wizard to easily configure Always Encrypted by setting up the CMK, CEK, and encrypted columns for you.</span></span>

1. <span data-ttu-id="ec303-155">Expandaa **Bancos de Dados** > **Clínica** > **Tabelas**.</span><span class="sxs-lookup"><span data-stu-id="ec303-155">Expand **Databases** > **Clinic** > **Tables**.</span></span>
2. <span data-ttu-id="ec303-156">Clique com o botão direito do mouse na tabela **Pacientes** e selecione **Criptografar Colunas** para abrir o Assistente Sempre Criptografado:</span><span class="sxs-lookup"><span data-stu-id="ec303-156">Right-click the **Patients** table and select **Encrypt Columns** to open the Always Encrypted wizard:</span></span>
   
    ![Criptografar Colunas](./media/sql-database-always-encrypted/encrypt-columns.png)

<span data-ttu-id="ec303-158">O assistente Always Encrypted inclui as seguintes seções: **Seleção de Coluna**, CMK (**Configuração da Chave Mestra**), **Validação** e **Resumo**.</span><span class="sxs-lookup"><span data-stu-id="ec303-158">The Always Encrypted wizard includes the following sections: **Column Selection**, **Master Key Configuration** (CMK), **Validation**, and **Summary**.</span></span>

### <a name="column-selection"></a><span data-ttu-id="ec303-159">Seleção de coluna</span><span class="sxs-lookup"><span data-stu-id="ec303-159">Column Selection</span></span>
<span data-ttu-id="ec303-160">Clique em **Avançar** na página **Introdução** para abrir a página **Seleção de Coluna**.</span><span class="sxs-lookup"><span data-stu-id="ec303-160">Click **Next** on the **Introduction** page to open the **Column Selection** page.</span></span> <span data-ttu-id="ec303-161">Nessa página, você escolherá as colunas que quer criptografar, [o tipo de criptografia e quais CEK (Chave de Criptografia da Coluna)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) usar.</span><span class="sxs-lookup"><span data-stu-id="ec303-161">On this page, you will select which columns you want to encrypt, [the type of encryption, and what column encryption key (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) to use.</span></span>

<span data-ttu-id="ec303-162">Criptografe as informações de **SSN** e **BirthDate** de cada paciente.</span><span class="sxs-lookup"><span data-stu-id="ec303-162">Encrypt **SSN** and **BirthDate** information for each patient.</span></span> <span data-ttu-id="ec303-163">A coluna **SSN** usará criptografia determinística, que dá suporte a pesquisas de igualdade, junções e agrupamentos por categoria.</span><span class="sxs-lookup"><span data-stu-id="ec303-163">The **SSN** column will use deterministic encryption, which supports equality lookups, joins, and group by.</span></span> <span data-ttu-id="ec303-164">A coluna **BirthDate** usará criptografia aleatória, que não permite operações.</span><span class="sxs-lookup"><span data-stu-id="ec303-164">The **BirthDate** column will use randomized encryption, which does not support operations.</span></span>

<span data-ttu-id="ec303-165">Defina o **Tipo de Criptografia** para a coluna **SSN** como **Determinístico** e a coluna **BirthDate** como **Aleatório**.</span><span class="sxs-lookup"><span data-stu-id="ec303-165">Set the **Encryption Type** for the **SSN** column to **Deterministic** and the **BirthDate** column to **Randomized**.</span></span> <span data-ttu-id="ec303-166">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="ec303-166">Click **Next**.</span></span>

![Criptografar Colunas](./media/sql-database-always-encrypted/column-selection.png)

### <a name="master-key-configuration"></a><span data-ttu-id="ec303-168">Configuração da Chave Mestra</span><span class="sxs-lookup"><span data-stu-id="ec303-168">Master Key Configuration</span></span>
<span data-ttu-id="ec303-169">Na página **Configuração da Chave Mestra** , é possível configurar a CMK e escolher o provedor do repositório de chaves em que a CMK será armazenada.</span><span class="sxs-lookup"><span data-stu-id="ec303-169">The **Master Key Configuration** page is where you set up your CMK and select the key store provider where the CMK will be stored.</span></span> <span data-ttu-id="ec303-170">No momento, é possível armazenar uma CMK no repositório de certificados do Windows, no Cofre de Chaves do Azure ou em um HSM (Módulo de Segurança de Hardware).</span><span class="sxs-lookup"><span data-stu-id="ec303-170">Currently, you can store a CMK in the Windows certificate store, Azure Key Vault, or a hardware security module (HSM).</span></span> <span data-ttu-id="ec303-171">Este tutorial mostra como armazenar suas chaves no repositório de certificados do Windows.</span><span class="sxs-lookup"><span data-stu-id="ec303-171">This tutorial shows how to store your keys in the Windows certificate store.</span></span>

<span data-ttu-id="ec303-172">Verifique se **Repositório de certificados do Windows** está marcado e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="ec303-172">Verify that **Windows certificate store** is selected and click **Next**.</span></span>

![Configuração da Chave Mestra](./media/sql-database-always-encrypted/master-key-configuration.png)

### <a name="validation"></a><span data-ttu-id="ec303-174">Validação</span><span class="sxs-lookup"><span data-stu-id="ec303-174">Validation</span></span>
<span data-ttu-id="ec303-175">Você pode criptografar as colunas agora ou salvar um script do PowerShell para execução posterior.</span><span class="sxs-lookup"><span data-stu-id="ec303-175">You can encrypt the columns now or save a PowerShell script to run later.</span></span> <span data-ttu-id="ec303-176">Para este tutorial, selecione **Seguir para a conclusão agora** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="ec303-176">For this tutorial, select **Proceed to finish now** and click **Next**.</span></span>

### <a name="summary"></a><span data-ttu-id="ec303-177">Resumo</span><span class="sxs-lookup"><span data-stu-id="ec303-177">Summary</span></span>
<span data-ttu-id="ec303-178">Verifique se as configurações estão corretas e clique em **Concluir** para finalizar a configuração do Always Encrypted.</span><span class="sxs-lookup"><span data-stu-id="ec303-178">Verify that the settings are all correct and click **Finish** to complete the setup for Always Encrypted.</span></span>

![Resumo](./media/sql-database-always-encrypted/summary.png)

### <a name="verify-the-wizards-actions"></a><span data-ttu-id="ec303-180">Verificar as ações do assistente</span><span class="sxs-lookup"><span data-stu-id="ec303-180">Verify the wizard's actions</span></span>
<span data-ttu-id="ec303-181">Após a conclusão do assistente, seu banco de dados estará configurado para o Always Encrypted.</span><span class="sxs-lookup"><span data-stu-id="ec303-181">After the wizard is finished, your database is set up for Always Encrypted.</span></span> <span data-ttu-id="ec303-182">O assistente executou as seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="ec303-182">The wizard performed the following actions:</span></span>

* <span data-ttu-id="ec303-183">Criou uma CMK.</span><span class="sxs-lookup"><span data-stu-id="ec303-183">Created a CMK.</span></span>
* <span data-ttu-id="ec303-184">Criou uma CEK.</span><span class="sxs-lookup"><span data-stu-id="ec303-184">Created a CEK.</span></span>
* <span data-ttu-id="ec303-185">Configuração das colunas selecionadas para criptografia.</span><span class="sxs-lookup"><span data-stu-id="ec303-185">Configured the selected columns for encryption.</span></span> <span data-ttu-id="ec303-186">Sua tabela **Pacientes** não tem dados no momento, mas todos os dados existentes nas colunas selecionadas agora estão criptografadas.</span><span class="sxs-lookup"><span data-stu-id="ec303-186">Your **Patients** table currently has no data, but any existing data in the selected columns is now encrypted.</span></span>

<span data-ttu-id="ec303-187">É possível verificar a criação das chaves no SSMS acessando **Clínica** > **Segurança** > **Chaves Always Encrypted**.</span><span class="sxs-lookup"><span data-stu-id="ec303-187">You can verify the creation of the keys in SSMS by going to **Clinic** > **Security** > **Always Encrypted Keys**.</span></span> <span data-ttu-id="ec303-188">Agora, é possível ver as chaves novas que o assistente gerou para você.</span><span class="sxs-lookup"><span data-stu-id="ec303-188">You can now see the new keys that the wizard generated for you.</span></span>

## <a name="create-a-client-application-that-works-with-the-encrypted-data"></a><span data-ttu-id="ec303-189">Criar um aplicativo cliente que funcione com os dados criptografados</span><span class="sxs-lookup"><span data-stu-id="ec303-189">Create a client application that works with the encrypted data</span></span>
<span data-ttu-id="ec303-190">Agora que o Always Encrypted está configurado, você pode compilar um aplicativo que execute *inserções* e *seleções* nas colunas criptografadas.</span><span class="sxs-lookup"><span data-stu-id="ec303-190">Now that Always Encrypted is set up, you can build an application that performs *inserts* and *selects* on the encrypted columns.</span></span> <span data-ttu-id="ec303-191">Para executar com sucesso o aplicativo de exemplo, você deve executá-lo no mesmo computador em que executou o assistente Always Encrypted.</span><span class="sxs-lookup"><span data-stu-id="ec303-191">To successfully run the sample application, you must run it on the same computer where you ran the Always Encrypted wizard.</span></span> <span data-ttu-id="ec303-192">Para executar o aplicativo em outro computador, é preciso implantar os certificados do Always Encrypted no computador que executa o aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="ec303-192">To run the application on another computer, you must deploy your Always Encrypted certificates to the computer running the client app.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="ec303-193">Seu aplicativo deve usar objetos [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) ao passar dados de texto sem formatação para o servidor com colunas do Sempre Criptografado.</span><span class="sxs-lookup"><span data-stu-id="ec303-193">Your application must use [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) objects when passing plaintext data to the server with Always Encrypted columns.</span></span> <span data-ttu-id="ec303-194">A passagem de valores literais sem usar objetos SqlParameter resultará em uma exceção.</span><span class="sxs-lookup"><span data-stu-id="ec303-194">Passing literal values without using SqlParameter objects will result in an exception.</span></span>
> 
> 

1. <span data-ttu-id="ec303-195">Abra o Visual Studio e crie um novo aplicativo de console em C#.</span><span class="sxs-lookup"><span data-stu-id="ec303-195">Open Visual Studio and create a new C# console application.</span></span> <span data-ttu-id="ec303-196">Verifique se seu projeto está definido como **.NET Framework 4.6** ou posterior.</span><span class="sxs-lookup"><span data-stu-id="ec303-196">Make sure your project is set to **.NET Framework 4.6** or later.</span></span>
2. <span data-ttu-id="ec303-197">Nomeie o projeto como **AlwaysEncryptedConsoleApp** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="ec303-197">Name the project **AlwaysEncryptedConsoleApp** and click **OK**.</span></span>

![Novo aplicativo de console](./media/sql-database-always-encrypted/console-app.png)

## <a name="modify-your-connection-string-to-enable-always-encrypted"></a><span data-ttu-id="ec303-199">Modificar a cadeia de conexão para habilitar o Always Encrypted</span><span class="sxs-lookup"><span data-stu-id="ec303-199">Modify your connection string to enable Always Encrypted</span></span>
<span data-ttu-id="ec303-200">Esta seção explica como habilitar o Always Encrypted na sua cadeia de conexão de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="ec303-200">This section explains how to enable Always Encrypted in your database connection string.</span></span> <span data-ttu-id="ec303-201">Você modificará o aplicativo de console que acabou de criar na próxima seção, "Exemplo de aplicativo de console do Always Encrypted".</span><span class="sxs-lookup"><span data-stu-id="ec303-201">You will modify the console app you just created in the next section, "Always Encrypted sample console application."</span></span>

<span data-ttu-id="ec303-202">Para habilitar o Always Encrypted, você precisa adicionar a palavra-chave **Column Encryption Setting** na cadeia de conexão e defini-la como **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="ec303-202">To enable Always Encrypted, you need to add the **Column Encryption Setting** keyword to your connection string and set it to **Enabled**.</span></span>

<span data-ttu-id="ec303-203">Isso pode ser definido diretamente na cadeia de conexão ou usando um [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span><span class="sxs-lookup"><span data-stu-id="ec303-203">You can set this directly in the connection string, or you can set it by using a [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span></span> <span data-ttu-id="ec303-204">O aplicativo de exemplo na próxima seção mostra como usar o **SqlConnectionStringBuilder**.</span><span class="sxs-lookup"><span data-stu-id="ec303-204">The sample application in the next section shows how to use **SqlConnectionStringBuilder**.</span></span>

> [!NOTE]
> <span data-ttu-id="ec303-205">Essa é a única alteração necessária em um aplicativo cliente específico para o Always Encrypted.</span><span class="sxs-lookup"><span data-stu-id="ec303-205">This is the only change required in a client application specific to Always Encrypted.</span></span> <span data-ttu-id="ec303-206">Se você tiver um aplicativo existente que armazene sua cadeia de conexão externamente (ou seja, em um arquivo de configuração), será possível habilitar o Always Encrypted sem alterar qualquer código.</span><span class="sxs-lookup"><span data-stu-id="ec303-206">If you have an existing application that stores its connection string externally (that is, in a config file), you might be able to enable Always Encrypted without changing any code.</span></span>
> 
> 

### <a name="enable-always-encrypted-in-the-connection-string"></a><span data-ttu-id="ec303-207">Habilitar o Always Encrypted na cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="ec303-207">Enable Always Encrypted in the connection string</span></span>
<span data-ttu-id="ec303-208">Adicione a palavra-chave a seguir na sua cadeia de conexão:</span><span class="sxs-lookup"><span data-stu-id="ec303-208">Add the following keyword to your connection string:</span></span>

    Column Encryption Setting=Enabled


### <a name="enable-always-encrypted-with-a-sqlconnectionstringbuilder"></a><span data-ttu-id="ec303-209">Habilitar o Always Encrypted com um SqlConnectionStringBuilder</span><span class="sxs-lookup"><span data-stu-id="ec303-209">Enable Always Encrypted with a SqlConnectionStringBuilder</span></span>
<span data-ttu-id="ec303-210">O código a seguir mostra como habilitar o Always Encrypted configurando o [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) como [Enabled](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span><span class="sxs-lookup"><span data-stu-id="ec303-210">The following code shows how to enable Always Encrypted by setting the [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) to [Enabled](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span></span>

    // Instantiate a SqlConnectionStringBuilder.
    SqlConnectionStringBuilder connStringBuilder =
       new SqlConnectionStringBuilder("replace with your connection string");

    // Enable Always Encrypted.
    connStringBuilder.ColumnEncryptionSetting =
       SqlConnectionColumnEncryptionSetting.Enabled;



## <a name="always-encrypted-sample-console-application"></a><span data-ttu-id="ec303-211">Aplicativo de console de exemplo do Always Encrypted</span><span class="sxs-lookup"><span data-stu-id="ec303-211">Always Encrypted sample console application</span></span>
<span data-ttu-id="ec303-212">Este exemplo demonstra como:</span><span class="sxs-lookup"><span data-stu-id="ec303-212">This sample demonstrates how to:</span></span>

* <span data-ttu-id="ec303-213">Modificar a cadeia de conexão para habilitar o Always Encrypted.</span><span class="sxs-lookup"><span data-stu-id="ec303-213">Modify your connection string to enable Always Encrypted.</span></span>
* <span data-ttu-id="ec303-214">Inserir dados nas colunas criptografadas.</span><span class="sxs-lookup"><span data-stu-id="ec303-214">Insert data into the encrypted columns.</span></span>
* <span data-ttu-id="ec303-215">Selecionar um registro por filtragem para um valor específico em uma coluna criptografada.</span><span class="sxs-lookup"><span data-stu-id="ec303-215">Select a record by filtering for a specific value in an encrypted column.</span></span>

<span data-ttu-id="ec303-216">Substitua o conteúdo de **Program.cs** pelo código a seguir.</span><span class="sxs-lookup"><span data-stu-id="ec303-216">Replace the contents of **Program.cs** with the following code.</span></span> <span data-ttu-id="ec303-217">Substitua a cadeia de conexão pela variável global connectionString na linha diretamente acima do método Principal com a cadeia de conexão válida do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ec303-217">Replace the connection string for the global connectionString variable in the line directly above the Main method with your valid connection string from the Azure portal.</span></span> <span data-ttu-id="ec303-218">Essa é a única alteração que você precisa fazer no código.</span><span class="sxs-lookup"><span data-stu-id="ec303-218">This is the only change you need to make to this code.</span></span>

<span data-ttu-id="ec303-219">Execute o aplicativo para ver o Always Encrypted em ação.</span><span class="sxs-lookup"><span data-stu-id="ec303-219">Run the app to see Always Encrypted in action.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Data;
    using System.Data.SqlClient;

    namespace AlwaysEncryptedConsoleApp
    {
    class Program
    {
        // Update this line with your Clinic database connection string from the Azure portal.
        static string connectionString = @"Replace with your connection string";

        static void Main(string[] args)
        {
            Console.WriteLine("Original connection string copied from the Azure portal:");
            Console.WriteLine(connectionString);

            // Create a SqlConnectionStringBuilder.
            SqlConnectionStringBuilder connStringBuilder =
                new SqlConnectionStringBuilder(connectionString);

            // Enable Always Encrypted for the connection.
            // This is the only change specific to Always Encrypted
            connStringBuilder.ColumnEncryptionSetting =
                SqlConnectionColumnEncryptionSetting.Enabled;

            Console.WriteLine(Environment.NewLine + "Updated connection string with Always Encrypted enabled:");
            Console.WriteLine(connStringBuilder.ConnectionString);

            // Update the connection string with a password supplied at runtime.
            Console.WriteLine(Environment.NewLine + "Enter server password:");
            connStringBuilder.Password = Console.ReadLine();


            // Assign the updated connection string to our global variable.
            connectionString = connStringBuilder.ConnectionString;


            // Delete all records to restart this demo app.
            ResetPatientsTable();

            // Add sample data to the Patients table.
            Console.Write(Environment.NewLine + "Adding sample patient data to the database...");

            InsertPatient(new Patient() {
                SSN = "999-99-0001", FirstName = "Orlando", LastName = "Gee", BirthDate = DateTime.Parse("01/04/1964") });
            InsertPatient(new Patient() {
                SSN = "999-99-0002", FirstName = "Keith", LastName = "Harris", BirthDate = DateTime.Parse("06/20/1977") });
            InsertPatient(new Patient() {
                SSN = "999-99-0003", FirstName = "Donna", LastName = "Carreras", BirthDate = DateTime.Parse("02/09/1973") });
            InsertPatient(new Patient() {
                SSN = "999-99-0004", FirstName = "Janet", LastName = "Gates", BirthDate = DateTime.Parse("08/31/1985") });
            InsertPatient(new Patient() {
                SSN = "999-99-0005", FirstName = "Lucy", LastName = "Harrington", BirthDate = DateTime.Parse("05/06/1993") });


            // Fetch and display all patients.
            Console.WriteLine(Environment.NewLine + "All the records currently in the Patients table:");

            foreach (Patient patient in SelectAllPatients())
            {
                Console.WriteLine(patient.FirstName + " " + patient.LastName + "\tSSN: " + patient.SSN + "\tBirthdate: " + patient.BirthDate);
            }

            // Get patients by SSN.
            Console.WriteLine(Environment.NewLine + "Now let's locate records by searching the encrypted SSN column.");

            string ssn;

            // This very simple validation only checks that the user entered 11 characters.
            // In production be sure to check all user input and use the best validation for your specific application.
            do
            {
                Console.WriteLine("Please enter a valid SSN (ex. 123-45-6789):");
                ssn = Console.ReadLine();
            } while (ssn.Length != 11);

            // The example allows duplicate SSN entries so we will return all records
            // that match the provided value and store the results in selectedPatients.
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

            Console.WriteLine("Press Enter to exit...");
            Console.ReadLine();
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
                    Console.WriteLine("The following error was encountered: ");
                    Console.WriteLine(ex.Message);
                    Console.WriteLine(Environment.NewLine + "Press Enter key to exit");
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


        // This method simply deletes all records in the Patients table to reset our demo.
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


## <a name="verify-that-the-data-is-encrypted"></a><span data-ttu-id="ec303-220">Verificar se os dados foram criptografados</span><span class="sxs-lookup"><span data-stu-id="ec303-220">Verify that the data is encrypted</span></span>
<span data-ttu-id="ec303-221">Você pode verificar rapidamente se os dados reais no servidor estão criptografados, consultando os dados de **Pacientes** dados com o SSMS.</span><span class="sxs-lookup"><span data-stu-id="ec303-221">You can quickly check that the actual data on the server is encrypted by querying the **Patients** data with SSMS.</span></span> <span data-ttu-id="ec303-222">(Use sua conexão atual em que a configuração de criptografia de coluna ainda não está habilitada.)</span><span class="sxs-lookup"><span data-stu-id="ec303-222">(Use your current connection where the column encryption setting is not yet enabled.)</span></span>

<span data-ttu-id="ec303-223">Execute a consulta a seguir no banco de dados Clínica.</span><span class="sxs-lookup"><span data-stu-id="ec303-223">Run the following query on the Clinic database.</span></span>

    SELECT FirstName, LastName, SSN, BirthDate FROM Patients;

<span data-ttu-id="ec303-224">É possível ver que as colunas criptografadas não contêm dados de texto não criptografado.</span><span class="sxs-lookup"><span data-stu-id="ec303-224">You can see that the encrypted columns do not contain any plaintext data.</span></span>

   ![Novo aplicativo de console](./media/sql-database-always-encrypted/ssms-encrypted.png)

<span data-ttu-id="ec303-226">Para usar o SSMS para acessar os dados de texto não criptografado, você pode adicionar o parâmetro **Column Encryption Setting=enabled** à conexão.</span><span class="sxs-lookup"><span data-stu-id="ec303-226">To use SSMS to access the plaintext data, you can add the **Column Encryption Setting=enabled** parameter to the connection.</span></span>

1. <span data-ttu-id="ec303-227">No SSMS, clique com o botão direito do mouse no seu servidor em **Pesquisador de Objetos** e clique em **Desconectar**.</span><span class="sxs-lookup"><span data-stu-id="ec303-227">In SSMS, right-click your server in **Object Explorer**, and then click **Disconnect**.</span></span>
2. <span data-ttu-id="ec303-228">Clique em **Connect** > **Mecanismo de Banco de Dados** para abrir a janela **Conectar ao Servidor** e clique em **Opções**.</span><span class="sxs-lookup"><span data-stu-id="ec303-228">Click **Connect** > **Database Engine** to open the **Connect to Server** window, and then click **Options**.</span></span>
3. <span data-ttu-id="ec303-229">Clique em **Parâmetros Adicionais de Conexão** e digite **Column Encryption Setting=enabled**.</span><span class="sxs-lookup"><span data-stu-id="ec303-229">Click **Additional Connection Parameters** and type **Column Encryption Setting=enabled**.</span></span>
   
    ![Novo aplicativo de console](./media/sql-database-always-encrypted/ssms-connection-parameter.png)
4. <span data-ttu-id="ec303-231">Execute a consulta a seguir no banco de dados **Clínica** .</span><span class="sxs-lookup"><span data-stu-id="ec303-231">Run the following query on the **Clinic** database.</span></span>
   
        SELECT FirstName, LastName, SSN, BirthDate FROM Patients;
   
     <span data-ttu-id="ec303-232">Agora você pode ver os dados de texto sem formatação em colunas criptografadas.</span><span class="sxs-lookup"><span data-stu-id="ec303-232">You can now see the plaintext data in the encrypted columns.</span></span>

    ![Novo aplicativo de console](./media/sql-database-always-encrypted/ssms-plaintext.png)



> [!NOTE]
> <span data-ttu-id="ec303-234">Se você se conectar ao SSMS (ou qualquer cliente) em outro computador, ele não terá acesso às chaves de criptografia e não será capaz de descriptografar os dados.</span><span class="sxs-lookup"><span data-stu-id="ec303-234">If you connect with SSMS (or any client) from a different computer, it will not have access to the encryption keys and will not be able to decrypt the data.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="ec303-235">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ec303-235">Next steps</span></span>
<span data-ttu-id="ec303-236">Depois de criar um banco de dados que usa o Always Encrypted, convém fazer o seguinte:</span><span class="sxs-lookup"><span data-stu-id="ec303-236">After you create a database that uses Always Encrypted, you may want to do the following:</span></span>

* <span data-ttu-id="ec303-237">Executar esse exemplo de um computador diferente.</span><span class="sxs-lookup"><span data-stu-id="ec303-237">Run this sample from a different computer.</span></span> <span data-ttu-id="ec303-238">Ele não terá acesso às chaves de criptografia e, portanto, não terá acesso aos dados de texto não criptografado e não será executado com êxito.</span><span class="sxs-lookup"><span data-stu-id="ec303-238">It won't have access to the encryption keys, so it will not have access to the plaintext data and will not run successfully.</span></span>
* <span data-ttu-id="ec303-239">[Girar e limpar suas chaves](https://msdn.microsoft.com/library/mt607048.aspx).</span><span class="sxs-lookup"><span data-stu-id="ec303-239">[Rotate and clean up your keys](https://msdn.microsoft.com/library/mt607048.aspx).</span></span>
* <span data-ttu-id="ec303-240">[Migrar dados que já foram criptografados com o Always Encrypted](https://msdn.microsoft.com/library/mt621539.aspx).</span><span class="sxs-lookup"><span data-stu-id="ec303-240">[Migrate data that is already encrypted with Always Encrypted](https://msdn.microsoft.com/library/mt621539.aspx).</span></span>
* <span data-ttu-id="ec303-241">[Implantar certificados do Always Encrypted em outros computadores cliente](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_1) (veja a seção "Disponibilizando certificados para aplicativos e usuários").</span><span class="sxs-lookup"><span data-stu-id="ec303-241">[Deploy Always Encrypted certificates to other client machines](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_1) (see the "Making Certificates Available to Applications and Users" section).</span></span>

## <a name="related-information"></a><span data-ttu-id="ec303-242">Informações relacionadas</span><span class="sxs-lookup"><span data-stu-id="ec303-242">Related information</span></span>
* [<span data-ttu-id="ec303-243">Always Encrypted (desenvolvimento de cliente)</span><span class="sxs-lookup"><span data-stu-id="ec303-243">Always Encrypted (client development)</span></span>](https://msdn.microsoft.com/library/mt147923.aspx)
* [<span data-ttu-id="ec303-244">Transparent Data Encryption</span><span class="sxs-lookup"><span data-stu-id="ec303-244">Transparent Data Encryption</span></span>](https://msdn.microsoft.com/library/bb934049.aspx)
* [<span data-ttu-id="ec303-245">Criptografia do SQL Server</span><span class="sxs-lookup"><span data-stu-id="ec303-245">SQL Server Encryption</span></span>](https://msdn.microsoft.com/library/bb510663.aspx)
* [<span data-ttu-id="ec303-246">Assistente do Always Encrypted</span><span class="sxs-lookup"><span data-stu-id="ec303-246">Always Encrypted Wizard</span></span>](https://msdn.microsoft.com/library/mt459280.aspx)
* [<span data-ttu-id="ec303-247">Blog do Always Encrypted</span><span class="sxs-lookup"><span data-stu-id="ec303-247">Always Encrypted Blog</span></span>](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

