---
title: "clientes de nível inferior do Data Warehouse aaaSQL suportam para auditoria de dados | Microsoft Docs"
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
ms.openlocfilehash: 377488680eb297c3e9b1dc754c003c5b19b47996
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse----downlevel-clients-support-for-auditing-and-dynamic-data-masking"></a><span data-ttu-id="fbab1-103">SQL Data Warehouse - Suporte de versão anterior a clientes para auditoria e Máscara de Dados Dinâmicos</span><span class="sxs-lookup"><span data-stu-id="fbab1-103">SQL Data Warehouse -  Downlevel clients support for auditing and Dynamic Data Masking</span></span>
<span data-ttu-id="fbab1-104">[Auditoria](sql-data-warehouse-auditing-overview.md) funciona com clientes SQL que oferecem suporte ao redirecionamento de TDS.</span><span class="sxs-lookup"><span data-stu-id="fbab1-104">[Auditing](sql-data-warehouse-auditing-overview.md) works with SQL clients that support TDS redirection.</span></span>

<span data-ttu-id="fbab1-105">Qualquer cliente que implemente o protocolo TDS 7.4 também deve dar suporte a redirecionamento.</span><span class="sxs-lookup"><span data-stu-id="fbab1-105">Any client which implements TDS 7.4 should also support redirection.</span></span> <span data-ttu-id="fbab1-106">Exceções toothis incluem JDBC 4.0 no qual recurso de redirecionamento Olá não é totalmente compatível e tediosas para Node. js em que o redirecionamento não foi implementado.</span><span class="sxs-lookup"><span data-stu-id="fbab1-106">Exceptions toothis include JDBC 4.0 in which hello redirection feature is not fully supported and Tedious for Node.JS in which redirection was not implemented.</span></span>

<span data-ttu-id="fbab1-107">Para clientes de nível inferior"", ou seja, que suporte o protocolo TDS versão 7.3 e abaixo - Olá FQDN do servidor na cadeia de caracteres de conexão Olá deve ser modificado:</span><span class="sxs-lookup"><span data-stu-id="fbab1-107">For "Downlevel clients", i.e. which support TDS version 7.3 and below - hello server FQDN in hello connection string should be modified:</span></span>

<span data-ttu-id="fbab1-108">FQDN do servidor original na cadeia de caracteres de conexão Olá: <*nome do servidor*>. t</span><span class="sxs-lookup"><span data-stu-id="fbab1-108">Original server FQDN in hello connection string: <*server name*>.database.windows.net</span></span>

<span data-ttu-id="fbab1-109">FQDN do servidor modificado na cadeia de caracteres de conexão de saudação: <*nome do servidor*>. Database. **seguro**. windows.net</span><span class="sxs-lookup"><span data-stu-id="fbab1-109">Modified server FQDN in hello connection string: <*server name*>.database.**secure**.windows.net</span></span>

<span data-ttu-id="fbab1-110">Uma lista parcial de "Clientes de versão anterior" inclui:</span><span class="sxs-lookup"><span data-stu-id="fbab1-110">A partial list of "Downlevel clients" includes:</span></span>

* <span data-ttu-id="fbab1-111">.NET 4.0 e inferior,</span><span class="sxs-lookup"><span data-stu-id="fbab1-111">.NET 4.0 and below,</span></span>
* <span data-ttu-id="fbab1-112">ODBC 10.0 e inferior.</span><span class="sxs-lookup"><span data-stu-id="fbab1-112">ODBC 10.0 and below.</span></span>
* <span data-ttu-id="fbab1-113">JDBC (enquanto JDBC suporta TDS 7.4, Olá recurso de redirecionamento do protocolo TDS não tem suporte total)</span><span class="sxs-lookup"><span data-stu-id="fbab1-113">JDBC (while JDBC does support TDS 7.4, hello TDS redirection feature is not fully supported)</span></span>
* <span data-ttu-id="fbab1-114">Tedious (para o Node.JS)</span><span class="sxs-lookup"><span data-stu-id="fbab1-114">Tedious (for Node.JS)</span></span>

<span data-ttu-id="fbab1-115">**Comentário:** Olá acima modificação FQDN do servidor pode ser útil também para aplicar uma política de auditoria de nível de servidor do SQL sem a necessidade de uma configuração de etapa em cada banco de dados (temporário mitigação).</span><span class="sxs-lookup"><span data-stu-id="fbab1-115">**Remark:** hello above server FDQN modification may be useful also for applying a SQL Server Level Auditing policy without a need for a configuration step in each database (Temporary mitigation).</span></span>     

