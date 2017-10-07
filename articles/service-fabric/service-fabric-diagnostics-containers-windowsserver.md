---
title: "aaaAzure diagnóstico e monitoramento de contêineres de malha do serviço | Microsoft Docs"
description: "Saiba como toomonitor e diagnosticar contêineres organizados em Service Fabric do Microsoft Azure com a solução de contêineres do OMS."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/10/2017
ms.author: dekapur
ms.openlocfilehash: cd79111cf78b9d76a60d489bb9953587aa06186d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-windows-server-containers-with-oms"></a>Monitorando contêineres do Windows Server com o OMS

## <a name="oms-containers-solution"></a>Solução de Contêineres do OMS

equipe do Operations Management Suite (OMS) Olá publicou uma solução de contêineres para diagnóstico e monitoramento para contêineres. Junto com suas soluções de malha do serviço, essa solução é uma excelente ferramenta toomonitor contêiner as implantações organizada na malha do serviço. Aqui está um exemplo simples de qual painel Olá na solução de saudação se parece com:

![Painel do OMS básico](./media/service-fabric-diagnostics-containers-windowsserver/oms-containers-dashboard.png)

Ele também coleta diferentes tipos de logs que podem ser consultados na ferramenta de análise de logs do OMS Olá, e pode ser usado toovisualize qualquer métricas ou eventos que está sendo gerados. Olá os tipos de log que são coletados são:

1. ContainerInventory: mostra informações sobre imagens, nome e localização do contêiner
2. ContainerImageInventory: informações sobre imagens implantadas, inclusive IDs ou tamanhos
3. ContainerLog: logs de erros específicos, logs de docker (stdout etc.) e outras entradas
4. ContainerServiceLog: comandos de daemon do docker que foram executados
5. Desempenho: contadores de desempenho incluindo o contêiner de cpu, memória, tráfego de rede, e/s de disco e métricas personalizadas de saudação hospedam máquinas

Este artigo aborda Olá etapas necessárias tooset o contêiner de monitoramento para seu cluster. toolearn mais sobre solução de contêineres do OMS, confira seus [documentação](../log-analytics/log-analytics-containers.md).

## <a name="1-set-up-a-service-fabric-cluster"></a>1. Configurar um cluster do Service Fabric

Criar um cluster usando o modelo do Azure Resource Manager Olá encontrado [aqui](https://github.com/dkkapur/Service-Fabric/tree/master/ARM%20Templates/SF%20OMS%20Sample). Certifique-se de que tooadd um nome exclusivo do espaço de trabalho do OMS. Esse modelo também padrões toodeploying criar um cluster na visualização de saudação do Service Fabric (v255.255), que significa que ele não pode ser usado na produção e não pode ser atualizado tooa outra versão do Service Fabric. Se você decidir toouse este modelo para longo prazo ou usar, altere o número de versão estável de tooa Olá versão de produção.

Depois de configurar o cluster hello, confirme que você instalou o certificado apropriado hello e verifique se que você está tooconnect capaz de toohello cluster.

Confirme se o grupo de recursos é configurado corretamente por título toohello [portal do Azure](https://portal.azure.com/) e Localizando a implantação de saudação. grupo de recursos de saudação deve conter todos os recursos de malha do serviço Olá e também tem uma solução de análise de Log, bem como uma solução de malha do serviço.

Para modificar um cluster existente do Service Fabric:
* Confirme se a opção diagnóstico está habilitado (se não, habilitá-la por meio de [atualizando o conjunto de escala de máquina virtual Olá](/rest/api/virtualmachinescalesets/create-or-update-a-set))
* Adicionar um espaço de trabalho do OMS, criando uma solução de "Análise de malha do serviço" via hello Azure Marketplace
* Editar fontes de dados de saudação de saudação do Service Fabric solução toopick backup de dados de tabelas de armazenamento do Azure apropriadas hello (definidos pelo WAD) em Olá grupo de recursos que Olá cluster está em
* Adicionar agente hello como um [conjunto de escalas da máquina virtual extensão toohello](/powershell/module/azurerm.compute/add-azurermvmssextension) por meio do PowerShell ou atualizando o conjunto de escala de máquina virtual de saudação (mesmo link acima, modelo de Gerenciador de recursos de saudação toomodify)

## <a name="2-deploy-a-container"></a>2. Implantar um contêiner

Depois que o cluster hello está pronto e confirmar que você pode acessá-lo, implante um contêiner tooit. Se você escolher versão de visualização de saudação toouse conforme definido pelo modelo de saudação, você também pode explorar docker novo do Service Fabric compor a funcionalidade. Tenha em mente que Olá a primeira vez que uma imagem de contêiner é cluster tooa implantado, ele entra em várias imagens de saudação toodownload minutos dependendo de seu tamanho.

## <a name="3-add-hello-containers-solution"></a>3. Adicionar solução de contêineres de saudação

No hello portal do Azure, crie um recurso de contêineres (em Olá monitoramento + gerenciamento categoria) através do Azure Marketplace. 

![Adicionando a solução de Contêineres](./media/service-fabric-diagnostics-containers-windowsserver/containers-solution.png)

Na etapa de criação de hello, ele solicita um espaço de trabalho do OMS. Selecione Olá que foi criado com a implantação de saudação acima. Esta etapa adiciona uma solução de contêineres dentro de seu espaço de trabalho do OMS e será detectada automaticamente pelo agente do OMS Olá implantado pelo modelo de saudação. Agente de saudação começará a coletar dados sobre processos de contêineres de saudação em cluster hello e em cerca de 10 a 15 minutos, você deve ver a solução de saudação destaque com dados como imagem de saudação do painel de saudação acima.

## <a name="4-next-steps"></a>4. Próximas etapas

O OMS oferece várias ferramentas em Olá toomake de espaço de trabalho se mais útil para você. Explore Olá opções toocustomize Olá solução tooyour necessidades a seguir:
- Obter trazido com hello [pesquisa e consulta de log](../log-analytics/log-analytics-log-searches.md) recursos oferecidos como parte da análise de Log
- Configurar Olá OMS agente toopick backup contadores de desempenho específicos (vá toohello espaço de trabalho inicial > Configurações > dados > contadores de desempenho do Windows)
- Configurar o OMS tooset [alerta automatizado](../log-analytics/log-analytics-alerts.md) tooaid regras na detecção e diagnóstico
