---
title: Gerenciar dados pessoais no Microsoft Azure | Microsoft Docs
description: diretrizes de como corrigir, atualizar, excluir e exportar dados pessoais no Azure Active Directory e no Banco de Dados SQL do Azure
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
ms.openlocfilehash: b04c745feb710d3d1d8a1fce23807168d6e6fa3d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-personal-data-in-microsoft-azure"></a><span data-ttu-id="09aa3-103">Gerenciar dados pessoais no Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="09aa3-103">Manage personal data in Microsoft Azure</span></span>

<span data-ttu-id="09aa3-104">Este artigo fornece diretrizes de como corrigir, atualizar, excluir e exportar dados pessoais no Azure Active Directory e no Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="09aa3-104">This article provides guidance on how to correct, update, delete, and export personal data in Azure Active Directory and Azure SQL Database.</span></span>

## <a name="scenario"></a><span data-ttu-id="09aa3-105">Cenário</span><span class="sxs-lookup"><span data-stu-id="09aa3-105">Scenario</span></span>

<span data-ttu-id="09aa3-106">Uma empresa localizada em Dublin fornece um único lugar de compras para casamentos em destinos de classe alta na Irlanda e no mundo para uma base de clientes local e internacional.</span><span class="sxs-lookup"><span data-stu-id="09aa3-106">A Dublin-based company provides one-stop shopping for high end destination weddings in Ireland and around the world for both a local and international customer base.</span></span> <span data-ttu-id="09aa3-107">Ela tem escritórios, clientes, funcionários e fornecedores localizados no mundo todo para prestar serviços completos para os locais oferecidos.</span><span class="sxs-lookup"><span data-stu-id="09aa3-107">They have offices, customers, employees, and vendors located around the world to fully service the venues they offer.</span></span>

<span data-ttu-id="09aa3-108">Entre muitos outros itens, a empresa acompanha os RSVPs que incluem alergias a alimentos e preferências alimentares.</span><span class="sxs-lookup"><span data-stu-id="09aa3-108">Among many other items, the company keeps track of RSVPs that include food allergies and dietary preferences.</span></span> <span data-ttu-id="09aa3-109">Os convidados do casamento podem se registrar em várias atividades, como passeios a cavalo, surfe, passeios de barco, etc. e até mesmo interagir entre si em uma página da Web central durante os meses anteriores ao evento.</span><span class="sxs-lookup"><span data-stu-id="09aa3-109">Wedding guests can register for various activities such as horseback riding, surfing, boat rides, etc., and even interact with one another on a central web page during the months leading up to the event.</span></span> <span data-ttu-id="09aa3-110">A empresa coleta informações pessoais de funcionários, fornecedores, clientes e convidados do casamento.</span><span class="sxs-lookup"><span data-stu-id="09aa3-110">The company collects personal information from employees, vendors, customers, and wedding guests.</span></span> <span data-ttu-id="09aa3-111">Devido à natureza internacional dos negócios, a empresa deve estar em conformidade com vários níveis de regulamentação.</span><span class="sxs-lookup"><span data-stu-id="09aa3-111">Because of the international nature of the business the company must comply with multiple levels of regulation.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="09aa3-112">Problema declarado</span><span class="sxs-lookup"><span data-stu-id="09aa3-112">Problem statement</span></span>

- <span data-ttu-id="09aa3-113">Os administradores de dados devem conseguir corrigir informações pessoais incorretas e atualizar informações pessoais incompletas ou alteradas.</span><span class="sxs-lookup"><span data-stu-id="09aa3-113">Data admins must be able to correct inaccurate personal information and update incomplete or changing personal information.</span></span>

- <span data-ttu-id="09aa3-114">Necessidade de administradores de dados deve ser capaz de excluir as informações pessoais na solicitação de uma entidade de dados.</span><span class="sxs-lookup"><span data-stu-id="09aa3-114">Data admins need must be able to delete personal information upon the request of a data subject.</span></span>

- <span data-ttu-id="09aa3-115">Os administradores de dados precisam exportar dados e fornecê-los a uma entidade de dados em um formato comum e estruturado mediante sua solicitação.</span><span class="sxs-lookup"><span data-stu-id="09aa3-115">Data admins need to export data and provide it to a data subject in a common, structured format upon his or her request.</span></span>

## <a name="company-goals"></a><span data-ttu-id="09aa3-116">Metas da empresa</span><span class="sxs-lookup"><span data-stu-id="09aa3-116">Company goals</span></span>

- <span data-ttu-id="09aa3-117">As informações pessoais incorretas ou incompletas de clientes, convidados do casamento, funcionários e fornecedores devem ser corrigidas ou atualizadas no Azure Active Directory e no Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="09aa3-117">Inaccurate or incomplete customer, wedding guest, employee, and vendor personal information must be corrected or updated in Azure Active Directory and Azure SQL Database.</span></span>

- <span data-ttu-id="09aa3-118">As informações pessoais devem ser excluídas do Azure Active Directory e do Banco de Dados SQL do Azure mediante a solicitação de uma entidade de dados.</span><span class="sxs-lookup"><span data-stu-id="09aa3-118">Personal information must be deleted in Azure Active Directory and Azure SQL Database upon the request of a data subject.</span></span>

- <span data-ttu-id="09aa3-119">Os dados pessoais devem ser exportados em um formato comum e estruturado mediante a solicitação de uma entidade de dados.</span><span class="sxs-lookup"><span data-stu-id="09aa3-119">Personal data must be exported in a common, structured format upon the request of a data subject.</span></span>

## <a name="solutions"></a><span data-ttu-id="09aa3-120">Soluções</span><span class="sxs-lookup"><span data-stu-id="09aa3-120">Solutions</span></span>

### <a name="azure-active-directory-rectifycorrect-inaccurate-or-incomplete-personal-data-and-erasedelete-personal-datauser-profiles"></a><span data-ttu-id="09aa3-121">Azure Active Directory: retificar/corrigir dados pessoais incorretos ou incompletos e apagar/excluir dados pessoais/perfis do usuário</span><span class="sxs-lookup"><span data-stu-id="09aa3-121">Azure Active Directory: rectify/correct inaccurate or incomplete personal data and erase/delete personal data/user profiles</span></span>

<span data-ttu-id="09aa3-122">O [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) é o serviço de gerenciamento de identidade e diretório multilocatário baseado em nuvem da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="09aa3-122">[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) is Microsoft’s cloud-based, multi-tenant directory and identity management service.</span></span>
<span data-ttu-id="09aa3-123">É possível corrigir, atualizar ou excluir perfis do usuário de clientes e funcionários e informações de trabalho dos usuários que contêm dados pessoais, como o nome de um usuário, cargo, endereço ou número de telefone, no ambiente do [AAD](https://azure.microsoft.com/services/active-directory/) (Azure Active Directory) usando o [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="09aa3-123">You can correct, update, or delete customer and employee user profiles and user work information that contain personal data, such as a user’s name, work title, address, or phone number, in your [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (AAD) environment by using the [Azure portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="09aa3-124">Entre com uma conta que seja um administrador global do diretório.</span><span class="sxs-lookup"><span data-stu-id="09aa3-124">You must sign in with an account that’s a global admin for the directory.</span></span>

#### <a name="how-do-i-correct-or-update-user-profile-and-work-information-in-azure-active-directory"></a><span data-ttu-id="09aa3-125">Como fazer para corrigir ou atualizar o perfil do usuário e as informações de trabalho no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="09aa3-125">How do I correct or update user profile and work information in Azure Active Directory?</span></span>

1. <span data-ttu-id="09aa3-126">Entre no [Portal do Azure](https://portal.azure.com) com uma conta que seja um administrador global do diretório.</span><span class="sxs-lookup"><span data-stu-id="09aa3-126">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>

2. <span data-ttu-id="09aa3-127">Escolha **Mais serviços**, insira **Usuários e grupos** na caixa de texto e selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="09aa3-127">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

    ![media/image1.png](media/manage-personal-data-azure/image001.png)

3. <span data-ttu-id="09aa3-129">Na folha **Usuários e grupos**, selecione **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="09aa3-129">On the **Users and groups** blade, select **Users**.</span></span>

    ![media/image2.png](media/manage-personal-data-azure/image003.png)

4. <span data-ttu-id="09aa3-131">Na folha **Usuários e grupos – Usuários**, selecione um usuário na lista e, em seguida, na folha do usuário selecionado, selecione **Perfil** para exibir as informações de perfil do usuário que precisam ser corrigidas ou atualizadas.</span><span class="sxs-lookup"><span data-stu-id="09aa3-131">On the **Users and groups - Users** blade, select a user from the list, and then, on the blade for the selected user, select **Profile** to view the user profile information that needs to be corrected or updated.</span></span>

    ![media/image3.png](media/manage-personal-data-azure/image005.png)

5. <span data-ttu-id="09aa3-133">Corrija ou atualize as informações e, em seguida, na barra de comandos, selecione **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="09aa3-133">Correct or update the information, and then, in the command bar, select **Save.**</span></span>

6.  <span data-ttu-id="09aa3-134">Na folha do usuário selecionado, selecione **Informações de Trabalho** para exibir as informações de trabalho dos usuários que precisam ser corrigidas ou atualizadas.</span><span class="sxs-lookup"><span data-stu-id="09aa3-134">On the blade for the selected user, select **Work Info** to view user work information that needs to be corrected or updated.</span></span>

    ![media/image4.png](media/manage-personal-data-azure/image007.png)

7. <span data-ttu-id="09aa3-136">Corrija ou atualize as informações de trabalho dos usuários e, em seguida, na barra de comandos, selecione **Salvar.**</span><span class="sxs-lookup"><span data-stu-id="09aa3-136">Correct or update the user work information, and then, in the command bar, select **Save.**</span></span>

#### <a name="how-do-i-delete-a-user-profile-in-azure-active-directory"></a><span data-ttu-id="09aa3-137">Como fazer para excluir um perfil do usuário do Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="09aa3-137">How do I delete a user profile in Azure Active Directory?</span></span>

1. <span data-ttu-id="09aa3-138">Entre no [Portal do Azure](https://portal.azure.com) com uma conta que seja um administrador global do diretório.</span><span class="sxs-lookup"><span data-stu-id="09aa3-138">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>

2. <span data-ttu-id="09aa3-139">Escolha **Mais serviços**, insira **Usuários e grupos** na caixa de texto e selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="09aa3-139">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

    ![](media/manage-personal-data-azure/image001.png)

3. <span data-ttu-id="09aa3-140">Na folha **Usuários e grupos**, selecione **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="09aa3-140">On the **Users and groups** blade, select **Users**.</span></span>

    ![media/image2.png](media/manage-personal-data-azure/image003.png)

4. <span data-ttu-id="09aa3-142">Na folha **Usuários e grupos - Usuários** , escolha um usuário na lista.</span><span class="sxs-lookup"><span data-stu-id="09aa3-142">On the **Users and groups - Users** blade, select a user from the list.</span></span>

    ![media/image3.png](media/manage-personal-data-azure/image007.png)

5. <span data-ttu-id="09aa3-144">Na folha para o usuário selecionado, escolha **Visão geral** e, na barra de comandos, escolha **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="09aa3-144">On the blade for the selected user, select **Overview**, and then in the command bar, select **Delete**.</span></span>

    ![](media/manage-personal-data-azure/image013.png)

### <a name="sql-database-rectifycorrect-inaccurate-or-incomplete-personal-data-erasedelete-personal-data-export-personal-data"></a><span data-ttu-id="09aa3-145">Banco de Dados SQL: retificar/corrigir dados pessoais incorretos ou incompletos; apagar/excluir dados pessoais; exportar dados pessoais</span><span class="sxs-lookup"><span data-stu-id="09aa3-145">SQL Database: rectify/correct inaccurate or incomplete personal data; erase/delete personal data; export personal data</span></span> 

<span data-ttu-id="09aa3-146">O [Banco de Dados SQL do Azure](https://azure.microsoft.com/services/sql-database/?v=16.50) é um banco de dados de nuvem que ajuda os desenvolvedores a criar e manter aplicativos.</span><span class="sxs-lookup"><span data-stu-id="09aa3-146">[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) is a cloud database that helps developers build and maintain applications.</span></span>

<span data-ttu-id="09aa3-147">Os dados pessoais podem ser atualizados no [Banco de Dados SQL do Azure](https://azure.microsoft.com/services/sql-database/?v=16.50) usando consultas SQL padrão e eles também podem ser excluídos.</span><span class="sxs-lookup"><span data-stu-id="09aa3-147">Personal data can be updated in [Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) using standard SQL queries, and it can also be deleted.</span></span> <span data-ttu-id="09aa3-148">Além disso, os dados pessoais podem ser exportados do Banco de Dados SQL usando uma variedade de métodos, incluindo o assistente para importação e exportação do SQL Server do Azure, e em uma variedade de formatos, incluindo um arquivo BACPAC.</span><span class="sxs-lookup"><span data-stu-id="09aa3-148">Additionally, personal data can be exported from SQL Database using a variety of methods, including the Azure SQL Server import and export wizard, and in a variety of formats, including a BACPAC file.</span></span>

#### <a name="how-do-i-correct-update-or-erase-personal-data-in-sql-database"></a><span data-ttu-id="09aa3-149">Como fazer para corrigir, atualizar ou apagar dados pessoais do Banco de Dados SQL?</span><span class="sxs-lookup"><span data-stu-id="09aa3-149">How do I correct, update, or erase personal data in SQL Database?</span></span>

<span data-ttu-id="09aa3-150">Para saber como corrigir ou atualizar dados pessoais no Banco de Dados SQL, visite a documentação [Atualizar (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql), [Atualizar Texto](https://docs.microsoft.com/sql/t-sql/queries/updatetext-transact-sql), [Atualizar com Expressão de Tabela Comum](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql) ou [Atualizar Texto de Gravação](https://docs.microsoft.com/sql/t-sql/queries/writetext-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="09aa3-150">To learn how to correct or update personal data in SQL Database, visit the [Update (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql), [Update Text](https://docs.microsoft.com/sql/t-sql/queries/updatetext-transact-sql), [Update with Common Table Expression](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql), or [Update Write Text](https://docs.microsoft.com/sql/t-sql/queries/writetext-transact-sql) documentation.</span></span>

<span data-ttu-id="09aa3-151">Para saber como excluir dados pessoais do Banco de Dados SQL, visite a documentação [Excluir (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="09aa3-151">To learn how to delete personal data in SQL Database, visit the [Delete (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql) documentation.</span></span>

#### <a name="how-do-i-export-personal-data-to-a-bacpac-file-in-sql-database"></a><span data-ttu-id="09aa3-152">Como fazer para exportar dados pessoais para um arquivo BACPAC no Banco de Dados SQL?</span><span class="sxs-lookup"><span data-stu-id="09aa3-152">How do I export personal data to a BACPAC file in SQL Database?</span></span>

<span data-ttu-id="09aa3-153">Um arquivo BACPAC inclui os dados e os metadados do Banco de Dados SQL e é um arquivo zip com uma extensão BACPAC.</span><span class="sxs-lookup"><span data-stu-id="09aa3-153">A BACPAC file includes the SQL Database data and metadata and is a zip file with a BACPAC extension.</span></span> <span data-ttu-id="09aa3-154">Faça isso usando o [portal do Azure](https://portal.azure.com/), o utilitário de linha de comando SQLPackage, o SSMS (SQL Server Management Studio) ou o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="09aa3-154">This can be done using the [Azure portal](https://portal.azure.com/), the SQLPackage command-line utility, SQL Server Management Studio (SSMS), or PowerShell.</span></span>

<span data-ttu-id="09aa3-155">Para saber como exportar dados para um arquivo BACPAC, visite a página [Exportar um banco de dados SQL do Azure para um arquivo BACPAC](https://docs.microsoft.com/azure/sql-database/sql-database-export), que inclui instruções detalhadas para cada método listado acima.</span><span class="sxs-lookup"><span data-stu-id="09aa3-155">To learn how to export data to a BACPAC file, visit the [Export an Azure SQL database to a BACPAC file](https://docs.microsoft.com/azure/sql-database/sql-database-export) page, which includes detailed instructions for each method listed above.</span></span>

<span data-ttu-id="09aa3-156">Como fazer para exportar dados pessoais do Banco de Dados SQL com o Assistente para Importação e Exportação do SQL Server?</span><span class="sxs-lookup"><span data-stu-id="09aa3-156">How do I export personal data from SQL Database with the SQL Server Import and Export Wizard?</span></span>

<span data-ttu-id="09aa3-157">Esse assistente ajuda você a copiar dados de uma origem para um destino.</span><span class="sxs-lookup"><span data-stu-id="09aa3-157">This wizard helps you copy data from a source to a destination.</span></span> <span data-ttu-id="09aa3-158">Para obter uma introdução ao assistente, incluindo como obtê-lo, informações sobre permissões e como obter ajuda com a ferramenta, visite a página da Web [Importar e exportar dados com o Assistente para Importação e Exportação do SQL Server](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard).</span><span class="sxs-lookup"><span data-stu-id="09aa3-158">For an introduction to the wizard, including how to get it, permissions information, and how to get help with the tool, visit the [Import and Export Data with the SQL Server Import and Export Wizard](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard) web page.</span></span>

<span data-ttu-id="09aa3-159">Para obter uma visão geral das etapas do assistente, visite a página da Web [Etapas do Assistente para Importação e Exportação do SQL Server](https://docs.microsoft.com/sql/integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard).</span><span class="sxs-lookup"><span data-stu-id="09aa3-159">For an overview of steps for the wizard, visit the [Steps in the SQL Server Import and Export Wizard](https://docs.microsoft.com/sql/integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard) web page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="09aa3-160">Próximas etapas:</span><span class="sxs-lookup"><span data-stu-id="09aa3-160">Next Steps:</span></span>

[<span data-ttu-id="09aa3-161">Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="09aa3-161">Azure SQL Database</span></span>](https://azure.microsoft.com/services/sql-database/?v=16.50) 

[<span data-ttu-id="09aa3-162">Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="09aa3-162">Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

