---
title: "Solução de problemas da Preview do Microsoft Power BI Embedded"
description: "Solução de problemas da Preview do Microsoft Power BI Embedded"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: c8aee652-ed8b-4c66-9c63-f798b7a655b4
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: f406d23e578acc825514aa5bd9eabcbf160bf9ec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoft-power-bi-embedded-preview-troubleshooting"></a><span data-ttu-id="81b93-103">Solução de problemas da Preview do Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="81b93-103">Microsoft Power BI Embedded Preview troubleshooting</span></span>
<span data-ttu-id="81b93-104">Este artigo fornece respostas para saber como solucionar problemas do **Power BI Embedded**.</span><span class="sxs-lookup"><span data-stu-id="81b93-104">This article provides answers for how  to troubleshoot **Power BI Embedded**.</span></span>

<a name="connection-string"/>

## <a name="setting-sql-server-connection-strings"></a><span data-ttu-id="81b93-105">Configurando cadeias de conexão do SQL Server</span><span class="sxs-lookup"><span data-stu-id="81b93-105">Setting SQL Server connection strings</span></span>
<span data-ttu-id="81b93-106">Para definir uma cadeia de conexão do SQL Server, você precisará seguir um formato específico.</span><span class="sxs-lookup"><span data-stu-id="81b93-106">To set a SQL Server connecting string, you need to follow a specific format.</span></span> <span data-ttu-id="81b93-107">Abaixo está um exemplo da cadeia de conexão para o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="81b93-107">Below is an example connection string for SQL Server.</span></span>

```
"Persist Security Info=False;Integrated Security=true;Initial Catalog=Northwind;server=(local)"
```

<span data-ttu-id="81b93-108">Para saber mais sobre cadeias de conexão do SQL Server, consulte os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="81b93-108">To learn more about SQL Server connection strings, see the following articles:</span></span>

* [<span data-ttu-id="81b93-109">Cadeias de Conexão do SQL Server</span><span class="sxs-lookup"><span data-stu-id="81b93-109">SQL Server Connection Strings</span></span>](https://msdn.microsoft.com/library/jj653752.aspx)
* [<span data-ttu-id="81b93-110">SqlConnection.ConnectionString</span><span class="sxs-lookup"><span data-stu-id="81b93-110">SqlConnection.ConnectionString</span></span>](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectionstring.aspx)

<a name="credentials"/>

## <a name="setting-credentials"></a><span data-ttu-id="81b93-111">Configurando credenciais</span><span class="sxs-lookup"><span data-stu-id="81b93-111">Setting credentials</span></span>
<span data-ttu-id="81b93-112">Em um caso em que você tenha as credenciais para um ambiente de preparo ou de desenvolvimento, como nome de usuário e senha, talvez seja necessário atualizar as credenciais que correspondem a uma solução de produção.</span><span class="sxs-lookup"><span data-stu-id="81b93-112">In the case where you have credentials for a development or staging environment, such as user name and password, you might need to update credentials that match a production solution.</span></span>

## <a name="see-also"></a><span data-ttu-id="81b93-113">Consulte também</span><span class="sxs-lookup"><span data-stu-id="81b93-113">See Also</span></span>
* [<span data-ttu-id="81b93-114">Introdução a exemplos</span><span class="sxs-lookup"><span data-stu-id="81b93-114">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)
* [<span data-ttu-id="81b93-115">O que é o Power BI Embedded?</span><span class="sxs-lookup"><span data-stu-id="81b93-115">What is Power BI Embedded</span></span>](power-bi-embedded-what-is-power-bi-embedded.md)

