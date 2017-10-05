---
title: Fontes de dados com suporte no Azure Analysis Services | Microsoft Docs
description: Descreve as fontes de fonte de dados com suporte para modelos de dados no Azure Analysis Services.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 6ec63319-ff9b-4b01-a1cd-274481dc8995
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 8bd6c3b5a923ce2f3cd0f60af82e59c5cc27cbb4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="data-sources-supported-in-azure-analysis-services"></a><span data-ttu-id="41571-103">Fontes de dados com suporte no Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="41571-103">Data sources supported in Azure Analysis Services</span></span>
<span data-ttu-id="41571-104">Os servidores do Azure Analysis Services oferecem suporte à conexão às fontes de dados na nuvem e locais na sua organização.</span><span class="sxs-lookup"><span data-stu-id="41571-104">Azure Analysis Services servers support connecting to data sources in the cloud and on-premises in your organization.</span></span> <span data-ttu-id="41571-105">O tempo todo são adicionadas mais fontes de dados com suporte.</span><span class="sxs-lookup"><span data-stu-id="41571-105">Additional supported data sources are being added all the time.</span></span> <span data-ttu-id="41571-106">Verifique com frequência.</span><span class="sxs-lookup"><span data-stu-id="41571-106">Check back often.</span></span> 

<span data-ttu-id="41571-107">Atualmente, há suporte às seguintes fontes de dados:</span><span class="sxs-lookup"><span data-stu-id="41571-107">The following data sources are currently supported:</span></span>

| <span data-ttu-id="41571-108">Nuvem</span><span class="sxs-lookup"><span data-stu-id="41571-108">Cloud</span></span>  |
|---|
| <span data-ttu-id="41571-109">Armazenamento de Blobs do Azure*</span><span class="sxs-lookup"><span data-stu-id="41571-109">Azure Blob Storage*</span></span>  |
| <span data-ttu-id="41571-110">Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="41571-110">Azure SQL Database</span></span>  |
| <span data-ttu-id="41571-111">Data Warehouse do Azure</span><span class="sxs-lookup"><span data-stu-id="41571-111">Azure Data Warehouse</span></span> |


| <span data-ttu-id="41571-112">Configuração local</span><span class="sxs-lookup"><span data-stu-id="41571-112">On-premises</span></span>  |   |   |   |
|---|---|---|---|
| <span data-ttu-id="41571-113">Banco de Dados do Access</span><span class="sxs-lookup"><span data-stu-id="41571-113">Access Database</span></span>  | <span data-ttu-id="41571-114">Pasta*</span><span class="sxs-lookup"><span data-stu-id="41571-114">Folder*</span></span> | <span data-ttu-id="41571-115">Banco de dados Oracle</span><span class="sxs-lookup"><span data-stu-id="41571-115">Oracle Database</span></span>  | <span data-ttu-id="41571-116">Banco de dados Teradata</span><span class="sxs-lookup"><span data-stu-id="41571-116">Teradata Database</span></span> |
| <span data-ttu-id="41571-117">Active Directory*</span><span class="sxs-lookup"><span data-stu-id="41571-117">Active Directory*</span></span>  | <span data-ttu-id="41571-118">Documento JSON*</span><span class="sxs-lookup"><span data-stu-id="41571-118">JSON document*</span></span>  | <span data-ttu-id="41571-119">Banco de Dados SQL Postgre*</span><span class="sxs-lookup"><span data-stu-id="41571-119">Postgre SQL Database*</span></span>  |<span data-ttu-id="41571-120">Tabela XML*</span><span class="sxs-lookup"><span data-stu-id="41571-120">XML table*</span></span> |
| <span data-ttu-id="41571-121">Serviços de análise</span><span class="sxs-lookup"><span data-stu-id="41571-121">Analysis Services</span></span>  | <span data-ttu-id="41571-122">Linhas de binário*</span><span class="sxs-lookup"><span data-stu-id="41571-122">Lines from binary*</span></span>  | <span data-ttu-id="41571-123">SAP HANA*</span><span class="sxs-lookup"><span data-stu-id="41571-123">SAP HANA*</span></span>  |
| <span data-ttu-id="41571-124">Analytics Platform System</span><span class="sxs-lookup"><span data-stu-id="41571-124">Analytics Platform System</span></span>  | <span data-ttu-id="41571-125">Banco de Dados MySQL</span><span class="sxs-lookup"><span data-stu-id="41571-125">MySQL Database</span></span>  | <span data-ttu-id="41571-126">SAP Business Warehouse*</span><span class="sxs-lookup"><span data-stu-id="41571-126">SAP Business Warehouse*</span></span>  | |
| <span data-ttu-id="41571-127">Dynamics CRM*</span><span class="sxs-lookup"><span data-stu-id="41571-127">Dynamics CRM*</span></span>  | <span data-ttu-id="41571-128">Feed OData*</span><span class="sxs-lookup"><span data-stu-id="41571-128">OData Feed*</span></span>  | <span data-ttu-id="41571-129">SharePoint*</span><span class="sxs-lookup"><span data-stu-id="41571-129">SharePoint*</span></span>  |
| <span data-ttu-id="41571-130">Pasta de trabalho do Excel</span><span class="sxs-lookup"><span data-stu-id="41571-130">Excel workbook</span></span>  | <span data-ttu-id="41571-131">Consulta ODBC</span><span class="sxs-lookup"><span data-stu-id="41571-131">ODBC query</span></span>  | <span data-ttu-id="41571-132">Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="41571-132">SQL Database</span></span>  |
| <span data-ttu-id="41571-133">Exchange*</span><span class="sxs-lookup"><span data-stu-id="41571-133">Exchange*</span></span>  | <span data-ttu-id="41571-134">OLE DB</span><span class="sxs-lookup"><span data-stu-id="41571-134">OLE DB</span></span>  | <span data-ttu-id="41571-135">Banco de dados Sybase</span><span class="sxs-lookup"><span data-stu-id="41571-135">Sybase Database</span></span>  |

<span data-ttu-id="41571-136">\*Somente modelos Tabular 1400.</span><span class="sxs-lookup"><span data-stu-id="41571-136">\* Tabular 1400 models only.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="41571-137">A conexão com fontes de dados locais exige um [gateway de dados local](analysis-services-gateway.md) instalado em um computador em seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="41571-137">Connecting to on-premises data sources require an [On-premises data gateway](analysis-services-gateway.md) installed on a computer in your environment.</span></span>

## <a name="data-providers"></a><span data-ttu-id="41571-138">Provedores de dados</span><span class="sxs-lookup"><span data-stu-id="41571-138">Data providers</span></span>

<span data-ttu-id="41571-139">Os modelos de dados no Azure Analysis Services podem exigir diferentes provedores de dados durante a conexão com certas fontes de dados.</span><span class="sxs-lookup"><span data-stu-id="41571-139">Data models in Azure Analysis Services may require different data providers when connecting to certain data sources.</span></span> <span data-ttu-id="41571-140">Em alguns casos, modelos de tabela que se conectam a fontes de dados usando provedores nativos, como o SQL Server Native Client (SQLNCLI11), podem retornar um erro.</span><span class="sxs-lookup"><span data-stu-id="41571-140">In some cases, tabular models connecting to data sources using native providers such as SQL Server Native Client (SQLNCLI11) may return an error.</span></span>

<span data-ttu-id="41571-141">Para modelos de dados que se conectam a uma fonte de dados de nuvem, como o Banco de Dados SQL do Azure, se você usar provedores nativos diferentes de SQLOLEDB, verá a mensagem de erro: **"O provedor 'SQLNCLI11.1' não está registrado"**.</span><span class="sxs-lookup"><span data-stu-id="41571-141">For data models that connect to a cloud data source such as Azure SQL Database, if you use native providers other than SQLOLEDB, you may see error message: **“The provider 'SQLNCLI11.1' is not registered.”**</span></span> <span data-ttu-id="41571-142">Ou, se você tiver um modelo DirectQuery que se conecta a fontes de dados locais, se você usar provedores nativos, verá a mensagem de erro: **"Erro ao criar o conjunto de linhas do OLE DB. Sintaxe incorreta próxima a 'LIMIT' "**.</span><span class="sxs-lookup"><span data-stu-id="41571-142">Or, if you have a DirectQuery model connecting to on-premises data sources, if you use native providers you may see error message: **“Error creating OLE DB row set. Incorrect syntax near 'LIMIT'”**.</span></span>

<span data-ttu-id="41571-143">Os provedores de fonte de dados a seguir têm suporte para modelos de dados na memória ou DirectQuery ao se conectar a fontes de dados da nuvem ou locais:</span><span class="sxs-lookup"><span data-stu-id="41571-143">The following datasource providers are supported for in-memory or DirectQuery data models when connecting to data sources in the cloud or on-premises:</span></span>

### <a name="cloud"></a><span data-ttu-id="41571-144">Nuvem</span><span class="sxs-lookup"><span data-stu-id="41571-144">Cloud</span></span>
| <span data-ttu-id="41571-145">**Fonte de dados**</span><span class="sxs-lookup"><span data-stu-id="41571-145">**Datasource**</span></span> | <span data-ttu-id="41571-146">**Na memória**</span><span class="sxs-lookup"><span data-stu-id="41571-146">**In-memory**</span></span> | <span data-ttu-id="41571-147">**DirectQuery**</span><span class="sxs-lookup"><span data-stu-id="41571-147">**DirectQuery**</span></span> |
|  --- | --- | --- |
| <span data-ttu-id="41571-148">SQL Data Warehouse do Azure</span><span class="sxs-lookup"><span data-stu-id="41571-148">Azure SQL Data Warehouse</span></span> |<span data-ttu-id="41571-149">Provedor de Dados .NET Framework para SQL Server</span><span class="sxs-lookup"><span data-stu-id="41571-149">.NET Framework Data Provider for SQL Server</span></span> |<span data-ttu-id="41571-150">Provedor de Dados .NET Framework para SQL Server</span><span class="sxs-lookup"><span data-stu-id="41571-150">.NET Framework Data Provider for SQL Server</span></span> |
| <span data-ttu-id="41571-151">Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="41571-151">Azure SQL Database</span></span> |<span data-ttu-id="41571-152">Provedor de Dados .NET Framework para SQL Server</span><span class="sxs-lookup"><span data-stu-id="41571-152">.NET Framework Data Provider for SQL Server</span></span> |<span data-ttu-id="41571-153">Provedor de Dados .NET Framework para SQL Server</span><span class="sxs-lookup"><span data-stu-id="41571-153">.NET Framework Data Provider for SQL Server</span></span> | |

### <a name="on-premises-via-gateway"></a><span data-ttu-id="41571-154">Local (via Gateway)</span><span class="sxs-lookup"><span data-stu-id="41571-154">On-premises (via Gateway)</span></span>
|<span data-ttu-id="41571-155">**Fonte de dados**</span><span class="sxs-lookup"><span data-stu-id="41571-155">**Datasource**</span></span> | <span data-ttu-id="41571-156">**Na memória**</span><span class="sxs-lookup"><span data-stu-id="41571-156">**In-memory**</span></span> | <span data-ttu-id="41571-157">**DirectQuery**</span><span class="sxs-lookup"><span data-stu-id="41571-157">**DirectQuery**</span></span> |
|  --- | --- | --- |
| <span data-ttu-id="41571-158">SQL Server</span><span class="sxs-lookup"><span data-stu-id="41571-158">SQL Server</span></span> |<span data-ttu-id="41571-159">SQL Server Native Client 11.0</span><span class="sxs-lookup"><span data-stu-id="41571-159">SQL Server Native Client 11.0</span></span> |<span data-ttu-id="41571-160">Provedor de Dados .NET Framework para SQL Server</span><span class="sxs-lookup"><span data-stu-id="41571-160">.NET Framework Data Provider for SQL Server</span></span> |
| <span data-ttu-id="41571-161">SQL Server</span><span class="sxs-lookup"><span data-stu-id="41571-161">SQL Server</span></span> |<span data-ttu-id="41571-162">Provedor Microsoft OLE DB para SQL Server</span><span class="sxs-lookup"><span data-stu-id="41571-162">Microsoft OLE DB Provider for SQL Server</span></span> |<span data-ttu-id="41571-163">Provedor de Dados .NET Framework para SQL Server</span><span class="sxs-lookup"><span data-stu-id="41571-163">.NET Framework Data Provider for SQL Server</span></span> | |
| <span data-ttu-id="41571-164">SQL Server</span><span class="sxs-lookup"><span data-stu-id="41571-164">SQL Server</span></span> |<span data-ttu-id="41571-165">Provedor de Dados .NET Framework para SQL Server</span><span class="sxs-lookup"><span data-stu-id="41571-165">.NET Framework Data Provider for SQL Server</span></span> |<span data-ttu-id="41571-166">Provedor de Dados .NET Framework para SQL Server</span><span class="sxs-lookup"><span data-stu-id="41571-166">.NET Framework Data Provider for SQL Server</span></span> | |
| <span data-ttu-id="41571-167">Oracle</span><span class="sxs-lookup"><span data-stu-id="41571-167">Oracle</span></span> |<span data-ttu-id="41571-168">Provedor Microsoft OLE DB para Oracle</span><span class="sxs-lookup"><span data-stu-id="41571-168">Microsoft OLE DB Provider for Oracle</span></span> |<span data-ttu-id="41571-169">Provedor de Dados Oracle para .NET</span><span class="sxs-lookup"><span data-stu-id="41571-169">Oracle Data Provider for .NET</span></span> | |
| <span data-ttu-id="41571-170">Oracle</span><span class="sxs-lookup"><span data-stu-id="41571-170">Oracle</span></span> |<span data-ttu-id="41571-171">Provedor de Dados Oracle para .NET</span><span class="sxs-lookup"><span data-stu-id="41571-171">Oracle Data Provider for .NET</span></span> |<span data-ttu-id="41571-172">Provedor de Dados Oracle para .NET</span><span class="sxs-lookup"><span data-stu-id="41571-172">Oracle Data Provider for .NET</span></span> | |
| <span data-ttu-id="41571-173">Teradata</span><span class="sxs-lookup"><span data-stu-id="41571-173">Teradata</span></span> |<span data-ttu-id="41571-174">Provedor OLE DB para Teradata</span><span class="sxs-lookup"><span data-stu-id="41571-174">OLE DB Provider for Teradata</span></span> |<span data-ttu-id="41571-175">Provedor de Dados Teradata para .NET</span><span class="sxs-lookup"><span data-stu-id="41571-175">Teradata Data Provider for .NET</span></span> | |
| <span data-ttu-id="41571-176">Teradata</span><span class="sxs-lookup"><span data-stu-id="41571-176">Teradata</span></span> |<span data-ttu-id="41571-177">Provedor de Dados Teradata para .NET</span><span class="sxs-lookup"><span data-stu-id="41571-177">Teradata Data Provider for .NET</span></span> |<span data-ttu-id="41571-178">Provedor de Dados Teradata para .NET</span><span class="sxs-lookup"><span data-stu-id="41571-178">Teradata Data Provider for .NET</span></span> | |
| <span data-ttu-id="41571-179">Analytics Platform System</span><span class="sxs-lookup"><span data-stu-id="41571-179">Analytics Platform System</span></span> |<span data-ttu-id="41571-180">Provedor de Dados .NET Framework para SQL Server</span><span class="sxs-lookup"><span data-stu-id="41571-180">.NET Framework Data Provider for SQL Server</span></span> |<span data-ttu-id="41571-181">Provedor de Dados .NET Framework para SQL Server</span><span class="sxs-lookup"><span data-stu-id="41571-181">.NET Framework Data Provider for SQL Server</span></span> | |

> [!NOTE]
> <span data-ttu-id="41571-182">Certifique-se de que os provedores de 64 bits estejam instalados ao usar o gateway Local.</span><span class="sxs-lookup"><span data-stu-id="41571-182">Ensure 64-bit providers are installed when using On-premises gateway.</span></span>
> 
> 

<span data-ttu-id="41571-183">Ao migrar um modelo de tabela local do SQL Server Analysis Services para o Azure Analysis Services, talvez seja necessário alterar o provedor.</span><span class="sxs-lookup"><span data-stu-id="41571-183">When migrating an on-premises SQL Server Analysis Services tabular model to Azure Analysis Services, it may be necessary to change the provider.</span></span>

<span data-ttu-id="41571-184">**Para especificar um provedor de fonte de dados**</span><span class="sxs-lookup"><span data-stu-id="41571-184">**To specify a datasource provider**</span></span>

1. <span data-ttu-id="41571-185">No SSDT > **Gerenciador de Modelo de Tabela** > **Fontes de Dados**, clique com o botão direito em uma conexão de fonte de dados e, em seguida, clique em **Editar Fonte de Dados**.</span><span class="sxs-lookup"><span data-stu-id="41571-185">In SSDT > **Tabular Model Explorer** > **Data Sources**, right-click a data source connection, and then click **Edit Data Source**.</span></span>
2. <span data-ttu-id="41571-186">Em **Editar Conexão**, clique em **Avançado** para abrir a janela Propriedades avançadas.</span><span class="sxs-lookup"><span data-stu-id="41571-186">In **Edit Connection**, click **Advanced** to open the Advance properties window.</span></span>
3. <span data-ttu-id="41571-187">Em **Definir Propriedades Avançadas** > **Provedores**, selecione o provedor apropriado.</span><span class="sxs-lookup"><span data-stu-id="41571-187">In **Set Advanced Properties** > **Providers**, then select the appropriate provider.</span></span>

## <a name="impersonation"></a><span data-ttu-id="41571-188">Representação</span><span class="sxs-lookup"><span data-stu-id="41571-188">Impersonation</span></span>
<span data-ttu-id="41571-189">Em alguns casos, pode ser necessário especificar uma conta de representação diferente.</span><span class="sxs-lookup"><span data-stu-id="41571-189">In some cases, it may be necessary to specify a different impersonation account.</span></span> <span data-ttu-id="41571-190">A conta de representação pode ser especificada no SSDT ou o no SSMS.</span><span class="sxs-lookup"><span data-stu-id="41571-190">Impersonation account can be specified in SSDT or SSMS.</span></span>

<span data-ttu-id="41571-191">Para fontes de dados locais:</span><span class="sxs-lookup"><span data-stu-id="41571-191">For on-premises data sources:</span></span>

* <span data-ttu-id="41571-192">Se estiver usando a autenticação SQL, a representação deverá ser a Conta de serviço.</span><span class="sxs-lookup"><span data-stu-id="41571-192">If using SQL authentication, impersonation should be Service Account.</span></span>
* <span data-ttu-id="41571-193">Se estiver usando a autenticação do Windows, defina o usuário/senha do Windows.</span><span class="sxs-lookup"><span data-stu-id="41571-193">If using Windows authentication, set Windows user/password.</span></span> <span data-ttu-id="41571-194">Para o SQL Server, há suporte para a autenticação do Windows com uma conta de representação específica apenas para modelos de dados na memória.</span><span class="sxs-lookup"><span data-stu-id="41571-194">For SQL Server, Windows authentication with a specific impersonation account is supported only for in-memory data models.</span></span>

<span data-ttu-id="41571-195">Para fontes de dados de nuvem:</span><span class="sxs-lookup"><span data-stu-id="41571-195">For cloud data sources:</span></span>

* <span data-ttu-id="41571-196">Se estiver usando a autenticação SQL, a representação deverá ser a Conta de serviço.</span><span class="sxs-lookup"><span data-stu-id="41571-196">If using SQL authentication, impersonation should be Service Account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="41571-197">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="41571-197">Next steps</span></span>
<span data-ttu-id="41571-198">Se você tiver fontes de dados locais, instale o [Gateway local](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="41571-198">If you have on-premises data sources, be sure to install the [On-premises gateway](analysis-services-gateway.md).</span></span>   
<span data-ttu-id="41571-199">Para saber mais sobre como gerenciar seu servidor no SSDT ou SSMS, consulte [Gerenciar seu servidor](analysis-services-manage.md).</span><span class="sxs-lookup"><span data-stu-id="41571-199">To learn more about managing your server in SSDT or SSMS, see [Manage your server](analysis-services-manage.md).</span></span>

