---
title: "aaaClient bibliotecas necessárias para conectar o tooAzure Analysis Services | Microsoft Docs"
description: "Descreve as bibliotecas de cliente necessárias para aplicativos e ferramentas de cliente tooconnect Azure Analysis Services"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 74ba5c05ba76c6587c5aed38f200a1ba469aa4f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="client-libraries-for-connecting-tooazure-analysis-services"></a>Bibliotecas de cliente para conectar o tooAzure Analysis Services

Bibliotecas de cliente são necessárias para aplicativos cliente e servidores de serviços de tooAnalysis de tooconnect de ferramentas. 

O Analysis Services utiliza três bibliotecas de cliente. O ADOMD.NET e o AMO (Objetos de Gerenciamento do Analysis Services) são bibliotecas de cliente gerenciadas. provedor de OLE DB do Analysis Services da saudação (MSOLAP DLL) é uma biblioteca do native client. Normalmente, todos os três são instalados em Olá simultaneamente. Serviços de análise do Azure requer versões mais recentes de saudação. 

Os aplicativos cliente da Microsoft, como o Power BI Desktop e o Excel, instalam as três bibliotecas de cliente. No entanto, dependendo da versão de saudação ou a frequência de atualizações, bibliotecas de cliente não podem ser versões mais recentes de saudação exigidas pelo Azure Analysis Services. Olá mesmo se aplica toocustom aplicativos ou outras interfaces, como AsCmd, TOM, ADOMD.NET. Esses aplicativos exigem a instalação manual de bibliotecas de saudação. bibliotecas de saudação do cliente para instalação manual estão incluídas nos pacotes de recursos do SQL Server como pacotes de distribuição. No entanto, essas bibliotecas de cliente são toohello empatados versão do SQL Server e não podem ser hello mais recente.  

Bibliotecas de cliente para conexões de cliente são diferentes das tooconnect necessária de provedores de dados de uma fonte de dados do Azure Analysis Services server tooa. toolearn mais informações sobre conexões de fonte de dados, consulte [conexões de fonte de dados](analysis-services-datasource.md).

## <a name="download-hello-latest-client-libraries"></a>Baixar Olá bibliotecas de cliente mais recentes  
Use Olá bibliotecas de cliente a seguir se você estiver em um ambiente de produção e exige as versões de lançamento e suportadas completos.

[MSOLAP (amd64)](https://go.microsoft.com/fwlink/?linkid=829576)</br>
[MSOLAP (x86)](https://go.microsoft.com/fwlink/?linkid=829575)</br>
[AMO](https://go.microsoft.com/fwlink/?linkid=829578)</br>
[ADOMD](https://go.microsoft.com/fwlink/?linkid=829577)</br>

## <a name="next-steps"></a>Próximas etapas
[Conectar com Excel](analysis-services-connect-excel.md)    
[Conectar com o Power BI](analysis-services-connect-pbi.md)
