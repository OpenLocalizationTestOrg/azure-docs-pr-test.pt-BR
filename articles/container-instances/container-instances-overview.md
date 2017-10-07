---
title: "Visão geral de instâncias de contêiner de aaaAzure | Documentos do Azure"
description: "Compreender as Instâncias de Contêiner do Azure"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/20/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: c0662ede1260b15d9841bfc2c3c4cec4c30338d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-instances"></a>Instâncias de Contêiner do Azure

Contêineres rapidamente estão se tornando toopackage de maneira Olá preferido, implantar e gerenciar aplicativos de nuvem. Instâncias de contêiner do Azure oferece hello mais rápido e toorun de maneira mais simples um contêiner no Azure, sem ter que tooprovision todas as máquinas virtuais e sem ter que tooadopt um serviço de nível superior. 

As Instâncias de Contêiner do Azure são uma ótima solução para qualquer cenário que possa ser usado em contêineres isolados, incluindo aplicativos simples, automação de tarefas e criação de trabalhos. Para cenários em que você precisa total orquestração de contêiner, incluindo descoberta do serviço em vários contêineres, dimensionamento automático e atualizações de coordenada de aplicativo, é recomendável Olá [serviço de contêiner do Azure](https://docs.microsoft.com/azure/container-service/).

## <a name="fast-startup-times"></a>Inicialização mais rápida

Os contêineres oferecem vantagens significativas de inicialização em relação às máquinas virtuais. Com instâncias de contêiner do Azure, você pode iniciar um contêiner no Azure em segundos, sem Olá necessidade tooprovision e gerenciar máquinas virtuais.

## <a name="hypervisor-level-security"></a>Segurança em nível de hipervisor

Historicamente, os contêineres ofereciam isolamento de dependência de aplicativo e governança de recursos, mas não eram considerados suficientemente protegidos para uso com vários locatários hostis. Com as Instâncias de Contêiner do Azure, seu aplicativo fica tão isolado em um contêiner quanto ficaria em uma VM.

## <a name="custom-sizes"></a>Tamanhos personalizados

Contêineres são normalmente otimizada toorun apenas um único aplicativo, mas necessidades Olá desses aplicativos podem diferir significativamente. Com as Instâncias de Contêiner do Azure, você pode solicitar exatamente o que precisa em termos de memória e núcleos de CPU. Você paga com base no qual você solicitar cobrado por Olá segundo, para que você pode otimizar eficiente seus gastos com base em suas necessidades.

## <a name="public-ip-connectivity"></a>Conectividade IP pública

Com instâncias de contêiner do Azure, você pode expor seus contêineres toohello diretamente à internet com um endereço IP público. Olá futuras, selecionamos expandir nossa rede recursos tooinclude a integração com redes virtuais, carregar balanceadores e outras partes do núcleo do hello infraestrutura de rede do Azure.

## <a name="persistent-storage"></a>Armazenamento persistente

tooretrieve e persistir o estado de instâncias de contêiner do Azure, nós oferecemos compartilhamentos de arquivos de montagem direta do Azure.

## <a name="linux-and-windows-containers"></a>Contêineres do Windows e do Linux

Com instâncias de contêiner do Azure, você pode agendar as duas janelas e contêineres do Linux com hello mesma API. Simplesmente indicar o tipo de sistema operacional base hello e todo o resto é idêntico.

## <a name="co-scheduled-groups"></a>Grupos coagendados

As Instâncias de Contêiner do Azure dão suporte à programação de grupos com vários contêineres que compartilham um computador host, uma rede local, um armazenamento e um ciclo de vida. Isso permite que você toocombine principal do seu aplicativo com outras pessoas atuando em uma função de suporte, como o registro em log.

## <a name="next-steps"></a>Próximas etapas

Tente implantar tooAzure um contêiner com um único comando usando nosso [guia de início rápido](container-instances-quickstart.md).
