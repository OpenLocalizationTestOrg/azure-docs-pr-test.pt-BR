---
title: "Limitações no Banco de Dados do Azure para PostgreSQL | Microsoft Docs"
description: "Descreve as limitações no Banco de Dados do Azure para PostgreSQL."
services: postgresql
author: kamathsun
ms.author: sukamat
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.topic: article
ms.date: 12/04/2017
ms.openlocfilehash: 6dbed1a834d74047178a9f996683d65520047e66
ms.sourcegitcommit: 0e1c4b925c778de4924c4985504a1791b8330c71
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2018
---
# <a name="limitations-in-azure-database-for-postgresql"></a>Limitações no Banco de Dados do Azure para PostgreSQL
O Banco de Dados do Azure para o serviço PostgreSQL está em visualização pública. As seções a seguir descrevem a capacidade e os limites funcionais no serviço de banco de dados.

## <a name="service-tier-maximums"></a>Limites máximos da camada de serviço
O Banco de Dados do Azure para PostgreSQL tem vários níveis de serviço que você pode escolher ao criar um servidor. Para saber mais, confira [Entenda o que está disponível em cada camada de serviço](concepts-service-tiers.md).  

Há um número máximo de conexões, unidades de computação e armazenamento em cada camada de serviço durante a visualização do serviço, da seguinte maneira: 

| | |
| :------------------------- | :---------------- |
| **Conexões máximas**        |                   |
| 50 unidades de computação básica     | 55 conexões    |
| 100 unidades de computação básica    | 105 conexões   |
| 100 unidades de computação standard | 150 conexões   |
| 200 unidades de computação standard | 250 conexões   |
| 400 unidades de computação standard | 480 conexões   |
| 800 unidades de computação standard | 950 conexões   |
| **Unidades de computação máxima**      |                   |
| Camada de serviço Básica         | 100 Unidades de computação |
| Camada de serviço Standard      | 800 Unidades de computação |
| **Armazenamento Máximo**            |                   |
| Camada de serviço Básica         | 1 TB              |
| Camada de serviço Standard      | 1 TB              |

O sistema do Azure exige cinco conexões para monitorar o Banco de Dados do Azure para o servidor PostgreSQL. Quando um número excessivo de conexões for atingido, você receberá o seguinte erro:
> FATAL: já existem muitos clientes


## <a name="preview-functional-limitations"></a>Limitações funcionais da versão prévia
### <a name="scale-operations"></a>Operações de dimensionamento
1.  Não há suporte para o dimensionamento dinâmico de servidores por meio de camadas de serviço. Ou seja, alternando entre as camadas de serviço Básico e Standard.
2.  Não há suporte para o aumento sob demanda dinâmico de armazenamento no servidor criado previamente.
3.  Não há suporte para diminuir o tamanho de armazenamento do servidor.

### <a name="server-version-upgrades"></a>Upgrade da versão do servidor
- Não há suporte para a migração automatizada entre versões de mecanismo de banco de dados principal.

### <a name="subscription-management"></a>Gerenciamento de assinaturas
- Não há suporte para mover dinamicamente servidores criados previamente entre a assinatura e o grupo de recursos.

### <a name="point-in-time-restore"></a>Restauração pontual
1.  Não é permitido restaurar para a camada de serviço diferente e/ou Unidades de computação e Tamanho do armazenamento.
2.  Não há suporte para restaurar um servidor eliminado.

## <a name="next-steps"></a>Próximas etapas
- Entenda [O que está disponível em cada tipo de preço](concepts-service-tiers.md)
- Entenda as [Versões de banco de dados PostgreSQL com suporte](concepts-supported-versions.md)
- Veja [Como fazer backup e restaurar um servidor no Banco de Dados do Azure para PostgreSQL usando o Portal do Azure](howto-restore-server-portal.md)
