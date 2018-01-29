---
title: "Política de manutenção de pilha do Azure | Microsoft Docs"
description: "Saiba mais sobre a manutenção de política e como manter um sistema integrado em um estado com suporte a pilha do Azure."
services: azure-stack
documentationcenter: 
author: mattbriggs
manager: femila
editor: 
ms.assetid: caac3d2f-11cc-4ff2-82d6-52b58fee4c39
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/25/2017
ms.author: mabrigg
ms.openlocfilehash: 498d0cdc3eac25b8efc7339e48381a4d167c0c7b
ms.sourcegitcommit: a5f16c1e2e0573204581c072cf7d237745ff98dc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2017
---
# <a name="azure-stack-servicing-policy"></a>Política de manutenção de pilha do Azure

*Aplica-se a: sistemas integrados de pilha do Azure*

Este artigo descreve a política de serviço para sistemas de pilha do Azure integradas, e que você deve fazer para manter o sistema em um estado com suporte. 

## <a name="update-package-types"></a>Tipos de pacote de atualização

Há dois tipos de pacotes de atualização para os sistemas integrados; As atualizações de software e atualizações que são específicas para o fornecedor do hardware fabricante (OEM), como drivers e firmware. Essas atualizações são entregues como pacotes de atualização separados pilha do Azure e são gerenciadas de forma independente.

- **As atualizações de software**. A Microsoft é responsável para o ciclo de vida de serviço de ponta a ponta para os pacotes de atualização de software da Microsoft. Esses pacotes podem incluir as últimas atualizações de segurança do Windows Server, atualizações de segurança não e atualizações de recurso da pilha do Azure. Você pode baixar pacotes de atualização essas políticas diretamente da Microsoft.
- **Atualizações de fornecido pelo fornecedor de hardware de OEM**. Parceiros de hardware de pilha do Azure são responsáveis por de ponta a ponta manutenção do ciclo de vida (incluindo orientação) para o firmware relacionado ao hardware e os pacotes de atualização de driver. Além disso, os parceiros de hardware de pilha do Azure possuam e mantêm orientação de hardware no host de ciclo de vida de hardware e software de todos os. O fornecedor do hardware OEM hospeda esses pacotes em seu próprio site de download de atualização.

## <a name="update-package-release-cadence"></a>Cadência de lançamento do pacote de atualização

A Microsoft espera liberar os pacotes de atualização de software em um ritmo mensal. No entanto, é possível ter várias ou nenhuma versões de atualização em um mês. Fornecedores de hardware de OEM liberar suas atualizações em uma base conforme necessário.

Um pacote de atualização da Microsoft tem a seguinte convenção de nomenclatura para ajudá-lo a identificar facilmente a data de liberação:

*MajorProductVersion.MinorProductVersion.YYMMDD.BuildNumber*

Por exemplo, uma atualização de software da Microsoft lançada em 15 de junho de 2017 teria a versão "1.0.170615.1".

## <a name="keep-your-system-under-support"></a>Manter o sistema com suporte

Para receber suporte para o seu sistema, você deve manter a pilha do Azure atualizada dentro de um intervalo de tempo específico. Nossa política de adiamento de atualizações de software da Microsoft é três meses. Se seu sistema estiver desatualizado mais de três meses, são consideradas fora de conformidade. Você deve atualizar o sistema para pelo menos o suporte mínimo de versão para receber suporte. 

Pacotes de atualização de software Microsoft são não cumulativas e requerem que o pacote de atualização anterior como um pré-requisito. Se você optar por adiar uma ou mais atualizações, considere o tempo de execução geral, se você deseja obter a versão mais recente.

A tabela a seguir mostra as versões de pacote de atualização de exemplo, seus pré-requisitos e a versão mínima com suporte que o sistema deve estar no manter o suporte. A tabela se baseia na versão inicial do sistemas de pilha do Azure integrado (compilação 1708), com a primeira versão de pacote de atualização (1709) em setembro de 2017. 

| Pacote de atualização mais recente (*exemplo*) | Pré-requisito | Versão mínima com suporte |
| -- | -- | -- |
| 1709 | Criar 1708 | N/D |
| 1710 | 1709 | N/D |
| 1711 | 1710 | N/D |
| 1712 | 1711 | 1709 |
| 1801 | 1712 | 1710 |
| 1802 | 1801 | 1711 |
| 1803 | 1802 | 1712 |
| 1804 | 1803 | 1801 |
| | | 

## <a name="next-steps"></a>Próximas etapas

- [Gerenciar atualizações na pilha do Azure](azure-stack-updates.md)


