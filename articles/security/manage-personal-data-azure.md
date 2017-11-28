---
title: dados pessoais de aaaManage no Microsoft Azure | Microsoft Docs
description: "orientação sobre como toocorrect, atualizar, excluir e exportar dados pessoais no Active Directory do Azure e banco de dados do SQL Azure"
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.openlocfilehash: 032f70d32377cb9395cb2c35c27dad05001537c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-personal-data-in-microsoft-azure"></a><span data-ttu-id="13dc1-103">Gerenciar dados pessoais no Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="13dc1-103">Manage personal data in Microsoft Azure</span></span>

<span data-ttu-id="13dc1-104">Este artigo fornece orientação sobre como toocorrect, atualizar, excluir e exportar dados pessoais no Active Directory do Azure e banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="13dc1-104">This article provides guidance on how toocorrect, update, delete, and export personal data in Azure Active Directory and Azure SQL Database.</span></span>

## <a name="scenario"></a><span data-ttu-id="13dc1-105">Cenário</span><span class="sxs-lookup"><span data-stu-id="13dc1-105">Scenario</span></span>

<span data-ttu-id="13dc1-106">Uma empresa Dublin fornece um único lugar para casamentos de destino de alto nível da Irlanda e Olá mundo para ambos os uma base de clientes locais e internacionais.</span><span class="sxs-lookup"><span data-stu-id="13dc1-106">A Dublin-based company provides one-stop shopping for high end destination weddings in Ireland and around hello world for both a local and international customer base.</span></span> <span data-ttu-id="13dc1-107">Eles têm escritórios, clientes, funcionários e fornecedores espalhados locais Olá mundo toofully serviço Olá oferecem.</span><span class="sxs-lookup"><span data-stu-id="13dc1-107">They have offices, customers, employees, and vendors located around hello world toofully service hello venues they offer.</span></span>

<span data-ttu-id="13dc1-108">Entre muitos outros itens, empresa Olá controla de RSVPs que incluem alergias alimentos e preferências dieta.</span><span class="sxs-lookup"><span data-stu-id="13dc1-108">Among many other items, hello company keeps track of RSVPs that include food allergies and dietary preferences.</span></span> <span data-ttu-id="13dc1-109">Convidados do casamento podem registrar para várias atividades, como a cavalo riding, navegar, barco percursos, etc. e até mesmo interagir entre si em uma página da web central durante os meses de saudação levam toohello eventos.</span><span class="sxs-lookup"><span data-stu-id="13dc1-109">Wedding guests can register for various activities such as horseback riding, surfing, boat rides, etc., and even interact with one another on a central web page during hello months leading up toohello event.</span></span> <span data-ttu-id="13dc1-110">empresa Olá coleta informações pessoais dos funcionários, fornecedores, clientes e convidados casamento.</span><span class="sxs-lookup"><span data-stu-id="13dc1-110">hello company collects personal information from employees, vendors, customers, and wedding guests.</span></span> <span data-ttu-id="13dc1-111">Devido a saudação internacional natureza da empresa de saudação de negócios Olá deve estar em conformidade com vários níveis de regulamentação.</span><span class="sxs-lookup"><span data-stu-id="13dc1-111">Because of hello international nature of hello business hello company must comply with multiple levels of regulation.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="13dc1-112">Problema declarado</span><span class="sxs-lookup"><span data-stu-id="13dc1-112">Problem statement</span></span>

- <span data-ttu-id="13dc1-113">Administradores de dados devem ser toocorrect capaz de imprecisas pessoal informações e atualização incompletas ou alteradas informações pessoais.</span><span class="sxs-lookup"><span data-stu-id="13dc1-113">Data admins must be able toocorrect inaccurate personal information and update incomplete or changing personal information.</span></span>

- <span data-ttu-id="13dc1-114">Necessidade de administradores de dados deve ser capaz de toodelete informações pessoais mediante solicitação saudação de uma entidade de dados.</span><span class="sxs-lookup"><span data-stu-id="13dc1-114">Data admins need must be able toodelete personal information upon hello request of a data subject.</span></span>

- <span data-ttu-id="13dc1-115">Administradores de dados precisam tooexport dados e fornecem-la tooa assunto de dados em um formato comum, estruturado após a sua solicitação.</span><span class="sxs-lookup"><span data-stu-id="13dc1-115">Data admins need tooexport data and provide it tooa data subject in a common, structured format upon his or her request.</span></span>

## <a name="company-goals"></a><span data-ttu-id="13dc1-116">Metas da empresa</span><span class="sxs-lookup"><span data-stu-id="13dc1-116">Company goals</span></span>

- <span data-ttu-id="13dc1-117">As informações pessoais incorretas ou incompletas de clientes, convidados do casamento, funcionários e fornecedores devem ser corrigidas ou atualizadas no Azure Active Directory e no Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="13dc1-117">Inaccurate or incomplete customer, wedding guest, employee, and vendor personal information must be corrected or updated in Azure Active Directory and Azure SQL Database.</span></span>

- <span data-ttu-id="13dc1-118">Informações pessoais devem ser excluídas no Active Directory do Azure e banco de dados do SQL Azure mediante solicitação saudação de uma entidade de dados.</span><span class="sxs-lookup"><span data-stu-id="13dc1-118">Personal information must be deleted in Azure Active Directory and Azure SQL Database upon hello request of a data subject.</span></span>

- <span data-ttu-id="13dc1-119">Dados pessoais devem ser exportados em um formato comum, estruturado mediante solicitação saudação de uma entidade de dados.</span><span class="sxs-lookup"><span data-stu-id="13dc1-119">Personal data must be exported in a common, structured format upon hello request of a data subject.</span></span>

## <a name="solutions"></a><span data-ttu-id="13dc1-120">Soluções</span><span class="sxs-lookup"><span data-stu-id="13dc1-120">Solutions</span></span>

### <a name="azure-active-directory-rectifycorrect-inaccurate-or-incomplete-personal-data-and-erasedelete-personal-datauser-profiles"></a><span data-ttu-id="13dc1-121">Azure Active Directory: retificar/corrigir dados pessoais incorretos ou incompletos e apagar/excluir dados pessoais/perfis do usuário</span><span class="sxs-lookup"><span data-stu-id="13dc1-121">Azure Active Directory: rectify/correct inaccurate or incomplete personal data and erase/delete personal data/user profiles</span></span>

<span data-ttu-id="13dc1-122">O [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) é o serviço de gerenciamento de identidade e diretório multilocatário baseado em nuvem da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="13dc1-122">[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) is Microsoft’s cloud-based, multi-tenant directory and identity management service.</span></span>
<span data-ttu-id="13dc1-123">Você pode corrigir, atualizar ou excluir perfis de usuário do cliente e do funcionário e informações de trabalho do usuário que contêm dados pessoais, como nome, nome do cargo, endereço ou número de telefone, um usuário em sua [Active Directory do Azure](https://azure.microsoft.com/services/active-directory/) (AAD) ambiente usando Olá [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="13dc1-123">You can correct, update, or delete customer and employee user profiles and user work information that contain personal data, such as a user’s name, work title, address, or phone number, in your [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (AAD) environment by using hello [Azure portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="13dc1-124">Você deve entrar com uma conta que seja um administrador global para o diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="13dc1-124">You must sign in with an account that’s a global admin for hello directory.</span></span>

#### <a name="how-do-i-correct-or-update-user-profile-and-work-information-in-azure-active-directory"></a><span data-ttu-id="13dc1-125">Como fazer para corrigir ou atualizar o perfil do usuário e as informações de trabalho no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="13dc1-125">How do I correct or update user profile and work information in Azure Active Directory?</span></span>

1. <span data-ttu-id="13dc1-126">Entrar toohello [portal do Azure](https://portal.azure.com) com uma conta que seja um administrador global para o diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="13dc1-126">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>

2. <span data-ttu-id="13dc1-127">Selecione **mais serviços**, digite **usuários e grupos** Olá caixa de texto e, em seguida, selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="13dc1-127">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

    ![media/image1.png](media/manage-personal-data-azure/image001.png)

3. <span data-ttu-id="13dc1-129">Em Olá **usuários e grupos** folha, selecione **usuários**.</span><span class="sxs-lookup"><span data-stu-id="13dc1-129">On hello **Users and groups** blade, select **Users**.</span></span>

    ![media/image2.png](media/manage-personal-data-azure/image003.png)

4. <span data-ttu-id="13dc1-131">Em Olá **usuários e grupos, usuários** folha, selecione um usuário na lista de saudação e, em seguida, na folha de saudação do usuário selecionado hello, selecione **perfil** tooview Olá informações perfil do usuário que precisa toobe corrigido ou atualizados.</span><span class="sxs-lookup"><span data-stu-id="13dc1-131">On hello **Users and groups - Users** blade, select a user from hello list, and then, on hello blade for hello selected user, select **Profile** tooview hello user profile information that needs toobe corrected or updated.</span></span>

    ![media/image3.png](media/manage-personal-data-azure/image005.png)

5. <span data-ttu-id="13dc1-133">Corrigir ou atualizar as informações de saudação e, em seguida, na barra de comandos hello, selecione **salvar.**</span><span class="sxs-lookup"><span data-stu-id="13dc1-133">Correct or update hello information, and then, in hello command bar, select **Save.**</span></span>

6.  <span data-ttu-id="13dc1-134">Na folha de saudação do usuário selecionado hello, selecione **informações de trabalho** tooview informações de trabalho de usuário que precisa toobe corrigido ou atualizado.</span><span class="sxs-lookup"><span data-stu-id="13dc1-134">On hello blade for hello selected user, select **Work Info** tooview user work information that needs toobe corrected or updated.</span></span>

    ![media/image4.png](media/manage-personal-data-azure/image007.png)

7. <span data-ttu-id="13dc1-136">Corrigir ou atualizar informações de trabalho do usuário hello e, em seguida, na barra de comandos hello, selecione **salvar.**</span><span class="sxs-lookup"><span data-stu-id="13dc1-136">Correct or update hello user work information, and then, in hello command bar, select **Save.**</span></span>

#### <a name="how-do-i-delete-a-user-profile-in-azure-active-directory"></a><span data-ttu-id="13dc1-137">Como fazer para excluir um perfil do usuário do Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="13dc1-137">How do I delete a user profile in Azure Active Directory?</span></span>

1. <span data-ttu-id="13dc1-138">Entrar toohello [portal do Azure](https://portal.azure.com) com uma conta que seja um administrador global para o diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="13dc1-138">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>

2. <span data-ttu-id="13dc1-139">Selecione **mais serviços**, digite **usuários e grupos** Olá caixa de texto e, em seguida, selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="13dc1-139">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

    ![](media/manage-personal-data-azure/image001.png)

3. <span data-ttu-id="13dc1-140">Em Olá **usuários e grupos** folha, selecione **usuários**.</span><span class="sxs-lookup"><span data-stu-id="13dc1-140">On hello **Users and groups** blade, select **Users**.</span></span>

    ![media/image2.png](media/manage-personal-data-azure/image003.png)

4. <span data-ttu-id="13dc1-142">Em Olá **usuários e grupos, usuários** folha, selecione um usuário na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="13dc1-142">On hello **Users and groups - Users** blade, select a user from hello list.</span></span>

    ![media/image3.png](media/manage-personal-data-azure/image007.png)

5. <span data-ttu-id="13dc1-144">Na folha de saudação do usuário selecionado hello, selecione **visão geral**e, em seguida, na barra de comandos hello, selecione **excluir**.</span><span class="sxs-lookup"><span data-stu-id="13dc1-144">On hello blade for hello selected user, select **Overview**, and then in hello command bar, select **Delete**.</span></span>

    ![](media/manage-personal-data-azure/image013.png)

### <a name="sql-database-rectifycorrect-inaccurate-or-incomplete-personal-data-erasedelete-personal-data-export-personal-data"></a><span data-ttu-id="13dc1-145">Banco de Dados SQL: retificar/corrigir dados pessoais incorretos ou incompletos; apagar/excluir dados pessoais; exportar dados pessoais</span><span class="sxs-lookup"><span data-stu-id="13dc1-145">SQL Database: rectify/correct inaccurate or incomplete personal data; erase/delete personal data; export personal data</span></span> 

<span data-ttu-id="13dc1-146">O [Banco de Dados SQL do Azure](https://azure.microsoft.com/services/sql-database/?v=16.50) é um banco de dados de nuvem que ajuda os desenvolvedores a criar e manter aplicativos.</span><span class="sxs-lookup"><span data-stu-id="13dc1-146">[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) is a cloud database that helps developers build and maintain applications.</span></span>

<span data-ttu-id="13dc1-147">Os dados pessoais podem ser atualizados no [Banco de Dados SQL do Azure](https://azure.microsoft.com/services/sql-database/?v=16.50) usando consultas SQL padrão e eles também podem ser excluídos.</span><span class="sxs-lookup"><span data-stu-id="13dc1-147">Personal data can be updated in [Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) using standard SQL queries, and it can also be deleted.</span></span> <span data-ttu-id="13dc1-148">Além disso, os dados pessoais podem ser exportados do banco de dados SQL usando uma variedade de métodos, incluindo hello importação do Azure SQL Server e o Assistente de exportação e em uma variedade de formatos, incluindo um arquivo BACPAC.</span><span class="sxs-lookup"><span data-stu-id="13dc1-148">Additionally, personal data can be exported from SQL Database using a variety of methods, including hello Azure SQL Server import and export wizard, and in a variety of formats, including a BACPAC file.</span></span>

#### <a name="how-do-i-correct-update-or-erase-personal-data-in-sql-database"></a><span data-ttu-id="13dc1-149">Como fazer para corrigir, atualizar ou apagar dados pessoais do Banco de Dados SQL?</span><span class="sxs-lookup"><span data-stu-id="13dc1-149">How do I correct, update, or erase personal data in SQL Database?</span></span>

<span data-ttu-id="13dc1-150">toolearn como toocorrect ou atualização de dados pessoais no banco de dados SQL, visite Olá [atualização (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql), [atualizar texto](https://docs.microsoft.com/sql/t-sql/queries/updatetext-transact-sql), [atualizar com expressão de tabela comum](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql), ou [ Atualizar gravar texto](https://docs.microsoft.com/sql/t-sql/queries/writetext-transact-sql) documentação.</span><span class="sxs-lookup"><span data-stu-id="13dc1-150">toolearn how toocorrect or update personal data in SQL Database, visit hello [Update (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql), [Update Text](https://docs.microsoft.com/sql/t-sql/queries/updatetext-transact-sql), [Update with Common Table Expression](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql), or [Update Write Text](https://docs.microsoft.com/sql/t-sql/queries/writetext-transact-sql) documentation.</span></span>

<span data-ttu-id="13dc1-151">toolearn como dados pessoais de toodelete no banco de dados SQL, visite Olá [excluir (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql) documentação.</span><span class="sxs-lookup"><span data-stu-id="13dc1-151">toolearn how toodelete personal data in SQL Database, visit hello [Delete (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql) documentation.</span></span>

#### <a name="how-do-i-export-personal-data-tooa-bacpac-file-in-sql-database"></a><span data-ttu-id="13dc1-152">Como Exportar arquivo BACPAC tooa dados pessoais no banco de dados SQL?</span><span class="sxs-lookup"><span data-stu-id="13dc1-152">How do I export personal data tooa BACPAC file in SQL Database?</span></span>

<span data-ttu-id="13dc1-153">Um arquivo BACPAC inclui os metadados e dados do banco de dados SQL de saudação e é um arquivo zip com uma extensão. BACPAC.</span><span class="sxs-lookup"><span data-stu-id="13dc1-153">A BACPAC file includes hello SQL Database data and metadata and is a zip file with a BACPAC extension.</span></span> <span data-ttu-id="13dc1-154">Isso pode ser feito usando Olá [portal do Azure](https://portal.azure.com/), Olá SQLPackage o utilitário de linha de comando, o SQL Server Management Studio (SSMS) ou o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="13dc1-154">This can be done using hello [Azure portal](https://portal.azure.com/), hello SQLPackage command-line utility, SQL Server Management Studio (SSMS), or PowerShell.</span></span>

<span data-ttu-id="13dc1-155">toolearn como tooexport tooa BACPAC arquivo de dados Olá visite [exportar um arquivo de BACPAC de tooa de banco de dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-export) página, que inclui instruções detalhadas para cada método listados acima.</span><span class="sxs-lookup"><span data-stu-id="13dc1-155">toolearn how tooexport data tooa BACPAC file, visit hello [Export an Azure SQL database tooa BACPAC file](https://docs.microsoft.com/azure/sql-database/sql-database-export) page, which includes detailed instructions for each method listed above.</span></span>

<span data-ttu-id="13dc1-156">Como exportar dados pessoais do banco de dados SQL com hello importação do SQL Server e o Assistente para exportação?</span><span class="sxs-lookup"><span data-stu-id="13dc1-156">How do I export personal data from SQL Database with hello SQL Server Import and Export Wizard?</span></span>

<span data-ttu-id="13dc1-157">Este assistente ajuda você a copiar dados de um origem tooa destino.</span><span class="sxs-lookup"><span data-stu-id="13dc1-157">This wizard helps you copy data from a source tooa destination.</span></span> <span data-ttu-id="13dc1-158">Assistente de toohello uma introdução, incluindo como tooget, informações sobre permissões e como ajudar a tooget com ferramenta hello, visite Olá [Import e exportar dados com hello SQL Server Import and Export Wizard](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard) página da web.</span><span class="sxs-lookup"><span data-stu-id="13dc1-158">For an introduction toohello wizard, including how tooget it, permissions information, and how tooget help with hello tool, visit hello [Import and Export Data with hello SQL Server Import and Export Wizard](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard) web page.</span></span>

<span data-ttu-id="13dc1-159">Para obter uma visão geral das etapas de assistente hello, visite Olá [as etapas no Assistente de exportação e saudação do SQL Server Import](https://docs.microsoft.com/sql/integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard) página da web.</span><span class="sxs-lookup"><span data-stu-id="13dc1-159">For an overview of steps for hello wizard, visit hello [Steps in hello SQL Server Import and Export Wizard](https://docs.microsoft.com/sql/integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard) web page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="13dc1-160">Próximas etapas:</span><span class="sxs-lookup"><span data-stu-id="13dc1-160">Next Steps:</span></span>

[<span data-ttu-id="13dc1-161">Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="13dc1-161">Azure SQL Database</span></span>](https://azure.microsoft.com/services/sql-database/?v=16.50) 

[<span data-ttu-id="13dc1-162">Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="13dc1-162">Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

