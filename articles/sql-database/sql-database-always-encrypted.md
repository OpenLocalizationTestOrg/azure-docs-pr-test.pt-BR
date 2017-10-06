---
title: 'Always Encrypted: Banco de Dados SQL do Azure - armazenamento de certificados do Windows | Microsoft Docs'
description: "Este artigo mostra como os dados confidenciais no banco de dados SQL com criptografia de banco de dados usando toosecure Olá Assistente do sempre criptografado no SQL Server Management Studio (SSMS). Ele também mostra como toostore suas chaves de criptografia no certificado do Windows hello armazenam."
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
ms.openlocfilehash: 483f9a2120cc42b732142fc07807d3d8830a0c33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="always-encrypted-protect-sensitive-data-in-sql-database-and-store-your-encryption-keys-in-hello-windows-certificate-store"></a><span data-ttu-id="9ed1c-105">Sempre criptografado: Proteger dados confidenciais no banco de dados SQL e armazenar as chaves de criptografia no repositório de certificados do Windows hello</span><span class="sxs-lookup"><span data-stu-id="9ed1c-105">Always Encrypted: Protect sensitive data in SQL Database and store your encryption keys in hello Windows certificate store</span></span>

<span data-ttu-id="9ed1c-106">Este artigo mostra como os dados confidenciais em um SQL toosecure banco de dados com criptografia de banco de dados usando Olá [Assistente do Always Encrypted](https://msdn.microsoft.com/library/mt459280.aspx) na [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span><span class="sxs-lookup"><span data-stu-id="9ed1c-106">This article shows you how toosecure sensitive data in a SQL database with database encryption by using hello [Always Encrypted Wizard](https://msdn.microsoft.com/library/mt459280.aspx) in [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span></span> <span data-ttu-id="9ed1c-107">Ele também mostra como toostore suas chaves de criptografia no certificado do Windows hello armazenam.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-107">It also shows you how toostore your encryption keys in hello Windows certificate store.</span></span>

<span data-ttu-id="9ed1c-108">Sempre criptografado é uma nova tecnologia de criptografia de dados no banco de dados do SQL Azure e SQL Server que ajuda a proteger dados confidenciais em repouso no servidor de saudação, durante a movimentação entre cliente e servidor e enquanto dados saudação estão em uso, garantir que os dados confidenciais nunca aparece como texto sem formatação no sistema de banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-108">Always Encrypted is a new data encryption technology in Azure SQL Database and SQL Server that helps protect sensitive data at rest on hello server, during movement between client and server, and while hello data is in use, ensuring that sensitive data never appears as plaintext inside hello database system.</span></span> <span data-ttu-id="9ed1c-109">Depois de criptografar dados, somente os aplicativos cliente ou servidores de aplicativos que têm acesso toohello chaves podem acessar dados de texto sem formatação.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-109">After you encrypt data, only client applications or app servers that have access toohello keys can access plaintext data.</span></span> <span data-ttu-id="9ed1c-110">Para obter informações detalhadas, consulte [Always Encrypted (Mecanismo do Banco de Dados)](https://msdn.microsoft.com/library/mt163865.aspx).</span><span class="sxs-lookup"><span data-stu-id="9ed1c-110">For detailed information, see [Always Encrypted (Database Engine)](https://msdn.microsoft.com/library/mt163865.aspx).</span></span>

<span data-ttu-id="9ed1c-111">Depois de configurar Olá toouse de banco de dados sempre criptografado, você criará um aplicativo cliente em c# com Visual Studio toowork com dados criptografado de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-111">After configuring hello database toouse Always Encrypted, you will create a client application in C# with Visual Studio toowork with hello encrypted data.</span></span>

<span data-ttu-id="9ed1c-112">Siga etapas Olá toolearn este artigo como tooset o sempre criptografado para um banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-112">Follow hello steps in this article toolearn how tooset up Always Encrypted for an Azure SQL database.</span></span> <span data-ttu-id="9ed1c-113">Neste artigo, você aprenderá como Olá tooperform seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="9ed1c-113">In this article, you will learn how tooperform hello following tasks:</span></span>

* <span data-ttu-id="9ed1c-114">Assistente de sempre criptografado Olá Use no SSMS toocreate [chaves Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span><span class="sxs-lookup"><span data-stu-id="9ed1c-114">Use hello Always Encrypted wizard in SSMS toocreate [Always Encrypted Keys](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span></span>
  * <span data-ttu-id="9ed1c-115">Crie uma [CMK (Chave Mestra da Coluna)](https://msdn.microsoft.com/library/mt146393.aspx).</span><span class="sxs-lookup"><span data-stu-id="9ed1c-115">Create a [Column Master Key (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).</span></span>
  * <span data-ttu-id="9ed1c-116">Crie uma [CEK (Chave de Criptografia da Coluna)](https://msdn.microsoft.com/library/mt146372.aspx).</span><span class="sxs-lookup"><span data-stu-id="9ed1c-116">Create a [Column Encryption Key (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).</span></span>
* <span data-ttu-id="9ed1c-117">Criar uma tabela de banco de dados e criptografar colunas.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-117">Create a database table and encrypt columns.</span></span>
* <span data-ttu-id="9ed1c-118">Crie um aplicativo que insere, seleciona e exibe dados de colunas Olá criptografado.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-118">Create an application that inserts, selects, and displays data from hello encrypted columns.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9ed1c-119">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9ed1c-119">Prerequisites</span></span>
<span data-ttu-id="9ed1c-120">Para este tutorial, será necessário:</span><span class="sxs-lookup"><span data-stu-id="9ed1c-120">For this tutorial, you'll need:</span></span>

* <span data-ttu-id="9ed1c-121">Uma conta e uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-121">An Azure account and subscription.</span></span> <span data-ttu-id="9ed1c-122">Se não tiver uma, inscreva-se em uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9ed1c-122">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="9ed1c-123">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) versão 13.0.700.242 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-123">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) version 13.0.700.242 or later.</span></span>
* <span data-ttu-id="9ed1c-124">[.NET framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) ou posterior (no computador do cliente de saudação).</span><span class="sxs-lookup"><span data-stu-id="9ed1c-124">[.NET Framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) or later (on hello client computer).</span></span>
* <span data-ttu-id="9ed1c-125">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="9ed1c-125">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span></span>

## <a name="create-a-blank-sql-database"></a><span data-ttu-id="9ed1c-126">Criar um banco de dados SQL em branco</span><span class="sxs-lookup"><span data-stu-id="9ed1c-126">Create a blank SQL database</span></span>
1. <span data-ttu-id="9ed1c-127">Entrar toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="9ed1c-127">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="9ed1c-128">Clique em **Novo** > **Dados + Armazenamento** > **Banco de Dados SQL**.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-128">Click **New** > **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="9ed1c-129">Crie um banco de dados **Em branco** chamado **Clínica** em um servidor novo ou existente.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-129">Create a **Blank** database named **Clinic** on a new or existing server.</span></span> <span data-ttu-id="9ed1c-130">Para obter instruções detalhadas sobre como criar um banco de dados no hello portal do Azure, consulte [seu primeiro banco de dados do SQL Azure](sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9ed1c-130">For detailed instructions about creating a database in hello Azure portal, see [Your first Azure SQL database](sql-database-get-started-portal.md).</span></span>
   
    ![Criar um banco de dados vazio](./media/sql-database-always-encrypted/create-database.png)

<span data-ttu-id="9ed1c-132">Você precisará de cadeia de caracteres de conexão Olá posteriormente no tutorial de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-132">You will need hello connection string later in hello tutorial.</span></span> <span data-ttu-id="9ed1c-133">Após a criação do banco de dados hello, vá toohello nova clínica banco de dados e copiar Olá conexão cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-133">After hello database is created, go toohello new Clinic database and copy hello connection string.</span></span> <span data-ttu-id="9ed1c-134">Você pode obter a cadeia de caracteres de conexão Olá a qualquer momento, mas é fácil toocopy, quando você está no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-134">You can get hello connection string at any time, but it's easy toocopy it when you're in hello Azure portal.</span></span>

1. <span data-ttu-id="9ed1c-135">Clique em **Bancos de dados SQL** > **Clínica** > **Mostrar cadeias de conexão do banco de dados**.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-135">Click **SQL databases** > **Clinic** > **Show database connection strings**.</span></span>
2. <span data-ttu-id="9ed1c-136">Copie a cadeia de caracteres de conexão de saudação para **ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-136">Copy hello connection string for **ADO.NET**.</span></span>
   
    ![Copie a cadeia de caracteres de conexão Olá](./media/sql-database-always-encrypted/connection-strings.png)

## <a name="connect-toohello-database-with-ssms"></a><span data-ttu-id="9ed1c-138">Conectar-se o banco de dados toohello com SSMS</span><span class="sxs-lookup"><span data-stu-id="9ed1c-138">Connect toohello database with SSMS</span></span>
<span data-ttu-id="9ed1c-139">Abra o SSMS e conecte o servidor de toohello com o banco de dados do hello clínica.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-139">Open SSMS and connect toohello server with hello Clinic database.</span></span>

1. <span data-ttu-id="9ed1c-140">Abra o SSMS.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-140">Open SSMS.</span></span> <span data-ttu-id="9ed1c-141">(Clique em **conectar** > **mecanismo de banco de dados** tooopen Olá **conectar tooServer** janela se não estiver aberto).</span><span class="sxs-lookup"><span data-stu-id="9ed1c-141">(Click **Connect** > **Database Engine** tooopen hello **Connect tooServer** window if it is not open).</span></span>
2. <span data-ttu-id="9ed1c-142">Insira o nome do servidor e credenciais.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-142">Enter your server name and credentials.</span></span> <span data-ttu-id="9ed1c-143">nome do servidor de saudação pode ser encontrada na folha de banco de dados SQL hello e na cadeia de caracteres de conexão Olá copiados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-143">hello server name can be found on hello SQL database blade and in hello connection string you copied earlier.</span></span> <span data-ttu-id="9ed1c-144">Incluindo do nome completo do servidor do tipo Olá *t*.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-144">Type hello complete server name including *database.windows.net*.</span></span>
   
    ![Copie a cadeia de caracteres de conexão Olá](./media/sql-database-always-encrypted/ssms-connect.png)

<span data-ttu-id="9ed1c-146">Se hello **nova regra de Firewall** abre a janela, entrar tooAzure e permitem SSMS criar uma nova regra de firewall para você.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-146">If hello **New Firewall Rule** window opens, sign in tooAzure and let SSMS create a new firewall rule for you.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="9ed1c-147">Criar uma tabela</span><span class="sxs-lookup"><span data-stu-id="9ed1c-147">Create a table</span></span>
<span data-ttu-id="9ed1c-148">Nesta seção, você criará um dados dos pacientes toohold da tabela.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-148">In this section, you will create a table toohold patient data.</span></span> <span data-ttu-id="9ed1c-149">Isso será uma tabela normal inicialmente – você irá configurar a criptografia na próxima seção, Olá.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-149">This will be a normal table initially--you will configure encryption in hello next section.</span></span>

1. <span data-ttu-id="9ed1c-150">Expanda **Bancos de Dados**.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-150">Expand **Databases**.</span></span>
2. <span data-ttu-id="9ed1c-151">Saudação de atalho **clínica** de banco de dados e clique em **nova consulta**.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-151">Right-click hello **Clinic** database and click **New Query**.</span></span>
3. <span data-ttu-id="9ed1c-152">Saudação de colar Transact-SQL (T-SQL) a seguir na nova janela de consulta hello e **Execute** -lo.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-152">Paste hello following Transact-SQL (T-SQL) into hello new query window and **Execute** it.</span></span>

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


## <a name="encrypt-columns-configure-always-encrypted"></a><span data-ttu-id="9ed1c-153">Criptografar colunas (configurar o Always Encrypted)</span><span class="sxs-lookup"><span data-stu-id="9ed1c-153">Encrypt columns (configure Always Encrypted)</span></span>
<span data-ttu-id="9ed1c-154">SSMS fornece um assistente tooeasily configurar o Always Encrypted Configurando Olá CMK, CEK e colunas criptografadas para você.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-154">SSMS provides a wizard tooeasily configure Always Encrypted by setting up hello CMK, CEK, and encrypted columns for you.</span></span>

1. <span data-ttu-id="9ed1c-155">Expandaa **Bancos de Dados** > **Clínica** > **Tabelas**.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-155">Expand **Databases** > **Clinic** > **Tables**.</span></span>
2. <span data-ttu-id="9ed1c-156">Atalho Olá **pacientes** de tabela e selecione **criptografar colunas** Assistente de sempre criptografado Olá tooopen:</span><span class="sxs-lookup"><span data-stu-id="9ed1c-156">Right-click hello **Patients** table and select **Encrypt Columns** tooopen hello Always Encrypted wizard:</span></span>
   
    ![Criptografar Colunas](./media/sql-database-always-encrypted/encrypt-columns.png)

<span data-ttu-id="9ed1c-158">Assistente de sempre criptografado Hello inclui Olá seções a seguir: **seleção de coluna**, **configuração da chave mestra** (CMK) **validação**, e  **Resumo**.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-158">hello Always Encrypted wizard includes hello following sections: **Column Selection**, **Master Key Configuration** (CMK), **Validation**, and **Summary**.</span></span>

### <a name="column-selection"></a><span data-ttu-id="9ed1c-159">Seleção de coluna</span><span class="sxs-lookup"><span data-stu-id="9ed1c-159">Column Selection</span></span>
<span data-ttu-id="9ed1c-160">Clique em **próximo** em Olá **Introdução** Olá de tooopen página **seleção de coluna** página.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-160">Click **Next** on hello **Introduction** page tooopen hello **Column Selection** page.</span></span> <span data-ttu-id="9ed1c-161">Nessa página, você seleciona as colunas que você deseja tooencrypt, [Olá tipo de criptografia e qual chave de criptografia de coluna (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-161">On this page, you will select which columns you want tooencrypt, [hello type of encryption, and what column encryption key (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse.</span></span>

<span data-ttu-id="9ed1c-162">Criptografe as informações de **SSN** e **BirthDate** de cada paciente.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-162">Encrypt **SSN** and **BirthDate** information for each patient.</span></span> <span data-ttu-id="9ed1c-163">Olá **SSN** coluna usará criptografia determinística, que dá suporte a pesquisas de igualdade, junções e group by.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-163">hello **SSN** column will use deterministic encryption, which supports equality lookups, joins, and group by.</span></span> <span data-ttu-id="9ed1c-164">Olá **BirthDate** coluna usará criptografia aleatória, que não oferece suporte a operações.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-164">hello **BirthDate** column will use randomized encryption, which does not support operations.</span></span>

<span data-ttu-id="9ed1c-165">Saudação de conjunto **tipo de criptografia** para Olá **SSN** coluna muito**determinística** e hello **BirthDate** coluna muito **Aleatória**.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-165">Set hello **Encryption Type** for hello **SSN** column too**Deterministic** and hello **BirthDate** column too**Randomized**.</span></span> <span data-ttu-id="9ed1c-166">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-166">Click **Next**.</span></span>

![Criptografar Colunas](./media/sql-database-always-encrypted/column-selection.png)

### <a name="master-key-configuration"></a><span data-ttu-id="9ed1c-168">Configuração da Chave Mestra</span><span class="sxs-lookup"><span data-stu-id="9ed1c-168">Master Key Configuration</span></span>
<span data-ttu-id="9ed1c-169">Olá **configuração da chave mestra** página é onde você configurar a CMK e provedor de repositório de chaves hello selecione onde hello CMK será armazenado.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-169">hello **Master Key Configuration** page is where you set up your CMK and select hello key store provider where hello CMK will be stored.</span></span> <span data-ttu-id="9ed1c-170">No momento, você pode armazenar uma CMK no repositório de certificados do Windows hello, o Cofre de chaves do Azure ou um módulo de segurança de hardware (HSM).</span><span class="sxs-lookup"><span data-stu-id="9ed1c-170">Currently, you can store a CMK in hello Windows certificate store, Azure Key Vault, or a hardware security module (HSM).</span></span> <span data-ttu-id="9ed1c-171">Este tutorial mostra como toostore suas chaves de certificado do Windows hello armazenam.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-171">This tutorial shows how toostore your keys in hello Windows certificate store.</span></span>

<span data-ttu-id="9ed1c-172">Verifique se **Repositório de certificados do Windows** está marcado e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-172">Verify that **Windows certificate store** is selected and click **Next**.</span></span>

![Configuração da Chave Mestra](./media/sql-database-always-encrypted/master-key-configuration.png)

### <a name="validation"></a><span data-ttu-id="9ed1c-174">Validação</span><span class="sxs-lookup"><span data-stu-id="9ed1c-174">Validation</span></span>
<span data-ttu-id="9ed1c-175">Você pode criptografar colunas Olá agora ou salvar um toorun de script do PowerShell mais tarde.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-175">You can encrypt hello columns now or save a PowerShell script toorun later.</span></span> <span data-ttu-id="9ed1c-176">Para este tutorial, selecione **continuar toofinish agora** e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-176">For this tutorial, select **Proceed toofinish now** and click **Next**.</span></span>

### <a name="summary"></a><span data-ttu-id="9ed1c-177">Resumo</span><span class="sxs-lookup"><span data-stu-id="9ed1c-177">Summary</span></span>
<span data-ttu-id="9ed1c-178">Verifique se as configurações de saudação estão corretas e clique em **concluir** toocomplete o programa de instalação de saudação do sempre criptografado.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-178">Verify that hello settings are all correct and click **Finish** toocomplete hello setup for Always Encrypted.</span></span>

![Resumo](./media/sql-database-always-encrypted/summary.png)

### <a name="verify-hello-wizards-actions"></a><span data-ttu-id="9ed1c-180">Verifique se ações do assistente Olá</span><span class="sxs-lookup"><span data-stu-id="9ed1c-180">Verify hello wizard's actions</span></span>
<span data-ttu-id="9ed1c-181">Concluído o Assistente de saudação, seu banco de dados está configurado para sempre criptografado.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-181">After hello wizard is finished, your database is set up for Always Encrypted.</span></span> <span data-ttu-id="9ed1c-182">Olá Olá de assistente executado ações a seguir:</span><span class="sxs-lookup"><span data-stu-id="9ed1c-182">hello wizard performed hello following actions:</span></span>

* <span data-ttu-id="9ed1c-183">Criou uma CMK.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-183">Created a CMK.</span></span>
* <span data-ttu-id="9ed1c-184">Criou uma CEK.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-184">Created a CEK.</span></span>
* <span data-ttu-id="9ed1c-185">Saudação configurado selecionado colunas para criptografia.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-185">Configured hello selected columns for encryption.</span></span> <span data-ttu-id="9ed1c-186">O **pacientes** tabela atualmente não tem dados, mas os dados existentes nas colunas de saudação selecionada agora são criptografados.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-186">Your **Patients** table currently has no data, but any existing data in hello selected columns is now encrypted.</span></span>

<span data-ttu-id="9ed1c-187">Verificar a criação de saudação de chaves Olá no SSMS indo muito**clínica** > **segurança** > **chaves Always Encrypted**.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-187">You can verify hello creation of hello keys in SSMS by going too**Clinic** > **Security** > **Always Encrypted Keys**.</span></span> <span data-ttu-id="9ed1c-188">Agora você pode ver Olá novas chaves Olá assistente gerado para você.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-188">You can now see hello new keys that hello wizard generated for you.</span></span>

## <a name="create-a-client-application-that-works-with-hello-encrypted-data"></a><span data-ttu-id="9ed1c-189">Criar um aplicativo cliente que funciona com dados saudação criptografado</span><span class="sxs-lookup"><span data-stu-id="9ed1c-189">Create a client application that works with hello encrypted data</span></span>
<span data-ttu-id="9ed1c-190">Agora que sempre criptografado estiver configurado, você pode criar um aplicativo que realiza *insere* e *seleciona* em Olá colunas criptografadas.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-190">Now that Always Encrypted is set up, you can build an application that performs *inserts* and *selects* on hello encrypted columns.</span></span> <span data-ttu-id="9ed1c-191">toosuccessfully executar o aplicativo de exemplo hello, você deve executá-lo em Olá mesmo computador em que você executou o Assistente de sempre criptografado hello.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-191">toosuccessfully run hello sample application, you must run it on hello same computer where you ran hello Always Encrypted wizard.</span></span> <span data-ttu-id="9ed1c-192">aplicativo de hello toorun em outro computador, você deve implantar o sempre criptografado certificados toohello computador executando o aplicativo cliente de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-192">toorun hello application on another computer, you must deploy your Always Encrypted certificates toohello computer running hello client app.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="9ed1c-193">O aplicativo deve usar [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) objetos ao passar o servidor de toohello de dados de texto sem formatação com colunas sempre criptografadas.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-193">Your application must use [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) objects when passing plaintext data toohello server with Always Encrypted columns.</span></span> <span data-ttu-id="9ed1c-194">A passagem de valores literais sem usar objetos SqlParameter resultará em uma exceção.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-194">Passing literal values without using SqlParameter objects will result in an exception.</span></span>
> 
> 

1. <span data-ttu-id="9ed1c-195">Abra o Visual Studio e crie um novo aplicativo de console em C#.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-195">Open Visual Studio and create a new C# console application.</span></span> <span data-ttu-id="9ed1c-196">Verifique se seu projeto está definido muito**do .NET Framework 4.6** ou posterior.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-196">Make sure your project is set too**.NET Framework 4.6** or later.</span></span>
2. <span data-ttu-id="9ed1c-197">Projeto de saudação do nome **AlwaysEncryptedConsoleApp** e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-197">Name hello project **AlwaysEncryptedConsoleApp** and click **OK**.</span></span>

![Novo aplicativo de console](./media/sql-database-always-encrypted/console-app.png)

## <a name="modify-your-connection-string-tooenable-always-encrypted"></a><span data-ttu-id="9ed1c-199">Modificar sua tooenable de cadeia de caracteres de conexão sempre criptografado</span><span class="sxs-lookup"><span data-stu-id="9ed1c-199">Modify your connection string tooenable Always Encrypted</span></span>
<span data-ttu-id="9ed1c-200">Esta seção explica como tooenable sempre criptografados em sua cadeia de conexão do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-200">This section explains how tooenable Always Encrypted in your database connection string.</span></span> <span data-ttu-id="9ed1c-201">Você modificará o aplicativo de console Olá que você acabou de criar na próxima seção hello, "Sempre criptografados exemplo de aplicativo de console."</span><span class="sxs-lookup"><span data-stu-id="9ed1c-201">You will modify hello console app you just created in hello next section, "Always Encrypted sample console application."</span></span>

<span data-ttu-id="9ed1c-202">tooenable sempre criptografado, você precisa Olá tooadd **Column Encryption Setting** conexão de tooyour de palavra-chave da cadeia de caracteres e defini-lo muito**habilitado**.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-202">tooenable Always Encrypted, you need tooadd hello **Column Encryption Setting** keyword tooyour connection string and set it too**Enabled**.</span></span>

<span data-ttu-id="9ed1c-203">Você pode definir isso diretamente na cadeia de caracteres de conexão hello, ou pode defini-lo usando um [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span><span class="sxs-lookup"><span data-stu-id="9ed1c-203">You can set this directly in hello connection string, or you can set it by using a [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span></span> <span data-ttu-id="9ed1c-204">aplicativo de exemplo Hello em Olá próxima seção mostra como toouse **SqlConnectionStringBuilder**.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-204">hello sample application in hello next section shows how toouse **SqlConnectionStringBuilder**.</span></span>

> [!NOTE]
> <span data-ttu-id="9ed1c-205">Isso é Olá alteração somente necessária em um cliente aplicativo específico tooAlways criptografado.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-205">This is hello only change required in a client application specific tooAlways Encrypted.</span></span> <span data-ttu-id="9ed1c-206">Se você tiver um aplicativo existente que armazena sua cadeia de conexão externamente (isto é, em um arquivo de configuração), você pode ser capaz de tooenable sempre criptografado sem alterar nenhum código.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-206">If you have an existing application that stores its connection string externally (that is, in a config file), you might be able tooenable Always Encrypted without changing any code.</span></span>
> 
> 

### <a name="enable-always-encrypted-in-hello-connection-string"></a><span data-ttu-id="9ed1c-207">Habilitar o sempre criptografado na cadeia de caracteres de conexão Olá</span><span class="sxs-lookup"><span data-stu-id="9ed1c-207">Enable Always Encrypted in hello connection string</span></span>
<span data-ttu-id="9ed1c-208">Adicione Olá cadeia de caracteres de conexão de tooyour palavra-chave a seguir:</span><span class="sxs-lookup"><span data-stu-id="9ed1c-208">Add hello following keyword tooyour connection string:</span></span>

    Column Encryption Setting=Enabled


### <a name="enable-always-encrypted-with-a-sqlconnectionstringbuilder"></a><span data-ttu-id="9ed1c-209">Habilitar o Always Encrypted com um SqlConnectionStringBuilder</span><span class="sxs-lookup"><span data-stu-id="9ed1c-209">Enable Always Encrypted with a SqlConnectionStringBuilder</span></span>
<span data-ttu-id="9ed1c-210">Olá código a seguir mostra como tooenable sempre criptografado, definindo Olá [Columnencryptionsetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) muito[habilitado](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span><span class="sxs-lookup"><span data-stu-id="9ed1c-210">hello following code shows how tooenable Always Encrypted by setting hello [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) too[Enabled](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span></span>

    // Instantiate a SqlConnectionStringBuilder.
    SqlConnectionStringBuilder connStringBuilder =
       new SqlConnectionStringBuilder("replace with your connection string");

    // Enable Always Encrypted.
    connStringBuilder.ColumnEncryptionSetting =
       SqlConnectionColumnEncryptionSetting.Enabled;



## <a name="always-encrypted-sample-console-application"></a><span data-ttu-id="9ed1c-211">Aplicativo de console de exemplo do Always Encrypted</span><span class="sxs-lookup"><span data-stu-id="9ed1c-211">Always Encrypted sample console application</span></span>
<span data-ttu-id="9ed1c-212">Este exemplo demonstra como:</span><span class="sxs-lookup"><span data-stu-id="9ed1c-212">This sample demonstrates how to:</span></span>

* <span data-ttu-id="9ed1c-213">Modifique seu tooenable de cadeia de caracteres de conexão sempre criptografado.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-213">Modify your connection string tooenable Always Encrypted.</span></span>
* <span data-ttu-id="9ed1c-214">Inserir dados nas colunas de saudação criptografada.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-214">Insert data into hello encrypted columns.</span></span>
* <span data-ttu-id="9ed1c-215">Selecionar um registro por filtragem para um valor específico em uma coluna criptografada.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-215">Select a record by filtering for a specific value in an encrypted column.</span></span>

<span data-ttu-id="9ed1c-216">Substitua o conteúdo de saudação do **Program.cs** com hello código a seguir.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-216">Replace hello contents of **Program.cs** with hello following code.</span></span> <span data-ttu-id="9ed1c-217">Substitua a cadeia de caracteres de conexão de saudação para a variável de connectionString global Olá na linha de saudação diretamente acima Olá método Main com a cadeia de conexão válida do hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-217">Replace hello connection string for hello global connectionString variable in hello line directly above hello Main method with your valid connection string from hello Azure portal.</span></span> <span data-ttu-id="9ed1c-218">Essa é Olá alteração só é necessário toomake toothis código.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-218">This is hello only change you need toomake toothis code.</span></span>

<span data-ttu-id="9ed1c-219">Execute Olá aplicativo toosee sempre criptografado em ação.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-219">Run hello app toosee Always Encrypted in action.</span></span>

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
        // Update this line with your Clinic database connection string from hello Azure portal.
        static string connectionString = @"Replace with your connection string";

        static void Main(string[] args)
        {
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
            Console.WriteLine(Environment.NewLine + "All hello records currently in hello Patients table:");

            foreach (Patient patient in SelectAllPatients())
            {
                Console.WriteLine(patient.FirstName + " " + patient.LastName + "\tSSN: " + patient.SSN + "\tBirthdate: " + patient.BirthDate);
            }

            // Get patients by SSN.
            Console.WriteLine(Environment.NewLine + "Now let's locate records by searching hello encrypted SSN column.");

            string ssn;

            // This very simple validation only checks that hello user entered 11 characters.
            // In production be sure toocheck all user input and use hello best validation for your specific application.
            do
            {
                Console.WriteLine("Please enter a valid SSN (ex. 123-45-6789):");
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


## <a name="verify-that-hello-data-is-encrypted"></a><span data-ttu-id="9ed1c-220">Verificar se os dados de saudação foi criptografados</span><span class="sxs-lookup"><span data-stu-id="9ed1c-220">Verify that hello data is encrypted</span></span>
<span data-ttu-id="9ed1c-221">Você pode verificar rapidamente que os dados reais de Olá no servidor de saudação é criptografados consultando Olá **pacientes** dados com o SSMS.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-221">You can quickly check that hello actual data on hello server is encrypted by querying hello **Patients** data with SSMS.</span></span> <span data-ttu-id="9ed1c-222">(Use a conexão atual qual configuração de criptografia de coluna Olá ainda não está habilitada.)</span><span class="sxs-lookup"><span data-stu-id="9ed1c-222">(Use your current connection where hello column encryption setting is not yet enabled.)</span></span>

<span data-ttu-id="9ed1c-223">Execute Olá consulta a seguir no banco de dados de clínica hello.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-223">Run hello following query on hello Clinic database.</span></span>

    SELECT FirstName, LastName, SSN, BirthDate FROM Patients;

<span data-ttu-id="9ed1c-224">Você pode ver que colunas Olá criptografado não contêm nenhum dado de texto sem formatação.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-224">You can see that hello encrypted columns do not contain any plaintext data.</span></span>

   ![Novo aplicativo de console](./media/sql-database-always-encrypted/ssms-encrypted.png)

<span data-ttu-id="9ed1c-226">toouse SSMS tooaccess Olá dados de texto sem formatação, você pode adicionar Olá **Column Encryption Setting = habilitado** conexão de toohello do parâmetro.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-226">toouse SSMS tooaccess hello plaintext data, you can add hello **Column Encryption Setting=enabled** parameter toohello connection.</span></span>

1. <span data-ttu-id="9ed1c-227">No SSMS, clique com o botão direito do mouse no seu servidor em **Pesquisador de Objetos** e clique em **Desconectar**.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-227">In SSMS, right-click your server in **Object Explorer**, and then click **Disconnect**.</span></span>
2. <span data-ttu-id="9ed1c-228">Clique em **conectar** > **mecanismo de banco de dados** tooopen Olá **conectar tooServer** janela e clique **opções**.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-228">Click **Connect** > **Database Engine** tooopen hello **Connect tooServer** window, and then click **Options**.</span></span>
3. <span data-ttu-id="9ed1c-229">Clique em **Parâmetros Adicionais de Conexão** e digite **Column Encryption Setting=enabled**.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-229">Click **Additional Connection Parameters** and type **Column Encryption Setting=enabled**.</span></span>
   
    ![Novo aplicativo de console](./media/sql-database-always-encrypted/ssms-connection-parameter.png)
4. <span data-ttu-id="9ed1c-231">Execução hello seguinte consulta no hello **clínica** banco de dados.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-231">Run hello following query on hello **Clinic** database.</span></span>
   
        SELECT FirstName, LastName, SSN, BirthDate FROM Patients;
   
     <span data-ttu-id="9ed1c-232">Agora você pode ver os dados de texto sem formatação de saudação em colunas criptografada de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-232">You can now see hello plaintext data in hello encrypted columns.</span></span>

    ![Novo aplicativo de console](./media/sql-database-always-encrypted/ssms-plaintext.png)



> [!NOTE]
> <span data-ttu-id="9ed1c-234">Se você se conectar com o SSMS (ou qualquer cliente) em um computador diferente, ele não terá acesso chaves de criptografia de toohello e não será capaz de toodecrypt dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-234">If you connect with SSMS (or any client) from a different computer, it will not have access toohello encryption keys and will not be able toodecrypt hello data.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="9ed1c-235">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9ed1c-235">Next steps</span></span>
<span data-ttu-id="9ed1c-236">Depois de criar um banco de dados que usa o sempre criptografado, você poderá desejar a seguir Olá toodo:</span><span class="sxs-lookup"><span data-stu-id="9ed1c-236">After you create a database that uses Always Encrypted, you may want toodo hello following:</span></span>

* <span data-ttu-id="9ed1c-237">Executar esse exemplo de um computador diferente.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-237">Run this sample from a different computer.</span></span> <span data-ttu-id="9ed1c-238">Ele não terá acesso chaves de criptografia toohello, para que ele não terá dados do access toohello em texto sem formatação e não será executado com êxito.</span><span class="sxs-lookup"><span data-stu-id="9ed1c-238">It won't have access toohello encryption keys, so it will not have access toohello plaintext data and will not run successfully.</span></span>
* <span data-ttu-id="9ed1c-239">[Girar e limpar suas chaves](https://msdn.microsoft.com/library/mt607048.aspx).</span><span class="sxs-lookup"><span data-stu-id="9ed1c-239">[Rotate and clean up your keys](https://msdn.microsoft.com/library/mt607048.aspx).</span></span>
* <span data-ttu-id="9ed1c-240">[Migrar dados que já foram criptografados com o Always Encrypted](https://msdn.microsoft.com/library/mt621539.aspx).</span><span class="sxs-lookup"><span data-stu-id="9ed1c-240">[Migrate data that is already encrypted with Always Encrypted](https://msdn.microsoft.com/library/mt621539.aspx).</span></span>
* <span data-ttu-id="9ed1c-241">[Implantar o sempre criptografado máquinas de clientes de tooother certificados](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_1) (consulte a seção de "Fazer tooApplications de certificados disponíveis e os usuários" hello).</span><span class="sxs-lookup"><span data-stu-id="9ed1c-241">[Deploy Always Encrypted certificates tooother client machines](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_1) (see hello "Making Certificates Available tooApplications and Users" section).</span></span>

## <a name="related-information"></a><span data-ttu-id="9ed1c-242">Informações relacionadas</span><span class="sxs-lookup"><span data-stu-id="9ed1c-242">Related information</span></span>
* [<span data-ttu-id="9ed1c-243">Always Encrypted (desenvolvimento de cliente)</span><span class="sxs-lookup"><span data-stu-id="9ed1c-243">Always Encrypted (client development)</span></span>](https://msdn.microsoft.com/library/mt147923.aspx)
* [<span data-ttu-id="9ed1c-244">Transparent Data Encryption</span><span class="sxs-lookup"><span data-stu-id="9ed1c-244">Transparent Data Encryption</span></span>](https://msdn.microsoft.com/library/bb934049.aspx)
* [<span data-ttu-id="9ed1c-245">Criptografia do SQL Server</span><span class="sxs-lookup"><span data-stu-id="9ed1c-245">SQL Server Encryption</span></span>](https://msdn.microsoft.com/library/bb510663.aspx)
* [<span data-ttu-id="9ed1c-246">Assistente do Always Encrypted</span><span class="sxs-lookup"><span data-stu-id="9ed1c-246">Always Encrypted Wizard</span></span>](https://msdn.microsoft.com/library/mt459280.aspx)
* [<span data-ttu-id="9ed1c-247">Blog do Always Encrypted</span><span class="sxs-lookup"><span data-stu-id="9ed1c-247">Always Encrypted Blog</span></span>](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

