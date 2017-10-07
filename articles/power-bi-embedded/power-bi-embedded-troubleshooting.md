---
title: "solução de problemas de visualização do Power BI Embedded aaaMicrosoft"
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
ms.openlocfilehash: a0a25cd73977c0ea0bd6b7c82e215412245771bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-power-bi-embedded-preview-troubleshooting"></a><span data-ttu-id="4e7ea-103">Solução de problemas da Preview do Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="4e7ea-103">Microsoft Power BI Embedded Preview troubleshooting</span></span>
<span data-ttu-id="4e7ea-104">Este artigo fornece respostas para como tootroubleshoot **Power BI inserido**.</span><span class="sxs-lookup"><span data-stu-id="4e7ea-104">This article provides answers for how  tootroubleshoot **Power BI Embedded**.</span></span>

<a name="connection-string"/>

## <a name="setting-sql-server-connection-strings"></a><span data-ttu-id="4e7ea-105">Configurando cadeias de conexão do SQL Server</span><span class="sxs-lookup"><span data-stu-id="4e7ea-105">Setting SQL Server connection strings</span></span>
<span data-ttu-id="4e7ea-106">tooset uma cadeia de caracteres de conexão do SQL Server, você precisa toofollow um formato específico.</span><span class="sxs-lookup"><span data-stu-id="4e7ea-106">tooset a SQL Server connecting string, you need toofollow a specific format.</span></span> <span data-ttu-id="4e7ea-107">Abaixo está um exemplo da cadeia de conexão para o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4e7ea-107">Below is an example connection string for SQL Server.</span></span>

```
"Persist Security Info=False;Integrated Security=true;Initial Catalog=Northwind;server=(local)"
```

<span data-ttu-id="4e7ea-108">toolearn mais informações sobre cadeias de caracteres de conexão do SQL Server, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="4e7ea-108">toolearn more about SQL Server connection strings, see hello following articles:</span></span>

* [<span data-ttu-id="4e7ea-109">Cadeias de Conexão do SQL Server</span><span class="sxs-lookup"><span data-stu-id="4e7ea-109">SQL Server Connection Strings</span></span>](https://msdn.microsoft.com/library/jj653752.aspx)
* [<span data-ttu-id="4e7ea-110">SqlConnection.ConnectionString</span><span class="sxs-lookup"><span data-stu-id="4e7ea-110">SqlConnection.ConnectionString</span></span>](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectionstring.aspx)

<a name="credentials"/>

## <a name="setting-credentials"></a><span data-ttu-id="4e7ea-111">Configurando credenciais</span><span class="sxs-lookup"><span data-stu-id="4e7ea-111">Setting credentials</span></span>
<span data-ttu-id="4e7ea-112">No caso de Olá onde você tem credenciais para um desenvolvimento ou ambiente de preparo, como nome de usuário e senha, talvez seja necessário tooupdate credenciais que correspondem a uma solução de produção.</span><span class="sxs-lookup"><span data-stu-id="4e7ea-112">In hello case where you have credentials for a development or staging environment, such as user name and password, you might need tooupdate credentials that match a production solution.</span></span>

## <a name="see-also"></a><span data-ttu-id="4e7ea-113">Consulte também</span><span class="sxs-lookup"><span data-stu-id="4e7ea-113">See Also</span></span>
* [<span data-ttu-id="4e7ea-114">Introdução a exemplos</span><span class="sxs-lookup"><span data-stu-id="4e7ea-114">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)
* [<span data-ttu-id="4e7ea-115">O que é o Power BI Embedded?</span><span class="sxs-lookup"><span data-stu-id="4e7ea-115">What is Power BI Embedded</span></span>](power-bi-embedded-what-is-power-bi-embedded.md)

