---
title: toowork aaaHow com fontes de dados de 'dados grandes' | Microsoft Docs
description: "Padrões de realce tooarticle como para usar o catálogo de dados do Azure com fontes de dados de 'dados grandes', incluindo o armazenamento de BLOBs do Azure, Azure Data Lake e Hadoop HDFS."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 626d1568-0780-4726-bad1-9c5000c6b31a
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: e478f71f26744975a7d7e1784b74bf50b424cf65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toowork-with-big-data-sources-in-azure-data-catalog"></a>Como fontes de toowork com dados grandes no catálogo de dados do Azure
## <a name="introduction"></a>Introdução
**Catálogo de Dados do Microsoft Azure** é um serviço de nuvem totalmente gerenciado que atua como um sistema de registro e sistema de descoberta em fontes de dados da empresa. É tudo sobre ajudando as pessoas a descobrir, entender e usar fontes de dados e ajudando as organizações tooget mais valor de suas fontes de dados existentes, incluindo dados grandes.

**Catálogo de dados do Azure** suporta Olá registro de blobs de armazenamento de Blog do Azure, diretórios, bem como Hadoop HDFS arquivos e diretórios. a natureza semi-estruturados Olá dessas fontes de dados fornece uma grande flexibilidade. No entanto, tooget Olá máximo de registrando-os com **Data Catalog do Azure**, os usuários devem considerar como fontes de dados de saudação são organizados.

## <a name="directories-as-logical-data-sets"></a>Diretórios como conjuntos de dados lógicos
Um padrão comum para a organização de grandes fontes de dados é tootreat diretórios como conjuntos de dados lógicos. Diretórios de alto nível são toodefine usado um conjunto de dados, enquanto as subpastas definem partições e arquivos Olá contiverem armazenam dados de saudação em si.

Um exemplo desse padrão pode ser:

    \vehicle_maintenance_events
        \2013
        \2014
        \2015
            \01
                \2015-01-trailer01.csv
                \2015-01-trailer92.csv
                \2015-01-canister9635.csv
                ...
    \location_tracking_events
        \2013
        ...

Neste exemplo, vehicle_maintenance_events e location_tracking_events representam conjuntos de dados lógicos. Cada uma dessas pastas contém arquivos de dados organizados por ano e mês em subpastas. Cada uma dessas pastas pode conter, potencialmente, centenas ou milhares de arquivos.

Nesse padrão, registrar arquivos individuais com o **Catálogo de Dados do Azure** provavelmente não faz sentido. Em vez disso, registre diretórios Olá que representam os conjuntos de dados de saudação ser significativo toohello usuários trabalhando com dados de saudação.

## <a name="reference-data-files"></a>Arquivos de dados de referência
Um padrão de complementar é toostore conjuntos de dados de referência como arquivos individuais. Esses conjuntos de dados pode ser pensados como lado de 'pequena' hello de big data e são geralmente toodimensions semelhante em um modelo de dados analíticos. Arquivos de dados de referência contêm registros de contexto tooprovide usado para bulk Olá Olá dos arquivos de dados armazenados em outro lugar no repositório de dados grande hello.

Um exemplo desse padrão pode ser:

    \vehicles.csv
    \maintenance_facilities.csv
    \maintenance_types.csv

Quando um cientista de dados ou analista está trabalhando com dados de saudação contidos nas estruturas de diretório maior hello, dados Olá nesses arquivos de referência podem ser usado tooprovide informações mais detalhadas para entidades que são chamados tooonly por nome ou ID de dados maior Olá conjunto.

Nesse padrão, isso faz sentido tooregister arquivos de dados de referência individual Olá com **Data Catalog do Azure**. Cada arquivo representa um conjunto de dados e cada um deles pode ser anotado e descoberto individualmente.

## <a name="alternate-patterns"></a>Padrões alternativos
padrões descritos em Olá anterior seção Hello são apenas duas maneiras possíveis de que um repositório de dados grandes pode ser organizado, mas cada implementação é diferente. Independentemente de como as fontes de dados são estruturadas, ao registrar fontes de dados grandes com **Data Catalog do Azure**, enfocam registrando Olá arquivos e diretórios representam os conjuntos de dados de saudação do valor tooothers dentro de sua organização. Registrar todos os arquivos e diretórios pode sobrecarregar o catálogo hello, tornando mais difícil para os usuários toofind que precisam.

## <a name="summary"></a>Resumo
Registrar fontes de dados com **Data Catalog do Azure** torna mais fácil toodiscover e entender. Registrando e anotar Olá dados grandes arquivos e diretórios representam os conjuntos de dados lógicos, você pode ajudar os usuários a localizar e utilizar Olá grandes fontes de dados que precisam.
