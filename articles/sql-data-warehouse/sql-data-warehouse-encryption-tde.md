---
title: aaaTransparent a criptografia de dados no Data Warehouse do SQL (Portal) | Microsoft Docs
description: TDE (Transparent Data Encryption) no SQL Data Warehouse
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: fabf75d3-9bbf-4e0d-9b31-8b5a8713f08d
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 8233886ecf170844104e0d1459e2a829cafa9b8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-transparent-data-encryption-tde-in-sql-data-warehouse"></a>Introdução aos dados TDE (Transparent Data Encryption) no SQL Data Warehouse
> [!div class="op_single_selector"]
> * [Visão Geral da Segurança](sql-data-warehouse-overview-manage-security.md)
> * [Autenticação](sql-data-warehouse-authentication.md)
> * [Criptografia (Portal)](sql-data-warehouse-encryption-tde.md)
> * [Criptografia (T-SQL)](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a>Permissões necessárias
tooenable criptografia de dados transparente (TDE), você deve ser um administrador ou um membro da função dbmanager de saudação.

## <a name="enabling-encryption"></a>Habilitando a criptografia
tooenable TDE para um SQL Data Warehouse, siga as etapas de saudação abaixo:

1. Banco de dados aberto Olá no hello [portal do Azure](https://portal.azure.com)
2. Na folha de banco de dados de saudação, clique em Olá **configurações** botão
3. Selecione Olá **criptografia transparente de dados** opção![][1]
4. Selecione Olá **em** configuração![][2]
5. Selecione **Salvar**
   ![][3]  

## <a name="disabling-encryption"></a>Desabilitando a criptografia
toodisable TDE para um SQL Data Warehouse, siga as etapas de saudação abaixo:

1. Banco de dados aberto Olá no hello [portal do Azure](https://portal.azure.com)
2. Na folha de banco de dados de saudação, clique em Olá **configurações** botão
3. Selecione Olá **criptografia transparente de dados** opção![][1]
4. Selecione Olá **Off** configuração![][4]
5. Selecione **Salvar**
   ![][5]  

## <a name="encryption-dmvs"></a>DMVs de criptografia
A criptografia pode ser confirmada com hello DMVs a seguir:

* [sys.databases]
* [sys.dm_pdw_nodes_database_encryption_keys]

<!--MSDN references-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx
[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx

<!--Image references-->
[1]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings.png
[2]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-on.png
[3]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save.png
[4]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-off.png
[5]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save2.png

<!--Link references-->
