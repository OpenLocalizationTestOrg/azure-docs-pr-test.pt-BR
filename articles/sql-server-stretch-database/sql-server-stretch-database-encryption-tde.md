---
title: aaaEnable criptografia transparente de dados para o Stretch Database - Azure | Microsoft Docs
description: Habilitar TDE (Transparent Data Encryption) para SQL Server Stretch Database no Azure
services: sql-server-stretch-database
documentationcenter: 
author: douglaslMS
manager: barbkess
editor: 
ms.assetid: a44ed8f5-b416-4c41-9b1e-b7271f10bdc3
ms.service: sql-server-stretch-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2016
ms.author: douglasl
ms.openlocfilehash: 1d6bff455030ac8851b2184c1e8097afd61361d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure"></a>Habilitar TDE (Transparent Data Encryption) para Stretch Database no Azure
> [!div class="op_single_selector"]
> * [Portal do Azure](sql-server-stretch-database-encryption-tde.md)
> * [TSQL](sql-server-stretch-database-tde-tsql.md)
>
>

Criptografia de dados transparente (TDE) ajuda a proteger contra a ameaça de saudação de atividades mal-intencionadas executando criptografia em tempo real e a descriptografia de banco de dados hello, backups associados e arquivos de log de transações em repouso sem exigir alterações toohello aplicativo.

Ela criptografa o armazenamento de saudação de um banco de dados inteiro usando uma chave de criptografia de banco de dados de saudação de chamada de chave simétrica. chave de criptografia de banco de dados de saudação é protegida por um certificado de servidor interno. certificado de saudação do servidor interno é exclusivo para cada servidor do Azure. A Microsoft alterna automaticamente esses certificados pelo menos a cada 90 dias. Para obter uma descrição geral da TDE, consulte [Transparent Data Encryption (TDE)].

## <a name="enabling-encryption"></a>Habilitando a criptografia
tooenable TDE para um banco de dados do Azure que está armazenando Olá migrar dados de um banco de dados do SQL Server habilitado para Stretch, Olá coisas a seguir:

1. Banco de dados aberto Olá no hello [portal do Azure](https://portal.azure.com)
2. Na folha de banco de dados de saudação, clique em Olá **configurações** botão
3. Selecione Olá **criptografia transparente de dados** opção![][1]
4. Selecione Olá **na** configuração e, em seguida, selecione **salvar**
   ![][2]

## <a name="disabling-encryption"></a>Desabilitando a criptografia
toodisable TDE para um banco de dados do Azure que está armazenando Olá migrar dados de um banco de dados do SQL Server habilitado para Stretch, Olá coisas a seguir:

1. Banco de dados aberto Olá no hello [portal do Azure](https://portal.azure.com)
2. Na folha de banco de dados de saudação, clique em Olá **configurações** botão
3. Selecione Olá **criptografia transparente de dados** opção
4. Selecione Olá **Off** configuração e, em seguida, selecione **salvar**

<!--Anchors-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->
[1]: ./media/sql-server-stretch-database-encryption-tde/stretchtde1.png
[2]: ./media/sql-server-stretch-database-encryption-tde/stretchtde2.png


<!--Link references-->
