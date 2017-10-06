---
title: "aaaRules de nomeação de entidades do Azure Data Factory | Microsoft Docs"
description: Descreve as regras de nomenclatura para entidades de Data Factory.
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: bc5e801d-0b3b-48ec-9501-bb4146ea17f1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 98c5fc5fc932b72b65894afad438b4dc321c8aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---naming-rules"></a>Azure Data Factory - regras de nomenclatura
Olá, a tabela a seguir fornece as regras de nomenclatura para artefatos de fábrica de dados.

| Nome | Exclusividade do nome | Verificações de validação |
|:--- |:--- |:--- |
| Data Factory |Exclusivo em todo o Microsoft Azure. Os nomes diferenciam maiusculas de minúsculas, isto é, `MyDF` e `mydf` consulte toohello mesma fábrica de dados. |<ul><li>Cada fábrica de dados é tooexactly associado uma assinatura do Azure.</li><li>Nomes de objeto devem começar com uma letra ou um número e podem conter apenas letras, números e caracteres de traço (-) hello.</li><li>Cada caractere traço (-) deve ser imediatamente precedido e seguido por uma letra ou um número. Não há permissão para traços consecutivos em nomes de contêiner.</li><li>O nome pode ter de 3 a 63 caracteres.</li></ul> |
| Serviços/tabelas/pipelines vinculados |Exclusivo em um mesmo data factory. Os nomes não diferenciam maiúsculas de minúsculas. |<ul><li>Número máximo de caracteres em um nome de tabela: 260.</li><li>Os nomes de objetos devem começar com uma letra, um número ou um sublinhado (_).</li><li>Os seguintes caracteres não são permitidos: “.”, “+”, “?”, “/”, “<”, ”>”,”*”,”%”,”&”,”:”,”\\”</li></ul> |
| Grupo de recursos |Exclusivo em todo o Microsoft Azure. Os nomes não diferenciam maiúsculas de minúsculas. |<ul><li>Número máximo de caracteres: 1000.</li><li>Nome pode conter letras, dígitos e Olá seguintes caracteres: "-", "_",","e"."</li></ul> |

