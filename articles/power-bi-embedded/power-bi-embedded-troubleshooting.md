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
# <a name="microsoft-power-bi-embedded-preview-troubleshooting"></a>Solução de problemas da Preview do Microsoft Power BI Embedded
Este artigo fornece respostas para saber como solucionar problemas do **Power BI Embedded**.

<a name="connection-string"/>

## <a name="setting-sql-server-connection-strings"></a>Configurando cadeias de conexão do SQL Server
Para definir uma cadeia de conexão do SQL Server, você precisará seguir um formato específico. Abaixo está um exemplo da cadeia de conexão para o SQL Server.

```
"Persist Security Info=False;Integrated Security=true;Initial Catalog=Northwind;server=(local)"
```

Para saber mais sobre cadeias de conexão do SQL Server, consulte os seguintes artigos:

* [Cadeias de Conexão do SQL Server](https://msdn.microsoft.com/library/jj653752.aspx)
* [SqlConnection.ConnectionString](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectionstring.aspx)

<a name="credentials"/>

## <a name="setting-credentials"></a>Configurando credenciais
Em um caso em que você tenha as credenciais para um ambiente de preparo ou de desenvolvimento, como nome de usuário e senha, talvez seja necessário atualizar as credenciais que correspondem a uma solução de produção.

## <a name="see-also"></a>Consulte também
* [Introdução a exemplos](power-bi-embedded-get-started-sample.md)
* [O que é o Power BI Embedded?](power-bi-embedded-what-is-power-bi-embedded.md)

