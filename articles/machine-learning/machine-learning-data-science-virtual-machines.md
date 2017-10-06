---
title: "aaaProvision máquinas virtuais do Azure dados ciência como servidores de bloco de anotações do IPython | Microsoft Docs"
description: "Configure uma Máquina Virtual de Ciência de Dados como um Servidor de Bloco de Anotações do IPython com ferramentas de suporte."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 95e1fa87-794a-4d03-80a4-af4f3f3ac31e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: bradsev
ms.openlocfilehash: 7c0abcbcb822918332f76a9f16690a72b90f4b3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="provision-azure-data-science-virtual-machines-as-ipython-notebook-servers"></a>Provisionar Máquinas Virtuais de Ciência de Dados do Azure como Servidores de Bloco de Anotações do IPython
As instruções são fornecidas aqui que descrevem como tooset uma VM do Azure e uma VM do Azure com o serviço do SQL, como servidores de bloco de anotações do IPython. máquina de virtual do Windows Hello está configurada com ferramentas como bloco de anotações do IPython, o Azure Storage Explorer e o AzCopy, bem como outros utilitários que são úteis para projetos de ciência de dados de suporte. Gerenciador de armazenamento do Azure e AzCopy, por exemplo, fornecem maneiras convenientes armazenamento de tooAzure tooupload dados do seu computador local ou toodownload-tooyour o computador local de armazenamento. 

Esse menu links tootopics que descrevem como tooset backup Olá vários ambientes de ciência de dados usado pelo Olá [processo de ciência de dados da equipe (TDSP)](data-science-process-overview.md).

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

Vários tipos de máquinas virtuais do Azure podem ser provisionados e configurados toobe usado como parte de um ambiente de ciência de dados com base em nuvem. Olá decisão sobre sobre qual tipo de máquina virtual toouse depende do tipo de saudação e a quantidade de dados toobe modelada com o aprendizado de máquina e o destino Olá para os dados na nuvem de saudação. 

* Para obter orientação sobre Olá perguntas tooconsider ao tomar essa decisão, consulte [planejar seu ambiente do Azure máquina aprendizado dados ciência](machine-learning-data-science-plan-your-environment.md). 
* Para um catálogo de alguns dos cenários de saudação, você pode encontrar ao fazer a análise avançada, consulte [cenários para Olá tecnologia no aprendizado de máquina do Azure e o processo de análise avançada](machine-learning-data-science-plan-sample-scenarios.md)

São fornecidos dois conjuntos de instruções:

* [Configurar uma máquina virtual do Azure como um servidor de bloco de anotações do IPython para análise avançada](machine-learning-data-science-setup-virtual-machine.md) mostra como tooprovision uma máquina virtual do Azure com o bloco de anotações do IPython e outras ferramentas usadas toodo ciência de dados para casos em que uma forma de armazenamento do Azure que não seja SQL pode ser usado toostore Olá dados.
* [Configurar uma máquina de virtual do Azure SQL Server como um servidor de bloco de anotações do IPython para análise avançada](machine-learning-data-science-setup-sql-server-virtual-machine.md) mostra como tooprovision uma máquina virtual de servidor do SQL Azure com o bloco de anotações do IPython e outras ferramentas usadas toodo ciência de dados para casos em que um banco de dados SQL pode ser usado toostore Olá dados.

Depois de provisionado e configurado, essas máquinas virtuais estão prontas para uso como servidores de bloco de anotações do IPython para exploração hello e processamento de dados e para outras tarefas necessárias em conjunto com o aprendizado de máquina do Azure e hello processo de ciência de dados da equipe (TDSP). Olá próximas etapas no processo de ciência de dados Olá estão mapeadas em Olá [aprendizado TDSP](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) e podem incluir etapas que movem dados no SQL Server ou HDInsight, processar e exemplo-lo na preparação para aprender com dados de saudação com o Azure Aprendizado de máquina.

> [!NOTE]
> A cobrança das máquinas virtuais do Azure ocorre na forma **pague somente pelo que usa**. tooensure que não estão sendo cobrado quando não estiver usando sua máquina virtual, ele tem toobe em Olá **parado (desalocado)** estado de saudação [Portal clássico do Azure](http://manage.windowsazure.com/). Para obter instruções passo a passo ou como toodeallocate você máquina virtual, consulte [desligamento e desalocar máquina virtual quando não estiver em uso](machine-learning-data-science-setup-virtual-machine.md#shutdown)
> 
> 

