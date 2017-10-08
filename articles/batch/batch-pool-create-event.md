---
title: "AAA \"evento de criação do pool de lote do Azure | Microsoft Docs\""
description: "Referência para o pool do lote criar um evento."
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: tamram
ms.openlocfilehash: ad31251969af553baa21e8c533d8ea95d3eeaf91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="pool-create-event"></a>Evento de criação de pool

 Esse evento é emitido quando um pool é criado. conteúdo de saudação do log Olá irá expor informações gerais sobre o pool de saudação. Observe que, se o tamanho de destino de saudação do pool de saudação for maior do que 0 nós de computação, um evento de início de redimensionamento do pool seguirá imediatamente depois deste evento.

 Olá exemplo a seguir mostra corpo de saudação de um pool de criar o evento de um pool criado usando a propriedade de CloudServiceConfiguration hello.

```
{
    "id": "myPool1",
    "displayName": "Production Pool",
    "vmSize": "Small",
    "cloudServiceConfiguration": {
        "osFamily": "3",
        "targetOsVersion": "*"
    },
    "networkConfiguration": {
        "subnetId": " "
    },
    "resizeTimeout": "300000",
    "targetDedicated": 2,
    "maxTasksPerNode": 1,
    "vmFillType": "Spread",
    "enableAutoScale": false,
    "enableInterNodeCommunication": false,
    "isAutoPool": false
}
```

|Elemento|Tipo|Observações|
|-------------|----------|-----------|
|ID|Cadeia de caracteres|id de saudação do pool de saudação.|
|displayName|Cadeia de caracteres|Olá exibir nome do pool de saudação.|
|vmSize|Cadeia de caracteres|tamanho de saudação de máquinas virtuais de saudação no pool de saudação. Todas as máquinas virtuais em um pool são Olá mesmo tamanho. <br/><br/> Para obter informações sobre tamanhos disponíveis de máquinas virtuais para pools de serviços de nuvem (pools criados com cloudServiceConfiguration), consulte [Tamanhos para serviços de nuvem](http://azure.microsoft.com/documentation/articles/cloud-services-sizes-specs/). O lote dá suporte a todos os tamanhos de VM de serviços de nuvem, exceto `ExtraSmall`.<br/><br/> Para obter informações sobre a VM disponível tamanhos de pools usando imagens de saudação Marketplace de máquinas virtuais (pools criados com virtualMachineConfiguration) consulte [tamanhos das máquinas virtuais](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-sizes/) (Linux) ou [tamanhos para Máquinas virtuais](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) (Windows). O Lote dá suporte a todos os tamanhos de VM do Azure, exceto `STANDARD_A0` e aqueles com armazenamento premium (série `STANDARD_GS`, `STANDARD_DS` e `STANDARD_DSV2`).|
|[cloudServiceConfiguration](#bk_csconf)|Tipo complexo|configuração do serviço de nuvem do Olá para o pool de saudação.|
|[virtualMachineConfiguration](#bk_vmconf)|Tipo complexo|configuração da máquina virtual para o pool de saudação Hello.|
|[networkConfiguration](#bk_netconf)|Tipo complexo|configuração de rede Olá para o pool de saudação.|
|resizeTimeout|Hora|Olá tempo limite de alocação de pool de toohello de nós de computação especificado para a última operação de redimensionamento Olá no pool de saudação.  (saudação inicial quando o pool de saudação é criado contagens como um redimensionamento de dimensionamento).|
|targetDedicated|Int32|número de saudação de nós de computação que são solicitadas para o pool de saudação.|
|enableAutoScale|Bool|Especifica se o tamanho do pool de saudação ajusta automaticamente ao longo do tempo.|
|enableInterNodeCommunication|Bool|Especifica se o pool de saudação está configurado para comunicação direta entre os nós.|
|isAutoPool|Bool|Especifica se o pool de saudação foi criado por meio do mecanismo de pool automático de um trabalho.|
|maxTasksPerNode|Int32|número máximo de saudação de tarefas que podem ser executados simultaneamente em um único nó de computação no pool de saudação.|
|vmFillType|Cadeia de caracteres|Define como Olá serviço em lotes distribui tarefas entre nós de computação no pool de saudação. Os valores válidos são Difundir ou Empacotar.|

###  <a name="bk_csconf"></a> cloudServiceConfiguration

|Nome do elemento|Tipo|Observações|
|------------------|----------|-----------|
|osFamily|Cadeia de caracteres|toobe de família de sistema operacional de convidado do Azure Olá instalado em máquinas virtuais de saudação no pool de saudação.<br /><br /> Os valores possíveis são:<br /><br /> **2** – OS família 2, equivalente tooWindows Server 2008 R2 SP1.<br /><br /> **3** – SOS da família 3, equivalente tooWindows Server 2012.<br /><br /> **4** – sistema operacional família 4, equivalente tooWindows Server 2012 R2.<br /><br /> Para obter mais informações, consulte [Lançamentos do SO convidado do Azure](https://azure.microsoft.com/documentation/articles/cloud-services-guestos-update-matrix/#releases).|
|targetOSVersion|Cadeia de caracteres|Olá toobe de versão de sistema operacional de convidado do Azure instalado em máquinas virtuais de saudação no pool de saudação.<br /><br /> valor padrão de saudação é  **\***  que especifica a versão do sistema operacional mais recente Olá para Olá especificado família.<br /><br /> Para outros valores permitidos, consulte [Lançamentos do SO convidado do Azure](https://azure.microsoft.com/documentation/articles/cloud-services-guestos-update-matrix/#releases).|

###  <a name="bk_vmconf"></a> virtualMachineConfiguration

|Nome do elemento|Tipo|Observações|
|------------------|----------|-----------|
|[imageReference](#bk_imgref)|Tipo complexo|Especifica informações sobre a plataforma de saudação ou toouse de imagem do Marketplace.|
|nodeAgentSKUId|Cadeia de caracteres|Olá SKU do agente de nó de lote Olá provisionado no nó de computação hello.|
|[windowsConfiguration](#bk_winconf)|Tipo complexo|Especifica as configurações de sistema operacional Windows na máquina virtual de saudação. Essa propriedade não deve ser especificado se Olá imageReference está fazendo referência a uma imagem do sistema operacional Linux.|

###  <a name="bk_imgref"></a> imageReference

|Nome do elemento|Tipo|Observações|
|------------------|----------|-----------|
|publicador|Cadeia de caracteres|publicador de saudação da imagem de saudação.|
|oferta|Cadeia de caracteres|oferta de saudação da imagem de saudação.|
|sku|Cadeia de caracteres|Olá SKU da imagem de saudação.|
|version|Cadeia de caracteres|versão de saudação da imagem de saudação.|

###  <a name="bk_winconf"></a> windowsConfiguration

|Nome do elemento|Tipo|Observações|
|------------------|----------|-----------|
|enableAutomaticUpdates|Booliano|Indica se a máquina virtual de saudação está habilitada para atualizações automáticas. Se essa propriedade não for especificada, o valor padrão de saudação é verdadeiro.|

###  <a name="bk_netconf"></a> networkConfiguration

|Nome do elemento|Tipo|Observações|
|------------------|--------------|----------|
|subnetId|Cadeia de caracteres|Especifica o identificador de recurso de saudação do sub-rede Olá na computação do pool que Olá nós são criados.|
