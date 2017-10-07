---
title: "Visão geral de tempo de execução de funções de aaaAzure | Microsoft Docs"
description: "Visão geral da saudação visualização de tempo de execução de funções do Azure"
services: functions
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 05/08/2017
ms.author: anwestg
ms.openlocfilehash: 8ce3e5037731d499c330b395c89c90109d18d65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-runtime-overview"></a>Visão geral do Azure Functions Runtime

saudação de tempo de execução de funções do Azure fornece uma nova maneira você tootake vantagem de manter a simplicidade hello e flexibilidade de funções do Azure Olá local do modelo de programação. Mesmo baseia Olá abra raízes de origem como funções do Azure, o tempo de execução de funções do Azure é implantado no local tooprovide um desenvolvimento quase idêntico experiência como serviço de nuvem hello.

![Portal de visualização do Azure Functions Runtime][1]

saudação de tempo de execução de funções do Azure fornece uma maneira para você tooexperience Azure funções antes de confirmar toohello nuvem. Dessa forma, ativos de código Olá que compilar podem, em seguida, ser executados com você toohello nuvem quando você migrar.  saudação de tempo de execução também abre novas opções para você, como o uso de capacidade de computação de reposição de saudação dos processos de lote local computadores toorun durante a noite. Você também pode usar dispositivos em sua organização tooconditionally enviar tooother sistemas de dados locais e na nuvem de saudação.

saudação de tempo de execução de funções do Azure consiste em duas partes:
* Função de Gerenciamento do Azure Functions Runtime
* Função de Trabalho do Azure Functions Runtime

## <a name="azure-functions-management-role"></a>Função de Gerenciamento do Azure Functions

Olá função de gerenciamento de funções do Azure fornece um host para o gerenciamento de saudação de sua funções no local. Esta função executa Olá tarefas a seguir:

* Hospedagem de saudação funções Portal de gerenciamento, que é Olá Olá mesmo que você vê no hello [portal do Azure](https://portal.azure.com). Isso permite que você desenvolver suas funções no mesmo Olá maneira como você faria no hello portal do Azure.
* Distribuição de funções por vários trabalhadores do Functions.
* Fornecimento de um ponto de extremidade de publicação, para que você possa publicar suas funções diretamente do Microsoft Visual Studio.

## <a name="azure-functions-worker-role"></a>Função de Trabalho do Azure Functions

Funções de trabalho Hello Azure funções são implantadas nos contêineres do Windows e é onde o código de função é executado.  Você pode implantar várias Funções de Trabalho em toda sua organização, e essa é uma maneira importante com a qual os clientes podem usar o poder da computação sobressalente.

## <a name="minimum-requirements"></a>Requisitos mínimos

tooget iniciado com hello tempo de execução de funções do Azure deve ter um computador com **Windows Server 2016 ou Windows 10 criadores Update** com acesso tooa **do SQL Server** instância.

## <a name="next-steps"></a>Próximas etapas

Instalar Olá [visualização de tempo de execução de funções do Azure](https://aka.ms/azafr)

<!--Image references-->
[1]: ./media/functions-runtime-overview/AzureFunctionsRuntime_Portal.png
