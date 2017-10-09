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
# <a name="sql-data-warehouse----downlevel-clients-support-for-auditing-and-dynamic-data-masking"></a>SQL Data Warehouse - Suporte de versão anterior a clientes para auditoria e Máscara de Dados Dinâmicos
[Auditoria](sql-data-warehouse-auditing-overview.md) funciona com clientes SQL que oferecem suporte ao redirecionamento de TDS.

Qualquer cliente que implemente o protocolo TDS 7.4 também deve dar suporte a redirecionamento. Exceções toothis incluem JDBC 4.0 no qual recurso de redirecionamento Olá não é totalmente compatível e tediosas para Node. js em que o redirecionamento não foi implementado.

Para clientes de nível inferior"", ou seja, que suporte o protocolo TDS versão 7.3 e abaixo - Olá FQDN do servidor na cadeia de caracteres de conexão Olá deve ser modificado:

FQDN do servidor original na cadeia de caracteres de conexão Olá: <*nome do servidor*>. t

FQDN do servidor modificado na cadeia de caracteres de conexão de saudação: <*nome do servidor*>. Database. **seguro**. windows.net

Uma lista parcial de "Clientes de versão anterior" inclui:

* .NET 4.0 e inferior,
* ODBC 10.0 e inferior.
* JDBC (enquanto JDBC suporta TDS 7.4, Olá recurso de redirecionamento do protocolo TDS não tem suporte total)
* Tedious (para o Node.JS)

**Comentário:** Olá acima modificação FQDN do servidor pode ser útil também para aplicar uma política de auditoria de nível de servidor do SQL sem a necessidade de uma configuração de etapa em cada banco de dados (temporário mitigação).     

