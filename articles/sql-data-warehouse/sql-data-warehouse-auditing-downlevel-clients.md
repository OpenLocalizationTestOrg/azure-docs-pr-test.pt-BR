---
title: "Suporte a clientes de versão anterior do SQL Data Warehouse para auditoria de dados | Microsoft Docs"
description: "Saiba mais sobre o suporte a clientes de versão anterior do SQL Data Warehouse para auditoria de dados"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: dfe29ff3-dfeb-4309-83c0-c1a300f4f44e
ms.service: sql-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: a7ea6141285a0098339f1e071af2592dd4535c12
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="sql-data-warehouse----downlevel-clients-support-for-auditing-and-dynamic-data-masking"></a><span data-ttu-id="e0049-103">SQL Data Warehouse - Suporte de versão anterior a clientes para auditoria e Máscara de Dados Dinâmicos</span><span class="sxs-lookup"><span data-stu-id="e0049-103">SQL Data Warehouse -  Downlevel clients support for auditing and Dynamic Data Masking</span></span>
<span data-ttu-id="e0049-104">[Auditoria](sql-data-warehouse-auditing-overview.md) funciona com clientes SQL que oferecem suporte ao redirecionamento de TDS.</span><span class="sxs-lookup"><span data-stu-id="e0049-104">[Auditing](sql-data-warehouse-auditing-overview.md) works with SQL clients that support TDS redirection.</span></span>

<span data-ttu-id="e0049-105">Qualquer cliente que implemente o protocolo TDS 7.4 também deve dar suporte a redirecionamento.</span><span class="sxs-lookup"><span data-stu-id="e0049-105">Any client which implements TDS 7.4 should also support redirection.</span></span> <span data-ttu-id="e0049-106">As exceções incluem o JDBC 4.0, no qual o recurso de redirecionamento não tem suporte completo, e o Tedious para Node.JS, no qual o redirecionamento não foi implementado.</span><span class="sxs-lookup"><span data-stu-id="e0049-106">Exceptions to this include JDBC 4.0 in which the redirection feature is not fully supported and Tedious for Node.JS in which redirection was not implemented.</span></span>

<span data-ttu-id="e0049-107">Para "clientes de versão anterior", ou seja, que oferecem suporte ao TDS versão 7.3 e inferior - o FQDN do servidor na cadeia de conexão deve ser modificado:</span><span class="sxs-lookup"><span data-stu-id="e0049-107">For "Downlevel clients", i.e. which support TDS version 7.3 and below - the server FQDN in the connection string should be modified:</span></span>

<span data-ttu-id="e0049-108">FQDN original do servidor na cadeia de conexão: <*nome do servidor*>.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="e0049-108">Original server FQDN in the connection string: <*server name*>.database.windows.net</span></span>

<span data-ttu-id="e0049-109">FQDN do servidor modificado na cadeia de conexão: <*nome do servidor*>.database.**secure**.windows.net</span><span class="sxs-lookup"><span data-stu-id="e0049-109">Modified server FQDN in the connection string: <*server name*>.database.**secure**.windows.net</span></span>

<span data-ttu-id="e0049-110">Uma lista parcial de "Clientes de versão anterior" inclui:</span><span class="sxs-lookup"><span data-stu-id="e0049-110">A partial list of "Downlevel clients" includes:</span></span>

* <span data-ttu-id="e0049-111">.NET 4.0 e inferior,</span><span class="sxs-lookup"><span data-stu-id="e0049-111">.NET 4.0 and below,</span></span>
* <span data-ttu-id="e0049-112">ODBC 10.0 e inferior.</span><span class="sxs-lookup"><span data-stu-id="e0049-112">ODBC 10.0 and below.</span></span>
* <span data-ttu-id="e0049-113">JDBC (embora o JDBC dê suporte ao TDS 7.4, o recurso de redirecionamento de TDS não recebe suporte total)</span><span class="sxs-lookup"><span data-stu-id="e0049-113">JDBC (while JDBC does support TDS 7.4, the TDS redirection feature is not fully supported)</span></span>
* <span data-ttu-id="e0049-114">Tedious (para o Node.JS)</span><span class="sxs-lookup"><span data-stu-id="e0049-114">Tedious (for Node.JS)</span></span>

<span data-ttu-id="e0049-115">**Comentário:** a modificação do FQDN do servidor acima pode ser útil também para aplicar uma política de Auditoria no Nível do SQL Server sem a necessidade de uma etapa de configuração em cada banco de dados (redução temporária).</span><span class="sxs-lookup"><span data-stu-id="e0049-115">**Remark:** The above server FDQN modification may be useful also for applying a SQL Server Level Auditing policy without a need for a configuration step in each database (Temporary mitigation).</span></span>     

