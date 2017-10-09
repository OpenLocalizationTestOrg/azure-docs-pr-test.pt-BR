---
title: "aaaMigrate tooSQL sua solução do Data Warehouse | Microsoft Docs"
description: "Orientação de migração para colocar sua plataforma de SQL Data Warehouse tooAzure solução."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 198365eb-7451-4222-b99c-d1d9ef687f1b
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/27/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: 27b51f15247603f054070f360ede7f24541c0288
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-solution-tooazure-sql-data-warehouse"></a>Migrar tooAzure sua solução SQL Data Warehouse
Veja o que está envolvido na migração de uma tooAzure de solução de banco de dados existente do SQL Data Warehouse. 

## <a name="profile-your-workload"></a>Criar o perfil de sua carga de trabalho
Antes de migrar, você deseja toobe determinado que SQL Data Warehouse é a solução certa Olá para sua carga de trabalho. SQL Data Warehouse é um sistema distribuído projetado tooperform análise dados grandes.  Migrando tooSQL Data Warehouse exige algumas alterações de design que não são muito difíceis toounderstand, mas podem levar algum tempo tooimplement. Se sua empresa exige um data warehouse corporativo, benefícios Olá valem esforço hello. No entanto, se não precisar de capacidade de saudação do SQL Data Warehouse, é mais econômico toouse do SQL Server ou banco de dados do SQL Azure.

Considere o uso do SQL Data Warehouse quando você:
- Tiver um ou mais Terabytes de dados
- Planejar toorun análise em grandes quantidades de dados
- Necessário Olá capacidade tooscale computação e armazenamento 
- Deseja que os custos de toosave pausando recursos de computação quando você não precisa deles.

Não use o SQL Data Warehouse para cargas de trabalho operacionais (OLTP) que têm:
- Alta frequência de leituras e gravações
- Grande quantidade de seleções singleton
- Muitos volumes de inserções de linha única
- Necessidades de processamento linha por linha
- Formatos incompatíveis (JSON, XML)


## <a name="plan-hello-migration"></a>Planejar migração Olá

Depois de ter decidido toomigrate um tooSQL de solução do Data Warehouse existente, é importante tooplan migração de saudação antes de começar. 

Uma meta de planejamento é tooensure seus dados, os esquemas de tabela, e seu código são compatíveis com o SQL Data Warehouse. Há algumas diferenças de compatibilidade toowork em torno entre seu sistema atual e o SQL Data Warehouse. Além disso, migrando grandes quantidades de dados tooAzure leva tempo. Um planejamento cuidadoso acelera obtendo tooAzure seus dados. 

Outro objetivo de planejamento é design toomake tooensure ajustes que sua solução aproveita Olá alto desempenho de consultas que SQL Data Warehouse é projetada tooprovide. Criação de data warehouses para escala apresenta padrões de design diferentes e abordagens tradicionais nem sempre são Olá melhor. Embora você possa fazer alguns ajustes de design após a migração, a fazer alterações mais cedo no processo de saudação economizará tempo mais tarde.

tooperform uma migração bem-sucedida, você precisa toomigrate os esquemas de tabela, seu código e seus dados. Para obter orientação sobre esses tópicos de migração, consulte:

-  [Migrar seus esquemas](sql-data-warehouse-migrate-schema.md)
-  [Migrar seu código](sql-data-warehouse-migrate-code.md)
-  [Migrar seus dados](sql-data-warehouse-migrate-data.md). 

<!--
## Perform hello migration


## Deploy hello solution


## Validate hello migration

-->

## <a name="next-steps"></a>Próximas etapas
Olá CAT (equipe de consultoria do cliente) também tem alguns excelente orientação de SQL Data Warehouse, que eles publicarem por meio de blogs.  Dê uma olhada em seu artigo, [migrando dados tooAzure SQL Data Warehouse na prática] [ Migrating data tooAzure SQL Data Warehouse in practice] para obter orientação adicional sobre a migração.

<!--Image references-->

<!--Article references-->

<!--MSDN references-->

<!--Other Web references-->
[Migrating data tooAzure SQL Data Warehouse in practice]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/
