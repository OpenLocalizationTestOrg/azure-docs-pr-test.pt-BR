---
title: CLI do Azure Service Fabric - sfctl is | Microsoft Docs
description: Descreve os comandos do sfctl is da CLI do Service Fabric.
services: service-fabric
documentationcenter: na
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: cli
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 12/22/2017
ms.author: ryanwi
ms.openlocfilehash: b611a447dd6669a09ca16c816de74acd7f3e8c7e
ms.sourcegitcommit: f1c1789f2f2502d683afaf5a2f46cc548c0dea50
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="sfctl-is"></a>sfctl is
Consultar e enviar comandos para o serviço de infraestrutura.

## <a name="commands"></a>Comandos

|Get-Help|DESCRIÇÃO|
| --- | --- |
|    command| Invoca um comando administrativo na instância do serviço de infraestrutura especificada.|
|    query  | Invoca uma consulta de somente leitura na instância do serviço de infraestrutura especificada.|


## <a name="sfctl-is-command"></a>comando sfctl is
Invoca um comando administrativo na instância do serviço de infraestrutura especificada.

Para clusters que têm uma ou mais instâncias do serviço de infraestrutura configurado, essa API fornece uma maneira para enviar comandos de infraestrutura específicos para uma determinada instância do serviço de infraestrutura. Comandos disponíveis e seus formatos de resposta correspondentes variam de acordo com a infraestrutura na qual o cluster está em execução. Essa API dá suporte à plataforma do Service Fabric; não é destinada a ser usada diretamente a partir do seu código. .

### <a name="arguments"></a>Argumentos

|Argumento|DESCRIÇÃO|
| --- | --- |
| --comando [obrigatório]| O texto do comando a ser invocado. O conteúdo do comando é específico da infraestrutura.  Padrão: comando is.|
| --id do serviço     | A identidade do serviço de infraestrutura. É o nome completo do serviço de infraestrutura sem o esquema de URI "fabric:". Esse parâmetro é necessário somente para clusters que têm mais de uma instância do serviço de infraestrutura em execução.|
| --timeout -t     | Tempo limite do servidor em segundos.  Padrão: 60.|

### <a name="global-arguments"></a>Argumentos globais

|Argumento|DESCRIÇÃO|
| --- | --- |
| --debug          | Aumentar o nível de detalhes do log para mostrar todos os logs de depuração.|
| --help -h        | Mostrar esta mensagem de ajuda e sair.|
| --output -o      | O formato da saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.|
| --query          | Cadeia de caracteres de consulta JMESPath. Para saber mais e obter exemplos, consulte http://jmespath.org/.|
| --verbose        | Aumentar o nível de detalhes do log. Use --debug para logs de depuração completos.|

## <a name="sfctl-is-query"></a>consulta sfctl is
Invoca uma consulta de somente leitura na instância do serviço de infraestrutura especificada.

Para clusters que têm uma ou mais instâncias do serviço de infraestrutura configurado, essa API fornece uma maneira para enviar consultas de infraestrutura específicos para uma determinada instância do serviço de infraestrutura. Comandos disponíveis e seus formatos de resposta correspondentes variam de acordo com a infraestrutura na qual o cluster está em execução. Essa API dá suporte à plataforma do Service Fabric; não é destinada a ser usada diretamente a partir do seu código.

### <a name="arguments"></a>Argumentos

|Argumento|DESCRIÇÃO|
| --- | --- |
| --comando [obrigatório]| O texto do comando a ser invocado. O conteúdo do comando é específico da infraestrutura.  Padrão: consulta is.|
| --id do serviço     | A identidade do serviço de infraestrutura. É o nome completo do serviço de infraestrutura sem o esquema de URI "fabric:". Esse parâmetro é necessário somente para clusters que têm mais de uma instância do serviço de infraestrutura em execução.|
| --timeout -t     | Tempo limite do servidor em segundos.  Padrão: 60.|

### <a name="global-arguments"></a>Argumentos globais

|Argumento|DESCRIÇÃO|
| --- | --- |
| --debug          | Aumentar o nível de detalhes do log para mostrar todos os logs de depuração.|
| --help -h        | Mostrar esta mensagem de ajuda e sair.|
| --output -o      | O formato da saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.|
| --query          | Cadeia de caracteres de consulta JMESPath. Para mais informações, consulte http://jmespath.org/.|
| --verbose        | Aumentar o nível de detalhes do log. Use --debug para logs de depuração completos.|

## <a name="next-steps"></a>Próximas etapas
- [Configurar](service-fabric-cli.md) a CLI do Service Fabric.
- Saiba como usar a CLI do Service Fabric usando os [scripts de exemplo](/azure/service-fabric/scripts/sfctl-upgrade-application).