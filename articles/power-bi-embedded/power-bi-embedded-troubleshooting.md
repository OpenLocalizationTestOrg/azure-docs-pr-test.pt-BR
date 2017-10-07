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
# <a name="microsoft-power-bi-embedded-preview-troubleshooting"></a>Solução de problemas da Preview do Microsoft Power BI Embedded
Este artigo fornece respostas para como tootroubleshoot **Power BI inserido**.

<a name="connection-string"/>

## <a name="setting-sql-server-connection-strings"></a>Configurando cadeias de conexão do SQL Server
tooset uma cadeia de caracteres de conexão do SQL Server, você precisa toofollow um formato específico. Abaixo está um exemplo da cadeia de conexão para o SQL Server.

```
"Persist Security Info=False;Integrated Security=true;Initial Catalog=Northwind;server=(local)"
```

toolearn mais informações sobre cadeias de caracteres de conexão do SQL Server, consulte Olá artigos a seguir:

* [Cadeias de Conexão do SQL Server](https://msdn.microsoft.com/library/jj653752.aspx)
* [SqlConnection.ConnectionString](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectionstring.aspx)

<a name="credentials"/>

## <a name="setting-credentials"></a>Configurando credenciais
No caso de Olá onde você tem credenciais para um desenvolvimento ou ambiente de preparo, como nome de usuário e senha, talvez seja necessário tooupdate credenciais que correspondem a uma solução de produção.

## <a name="see-also"></a>Consulte também
* [Introdução a exemplos](power-bi-embedded-get-started-sample.md)
* [O que é o Power BI Embedded?](power-bi-embedded-what-is-power-bi-embedded.md)

