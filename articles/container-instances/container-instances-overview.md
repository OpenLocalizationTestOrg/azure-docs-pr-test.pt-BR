---
title: "Visão geral das Instâncias de Contêiner do Azure"
description: "Compreender as Instâncias de Contêiner do Azure"
services: container-instances
author: seanmck
manager: timlt
ms.service: container-instances
ms.topic: overview
ms.date: 01/02/2018
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 01e539856adbdcf02dc4e49087a3ab71b328db5a
ms.sourcegitcommit: 3cdc82a5561abe564c318bd12986df63fc980a5a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/05/2018
---
# <a name="azure-container-instances"></a>Instâncias de Contêiner do Azure

Os contêineres estão se tornando o modo preferido para empacotar, implantar e gerenciar aplicativos de nuvem. As Instâncias de Contêiner do Azure oferecem a maneira mais rápida e simples para executar um contêiner no Azure, sem a necessidade de provisionar máquinas virtuais nem adotar um serviço de nível superior.

As Instâncias de Contêiner do Azure são uma ótima solução para qualquer cenário que possa ser usado em contêineres isolados, incluindo aplicativos simples, automação de tarefas e criação de trabalhos. Para cenários em que você precisa de orquestração de contêineres completa, incluindo descoberta do serviço em vários contêineres, dimensionamento automático e atualizações de aplicativo coordenadas, recomendamos o [AKS (Serviço de Contêiner do Azure)](../aks/index.yml).

## <a name="fast-startup-times"></a>Inicialização mais rápida

Os contêineres oferecem vantagens significativas de inicialização em relação às máquinas virtuais. Com as Instâncias de Contêiner do Azure, você pode iniciar um contêiner no Azure em segundos, sem a necessidade de provisionar nem gerenciar máquinas virtuais.

## <a name="hypervisor-level-security"></a>Segurança em nível de hipervisor

Historicamente, os contêineres ofereciam isolamento de dependência de aplicativo e governança de recursos, mas não eram considerados suficientemente protegidos para uso com vários locatários hostis. Com as Instâncias de Contêiner do Azure, seu aplicativo fica tão isolado em um contêiner quanto ficaria em uma VM.

## <a name="custom-sizes"></a>Tamanhos personalizados

Os contêineres normalmente são otimizados para executar apenas um único aplicativo, mas as necessidades exatas desses aplicativos podem variar significativamente. Com as Instâncias de Contêiner do Azure, você pode solicitar exatamente o que precisa em termos de memória e núcleos de CPU. Você paga com base no que solicitar, cobrado por segundo, para poder otimizar seus gastos eficientemente com base em suas necessidades.

## <a name="public-ip-connectivity"></a>Conectividade IP pública

Com as Instâncias de Contêiner do Azure, você pode expor seus contêineres diretamente à Internet com um endereço IP público. No futuro, vamos expandir nossos recursos de rede para incluir a integração com redes virtuais, balanceadores de carga e outras partes principais da infraestrutura de rede do Azure.

## <a name="persistent-storage"></a>Armazenamento persistente

Para recuperar e persistir estados com as Instâncias de Contêiner do Azure, nós oferecemos a [montagem direta de compartilhamentos de arquivos do Azure](container-instances-mounting-azure-files-volume.md).

## <a name="linux-and-windows-containers"></a>Contêineres do Windows e do Linux

Com as Instâncias de Contêiner do Azure, você pode agendar contêineres do Windows e do Linux com a mesma API. Basta especificar o tipo de sistema operacional ao criar seus [grupos de contêiner](container-instances-container-groups.md).

Alguns recursos são atualmente restritos a contêineres do Linux. Enquanto estamos trabalhando para trazer todos os recursos para contêineres do Windows, você pode encontrar as diferenças atuais de plataforma em [Cotas e disponibilidade de região para Instâncias de Contêiner do Azure](container-instances-quotas.md).

## <a name="co-scheduled-groups"></a>Grupos coagendados

As Instâncias de Contêiner do Azure são compatíveis com a programação de [grupos com vários contêineres](container-instances-container-groups.md) que compartilham um computador host, uma rede local, um armazenamento e um ciclo de vida. Isso permite que você combine seu aplicativo principal com outros que atuam em uma função de suporte, como o registro em log.

## <a name="next-steps"></a>Próximas etapas

Tente implantar um contêiner no Azure com um único comando usando nosso [guia de início rápido](container-instances-quickstart.md).