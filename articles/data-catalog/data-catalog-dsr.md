---
title: "fontes de dados aaaSupported no catálogo de dados do Azure | Microsoft Docs"
description: "Este artigo lista as especificações de saudação atualmente há suporte para fontes de dados."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: jstevens
editor: 
tags: 
ms.assetid: fd4345ca-2ed8-4c5e-9c4b-f954be2fc9f9
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 4bfcabf31bf9fd781c939a5026abc42a5407df32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="supported-data-sources-in-azure-data-catalog"></a><span data-ttu-id="35539-103">Fontes de dados com suporte no Catálogo de Dados do Azure</span><span class="sxs-lookup"><span data-stu-id="35539-103">Supported data sources in Azure Data Catalog</span></span>

<span data-ttu-id="35539-104">Você pode publicar metadados usando uma API pública ou um clique-uma vez a ferramenta de registro, ou inserindo manualmente informações diretamente de portal da web toohello Data Catalog do Azure.</span><span class="sxs-lookup"><span data-stu-id="35539-104">You can publish metadata by using a public API or a click-once registration tool, or by manually entering information directly toohello Azure Data Catalog web portal.</span></span> <span data-ttu-id="35539-105">Olá tabela a seguir resume todas as fontes de dados que são aceitos pelo catálogo de saudação hoje e hello recursos de publicação para cada um.</span><span class="sxs-lookup"><span data-stu-id="35539-105">hello following table summarizes all data sources that are supported by hello catalog today, and hello publishing capabilities for each.</span></span> <span data-ttu-id="35539-106">Também está listados Olá ferramentas de dados externos que pode iniciar cada fonte de dados de nossa experiência do portal "open-in".</span><span class="sxs-lookup"><span data-stu-id="35539-106">Also listed are hello external data tools that each data source can launch from our portal "open-in" experience.</span></span> <span data-ttu-id="35539-107">Olá segunda tabela contém uma especificação de mais técnica de cada propriedade de conexão de fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="35539-107">hello second table contains a more technical specification of each data-source connection property.</span></span>


## <a name="list-of-supported-data-sources"></a><span data-ttu-id="35539-108">Lista das fontes de dados com suporte</span><span class="sxs-lookup"><span data-stu-id="35539-108">List of supported data sources</span></span>

<table>
    <tr>
       <td><span data-ttu-id="35539-109"><b>Objeto da fonte de dados</b></span><span class="sxs-lookup"><span data-stu-id="35539-109"><b>Data source object</b></span></span></td>
       <td><span data-ttu-id="35539-110"><b>API</b></span><span class="sxs-lookup"><span data-stu-id="35539-110"><b>API</b></span></span></td>
       <td><span data-ttu-id="35539-111"><b>Entrada manual</b></span><span class="sxs-lookup"><span data-stu-id="35539-111"><b>Manual entry</b></span></span></td>
       <td><span data-ttu-id="35539-112"><b>Ferramenta de registro</b></span><span class="sxs-lookup"><span data-stu-id="35539-112"><b>Registration tool</b></span></span></td>
       <td><span data-ttu-id="35539-113"><b>Ferramentas abertas</b></span><span class="sxs-lookup"><span data-stu-id="35539-113"><b>Open-in tools</b></span></span></td>
       <td><span data-ttu-id="35539-114"><b>Observações</b></span><span class="sxs-lookup"><span data-stu-id="35539-114"><b>Notes</b></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-115">Diretório do Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="35539-115">Azure Data Lake Store directory</span></span></td>
      <td><span data-ttu-id="35539-116">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-116">✓</span></span></td>
      <td><span data-ttu-id="35539-117">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-117">✓</span></span></td>
      <td><span data-ttu-id="35539-118">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-118">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-119">Arquivo do Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="35539-119">Azure Data Lake Store file</span></span></td>
      <td><span data-ttu-id="35539-120">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-120">✓</span></span></td>
      <td><span data-ttu-id="35539-121">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-121">✓</span></span></td>
      <td><span data-ttu-id="35539-122">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-122">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-123">Armazenamento de Blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="35539-123">Azure Blob storage</span></span></td>
      <td><span data-ttu-id="35539-124">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-124">✓</span></span></td>
      <td><span data-ttu-id="35539-125">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-125">✓</span></span></td>
      <td><span data-ttu-id="35539-126">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-126">✓</span></span></td>
      <td><span data-ttu-id="35539-127"><font size=2>Power BI</font></span><span class="sxs-lookup"><span data-stu-id="35539-127"><font size=2>Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-128">Diretório de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="35539-128">Azure Storage directory</span></span></td>
      <td><span data-ttu-id="35539-129">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-129">✓</span></span></td>
      <td><span data-ttu-id="35539-130">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-130">✓</span></span></td>
      <td><span data-ttu-id="35539-131">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-131">✓</span></span></td>
      <td><span data-ttu-id="35539-132"><font size=2>Power BI</font></span><span class="sxs-lookup"><span data-stu-id="35539-132"><font size=2>Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-133">Tabela do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="35539-133">Azure Storage table</span></span></td>
      <td><span data-ttu-id="35539-134">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-134">✓</span></span></td>
      <td><span data-ttu-id="35539-135">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-135">✓</span></span></td>
      <td><span data-ttu-id="35539-136">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-136">✓</span></span></td>
      <td>
        <font size="2"></font>
      </td>
      <td>
        <font size="2"></font>
      </td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-137">Diretório do HDFS</span><span class="sxs-lookup"><span data-stu-id="35539-137">HDFS directory</span></span></td>
      <td><span data-ttu-id="35539-138">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-138">✓</span></span></td>
      <td><span data-ttu-id="35539-139">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-139">✓</span></span></td>
      <td><span data-ttu-id="35539-140">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-140">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-141">Arquivo do HDFS</span><span class="sxs-lookup"><span data-stu-id="35539-141">HDFS file</span></span></td>
      <td><span data-ttu-id="35539-142">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-142">✓</span></span></td>
      <td><span data-ttu-id="35539-143">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-143">✓</span></span></td>
      <td><span data-ttu-id="35539-144">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-144">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-145">Tabela do Hive</span><span class="sxs-lookup"><span data-stu-id="35539-145">Hive table</span></span></td>
      <td><span data-ttu-id="35539-146">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-146">✓</span></span></td>
      <td><span data-ttu-id="35539-147">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-147">✓</span></span></td>
      <td><span data-ttu-id="35539-148">✓</span><span class="sxs-lookup"><span data-stu-id="35539-148">✓</span></span></td>
      <td><span data-ttu-id="35539-149"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="35539-149"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-150">Exibição de Hive</span><span class="sxs-lookup"><span data-stu-id="35539-150">Hive view</span></span></td>
      <td><span data-ttu-id="35539-151">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-151">✓</span></span></td>
      <td><span data-ttu-id="35539-152">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-152">✓</span></span></td>
      <td><span data-ttu-id="35539-153">✓</span><span class="sxs-lookup"><span data-stu-id="35539-153">✓</span></span></td>
      <td><span data-ttu-id="35539-154"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="35539-154"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-155">Tabela do MySQL</span><span class="sxs-lookup"><span data-stu-id="35539-155">MySQL table</span></span></td>
      <td><span data-ttu-id="35539-156">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-156">✓</span></span></td>
      <td><span data-ttu-id="35539-157">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-157">✓</span></span></td>
      <td><span data-ttu-id="35539-158">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-158">✓</span></span></td>
      <td><span data-ttu-id="35539-159"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="35539-159"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-160">Exibição do MySQL</span><span class="sxs-lookup"><span data-stu-id="35539-160">MySQL view</span></span></td>
      <td><span data-ttu-id="35539-161">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-161">✓</span></span></td>
      <td><span data-ttu-id="35539-162">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-162">✓</span></span></td>
      <td><span data-ttu-id="35539-163">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-163">✓</span></span></td>
      <td><span data-ttu-id="35539-164"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="35539-164"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-165">Tabela do Oracle Database</span><span class="sxs-lookup"><span data-stu-id="35539-165">Oracle Database table</span></span></td>
      <td><span data-ttu-id="35539-166">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-166">✓</span></span></td>
      <td><span data-ttu-id="35539-167">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-167">✓</span></span></td>
      <td><span data-ttu-id="35539-168">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-168">✓</span></span></td>
      <td><span data-ttu-id="35539-169"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="35539-169"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-170">Exibição do Oracle Database</span><span class="sxs-lookup"><span data-stu-id="35539-170">Oracle Database view</span></span></td>
      <td><span data-ttu-id="35539-171">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-171">✓</span></span></td>
      <td><span data-ttu-id="35539-172">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-172">✓</span></span></td>
      <td><span data-ttu-id="35539-173">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-173">✓</span></span></td>
      <td><span data-ttu-id="35539-174"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="35539-174"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-175">Outros (ativo genérico)</span><span class="sxs-lookup"><span data-stu-id="35539-175">Other (generic asset)</span></span></td>
      <td><span data-ttu-id="35539-176">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-176">✓</span></span></td>
      <td><span data-ttu-id="35539-177">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-177">✓</span></span></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-178">Tabela do SQL Data Warehouse do Azure</span><span class="sxs-lookup"><span data-stu-id="35539-178">Azure SQL Data Warehouse table</span></span></td>
      <td><span data-ttu-id="35539-179">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-179">✓</span></span></td>
      <td><span data-ttu-id="35539-180">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-180">✓</span></span></td>
      <td><span data-ttu-id="35539-181">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-181">✓</span></span></td>
      <td><span data-ttu-id="35539-182"><font size=2>Excel, Power BI, SQL Server Data Tools</font></span><span class="sxs-lookup"><span data-stu-id="35539-182"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-183">Exibição do SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="35539-183">SQL Data Warehouse view</span></span></td>
      <td><span data-ttu-id="35539-184">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-184">✓</span></span></td>
      <td><span data-ttu-id="35539-185">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-185">✓</span></span></td>
      <td><span data-ttu-id="35539-186">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-186">✓</span></span></td>
      <td><span data-ttu-id="35539-187"><font size=2>Excel, Power BI, SQL Server Data Tools</font></span><span class="sxs-lookup"><span data-stu-id="35539-187"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-188">Dimensão do SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="35539-188">SQL Server Analysis Services dimension</span></span></td>
      <td><span data-ttu-id="35539-189">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-189">✓</span></span></td>
      <td><span data-ttu-id="35539-190">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-190">✓</span></span></td>
      <td><span data-ttu-id="35539-191">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-191">✓</span></span></td>
      <td><span data-ttu-id="35539-192"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="35539-192"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-193">KPI do SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="35539-193">SQL Server Analysis Services KPI</span></span></td>
      <td><span data-ttu-id="35539-194">✓</span><span class="sxs-lookup"><span data-stu-id="35539-194">✓</span></span></td>
      <td><span data-ttu-id="35539-195">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-195">✓</span></span></td>
      <td><span data-ttu-id="35539-196">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-196">✓</span></span></td>
      <td><span data-ttu-id="35539-197"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="35539-197"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-198">Medida do SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="35539-198">SQL Server Analysis Services measure</span></span></td>
      <td><span data-ttu-id="35539-199">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-199">✓</span></span></td>
      <td><span data-ttu-id="35539-200">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-200">✓</span></span></td>
      <td><span data-ttu-id="35539-201">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-201">✓</span></span></td>
      <td><span data-ttu-id="35539-202"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="35539-202"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-203">Tabela do SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="35539-203">SQL Server Analysis Services table</span></span></td>
      <td><span data-ttu-id="35539-204">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-204">✓</span></span></td>
      <td><span data-ttu-id="35539-205">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-205">✓</span></span></td>
      <td><span data-ttu-id="35539-206">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-206">✓</span></span></td>
      <td><span data-ttu-id="35539-207"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="35539-207"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-208">Relatório do SQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="35539-208">SQL Server Reporting Services report</span></span></td>
      <td><span data-ttu-id="35539-209">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-209">✓</span></span></td>
      <td><span data-ttu-id="35539-210">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-210">✓</span></span></td>
      <td><span data-ttu-id="35539-211">✓</span><span class="sxs-lookup"><span data-stu-id="35539-211">✓</span></span></td>
      <td><span data-ttu-id="35539-212"><font size=2>Navegador</font></span><span class="sxs-lookup"><span data-stu-id="35539-212"><font size=2>Browser</font></span></span></td>
      <td><span data-ttu-id="35539-213"><font size=2>Somente os servidores de modo nativo. Não há suporte para o modo do SharePoint.</font></span><span class="sxs-lookup"><span data-stu-id="35539-213"><font size=2>Native mode servers only. SharePoint mode is not supported.</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-214">Tabela do SQL Server</span><span class="sxs-lookup"><span data-stu-id="35539-214">SQL Server table</span></span></td>
      <td><span data-ttu-id="35539-215">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-215">✓</span></span></td>
      <td><span data-ttu-id="35539-216">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-216">✓</span></span></td>
      <td><span data-ttu-id="35539-217">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-217">✓</span></span></td>
      <td><span data-ttu-id="35539-218"><font size=2>Excel, Power BI, SQL Server Data Tools</font></span><span class="sxs-lookup"><span data-stu-id="35539-218"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-219">Exibição do SQL Server</span><span class="sxs-lookup"><span data-stu-id="35539-219">SQL Server view</span></span></td>
      <td><span data-ttu-id="35539-220">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-220">✓</span></span></td>
      <td><span data-ttu-id="35539-221">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-221">✓</span></span></td>
      <td><span data-ttu-id="35539-222">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-222">✓</span></span></td>
      <td><span data-ttu-id="35539-223"><font size=2>Excel, Power BI, SQL Server Data Tools</font></span><span class="sxs-lookup"><span data-stu-id="35539-223"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-224">Tabela do Teradata</span><span class="sxs-lookup"><span data-stu-id="35539-224">Teradata table</span></span></td>
      <td><span data-ttu-id="35539-225">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-225">✓</span></span></td>
      <td><span data-ttu-id="35539-226">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-226">✓</span></span></td>
      <td><span data-ttu-id="35539-227">✓</span><span class="sxs-lookup"><span data-stu-id="35539-227">✓</span></span></td>
      <td><span data-ttu-id="35539-228"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="35539-228"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-229">Exibição do Teradata</span><span class="sxs-lookup"><span data-stu-id="35539-229">Teradata view</span></span></td>
      <td><span data-ttu-id="35539-230">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-230">✓</span></span></td>
      <td><span data-ttu-id="35539-231">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-231">✓</span></span></td>
      <td><span data-ttu-id="35539-232">✓</span><span class="sxs-lookup"><span data-stu-id="35539-232">✓</span></span></td>
      <td><span data-ttu-id="35539-233"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="35539-233"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-234">Exibição do SAP HANA</span><span class="sxs-lookup"><span data-stu-id="35539-234">SAP HANA view</span></span></td>
      <td><span data-ttu-id="35539-235">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-235">✓</span></span></td>
      <td><span data-ttu-id="35539-236">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-236">✓</span></span></td>
      <td><span data-ttu-id="35539-237">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-237">✓</span></span></td>
      <td><span data-ttu-id="35539-238"><font size=2>Power BI</font></span><span class="sxs-lookup"><span data-stu-id="35539-238"><font size=2>Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-239">Tabela do DB2</span><span class="sxs-lookup"><span data-stu-id="35539-239">DB2 table</span></span></td>
      <td><span data-ttu-id="35539-240">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-240">✓</span></span></td>
      <td><span data-ttu-id="35539-241">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-241">✓</span></span></td>
      <td><span data-ttu-id="35539-242">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-242">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-243">Exibição do DB2</span><span class="sxs-lookup"><span data-stu-id="35539-243">DB2 view</span></span></td>
      <td><span data-ttu-id="35539-244">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-244">✓</span></span></td>
      <td><span data-ttu-id="35539-245">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-245">✓</span></span></td>
      <td><span data-ttu-id="35539-246">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-246">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-247">Arquivo do sistema de arquivos</span><span class="sxs-lookup"><span data-stu-id="35539-247">File system file</span></span></td>
      <td><span data-ttu-id="35539-248">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-248">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-249">Diretório do FTP</span><span class="sxs-lookup"><span data-stu-id="35539-249">FTP directory</span></span></td>
      <td><span data-ttu-id="35539-250">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-250">✓</span></span></td>
      <td><span data-ttu-id="35539-251">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-251">✓</span></span></td>
      <td><span data-ttu-id="35539-252">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-252">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-253">Arquivo do FTP</span><span class="sxs-lookup"><span data-stu-id="35539-253">FTP file</span></span></td>
      <td><span data-ttu-id="35539-254">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-254">✓</span></span></td>
      <td><span data-ttu-id="35539-255">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-255">✓</span></span></td>
      <td><span data-ttu-id="35539-256">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-256">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-257">Relatório HTTP</span><span class="sxs-lookup"><span data-stu-id="35539-257">HTTP report</span></span></td>
      <td><span data-ttu-id="35539-258">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-258">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-259">Ponto de extremidade HTTP</span><span class="sxs-lookup"><span data-stu-id="35539-259">HTTP endpoint</span></span></td>
      <td><span data-ttu-id="35539-260">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-260">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-261">Arquivo HTTP</span><span class="sxs-lookup"><span data-stu-id="35539-261">HTTP file</span></span></td>
      <td><span data-ttu-id="35539-262">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-262">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-263">Conjunto de entidades do OData</span><span class="sxs-lookup"><span data-stu-id="35539-263">OData entity set</span></span></td>
      <td><span data-ttu-id="35539-264">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-264">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-265">Função do OData</span><span class="sxs-lookup"><span data-stu-id="35539-265">OData function</span></span></td>
      <td><span data-ttu-id="35539-266">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-266">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-267">Tabela do PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="35539-267">PostgreSQL table</span></span></td>
      <td><span data-ttu-id="35539-268">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-268">✓</span></span></td>
      <td><span data-ttu-id="35539-269">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-269">✓</span></span></td>
      <td><span data-ttu-id="35539-270">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-270">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-271">Exibição do PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="35539-271">PostgreSQL view</span></span></td>
      <td><span data-ttu-id="35539-272">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-272">✓</span></span></td>
      <td><span data-ttu-id="35539-273">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-273">✓</span></span></td>
      <td><span data-ttu-id="35539-274">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-274">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-275">Exibição do SAP HANA</span><span class="sxs-lookup"><span data-stu-id="35539-275">SAP HANA view</span></span></td>
      <td><span data-ttu-id="35539-276">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-276">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td> <span data-ttu-id="35539-277">Objeto do SalesForce</span><span class="sxs-lookup"><span data-stu-id="35539-277">Salesforce object</span></span></td>
      <td><span data-ttu-id="35539-278">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-278">✓</span></span></td>
      <td><span data-ttu-id="35539-279">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-279">✓</span></span></td>
      <td><span data-ttu-id="35539-280">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-280">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-281">Lista do SharePoint</span><span class="sxs-lookup"><span data-stu-id="35539-281">SharePoint list</span></span> </td>
      <td><span data-ttu-id="35539-282">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-282">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-283">Coleção do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="35539-283">Azure Cosmos DB collection</span></span></td>
      <td><span data-ttu-id="35539-284">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-284">✓</span></span></td>
      <td><span data-ttu-id="35539-285">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-285">✓</span></span></td>
      <td><span data-ttu-id="35539-286">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-286">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-287">Tabela ODBC Genérica</span><span class="sxs-lookup"><span data-stu-id="35539-287">Generic ODBC table</span></span></td>
      <td><span data-ttu-id="35539-288">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-288">✓</span></span></td>
      <td><span data-ttu-id="35539-289">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-289">✓</span></span></td>
      <td><span data-ttu-id="35539-290">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-290">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-291">Exibição ODBC Genérica</span><span class="sxs-lookup"><span data-stu-id="35539-291">Generic ODBC view</span></span></td>
      <td><span data-ttu-id="35539-292">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-292">✓</span></span></td>
      <td><span data-ttu-id="35539-293">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-293">✓</span></span></td>
      <td><span data-ttu-id="35539-294">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-294">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-295">Tabela do Cassandra</span><span class="sxs-lookup"><span data-stu-id="35539-295">Cassandra table</span></span></td>
      <td><span data-ttu-id="35539-296">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-296">✓</span></span></td>
      <td><span data-ttu-id="35539-297">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-297">✓</span></span></td>
      <td><span data-ttu-id="35539-298">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-298">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="35539-299"><font size=2>Publicar como um ativo ODBC genérico</font></span><span class="sxs-lookup"><span data-stu-id="35539-299"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-300">Exibição do Cassandra</span><span class="sxs-lookup"><span data-stu-id="35539-300">Cassandra view</span></span></td>
      <td><span data-ttu-id="35539-301">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-301">✓</span></span></td>
      <td><span data-ttu-id="35539-302">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-302">✓</span></span></td>
      <td><span data-ttu-id="35539-303">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-303">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="35539-304"><font size=2>Publicar como um ativo ODBC genérico</font></span><span class="sxs-lookup"><span data-stu-id="35539-304"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-305">Tabela do Sybase</span><span class="sxs-lookup"><span data-stu-id="35539-305">Sybase table</span></span></td>
      <td><span data-ttu-id="35539-306">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-306">✓</span></span></td>
      <td><span data-ttu-id="35539-307">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-307">✓</span></span></td>
      <td><span data-ttu-id="35539-308">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-308">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-309">Exibição do Sybase</span><span class="sxs-lookup"><span data-stu-id="35539-309">Sybase view</span></span></td>
      <td><span data-ttu-id="35539-310">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-310">✓</span></span></td>
      <td><span data-ttu-id="35539-311">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-311">✓</span></span></td>
      <td><span data-ttu-id="35539-312">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-312">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-313">Tabela do MongoDB</span><span class="sxs-lookup"><span data-stu-id="35539-313">MongoDB table</span></span></td>
      <td><span data-ttu-id="35539-314">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-314">✓</span></span></td>
      <td><span data-ttu-id="35539-315">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-315">✓</span></span></td>
      <td><span data-ttu-id="35539-316">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-316">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="35539-317"><font size=2>Publicar como um ativo ODBC genérico</font></span><span class="sxs-lookup"><span data-stu-id="35539-317"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-318">Exibição do MongoDB</span><span class="sxs-lookup"><span data-stu-id="35539-318">MongoDB view</span></span></td>
      <td><span data-ttu-id="35539-319">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-319">✓</span></span></td>
      <td><span data-ttu-id="35539-320">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-320">✓</span></span></td>
      <td><span data-ttu-id="35539-321">✓ </span><span class="sxs-lookup"><span data-stu-id="35539-321">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="35539-322"><font size=2>Publicar como um ativo ODBC genérico</font></span><span class="sxs-lookup"><span data-stu-id="35539-322"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
</table>

<span data-ttu-id="35539-323">Se você precisar de suporte para outras fontes, enviar um toohello de solicitação de recurso [Fórum do catálogo de dados do Azure](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="35539-323">If you need support for additional sources, submit a feature request toohello [Azure Data Catalog forum](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).</span></span>


## <a name="data-source-reference-specification"></a><span data-ttu-id="35539-324">Especificação de referência da fonte de dados</span><span class="sxs-lookup"><span data-stu-id="35539-324">Data-source reference specification</span></span>
> [!NOTE]
> <span data-ttu-id="35539-325">Olá **estrutura DSL** coluna Olá a tabela a seguir relaciona apenas Olá conexão as propriedades para o recipiente de propriedades "address" que são usadas pelo catálogo de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="35539-325">hello **DSL structure** column in hello following table lists only hello connection properties for "address" property bag that are used by Azure Data Catalog.</span></span> <span data-ttu-id="35539-326">Ou seja, o recipiente de propriedades de "address" pode conter outras propriedades de conexão da fonte de dados de saudação que persiste Data Catalog do Azure, mas não usa.</span><span class="sxs-lookup"><span data-stu-id="35539-326">That is, "address" property bag can contain other connection properties of hello data source which Azure Data Catalog persists, but does not use.</span></span>

<table>
    <tr>
       <td><span data-ttu-id="35539-327"><b>Tipo de fonte</b></span><span class="sxs-lookup"><span data-stu-id="35539-327"><b>Source type</b></span></span></td>
       <td><span data-ttu-id="35539-328"><b>Tipo de ativo</b></span><span class="sxs-lookup"><span data-stu-id="35539-328"><b>Asset type</b></span></span></td>
       <td><span data-ttu-id="35539-329"><b>Tipos de objeto</b></span><span class="sxs-lookup"><span data-stu-id="35539-329"><b>Object types</b></span></span></td>
       <td><span data-ttu-id="35539-330"><b>Estrutura de DSL<b></span><span class="sxs-lookup"><span data-stu-id="35539-330"><b>DSL structure<b></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-331">Repositório Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="35539-331">Azure Data Lake Store</span></span></td>
      <td><span data-ttu-id="35539-332">Contêiner</span><span class="sxs-lookup"><span data-stu-id="35539-332">Container</span></span></td>
      <td><span data-ttu-id="35539-333">Data Lake</span><span class="sxs-lookup"><span data-stu-id="35539-333">Data Lake</span></span></td>
      <td><span data-ttu-id="35539-334">
        <font size=2> Protocolo: webhdfs</span><span class="sxs-lookup"><span data-stu-id="35539-334">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="35539-335">Autenticação: {básica, oauth}</span><span class="sxs-lookup"><span data-stu-id="35539-335">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="35539-336">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-336">Address:</span></span> <br><span data-ttu-id="35539-337">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-337">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-338">Repositório Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="35539-338">Azure Data Lake Store</span></span></td>
      <td><span data-ttu-id="35539-339">Tabela</span><span class="sxs-lookup"><span data-stu-id="35539-339">Table</span></span></td>
      <td><span data-ttu-id="35539-340">Diretório, arquivo</span><span class="sxs-lookup"><span data-stu-id="35539-340">Directory, file</span></span></td>
      <td><span data-ttu-id="35539-341">
        <font size=2> Protocolo: webhdfs</span><span class="sxs-lookup"><span data-stu-id="35539-341">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="35539-342">Autenticação: {básica, oauth}</span><span class="sxs-lookup"><span data-stu-id="35539-342">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="35539-343">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-343">Address:</span></span> <br><span data-ttu-id="35539-344">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-344">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-345">Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="35539-345">Azure Storage</span></span></td>
      <td><span data-ttu-id="35539-346">Contêiner</span><span class="sxs-lookup"><span data-stu-id="35539-346">Container</span></span></td>
      <td><span data-ttu-id="35539-347">Contêiner</span><span class="sxs-lookup"><span data-stu-id="35539-347">Container</span></span></td>
      <td><span data-ttu-id="35539-348">
        <font size=2> Protocolo: azure-blobs</span><span class="sxs-lookup"><span data-stu-id="35539-348">
        <font size=2> Protocol: azure-blobs</span></span> <br><span data-ttu-id="35539-349">Autenticação: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="35539-349">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="35539-350">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-350">Address:</span></span> <br><span data-ttu-id="35539-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domínio</span><span class="sxs-lookup"><span data-stu-id="35539-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="35539-352">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; conta</span><span class="sxs-lookup"><span data-stu-id="35539-352">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span></span> <br><span data-ttu-id="35539-353">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; contêiner </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-353">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; container </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-354">Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="35539-354">Azure Storage</span></span></td>
      <td><span data-ttu-id="35539-355">Tabela</span><span class="sxs-lookup"><span data-stu-id="35539-355">Table</span></span></td>
      <td><span data-ttu-id="35539-356">Blob, diretório</span><span class="sxs-lookup"><span data-stu-id="35539-356">Blob, directory</span></span></td>
      <td><span data-ttu-id="35539-357">
        <font size=2> Protocolo: azure-blobs</span><span class="sxs-lookup"><span data-stu-id="35539-357">
        <font size=2> Protocol: azure-blobs</span></span> <br><span data-ttu-id="35539-358">Autenticação: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="35539-358">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="35539-359">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-359">Address:</span></span> <br><span data-ttu-id="35539-360">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domínio</span><span class="sxs-lookup"><span data-stu-id="35539-360">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="35539-361">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; conta</span><span class="sxs-lookup"><span data-stu-id="35539-361">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span></span> <br><span data-ttu-id="35539-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; contêiner</span><span class="sxs-lookup"><span data-stu-id="35539-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; container</span></span> <br><span data-ttu-id="35539-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; nome </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; name </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-364">Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="35539-364">Azure Storage</span></span></td>
      <td><span data-ttu-id="35539-365">Contêiner</span><span class="sxs-lookup"><span data-stu-id="35539-365">Container</span></span></td>
      <td><span data-ttu-id="35539-366">Contêiner</span><span class="sxs-lookup"><span data-stu-id="35539-366">Container</span></span></td>
      <td><span data-ttu-id="35539-367">
        <font size=2> Protocolo: azure-tables</span><span class="sxs-lookup"><span data-stu-id="35539-367">
        <font size=2> Protocol: azure-tables</span></span> <br><span data-ttu-id="35539-368">Autenticação: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="35539-368">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="35539-369">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-369">Address:</span></span> <br><span data-ttu-id="35539-370">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domínio</span><span class="sxs-lookup"><span data-stu-id="35539-370">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="35539-371">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; conta </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-371">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-372">Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="35539-372">Azure Storage</span></span></td>
      <td><span data-ttu-id="35539-373">Tabela</span><span class="sxs-lookup"><span data-stu-id="35539-373">Table</span></span></td>
      <td><span data-ttu-id="35539-374">Tabela</span><span class="sxs-lookup"><span data-stu-id="35539-374">Table</span></span></td>
      <td><span data-ttu-id="35539-375">
        <font size=2> Protocolo: azure-tables</span><span class="sxs-lookup"><span data-stu-id="35539-375">
        <font size=2> Protocol: azure-tables</span></span> <br><span data-ttu-id="35539-376">Autenticação: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="35539-376">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="35539-377">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-377">Address:</span></span> <br><span data-ttu-id="35539-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domínio</span><span class="sxs-lookup"><span data-stu-id="35539-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="35539-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; conta</span><span class="sxs-lookup"><span data-stu-id="35539-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span></span> <br><span data-ttu-id="35539-380">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; nome </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-380">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; name </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-381">Cosmos</span><span class="sxs-lookup"><span data-stu-id="35539-381">Cosmos</span></span></td>
      <td><span data-ttu-id="35539-382">Contêiner</span><span class="sxs-lookup"><span data-stu-id="35539-382">Container</span></span></td>
      <td><span data-ttu-id="35539-383">Cluster virtual</span><span class="sxs-lookup"><span data-stu-id="35539-383">Virtual cluster</span></span></td>
      <td><span data-ttu-id="35539-384">
        <font size=2> Protocolo: cosmos</span><span class="sxs-lookup"><span data-stu-id="35539-384">
        <font size=2> Protocol: cosmos</span></span> <br><span data-ttu-id="35539-385">Autenticação: {básica, windows}</span><span class="sxs-lookup"><span data-stu-id="35539-385">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="35539-386">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-386">Address:</span></span> <br><span data-ttu-id="35539-387">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-387">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-388">Cosmos</span><span class="sxs-lookup"><span data-stu-id="35539-388">Cosmos</span></span></td>
      <td><span data-ttu-id="35539-389">Tabela</span><span class="sxs-lookup"><span data-stu-id="35539-389">Table</span></span></td>
      <td><span data-ttu-id="35539-390">Fluxo, conjunto de fluxos, exibição</span><span class="sxs-lookup"><span data-stu-id="35539-390">Stream, stream set, view</span></span></td>
      <td><span data-ttu-id="35539-391">
        <font size=2> Protocolo: cosmos</span><span class="sxs-lookup"><span data-stu-id="35539-391">
        <font size=2> Protocol: cosmos</span></span> <br><span data-ttu-id="35539-392">Autenticação: {básica, windows}</span><span class="sxs-lookup"><span data-stu-id="35539-392">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="35539-393">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-393">Address:</span></span> <br><span data-ttu-id="35539-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-395">Datazen</span><span class="sxs-lookup"><span data-stu-id="35539-395">Datazen</span></span></td>
      <td><span data-ttu-id="35539-396">Contêiner</span><span class="sxs-lookup"><span data-stu-id="35539-396">Container</span></span></td>
      <td><span data-ttu-id="35539-397">Site</span><span class="sxs-lookup"><span data-stu-id="35539-397">Site</span></span></td>
      <td><span data-ttu-id="35539-398">
        <font size=2> Protocolo: http</span><span class="sxs-lookup"><span data-stu-id="35539-398">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="35539-399">Autenticação: {nenhuma, básica, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="35539-399">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="35539-400">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-400">Address:</span></span> <br><span data-ttu-id="35539-401">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-401">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-402">Datazen</span><span class="sxs-lookup"><span data-stu-id="35539-402">Datazen</span></span></td>
      <td><span data-ttu-id="35539-403">Relatório</span><span class="sxs-lookup"><span data-stu-id="35539-403">Report</span></span></td>
      <td><span data-ttu-id="35539-404">Relatório, painel</span><span class="sxs-lookup"><span data-stu-id="35539-404">Report, dashboard</span></span></td>
      <td><span data-ttu-id="35539-405">
        <font size=2> Protocolo: http</span><span class="sxs-lookup"><span data-stu-id="35539-405">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="35539-406">Autenticação: {nenhuma, básica, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="35539-406">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="35539-407">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-407">Address:</span></span> <br><span data-ttu-id="35539-408">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-408">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-409">DB2</span><span class="sxs-lookup"><span data-stu-id="35539-409">DB2</span></span></td>
      <td><span data-ttu-id="35539-410">Contêiner</span><span class="sxs-lookup"><span data-stu-id="35539-410">Container</span></span></td>
      <td><span data-ttu-id="35539-411">Banco de dados</span><span class="sxs-lookup"><span data-stu-id="35539-411">Database</span></span></td>
      <td><span data-ttu-id="35539-412">
        <font size=2> Protocolo: db2</span><span class="sxs-lookup"><span data-stu-id="35539-412">
        <font size=2> Protocol: db2</span></span> <br><span data-ttu-id="35539-413">Autenticação: {básica, windows}</span><span class="sxs-lookup"><span data-stu-id="35539-413">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="35539-414">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-414">Address:</span></span> <br><span data-ttu-id="35539-415">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="35539-415">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="35539-416">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; banco de dados </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-416">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-417">DB2</span><span class="sxs-lookup"><span data-stu-id="35539-417">DB2</span></span></td>
      <td><span data-ttu-id="35539-418">Tabela</span><span class="sxs-lookup"><span data-stu-id="35539-418">Table</span></span></td>
      <td><span data-ttu-id="35539-419">Tabela, exibição</span><span class="sxs-lookup"><span data-stu-id="35539-419">Table, view</span></span></td>
      <td><span data-ttu-id="35539-420">
        <font size=2> Protocolo: db2</span><span class="sxs-lookup"><span data-stu-id="35539-420">
        <font size=2> Protocol: db2</span></span> <br><span data-ttu-id="35539-421">Autenticação: {básica, windows}</span><span class="sxs-lookup"><span data-stu-id="35539-421">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="35539-422">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-422">Address:</span></span> <br><span data-ttu-id="35539-423">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="35539-423">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="35539-424">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; banco de dados</span><span class="sxs-lookup"><span data-stu-id="35539-424">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="35539-425">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto</span><span class="sxs-lookup"><span data-stu-id="35539-425">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="35539-426">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; esquema </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-426">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-427">Sistema de arquivos</span><span class="sxs-lookup"><span data-stu-id="35539-427">File system</span></span></td>
      <td><span data-ttu-id="35539-428">Tabela</span><span class="sxs-lookup"><span data-stu-id="35539-428">Table</span></span></td>
      <td><span data-ttu-id="35539-429">Arquivo</span><span class="sxs-lookup"><span data-stu-id="35539-429">File</span></span></td>
      <td><span data-ttu-id="35539-430">
        <font size=2> Protocolo: file</span><span class="sxs-lookup"><span data-stu-id="35539-430">
        <font size=2> Protocol: file</span></span> <br><span data-ttu-id="35539-431">Autenticação: {nenhuma, básica, windows}</span><span class="sxs-lookup"><span data-stu-id="35539-431">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="35539-432">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-432">Address:</span></span> <br><span data-ttu-id="35539-433">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; caminho </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-433">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; path </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-434">FTP</span><span class="sxs-lookup"><span data-stu-id="35539-434">FTP</span></span></td>
      <td><span data-ttu-id="35539-435">Tabela</span><span class="sxs-lookup"><span data-stu-id="35539-435">Table</span></span></td>
      <td><span data-ttu-id="35539-436">Diretório, arquivo</span><span class="sxs-lookup"><span data-stu-id="35539-436">Directory, file</span></span></td>
      <td><span data-ttu-id="35539-437">
        <font size=2> Protocolo: ftp</span><span class="sxs-lookup"><span data-stu-id="35539-437">
        <font size=2> Protocol: ftp</span></span> <br><span data-ttu-id="35539-438">Autenticação: {nenhuma, básica, windows}</span><span class="sxs-lookup"><span data-stu-id="35539-438">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="35539-439">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-439">Address:</span></span> <br><span data-ttu-id="35539-440">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-440">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-441">Sistema de Arquivos Distribuído Hadoop</span><span class="sxs-lookup"><span data-stu-id="35539-441">Hadoop Distributed File System</span></span></td>
      <td><span data-ttu-id="35539-442">Contêiner</span><span class="sxs-lookup"><span data-stu-id="35539-442">Container</span></span></td>
      <td><span data-ttu-id="35539-443">HDInsight</span><span class="sxs-lookup"><span data-stu-id="35539-443">Cluster</span></span></td>
      <td><span data-ttu-id="35539-444">
        <font size=2> Protocolo: webhdfs</span><span class="sxs-lookup"><span data-stu-id="35539-444">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="35539-445">Autenticação: {básica, oauth}</span><span class="sxs-lookup"><span data-stu-id="35539-445">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="35539-446">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-446">Address:</span></span> <br><span data-ttu-id="35539-447">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-447">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-448">Sistema de Arquivos Distribuído Hadoop</span><span class="sxs-lookup"><span data-stu-id="35539-448">Hadoop Distributed File System</span></span></td>
      <td><span data-ttu-id="35539-449">Tabela</span><span class="sxs-lookup"><span data-stu-id="35539-449">Table</span></span></td>
      <td><span data-ttu-id="35539-450">Diretório, arquivo</span><span class="sxs-lookup"><span data-stu-id="35539-450">Directory, file</span></span></td>
      <td><span data-ttu-id="35539-451">
        <font size=2> Protocolo: webhdfs</span><span class="sxs-lookup"><span data-stu-id="35539-451">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="35539-452">Autenticação: {básica, oauth}</span><span class="sxs-lookup"><span data-stu-id="35539-452">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="35539-453">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-453">Address:</span></span> <br><span data-ttu-id="35539-454">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-454">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-455">Hive</span><span class="sxs-lookup"><span data-stu-id="35539-455">Hive</span></span></td>
      <td><span data-ttu-id="35539-456">Contêiner</span><span class="sxs-lookup"><span data-stu-id="35539-456">Container</span></span></td>
      <td><span data-ttu-id="35539-457">Banco de dados</span><span class="sxs-lookup"><span data-stu-id="35539-457">Database</span></span></td>
      <td><span data-ttu-id="35539-458">
        <font size=2> Protocolo: hive</span><span class="sxs-lookup"><span data-stu-id="35539-458">
        <font size=2> Protocol: hive</span></span> <br><span data-ttu-id="35539-459">Autenticação: {HDInsight, básica, nome de usuário, nenhuma}</span><span class="sxs-lookup"><span data-stu-id="35539-459">Authentication: {HDInsight, basic, username, none}</span></span> <br><span data-ttu-id="35539-460">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-460">Address:</span></span> <br><span data-ttu-id="35539-461">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="35539-461">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="35539-462">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; banco de dados</span><span class="sxs-lookup"><span data-stu-id="35539-462">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="35539-463">connectionProperties:</span><span class="sxs-lookup"><span data-stu-id="35539-463">connectionProperties:</span></span> <br><span data-ttu-id="35539-464">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-464">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-465">Hive</span><span class="sxs-lookup"><span data-stu-id="35539-465">Hive</span></span></td>
      <td><span data-ttu-id="35539-466">Tabela</span><span class="sxs-lookup"><span data-stu-id="35539-466">Table</span></span></td>
      <td><span data-ttu-id="35539-467">Tabela, exibição</span><span class="sxs-lookup"><span data-stu-id="35539-467">Table, view</span></span></td>
      <td><span data-ttu-id="35539-468">
        <font size=2> Protocolo: hive</span><span class="sxs-lookup"><span data-stu-id="35539-468">
        <font size=2> Protocol: hive</span></span> <br><span data-ttu-id="35539-469">Autenticação: {HDInsight, básica, nome de usuário, nenhuma}</span><span class="sxs-lookup"><span data-stu-id="35539-469">Authentication: {HDInsight, basic, username, none}</span></span> <br><span data-ttu-id="35539-470">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-470">Address:</span></span> <br><span data-ttu-id="35539-471">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="35539-471">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="35539-472">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; banco de dados</span><span class="sxs-lookup"><span data-stu-id="35539-472">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="35539-473">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto</span><span class="sxs-lookup"><span data-stu-id="35539-473">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="35539-474">connectionProperties:</span><span class="sxs-lookup"><span data-stu-id="35539-474">connectionProperties:</span></span> <br><span data-ttu-id="35539-475">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-475">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-476">HTTP</span><span class="sxs-lookup"><span data-stu-id="35539-476">HTTP</span></span></td>
      <td><span data-ttu-id="35539-477">Contêiner</span><span class="sxs-lookup"><span data-stu-id="35539-477">Container</span></span></td>
      <td><span data-ttu-id="35539-478">Site</span><span class="sxs-lookup"><span data-stu-id="35539-478">Site</span></span></td>
      <td><span data-ttu-id="35539-479">
        <font size=2> Protocolo: http</span><span class="sxs-lookup"><span data-stu-id="35539-479">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="35539-480">Autenticação: {nenhuma, básica, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="35539-480">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="35539-481">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-481">Address:</span></span> <br><span data-ttu-id="35539-482">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-482">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-483">HTTP</span><span class="sxs-lookup"><span data-stu-id="35539-483">HTTP</span></span></td>
      <td><span data-ttu-id="35539-484">Relatório</span><span class="sxs-lookup"><span data-stu-id="35539-484">Report</span></span></td>
      <td><span data-ttu-id="35539-485">Relatório, painel</span><span class="sxs-lookup"><span data-stu-id="35539-485">Report, dashboard</span></span></td>
      <td><span data-ttu-id="35539-486">
        <font size=2> Protocolo: http</span><span class="sxs-lookup"><span data-stu-id="35539-486">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="35539-487">Autenticação: {nenhuma, básica, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="35539-487">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="35539-488">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-488">Address:</span></span> <br><span data-ttu-id="35539-489">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-489">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-490">HTTP</span><span class="sxs-lookup"><span data-stu-id="35539-490">HTTP</span></span></td>
      <td><span data-ttu-id="35539-491">Tabela</span><span class="sxs-lookup"><span data-stu-id="35539-491">Table</span></span></td>
      <td><span data-ttu-id="35539-492">Ponto de extremidade, arquivo</span><span class="sxs-lookup"><span data-stu-id="35539-492">Endpoint, file</span></span></td>
      <td><span data-ttu-id="35539-493">
        <font size=2> Protocolo: http</span><span class="sxs-lookup"><span data-stu-id="35539-493">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="35539-494">Autenticação: {nenhuma, básica, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="35539-494">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="35539-495">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-495">Address:</span></span> <br><span data-ttu-id="35539-496">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-496">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-497">MySQL</span><span class="sxs-lookup"><span data-stu-id="35539-497">MySQL</span></span></td>
      <td><span data-ttu-id="35539-498">Contêiner</span><span class="sxs-lookup"><span data-stu-id="35539-498">Container</span></span></td>
      <td><span data-ttu-id="35539-499">Banco de dados</span><span class="sxs-lookup"><span data-stu-id="35539-499">Database</span></span></td>
      <td><span data-ttu-id="35539-500">
        <font size=2> Protocolo: mysql</span><span class="sxs-lookup"><span data-stu-id="35539-500">
        <font size=2> Protocol: mysql</span></span> <br><span data-ttu-id="35539-501">Autenticação: {protocolo, windows}</span><span class="sxs-lookup"><span data-stu-id="35539-501">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="35539-502">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-502">Address:</span></span> <br><span data-ttu-id="35539-503">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="35539-503">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="35539-504">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; banco de dados </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-504">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-505">MySQL</span><span class="sxs-lookup"><span data-stu-id="35539-505">MySQL</span></span></td>
      <td><span data-ttu-id="35539-506">Tabela</span><span class="sxs-lookup"><span data-stu-id="35539-506">Table</span></span></td>
      <td><span data-ttu-id="35539-507">Tabela, exibição</span><span class="sxs-lookup"><span data-stu-id="35539-507">Table, view</span></span></td>
      <td><span data-ttu-id="35539-508">
        <font size=2> Protocolo: mysql</span><span class="sxs-lookup"><span data-stu-id="35539-508">
        <font size=2> Protocol: mysql</span></span> <br><span data-ttu-id="35539-509">Autenticação: {protocolo, windows}</span><span class="sxs-lookup"><span data-stu-id="35539-509">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="35539-510">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-510">Address:</span></span> <br><span data-ttu-id="35539-511">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="35539-511">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="35539-512">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; banco de dados</span><span class="sxs-lookup"><span data-stu-id="35539-512">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="35539-513">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-513">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-514">OData</span><span class="sxs-lookup"><span data-stu-id="35539-514">OData</span></span></td>
      <td><span data-ttu-id="35539-515">Contêiner</span><span class="sxs-lookup"><span data-stu-id="35539-515">Container</span></span></td>
      <td><span data-ttu-id="35539-516">Contêiner de entidade</span><span class="sxs-lookup"><span data-stu-id="35539-516">Entity container</span></span></td>
      <td><span data-ttu-id="35539-517">
        <font size=2> Protocolo: odata</span><span class="sxs-lookup"><span data-stu-id="35539-517">
        <font size=2> Protocol: odata</span></span> <br><span data-ttu-id="35539-518">Autenticação: {nenhuma, básica, windows}</span><span class="sxs-lookup"><span data-stu-id="35539-518">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="35539-519">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-519">Address:</span></span> <br><span data-ttu-id="35539-520">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-520">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-521">OData</span><span class="sxs-lookup"><span data-stu-id="35539-521">OData</span></span></td>
      <td><span data-ttu-id="35539-522">Tabela</span><span class="sxs-lookup"><span data-stu-id="35539-522">Table</span></span></td>
      <td><span data-ttu-id="35539-523">Conjunto de entidades, função</span><span class="sxs-lookup"><span data-stu-id="35539-523">Entity set, function</span></span></td>
      <td><span data-ttu-id="35539-524">
        <font size=2> Protocolo: odata</span><span class="sxs-lookup"><span data-stu-id="35539-524">
        <font size=2> Protocol: odata</span></span> <br><span data-ttu-id="35539-525">Autenticação: {nenhuma, básica, windows}</span><span class="sxs-lookup"><span data-stu-id="35539-525">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="35539-526">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-526">Address:</span></span> <br><span data-ttu-id="35539-527">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="35539-527">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="35539-528">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; recurso </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-528">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; resource </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-529">Banco de dados Oracle</span><span class="sxs-lookup"><span data-stu-id="35539-529">Oracle Database</span></span></td>
      <td><span data-ttu-id="35539-530">Contêiner</span><span class="sxs-lookup"><span data-stu-id="35539-530">Container</span></span></td>
      <td><span data-ttu-id="35539-531">Banco de dados</span><span class="sxs-lookup"><span data-stu-id="35539-531">Database</span></span></td>
      <td><span data-ttu-id="35539-532">
        <font size=2> Protocolo: oracle</span><span class="sxs-lookup"><span data-stu-id="35539-532">
        <font size=2> Protocol: oracle</span></span> <br><span data-ttu-id="35539-533">Autenticação: {protocolo, windows}</span><span class="sxs-lookup"><span data-stu-id="35539-533">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="35539-534">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-534">Address:</span></span> <br><span data-ttu-id="35539-535">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="35539-535">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="35539-536">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; banco de dados </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-536">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-537">Banco de dados Oracle</span><span class="sxs-lookup"><span data-stu-id="35539-537">Oracle Database</span></span></td>
      <td><span data-ttu-id="35539-538">Tabela</span><span class="sxs-lookup"><span data-stu-id="35539-538">Table</span></span></td>
      <td><span data-ttu-id="35539-539">Tabela, exibição</span><span class="sxs-lookup"><span data-stu-id="35539-539">Table, view</span></span></td>
      <td><span data-ttu-id="35539-540">
        <font size=2> Protocolo: oracle</span><span class="sxs-lookup"><span data-stu-id="35539-540">
        <font size=2> Protocol: oracle</span></span> <br><span data-ttu-id="35539-541">Autenticação: {protocolo, windows}</span><span class="sxs-lookup"><span data-stu-id="35539-541">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="35539-542">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-542">Address:</span></span> <br><span data-ttu-id="35539-543">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="35539-543">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="35539-544">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; banco de dados</span><span class="sxs-lookup"><span data-stu-id="35539-544">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="35539-545">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; esquema</span><span class="sxs-lookup"><span data-stu-id="35539-545">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="35539-546">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-546">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-547">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="35539-547">PostgreSQL</span></span></td>
      <td><span data-ttu-id="35539-548">Contêiner</span><span class="sxs-lookup"><span data-stu-id="35539-548">Container</span></span></td>
      <td><span data-ttu-id="35539-549">Banco de dados</span><span class="sxs-lookup"><span data-stu-id="35539-549">Database</span></span></td>
      <td><span data-ttu-id="35539-550">
        <font size=2> Protocolo: postgresql</span><span class="sxs-lookup"><span data-stu-id="35539-550">
        <font size=2> Protocol: postgresql</span></span> <br><span data-ttu-id="35539-551">Autenticação: {básica, windows}</span><span class="sxs-lookup"><span data-stu-id="35539-551">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="35539-552">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-552">Address:</span></span> <br><span data-ttu-id="35539-553">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="35539-553">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="35539-554">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; banco de dados </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-554">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-555">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="35539-555">PostgreSQL</span></span></td>
      <td><span data-ttu-id="35539-556">Tabela</span><span class="sxs-lookup"><span data-stu-id="35539-556">Table</span></span></td>
      <td><span data-ttu-id="35539-557">Tabela, exibição</span><span class="sxs-lookup"><span data-stu-id="35539-557">Table, view</span></span></td>
      <td><span data-ttu-id="35539-558">
        <font size=2> Protocolo: postgresql</span><span class="sxs-lookup"><span data-stu-id="35539-558">
        <font size=2> Protocol: postgresql</span></span> <br><span data-ttu-id="35539-559">Autenticação: {básica, windows}</span><span class="sxs-lookup"><span data-stu-id="35539-559">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="35539-560">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-560">Address:</span></span> <br><span data-ttu-id="35539-561">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="35539-561">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="35539-562">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; banco de dados</span><span class="sxs-lookup"><span data-stu-id="35539-562">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="35539-563">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; esquema</span><span class="sxs-lookup"><span data-stu-id="35539-563">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="35539-564">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-564">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-565">Power BI</span><span class="sxs-lookup"><span data-stu-id="35539-565">Power BI</span></span></td>
      <td><span data-ttu-id="35539-566">Contêiner</span><span class="sxs-lookup"><span data-stu-id="35539-566">Container</span></span></td>
      <td><span data-ttu-id="35539-567">Site</span><span class="sxs-lookup"><span data-stu-id="35539-567">Site</span></span></td>
      <td><span data-ttu-id="35539-568">
        <font size=2> Protocolo: http</span><span class="sxs-lookup"><span data-stu-id="35539-568">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="35539-569">Autenticação: {nenhuma, básica, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="35539-569">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="35539-570">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-570">Address:</span></span> <br><span data-ttu-id="35539-571">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-571">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-572">Power BI</span><span class="sxs-lookup"><span data-stu-id="35539-572">Power BI</span></span></td>
      <td><span data-ttu-id="35539-573">Relatório</span><span class="sxs-lookup"><span data-stu-id="35539-573">Report</span></span></td>
      <td><span data-ttu-id="35539-574">Relatório, painel</span><span class="sxs-lookup"><span data-stu-id="35539-574">Report, dashboard</span></span></td>
      <td><span data-ttu-id="35539-575">
        <font size=2> Protocolo: http</span><span class="sxs-lookup"><span data-stu-id="35539-575">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="35539-576">Autenticação: {nenhuma, básica, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="35539-576">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="35539-577">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-577">Address:</span></span> <br><span data-ttu-id="35539-578">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-578">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-579">Power Query</span><span class="sxs-lookup"><span data-stu-id="35539-579">Power Query</span></span></td>
      <td><span data-ttu-id="35539-580">Tabela</span><span class="sxs-lookup"><span data-stu-id="35539-580">Table</span></span></td>
      <td><span data-ttu-id="35539-581">Mashup de dados</span><span class="sxs-lookup"><span data-stu-id="35539-581">Data mashup</span></span></td>
      <td><span data-ttu-id="35539-582">
        <font size=2> Protocolo: power-query</span><span class="sxs-lookup"><span data-stu-id="35539-582">
        <font size=2> Protocol: power-query</span></span> <br><span data-ttu-id="35539-583">Autenticação: {oauth}</span><span class="sxs-lookup"><span data-stu-id="35539-583">Authentication: {oauth}</span></span> <br><span data-ttu-id="35539-584">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-584">Address:</span></span> <br><span data-ttu-id="35539-585">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-585">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-586">Salesforce</span><span class="sxs-lookup"><span data-stu-id="35539-586">Salesforce</span></span></td>
      <td><span data-ttu-id="35539-587">Tabela</span><span class="sxs-lookup"><span data-stu-id="35539-587">Table</span></span></td>
      <td><span data-ttu-id="35539-588">Objeto</span><span class="sxs-lookup"><span data-stu-id="35539-588">Object</span></span></td>
      <td><span data-ttu-id="35539-589">
        <font size=2> Protocolo: salesforce-com</span><span class="sxs-lookup"><span data-stu-id="35539-589">
        <font size=2> Protocol: salesforce-com</span></span> <br><span data-ttu-id="35539-590">Autenticação: {básica, windows}</span><span class="sxs-lookup"><span data-stu-id="35539-590">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="35539-591">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-591">Address:</span></span> <br><span data-ttu-id="35539-592">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; loginServer</span><span class="sxs-lookup"><span data-stu-id="35539-592">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; loginServer</span></span> <br><span data-ttu-id="35539-593">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; classe</span><span class="sxs-lookup"><span data-stu-id="35539-593">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; class</span></span> <br><span data-ttu-id="35539-594">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; itemName </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-594">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; itemName </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-595">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="35539-595">SAP HANA</span></span></td>
      <td><span data-ttu-id="35539-596">Contêiner</span><span class="sxs-lookup"><span data-stu-id="35539-596">Container</span></span></td>
      <td><span data-ttu-id="35539-597">Servidor</span><span class="sxs-lookup"><span data-stu-id="35539-597">Server</span></span></td>
      <td><span data-ttu-id="35539-598">
        <font size=2> Protocolo: sap-hana-sql</span><span class="sxs-lookup"><span data-stu-id="35539-598">
        <font size=2> Protocol: sap-hana-sql</span></span> <br><span data-ttu-id="35539-599">Autenticação: {protocolo, windows}</span><span class="sxs-lookup"><span data-stu-id="35539-599">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="35539-600">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-600">Address:</span></span> <br><span data-ttu-id="35539-601">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-601">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-602">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="35539-602">SAP HANA</span></span></td>
      <td><span data-ttu-id="35539-603">Tabela</span><span class="sxs-lookup"><span data-stu-id="35539-603">Table</span></span></td>
      <td><span data-ttu-id="35539-604">Visualizar</span><span class="sxs-lookup"><span data-stu-id="35539-604">View</span></span></td>
      <td><span data-ttu-id="35539-605">
        <font size=2> Protocolo: sap-hana-sql</span><span class="sxs-lookup"><span data-stu-id="35539-605">
        <font size=2> Protocol: sap-hana-sql</span></span> <br><span data-ttu-id="35539-606">Autenticação: {protocolo, windows}</span><span class="sxs-lookup"><span data-stu-id="35539-606">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="35539-607">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-607">Address:</span></span> <br><span data-ttu-id="35539-608">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="35539-608">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="35539-609">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; esquema</span><span class="sxs-lookup"><span data-stu-id="35539-609">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="35539-610">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-610">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-611">SharePoint</span><span class="sxs-lookup"><span data-stu-id="35539-611">SharePoint</span></span></td>
      <td><span data-ttu-id="35539-612">Tabela</span><span class="sxs-lookup"><span data-stu-id="35539-612">Table</span></span></td>
      <td><span data-ttu-id="35539-613">Listar</span><span class="sxs-lookup"><span data-stu-id="35539-613">List</span></span></td>
      <td><span data-ttu-id="35539-614">
        <font size=2> Protocolo: sharepoint-list</span><span class="sxs-lookup"><span data-stu-id="35539-614">
        <font size=2> Protocol: sharepoint-list</span></span> <br><span data-ttu-id="35539-615">Autenticação: {básica, windows}</span><span class="sxs-lookup"><span data-stu-id="35539-615">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="35539-616">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-616">Address:</span></span> <br><span data-ttu-id="35539-617">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-617">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-618">SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="35539-618">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="35539-619">Command</span><span class="sxs-lookup"><span data-stu-id="35539-619">Command</span></span></td>
      <td><span data-ttu-id="35539-620">Procedimento armazenado</span><span class="sxs-lookup"><span data-stu-id="35539-620">Stored procedure</span></span></td>
      <td><span data-ttu-id="35539-621">
        <font size=2> Protocolo: tds</span><span class="sxs-lookup"><span data-stu-id="35539-621">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="35539-622">Autenticação: {protocolo, windows}</span><span class="sxs-lookup"><span data-stu-id="35539-622">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="35539-623">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-623">Address:</span></span> <br><span data-ttu-id="35539-624">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="35539-624">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="35539-625">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; banco de dados</span><span class="sxs-lookup"><span data-stu-id="35539-625">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="35539-626">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; esquema</span><span class="sxs-lookup"><span data-stu-id="35539-626">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="35539-627">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-627">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-628">SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="35539-628">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="35539-629">TableValuedFunction</span><span class="sxs-lookup"><span data-stu-id="35539-629">TableValuedFunction</span></span></td>
      <td><span data-ttu-id="35539-630">Função com valor de tabela</span><span class="sxs-lookup"><span data-stu-id="35539-630">Table-valued function</span></span></td>
      <td><span data-ttu-id="35539-631">
        <font size=2> Protocolo: tds</span><span class="sxs-lookup"><span data-stu-id="35539-631">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="35539-632">Autenticação: {protocolo, windows}</span><span class="sxs-lookup"><span data-stu-id="35539-632">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="35539-633">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-633">Address:</span></span> <br><span data-ttu-id="35539-634">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="35539-634">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="35539-635">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; banco de dados</span><span class="sxs-lookup"><span data-stu-id="35539-635">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="35539-636">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; esquema</span><span class="sxs-lookup"><span data-stu-id="35539-636">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="35539-637">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-637">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-638">SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="35539-638">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="35539-639">Contêiner</span><span class="sxs-lookup"><span data-stu-id="35539-639">Container</span></span></td>
      <td><span data-ttu-id="35539-640">Banco de dados</span><span class="sxs-lookup"><span data-stu-id="35539-640">Database</span></span></td>
      <td><span data-ttu-id="35539-641">
        <font size=2> Protocolo: tds</span><span class="sxs-lookup"><span data-stu-id="35539-641">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="35539-642">Autenticação: {protocolo, windows}</span><span class="sxs-lookup"><span data-stu-id="35539-642">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="35539-643">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-643">Address:</span></span> <br><span data-ttu-id="35539-644">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="35539-644">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="35539-645">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; banco de dados </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-645">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-646">SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="35539-646">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="35539-647">Tabela</span><span class="sxs-lookup"><span data-stu-id="35539-647">Table</span></span></td>
      <td><span data-ttu-id="35539-648">Tabela, exibição</span><span class="sxs-lookup"><span data-stu-id="35539-648">Table, view</span></span></td>
      <td><span data-ttu-id="35539-649">
        <font size=2> Protocolo: tds</span><span class="sxs-lookup"><span data-stu-id="35539-649">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="35539-650">Autenticação: {protocolo, windows}</span><span class="sxs-lookup"><span data-stu-id="35539-650">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="35539-651">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-651">Address:</span></span> <br><span data-ttu-id="35539-652">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="35539-652">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="35539-653">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; banco de dados</span><span class="sxs-lookup"><span data-stu-id="35539-653">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="35539-654">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; esquema</span><span class="sxs-lookup"><span data-stu-id="35539-654">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="35539-655">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-655">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-656">SQL Server</span><span class="sxs-lookup"><span data-stu-id="35539-656">SQL Server</span></span></td>
      <td><span data-ttu-id="35539-657">Command</span><span class="sxs-lookup"><span data-stu-id="35539-657">Command</span></span></td>
      <td><span data-ttu-id="35539-658">Procedimento armazenado</span><span class="sxs-lookup"><span data-stu-id="35539-658">Stored procedure</span></span></td>
      <td><span data-ttu-id="35539-659">
        <font size=2> Protocolo: tds</span><span class="sxs-lookup"><span data-stu-id="35539-659">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="35539-660">Autenticação: {protocolo, windows}</span><span class="sxs-lookup"><span data-stu-id="35539-660">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="35539-661">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-661">Address:</span></span> <br><span data-ttu-id="35539-662">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="35539-662">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="35539-663">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; banco de dados</span><span class="sxs-lookup"><span data-stu-id="35539-663">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="35539-664">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; esquema</span><span class="sxs-lookup"><span data-stu-id="35539-664">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="35539-665">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-665">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-666">SQL Server</span><span class="sxs-lookup"><span data-stu-id="35539-666">SQL Server</span></span></td>
      <td><span data-ttu-id="35539-667">TableValuedFunction</span><span class="sxs-lookup"><span data-stu-id="35539-667">TableValuedFunction</span></span></td>
      <td><span data-ttu-id="35539-668">Função com valor de tabela</span><span class="sxs-lookup"><span data-stu-id="35539-668">Table-valued function</span></span></td>
      <td><span data-ttu-id="35539-669">
        <font size=2> Protocolo: tds</span><span class="sxs-lookup"><span data-stu-id="35539-669">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="35539-670">Autenticação: {protocolo, windows}</span><span class="sxs-lookup"><span data-stu-id="35539-670">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="35539-671">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-671">Address:</span></span> <br><span data-ttu-id="35539-672">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="35539-672">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="35539-673">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; banco de dados</span><span class="sxs-lookup"><span data-stu-id="35539-673">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="35539-674">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; esquema</span><span class="sxs-lookup"><span data-stu-id="35539-674">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="35539-675">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-675">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-676">SQL Server</span><span class="sxs-lookup"><span data-stu-id="35539-676">SQL Server</span></span></td>
      <td><span data-ttu-id="35539-677">Contêiner</span><span class="sxs-lookup"><span data-stu-id="35539-677">Container</span></span></td>
      <td><span data-ttu-id="35539-678">Banco de dados</span><span class="sxs-lookup"><span data-stu-id="35539-678">Database</span></span></td>
      <td><span data-ttu-id="35539-679">
        <font size=2> Protocolo: tds</span><span class="sxs-lookup"><span data-stu-id="35539-679">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="35539-680">Autenticação: {protocolo, windows}</span><span class="sxs-lookup"><span data-stu-id="35539-680">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="35539-681">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-681">Address:</span></span> <br><span data-ttu-id="35539-682">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="35539-682">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="35539-683">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; banco de dados </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-683">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-684">SQL Server</span><span class="sxs-lookup"><span data-stu-id="35539-684">SQL Server</span></span></td>
      <td><span data-ttu-id="35539-685">Tabela</span><span class="sxs-lookup"><span data-stu-id="35539-685">Table</span></span></td>
      <td><span data-ttu-id="35539-686">Tabela, exibição</span><span class="sxs-lookup"><span data-stu-id="35539-686">Table, view</span></span></td>
      <td><span data-ttu-id="35539-687">
        <font size=2> Protocolo: tds</span><span class="sxs-lookup"><span data-stu-id="35539-687">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="35539-688">Autenticação: {protocolo, windows}</span><span class="sxs-lookup"><span data-stu-id="35539-688">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="35539-689">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-689">Address:</span></span> <br><span data-ttu-id="35539-690">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="35539-690">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="35539-691">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; banco de dados</span><span class="sxs-lookup"><span data-stu-id="35539-691">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="35539-692">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; esquema</span><span class="sxs-lookup"><span data-stu-id="35539-692">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="35539-693">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-693">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-694">Multidimensional do SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="35539-694">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="35539-695">Contêiner</span><span class="sxs-lookup"><span data-stu-id="35539-695">Container</span></span></td>
      <td><span data-ttu-id="35539-696">Modelo</span><span class="sxs-lookup"><span data-stu-id="35539-696">Model</span></span></td>
      <td><span data-ttu-id="35539-697">
        <font size=2> Protocolo: analysis-services</span><span class="sxs-lookup"><span data-stu-id="35539-697">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="35539-698">Autenticação: {windows, básica, anônima, nenhuma}</span><span class="sxs-lookup"><span data-stu-id="35539-698">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="35539-699">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-699">Address:</span></span> <br><span data-ttu-id="35539-700">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="35539-700">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="35539-701">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; banco de dados</span><span class="sxs-lookup"><span data-stu-id="35539-701">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="35539-702">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modelo </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-702">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-703">Multidimensional do SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="35539-703">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="35539-704">KPI</span><span class="sxs-lookup"><span data-stu-id="35539-704">KPI</span></span></td>
      <td><span data-ttu-id="35539-705">KPI</span><span class="sxs-lookup"><span data-stu-id="35539-705">KPI</span></span></td>
      <td><span data-ttu-id="35539-706">
        <font size=2> Protocolo: analysis-services</span><span class="sxs-lookup"><span data-stu-id="35539-706">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="35539-707">Autenticação: {windows, básica, anônima, nenhuma}</span><span class="sxs-lookup"><span data-stu-id="35539-707">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="35539-708">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-708">Address:</span></span> <br><span data-ttu-id="35539-709">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="35539-709">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="35539-710">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; banco de dados</span><span class="sxs-lookup"><span data-stu-id="35539-710">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="35539-711">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modelo</span><span class="sxs-lookup"><span data-stu-id="35539-711">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="35539-712">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto</span><span class="sxs-lookup"><span data-stu-id="35539-712">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="35539-713">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-713">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-714">Multidimensional do SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="35539-714">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="35539-715">Medida</span><span class="sxs-lookup"><span data-stu-id="35539-715">Measure</span></span></td>
      <td><span data-ttu-id="35539-716">Medida</span><span class="sxs-lookup"><span data-stu-id="35539-716">Measure</span></span></td>
      <td><span data-ttu-id="35539-717">
        <font size=2> Protocolo: analysis-services</span><span class="sxs-lookup"><span data-stu-id="35539-717">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="35539-718">Autenticação: {windows, básica, anônima, nenhuma}</span><span class="sxs-lookup"><span data-stu-id="35539-718">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="35539-719">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-719">Address:</span></span> <br><span data-ttu-id="35539-720">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="35539-720">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="35539-721">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; banco de dados</span><span class="sxs-lookup"><span data-stu-id="35539-721">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="35539-722">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modelo</span><span class="sxs-lookup"><span data-stu-id="35539-722">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="35539-723">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto</span><span class="sxs-lookup"><span data-stu-id="35539-723">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="35539-724">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Medida} </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-724">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-725">Multidimensional do SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="35539-725">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="35539-726">Tabela</span><span class="sxs-lookup"><span data-stu-id="35539-726">Table</span></span></td>
      <td><span data-ttu-id="35539-727">Dimensão</span><span class="sxs-lookup"><span data-stu-id="35539-727">Dimension</span></span></td>
      <td><span data-ttu-id="35539-728">
        <font size=2> Protocolo: analysis-services</span><span class="sxs-lookup"><span data-stu-id="35539-728">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="35539-729">Autenticação: {windows, básica, anônima, nenhuma}</span><span class="sxs-lookup"><span data-stu-id="35539-729">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="35539-730">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-730">Address:</span></span> <br><span data-ttu-id="35539-731">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="35539-731">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="35539-732">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; banco de dados</span><span class="sxs-lookup"><span data-stu-id="35539-732">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="35539-733">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modelo</span><span class="sxs-lookup"><span data-stu-id="35539-733">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="35539-734">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto</span><span class="sxs-lookup"><span data-stu-id="35539-734">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="35539-735">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Dimensão} </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-735">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Dimension} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-736">Tabela do SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="35539-736">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="35539-737">Contêiner</span><span class="sxs-lookup"><span data-stu-id="35539-737">Container</span></span></td>
      <td><span data-ttu-id="35539-738">Modelo</span><span class="sxs-lookup"><span data-stu-id="35539-738">Model</span></span></td>
      <td><span data-ttu-id="35539-739">
        <font size=2> Protocolo: analysis-services</span><span class="sxs-lookup"><span data-stu-id="35539-739">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="35539-740">Autenticação: {windows, básica, anônima, nenhuma}</span><span class="sxs-lookup"><span data-stu-id="35539-740">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="35539-741">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-741">Address:</span></span> <br><span data-ttu-id="35539-742">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="35539-742">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="35539-743">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; banco de dados</span><span class="sxs-lookup"><span data-stu-id="35539-743">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="35539-744">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modelo </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-744">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-745">Tabela do SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="35539-745">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="35539-746">KPI</span><span class="sxs-lookup"><span data-stu-id="35539-746">KPI</span></span></td>
      <td><span data-ttu-id="35539-747">KPI</span><span class="sxs-lookup"><span data-stu-id="35539-747">KPI</span></span></td>
      <td><span data-ttu-id="35539-748">
        <font size=2> Protocolo: analysis-services</span><span class="sxs-lookup"><span data-stu-id="35539-748">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="35539-749">Autenticação: {windows, básica, anônima, nenhuma}</span><span class="sxs-lookup"><span data-stu-id="35539-749">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="35539-750">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-750">Address:</span></span> <br><span data-ttu-id="35539-751">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="35539-751">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="35539-752">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; banco de dados</span><span class="sxs-lookup"><span data-stu-id="35539-752">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="35539-753">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modelo</span><span class="sxs-lookup"><span data-stu-id="35539-753">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="35539-754">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto</span><span class="sxs-lookup"><span data-stu-id="35539-754">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="35539-755">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-755">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-756">Tabela do SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="35539-756">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="35539-757">Medida</span><span class="sxs-lookup"><span data-stu-id="35539-757">Measure</span></span></td>
      <td><span data-ttu-id="35539-758">Medida</span><span class="sxs-lookup"><span data-stu-id="35539-758">Measure</span></span></td>
      <td><span data-ttu-id="35539-759">
        <font size=2> Protocolo: analysis-services</span><span class="sxs-lookup"><span data-stu-id="35539-759">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="35539-760">Autenticação: {windows, básica, anônima, nenhuma}</span><span class="sxs-lookup"><span data-stu-id="35539-760">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="35539-761">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-761">Address:</span></span> <br><span data-ttu-id="35539-762">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="35539-762">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="35539-763">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; banco de dados</span><span class="sxs-lookup"><span data-stu-id="35539-763">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="35539-764">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modelo</span><span class="sxs-lookup"><span data-stu-id="35539-764">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="35539-765">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto</span><span class="sxs-lookup"><span data-stu-id="35539-765">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="35539-766">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Medida} </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-766">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-767">Tabela do SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="35539-767">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="35539-768">Tabela</span><span class="sxs-lookup"><span data-stu-id="35539-768">Table</span></span></td>
      <td><span data-ttu-id="35539-769">Tabela</span><span class="sxs-lookup"><span data-stu-id="35539-769">Table</span></span></td>
      <td><span data-ttu-id="35539-770">
        <font size=2> Protocolo: analysis-services</span><span class="sxs-lookup"><span data-stu-id="35539-770">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="35539-771">Autenticação: {windows, básica, anônima, nenhuma}</span><span class="sxs-lookup"><span data-stu-id="35539-771">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="35539-772">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-772">Address:</span></span> <br><span data-ttu-id="35539-773">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="35539-773">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="35539-774">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; banco de dados</span><span class="sxs-lookup"><span data-stu-id="35539-774">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="35539-775">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modelo</span><span class="sxs-lookup"><span data-stu-id="35539-775">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="35539-776">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto</span><span class="sxs-lookup"><span data-stu-id="35539-776">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="35539-777">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Tabela} </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-777">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Table} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-778">SQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="35539-778">SQL Server Reporting Services</span></span></td>
      <td><span data-ttu-id="35539-779">Contêiner</span><span class="sxs-lookup"><span data-stu-id="35539-779">Container</span></span></td>
      <td><span data-ttu-id="35539-780">Servidor</span><span class="sxs-lookup"><span data-stu-id="35539-780">Server</span></span></td>
      <td><span data-ttu-id="35539-781">
        <font size=2> Protocolo: reporting-services</span><span class="sxs-lookup"><span data-stu-id="35539-781">
        <font size=2> Protocol: reporting-services</span></span> <br><span data-ttu-id="35539-782">Autenticação: {windows}</span><span class="sxs-lookup"><span data-stu-id="35539-782">Authentication: {windows}</span></span> <br><span data-ttu-id="35539-783">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-783">Address:</span></span> <br><span data-ttu-id="35539-784">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="35539-784">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="35539-785">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; versão: {ReportingService2010} </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-785">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-786">SQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="35539-786">SQL Server Reporting Services</span></span></td>
      <td><span data-ttu-id="35539-787">Relatório</span><span class="sxs-lookup"><span data-stu-id="35539-787">Report</span></span></td>
      <td><span data-ttu-id="35539-788">Relatório</span><span class="sxs-lookup"><span data-stu-id="35539-788">Report</span></span></td>
      <td><span data-ttu-id="35539-789">
        <font size=2> Protocolo: reporting-services</span><span class="sxs-lookup"><span data-stu-id="35539-789">
        <font size=2> Protocol: reporting-services</span></span> <br><span data-ttu-id="35539-790">Autenticação: {windows}</span><span class="sxs-lookup"><span data-stu-id="35539-790">Authentication: {windows}</span></span> <br><span data-ttu-id="35539-791">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-791">Address:</span></span> <br><span data-ttu-id="35539-792">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="35539-792">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="35539-793">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; caminho</span><span class="sxs-lookup"><span data-stu-id="35539-793">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; path</span></span> <br><span data-ttu-id="35539-794">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; versão: {ReportingService2010} </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-794">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-795">Teradata</span><span class="sxs-lookup"><span data-stu-id="35539-795">Teradata</span></span></td>
      <td><span data-ttu-id="35539-796">Contêiner</span><span class="sxs-lookup"><span data-stu-id="35539-796">Container</span></span></td>
      <td><span data-ttu-id="35539-797">Banco de dados</span><span class="sxs-lookup"><span data-stu-id="35539-797">Database</span></span></td>
      <td><span data-ttu-id="35539-798">
        <font size=2> Protocolo: teradata</span><span class="sxs-lookup"><span data-stu-id="35539-798">
        <font size=2> Protocol: teradata</span></span> <br><span data-ttu-id="35539-799">Autenticação: {protocolo, windows}</span><span class="sxs-lookup"><span data-stu-id="35539-799">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="35539-800">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-800">Address:</span></span> <br><span data-ttu-id="35539-801">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="35539-801">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="35539-802">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; banco de dados </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-802">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-803">Teradata</span><span class="sxs-lookup"><span data-stu-id="35539-803">Teradata</span></span></td>
      <td><span data-ttu-id="35539-804">Tabela</span><span class="sxs-lookup"><span data-stu-id="35539-804">Table</span></span></td>
      <td><span data-ttu-id="35539-805">Tabela, exibição</span><span class="sxs-lookup"><span data-stu-id="35539-805">Table, view</span></span></td>
      <td><span data-ttu-id="35539-806">
        <font size=2> Protocolo: teradata</span><span class="sxs-lookup"><span data-stu-id="35539-806">
        <font size=2> Protocol: teradata</span></span> <br><span data-ttu-id="35539-807">Autenticação: {protocolo, windows}</span><span class="sxs-lookup"><span data-stu-id="35539-807">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="35539-808">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-808">Address:</span></span> <br><span data-ttu-id="35539-809">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="35539-809">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="35539-810">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; banco de dados</span><span class="sxs-lookup"><span data-stu-id="35539-810">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="35539-811">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-811">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-812">SQL Server Master Data Services</span><span class="sxs-lookup"><span data-stu-id="35539-812">SQL Server Master Data Services</span></span></td>
      <td><span data-ttu-id="35539-813">Contêiner</span><span class="sxs-lookup"><span data-stu-id="35539-813">Container</span></span></td>
      <td><span data-ttu-id="35539-814">Modelo</span><span class="sxs-lookup"><span data-stu-id="35539-814">Model</span></span></td>
      <td><span data-ttu-id="35539-815">
        <font size="2"> Protocolo: mssql-mds</span><span class="sxs-lookup"><span data-stu-id="35539-815">
        <font size="2"> Protocol: mssql-mds</span></span> <br><span data-ttu-id="35539-816">Autenticação: {windows}</span><span class="sxs-lookup"><span data-stu-id="35539-816">Authentication: {windows}</span></span> <br><span data-ttu-id="35539-817">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-817">Address:</span></span> <br><span data-ttu-id="35539-818">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="35539-818">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="35539-819">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modelo</span><span class="sxs-lookup"><span data-stu-id="35539-819">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="35539-820">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; versão </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-820">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-821">SQL Server Master Data Services</span><span class="sxs-lookup"><span data-stu-id="35539-821">SQL Server Master Data Services</span></span></td>
      <td><span data-ttu-id="35539-822">Tabela</span><span class="sxs-lookup"><span data-stu-id="35539-822">Table</span></span></td>
      <td><span data-ttu-id="35539-823">Entidade</span><span class="sxs-lookup"><span data-stu-id="35539-823">Entity</span></span></td>
      <td><span data-ttu-id="35539-824">
        <font size="2"> Protocolo: mssql-mds</span><span class="sxs-lookup"><span data-stu-id="35539-824">
        <font size="2"> Protocol: mssql-mds</span></span> <br><span data-ttu-id="35539-825">Autenticação: {windows}</span><span class="sxs-lookup"><span data-stu-id="35539-825">Authentication: {windows}</span></span> <br><span data-ttu-id="35539-826">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-826">Address:</span></span> <br><span data-ttu-id="35539-827">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="35539-827">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="35539-828">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modelo</span><span class="sxs-lookup"><span data-stu-id="35539-828">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="35539-829">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; versão</span><span class="sxs-lookup"><span data-stu-id="35539-829">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version</span></span> <br><span data-ttu-id="35539-830">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; entidade </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-830">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; entity </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-831">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="35539-831">Azure Cosmos DB</span></span></td>
      <td><span data-ttu-id="35539-832">Contêiner</span><span class="sxs-lookup"><span data-stu-id="35539-832">Container</span></span></td>
      <td><span data-ttu-id="35539-833">Banco de dados</span><span class="sxs-lookup"><span data-stu-id="35539-833">Database</span></span></td>
      <td><span data-ttu-id="35539-834">
        <font size=2> Protocolo: document-db</span><span class="sxs-lookup"><span data-stu-id="35539-834">
        <font size=2> Protocol: document-db</span></span> <br><span data-ttu-id="35539-835">Autenticação: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="35539-835">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="35539-836">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-836">Address:</span></span> <br><span data-ttu-id="35539-837">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="35539-837">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="35539-838">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; banco de dados </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-838">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-839">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="35539-839">Azure Cosmos DB</span></span></td>
      <td><span data-ttu-id="35539-840">Coleção</span><span class="sxs-lookup"><span data-stu-id="35539-840">Collection</span></span></td>
      <td><span data-ttu-id="35539-841">Coleção</span><span class="sxs-lookup"><span data-stu-id="35539-841">Collection</span></span></td>
      <td><span data-ttu-id="35539-842">
        <font size=2> Protocolo: document-db</span><span class="sxs-lookup"><span data-stu-id="35539-842">
        <font size=2> Protocol: document-db</span></span> <br><span data-ttu-id="35539-843">Autenticação: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="35539-843">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="35539-844">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-844">Address:</span></span> <br><span data-ttu-id="35539-845">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="35539-845">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="35539-846">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; banco de dados</span><span class="sxs-lookup"><span data-stu-id="35539-846">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="35539-847">Coleção &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-847">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; collection </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-848">ODBC Genérico</span><span class="sxs-lookup"><span data-stu-id="35539-848">Generic ODBC</span></span></td>
      <td><span data-ttu-id="35539-849">Contêiner</span><span class="sxs-lookup"><span data-stu-id="35539-849">Container</span></span></td>
      <td><span data-ttu-id="35539-850">Banco de dados</span><span class="sxs-lookup"><span data-stu-id="35539-850">Database</span></span></td>
      <td><span data-ttu-id="35539-851">
        <font size=2> Protocolo: odbc</span><span class="sxs-lookup"><span data-stu-id="35539-851">
        <font size=2> Protocol: odbc</span></span> <br><span data-ttu-id="35539-852">Autenticação: {básica, windows}</span><span class="sxs-lookup"><span data-stu-id="35539-852">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="35539-853">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-853">Address:</span></span> <br><span data-ttu-id="35539-854">Opções &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="35539-854">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; options</span></span> <br><span data-ttu-id="35539-855">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; banco de dados </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-855">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-856">ODBC Genérico</span><span class="sxs-lookup"><span data-stu-id="35539-856">Generic ODBC</span></span></td>
      <td><span data-ttu-id="35539-857">Tabela</span><span class="sxs-lookup"><span data-stu-id="35539-857">Table</span></span></td>
      <td><span data-ttu-id="35539-858">Tabela, exibição</span><span class="sxs-lookup"><span data-stu-id="35539-858">Table, View</span></span></td>
      <td><span data-ttu-id="35539-859">
        <font size=2> Protocolo: odbc</span><span class="sxs-lookup"><span data-stu-id="35539-859">
        <font size=2> Protocol: odbc</span></span> <br><span data-ttu-id="35539-860">Autenticação: {básica, windows}</span><span class="sxs-lookup"><span data-stu-id="35539-860">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="35539-861">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-861">Address:</span></span> <br><span data-ttu-id="35539-862">Opções &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="35539-862">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; options</span></span> <br><span data-ttu-id="35539-863">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; banco de dados</span><span class="sxs-lookup"><span data-stu-id="35539-863">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="35539-864">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto</span><span class="sxs-lookup"><span data-stu-id="35539-864">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="35539-865">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; esquema </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-865">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-866">Sybase</span><span class="sxs-lookup"><span data-stu-id="35539-866">Sybase</span></span></td>
      <td><span data-ttu-id="35539-867">Contêiner</span><span class="sxs-lookup"><span data-stu-id="35539-867">Container</span></span></td>
      <td><span data-ttu-id="35539-868">Banco de dados</span><span class="sxs-lookup"><span data-stu-id="35539-868">Database</span></span></td>
      <td><span data-ttu-id="35539-869">
        <font size=2> Protocolo: sybase</span><span class="sxs-lookup"><span data-stu-id="35539-869">
        <font size=2> protocol: sybase</span></span> <br><span data-ttu-id="35539-870">autenticação: {básica, windows}</span><span class="sxs-lookup"><span data-stu-id="35539-870">authentication: {basic, windows}</span></span> <br><span data-ttu-id="35539-871">endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-871">address:</span></span> <br><span data-ttu-id="35539-872">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="35539-872">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="35539-873">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; banco de dados </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-873">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-874">Sybase</span><span class="sxs-lookup"><span data-stu-id="35539-874">Sybase</span></span></td>
      <td><span data-ttu-id="35539-875">Tabela</span><span class="sxs-lookup"><span data-stu-id="35539-875">Table</span></span></td>
      <td><span data-ttu-id="35539-876">Tabela, exibição</span><span class="sxs-lookup"><span data-stu-id="35539-876">Table, View</span></span></td>
      <td><span data-ttu-id="35539-877">
        <font size=2> Protocolo: sybase</span><span class="sxs-lookup"><span data-stu-id="35539-877">
        <font size=2> protocol: sybase</span></span> <br><span data-ttu-id="35539-878">autenticação: {básica, windows}</span><span class="sxs-lookup"><span data-stu-id="35539-878">authentication: {basic, windows}</span></span> <br><span data-ttu-id="35539-879">endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-879">address:</span></span> <br><span data-ttu-id="35539-880">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; servidor</span><span class="sxs-lookup"><span data-stu-id="35539-880">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="35539-881">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; banco de dados</span><span class="sxs-lookup"><span data-stu-id="35539-881">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="35539-882">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; esquema</span><span class="sxs-lookup"><span data-stu-id="35539-882">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="35539-883">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objeto </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-883">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="35539-884">Outros (nenhum Olá acima)</span><span class="sxs-lookup"><span data-stu-id="35539-884">Other (none of hello above)</span></span></td>
      <td>\*</td>
      <td>\*</td>
      <td><span data-ttu-id="35539-885">
        <font size=2> Protocolo: generic-asset</span><span class="sxs-lookup"><span data-stu-id="35539-885">
        <font size=2> Protocol: generic-asset</span></span> <br><span data-ttu-id="35539-886">Endereço:</span><span class="sxs-lookup"><span data-stu-id="35539-886">Address:</span></span> <br><span data-ttu-id="35539-887">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; assetId </font>
      </span><span class="sxs-lookup"><span data-stu-id="35539-887">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; assetId </font>
      </span></span></td>
    </tr>
</table>
