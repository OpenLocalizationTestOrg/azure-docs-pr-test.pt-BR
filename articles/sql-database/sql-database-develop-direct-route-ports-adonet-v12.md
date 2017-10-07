---
title: "aaaPorts além 1433 para o banco de dados SQL | Microsoft Docs"
description: "Conexões de cliente do ADO.NET tooAzure banco de dados SQL, às vezes, ignoram proxy hello e interagem diretamente com o banco de dados de saudação. Outras portas diferentes da 1433 se tornam importantes."
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.assetid: 3f17106a-92fd-4aa4-b6a9-1daa29421f64
ms.service: sql-database
ms.custom: develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: sstein
ms.openlocfilehash: a35ff2d827ae3fa29b3ea855dbb7ed78583c82eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="ports-beyond-1433-for-adonet-45"></a>Portas além da 1433 para ADO.NET 4.5
Este tópico descreve o comportamento de conexão de banco de dados do Azure SQL Olá para clientes que usam o ADO.NET 4.5 ou posterior. 

> [!IMPORTANT]
> Para obter informações sobre a arquitetura de conectividade, confira [Arquitetura de conectividade de Banco de Dados SQL do Azure](sql-database-connectivity-architecture.md).
>

## <a name="outside-vs-inside"></a>Fora versus dentro
Para conexões tooAzure banco de dados SQL, deve primeiro pedimos que se seu programa cliente executa *fora* ou *dentro* limites de nuvem do Azure hello. subseções Olá discutem dois cenários comuns.

#### <a name="outside-client-runs-on-your-desktop-computer"></a>*Fora:* o cliente é executado em seu computador desktop
A porta 1433 é Olá somente a porta que deve ser aberta no computador desktop que hospede o aplicativo de cliente do banco de dados SQL.

#### <a name="inside-client-runs-on-azure"></a>*Dentro:* o cliente é executado no Azure
Quando o cliente é executado dentro do limite de nuvem do Azure hello, ele usa o que podemos chamar um *direta de rota* toointeract com o servidor de banco de dados SQL hello. Depois que uma conexão é estabelecida, outras interações entre o cliente hello e banco de dados não envolvem nenhum proxy de middleware.

sequência de saudação é da seguinte maneira:

1. ADO.NET 4.5 (ou posterior) inicia uma breve interação com hello nuvem do Azure e recebe um número de porta dinamicamente identificado.
   
   * número da porta Olá dinamicamente identificado está no intervalo de saudação de 11.000 a 11.999 ou 14.000 a 14.999.
2. ADO.NET, em seguida, conecta-se servidor de banco de dados SQL toohello diretamente, com nenhum middleware entre.
3. As consultas são enviadas diretamente toohello banco de dados e os resultados são retornados diretamente toohello cliente.

Verifique se essa porta Olá intervalos de 11.000 a 11.999 e 14.000 a 14.999 do computador cliente do Azure ficam disponíveis para ADO.NET 4.5 interações de cliente com o banco de dados SQL.

* Em particular, as portas no intervalo de saudação devem estar livres de quaisquer outros bloqueadores de saída.
* Na sua VM do Azure, Olá **Firewall do Windows com segurança avançada** controles Olá configurações de porta.
  
  * Você pode usar o hello [interface de usuário do firewall](http://msdn.microsoft.com/library/cc646023.aspx) tooadd uma regra para que você especificar Olá **TCP** como o protocolo junto com um intervalo de portas com sintaxe Olá **11.000 a 11.999**.

## <a name="version-clarifications"></a>Esclarecimentos da versão
Esta seção explica monikers Olá que fazem referência tooproduct versões. Ela também lista alguns emparelhamentos de versões entre produtos.

#### <a name="adonet"></a>ADO.NET
* ADO.NET 4.0 oferece suporte a protocolo de saudação 7.3 TDS, mas não 7.4.
* ADO.NET 4.5 e posterior oferece suporte ao protocolo de saudação TDS 7.4.

## <a name="related-links"></a>Links relacionados
* O ADO.NET 4.6 foi lançado em 20 de julho de 2015. Um comunicado do blog da equipe do .NET hello está disponível [aqui](http://blogs.msdn.com/b/dotnet/archive/2015/07/20/announcing-net-framework-4-6.aspx).
* O ADO.NET 4.5 foi lançado em 15 de agosto de 2012. Um comunicado do blog da equipe do .NET hello está disponível [aqui](http://blogs.msdn.com/b/dotnet/archive/2012/08/15/announcing-the-release-of-net-framework-4-5-rtm-product-and-source-code.aspx).
  
  * Uma postagem no blog sobre o ADO.NET 4.5.1 está disponível [aqui](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx).
* [Lista de versões do protocolo TDS](http://www.freetds.org/userguide/tdshistory.htm)
* [Visão geral do desenvolvimento de Banco de Dados SQL](sql-database-develop-overview.md)
* [Firewall do Banco de Dados SQL do Azure](sql-database-firewall-configure.md)
* [Como definir as configurações de firewall no Banco de Dados SQL](sql-database-configure-firewall-settings.md)

