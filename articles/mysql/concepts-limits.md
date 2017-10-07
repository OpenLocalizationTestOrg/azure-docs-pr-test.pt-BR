---
title: aaaLimitations no banco de dados do Azure para MySQL | Microsoft Docs
description: "Descreve as limitações de visualização no Banco de Dados para MySQL."
services: mysql
author: jasonh
ms.author: kamathsun
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 9c877c592bf640f62182d8761c9c51363882d706
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-in-azure-database-for-mysql-preview"></a>Limitações no Banco de Dados do Azure para MySQL (Visualização)
saudação de banco de dados do Azure para o serviço MySQL está em visualização pública. Olá seções a seguir descrevem funcionais limites no serviço de banco de dados de saudação e capacidade.

## <a name="service-tier-maximums"></a>Limites máximos da camada de serviço
O Banco de Dados do Azure para MySQL tem vários níveis de serviço que você pode escolher ao criar um servidor. Para saber mais, confira [Entenda o que está disponível em cada camada de serviço](concepts-service-tiers.md).  

Há um número máximo de conexões, as unidades de computação e armazenamento em cada camada de serviço durante a visualização de serviço hello, da seguinte maneira: 

|                            |                   |
| :------------------------- | :---------------- |
| **Conexões máximas**        |                   |
| 50 unidades de computação básica     | 50 conexões    |
| 100 unidades de computação básica    | 100 conexões   |
| 100 unidades de computação standard | 200 conexões   |
| 200 unidades de computação standard | 300 conexões   |
| 400 unidades de computação standard | 400 conexões   |
| 800 unidades de computação standard | 500 conexões   |
| **Unidades de computação máxima**      |                   |
| Camada de serviço Básica         | 100 Unidades de computação |
| Camada de serviço Standard      | 800 Unidades de computação |
| **Armazenamento Máximo**            |                   |
| Camada de serviço Básica         | 1 TB              |
| Camada de serviço Standard      | 1 TB              |

Quando muitas conexões são alcançadas, você pode receber Olá erro a seguir:
> ERRO 1040 (08004): número excessivo de conexões

## <a name="preview-functional-limitations"></a>Limitações funcionais de visualização:
### <a name="scale-operations"></a>Operações de dimensionamento:
1.  Não há suporte para o dimensionamento dinâmico de servidores por meio de camadas de serviço. Ou seja, alternando entre as camadas de serviço Básico e Standard.
2.  Não há suporte para o aumento sob demanda dinâmico de armazenamento no servidor criado previamente.
3.  Não há suporte para diminuir o tamanho de armazenamento do servidor.

### <a name="server-version-upgrades"></a>Atualizações da versão do servidor:
- Não há suporte para a migração automatizada entre versões de mecanismo de banco de dados principal.

### <a name="subscription-management"></a>Gerenciamento de assinaturas:
- Não há suporte para mover dinamicamente servidores criados previamente entre a assinatura e o grupo de recursos.

### <a name="point-in-time-restore"></a>Recuperação pontual:
1.  Não é permitido restaurar toodifferent da camada de serviço e/ou tamanho de unidades de computação e armazenamento.
2.  Não há suporte para restaurar um servidor eliminado.

## <a name="next-steps"></a>Próximas etapas:
[O que está disponível em cada camada de serviço](concepts-service-tiers.md)
[Versões de Banco de Dados MySQL com suporte](concepts-supported-versions.md)
