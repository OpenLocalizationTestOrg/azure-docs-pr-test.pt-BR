---
title: "Explicando Unidades de Computação no Banco de Dados do Azure para MySQL | Microsoft Docs"
description: "Banco de dados do Azure para MySQL: Este artigo explica conceitos de saudação de unidades de computação e o que acontece quando sua carga de trabalho atinge Olá unidades máximas de computação."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/23/2017
ms.openlocfilehash: 751b4fff2760e55565e2bc80d49db17a57397779
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="explaining-compute-units-in-azure-database-for-mysql"></a>Explicando Unidades de Computação no Banco de Dados do Azure para MySQL
Este artigo explica o conceito de saudação de unidades de computação e o que acontece quando sua carga de trabalho atinge Olá unidades máximas de computação.

## <a name="what-are-compute-units"></a>O que são unidades de computação?
Computação unidades são uma medida de taxa de transferência de processamento de CPU que tem a garantia tooa disponível toobe um único banco de dados do Azure para o MySQL server. Uma unidade de computação é uma medida combinada de recursos de CPU e memória. Em geral, 50 unidades de computação serão iguais a toohalf de um núcleo. 100 unidades de computação serão iguais tooone core. Unidades de computação de 2000 igualar tootwenty núcleos do servidor de tooyour disponíveis de taxa de transferência garantida de processamento.

quantidade de saudação de memória por unidade de computação é otimizada para hello Basic e Standard camadas de preços. Duplicar Olá unidades de computação, aumentando o nível de desempenho de saudação é igual a toodoubling conjunto de saudação do toothat disponíveis do recurso único banco de dados do Azure para MySQL.

Por exemplo, um tipo Standard de 800 Unidades de Computação fornece 8 vezes mais taxa de transferência de CPU e memória que uma configuração Standard com 100 Unidades de Computação. No entanto, enquanto fornecem unidades de computação padrão de 100 Olá mesmo taxa de transferência de CPU comparados tooBasic 100 unidades de computação, quantidade de saudação de memória que é pré-configurado de preços padrão é duplo de Olá quantidade de memória configurada para Basic preço. Portanto, preços padrão fornece um melhor desempenho de carga de trabalho e menor latência de transação de camada de preços básico com hello que unidades de computação mesmo selecionada.

## <a name="how-can-i-determine-hello-number-of-compute-units-needed-for-my-workload"></a>Como determinar o número de saudação de unidades de computação necessária para meu carga de trabalho?
Se você estiver procurando toomigrate um servidor existente do MySQL em execução no local ou em uma máquina virtual, você pode determinar o número de saudação de unidades de computação por estimativa precisa de sua carga de trabalho quantos núcleos de processamento de taxa de transferência. 

Se o seu servidor local ou de máquina virtual existente estiver utilizando 4 núcleos (sem contar o hiperthread da CPU), comece configurando 400 Unidades de Computação para o seu Banco de Dados do Azure para o servidor MySQL. É possível aumentar ou diminuir dinamicamente as Unidades de Computação conforme as suas necessidades de carga de trabalho sem praticamente nenhum tempo de inatividade do aplicativo. 

Gráfico de métricas do monitor Olá no hello Azure portal ou gravação CLI do Azure comandos - toomeasure unidades de computação. Toomonitor relevante de métricas são porcentagem de unidade de computação hello e limite de unidade de computação.

>[!IMPORTANT]
> Se você encontrar armazenamento IOPS não são totalmente utilizados toohello máximo, considere a possibilidade de monitorar Olá computação unidades utilização. Gerar Olá unidades de computação pode permitir maior taxa de transferência de e/s, reduzindo o afunilamento de desempenho Olá devido toolimited CPU ou memória.

## <a name="what-happens-when-i-hit-my-maximum-compute-units"></a>O que acontece quando eu atinjo o máximo de Unidades de Computação?
Níveis de desempenho são calibrados e regido tooprovide recursos toorun sua carga de trabalho do banco de dados se os limites máximo toohello para a camada de preços selecionada hello e nível de desempenho. 

Se sua carga de trabalho atingir limites máximos de saudação em uma saudação computação unidades ou limites IOPS provisionados, você pode continuar a recursos de saudação tooutilize nível Olá máximo permitido, mas as consultas são provavelmente toosee aumentado latências. Esses limites não resultam em erros, mas em vez disso, uma diminuição na carga de trabalho hello, a menos que lentidão Olá fica tão grave que consulta o tempo limite. 

Se sua carga de trabalho atingir limites máximos de saudação no número de conexões, são gerados erros explícitos. Para saber mais sobre os limites de recursos, veja [Limites no Banco de Dados do Azure para MySQL](concepts-limits.md).

## <a name="next-steps"></a>Próximas etapas
Para saber mais sobre tipos de preço, confira [Tipos de preço do Banco de Dados do Azure para MySQL](./concepts-service-tiers.md).
