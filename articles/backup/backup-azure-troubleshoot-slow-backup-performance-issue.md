---
title: backup de aaaTroubleshoot lenta de arquivos e pastas no Backup do Azure | Microsoft Docs
description: "Fornece orientação toohelp de solução de problemas você diagnostica a causa de saudação dos problemas de desempenho de Backup do Azure"
services: backup
documentationcenter: 
author: genlin
manager: cshepard
editor: 
ms.assetid: e379180a-db13-4e0c-90e4-28e5dd6f5b14
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 21d79bbd03c2706bc43fcc7c14020cffd6b919c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-slow-backup-of-files-and-folders-in-azure-backup"></a>Solução de problemas de lentidão de backup de arquivos e pastas no Backup do Azure
Este artigo fornece orientação para a solução toohelp diagnosticar causa Olá de baixo desempenho de backup de arquivos e pastas quando você estiver usando o Backup do Azure. Quando você usa hello Azure Backup agent tooback backup de arquivos, o processo de backup Olá pode demorar mais do que o esperado. Esse atraso pode ser causado por um ou mais dos seguintes hello:

* [Existem afunilamentos de desempenho no computador de saudação que está sendo feito.](#cause1)
* [Outro processo ou um software antivírus está interferindo Olá processo de Backup do Azure.](#cause2)
* [Agente de Backup Hello está em execução em uma máquina virtual do Azure (VM).](#cause3)  
* [Você está fazendo backup de um grande número de arquivos (milhões).](#cause4)

Antes de iniciar a solução de problemas, recomendamos que você baixe e instale Olá [agente mais recente do Backup do Azure](http://aka.ms/azurebackup_agent). Fazer atualizações frequentes toohello Backup agent toofix vários problemas, adicionar recursos e melhorar o desempenho.

Também recomendamos que você revise Olá [perguntas frequentes sobre o serviço de Backup do Azure](backup-azure-backup-faq.md) toomake-se de que você não está enfrentando problemas de configuração comuns hello.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

<a id="cause1"></a>

## <a name="cause-performance-bottlenecks-on-hello-computer"></a>Causa: Afunilamentos de desempenho em computador Olá
Afunilamentos no computador de saudação que está sendo feito backup podem causar atrasos. Por exemplo, Olá toodisk de tooread ou gravação de capacidade do computador ou dados de toosend de largura de banda disponível pela rede hello, pode provocar afunilamentos.

O Windows fornece uma ferramenta interna que é chamada [Monitor de desempenho](https://technet.microsoft.com/magazine/2008.08.pulse.aspx) (Perfmon) toodetect esses afunilamentos.

Veja alguns contadores de desempenho e intervalos que podem ser úteis para diagnosticar afunilamentos para obter o backup ideal.

| Contador | Status |
| --- | --- |
| Disco Lógico(Disco Físico) – %ocioso |• too50 ocioso 100% % ocioso = Íntegro</br>• too20 ocioso 49% % ocioso = aviso ou Monitor</br>• too0 ocioso 19% % ocioso = crítico ou especificação |
| Disco Lógico(Disco Físico) -- %média Leitura ou Gravação do Disco por S |• 0,001 ms de too0.015 ms = Íntegro</br>• 0,015 ms de too0.025 ms = aviso ou Monitor</br>• 0,026 ms ou mais = Crítico ou Fora de Especificação |
| Disco Lógico(Disco Físico) -- Comprimento da Fila do Disco Atual (para todas as instâncias) |80 solicitações por mais de seis minutos |
| Memória--Bytes de Pool não Pagináveis |• Menos de 60% do pool consumidos = Íntegro<br>• too80 61% % do pool consumido = aviso ou Monitor</br>• Mais de 80% do pool consumidos = Crítico ou Fora de Especificação |
| Memória--Bytes de Pool Pagináveis |• Menos de 60% do pool consumidos = Íntegro</br>• too80 61% % do pool consumido = aviso ou Monitor</br>• Mais de 80% do pool consumidos = Crítico ou Fora de Especificação |
| Memória--Megabytes disponíveis |• 50% de memória livre disponíveis ou mais = Íntegro</br>• 25% de memória livre disponível = Monitor</br>• 10% de memória livre disponível = Aviso</br>• Menos de 100 MB ou 100% de memória livre disponíveis = Crítico ou Fora de Especificação |
| Processor--\%Tempo do Processor (todas as instâncias) |• Menos de 60% consumido = Íntegro</br>• 61% too90% consumido = Monitor ou cuidado</br>• 91% too100% consumido = crítico |

> [!NOTE]
> Se você determinar que a infraestrutura Olá é responsável hello, recomendamos que você desfragmentar discos Olá regularmente para melhorar o desempenho.
>
>

<a id="cause2"></a>

## <a name="cause-another-process-or-antivirus-software-interfering-with-azure-backup"></a>Causa: outro processo ou software antivírus está interferindo com o Backup do Azure
Já vimos várias instâncias em que outros processos no sistema Windows de saudação piorar significativamente o desempenho de saudação processo do agente de Backup do Azure. Por exemplo, se você usar o agente de Backup do Azure hello e tooback de programa outro backup de dados, ou se o software antivírus está em execução e tem um bloqueio em arquivos toobe backup, Olá vários bloqueios nos arquivos podem causar contenção. Nessa situação, Olá backup pode falhar ou trabalho Olá pode levar mais tempo do que o esperado.

Olá recomendada neste cenário é tooturn off Olá toosee outro programa de backup se Olá horário de backup para o agente de Backup Azure hello. Geralmente, certificando-se de que vários trabalhos de backup não estão em execução no hello simultaneamente é suficiente tooprevent eles afetem uns aos outros.

Para programas antivírus, recomendamos que você exclua a seguir Olá arquivos e locais:

* C:\Program Files\Microsoft Azure Recovery Services Agent\bin\cbengine.exe como um processo
* C:\Program Files\Microsoft Azure Recovery Services Agent\ pastas
* Rascunho local (se você não estiver usando o local padrão de saudação)

<a id="cause3"></a>

## <a name="cause-backup-agent-running-on-an-azure-virtual-machine"></a>Causa: agente de backup em execução em uma máquina virtual do Azure
Se você estiver executando o agente de Backup de saudação em uma máquina virtual, o desempenho será mais lento do que quando você executá-lo em um computador físico. Isso é esperado, devido a limitações de tooIOPS.  No entanto, você pode otimizar o desempenho de saudação ao alternar as unidades de dados de saudação que estão sendo feitas backup tooAzure armazenamento Premium. Estamos trabalhando para corrigir esse problema e correção de saudação estará disponível em uma versão futura.

<a id="cause4"></a>

## <a name="cause-backing-up-a-large-number-millions-of-files"></a>Causa: backup de um grande número de arquivos (milhões)
Mover um grande volume de dados levará mais tempo do que mover um menor volume de dados. Em alguns casos, o tempo de backup está relacionado toonot Olá somente o tamanho dos dados hello, mas o número Olá dos arquivos ou pastas. Isso é especialmente verdadeiro quando milhões de arquivos pequenos (alguns tooa de bytes alguns quilobytes) está sendo feito backup.

Esse comportamento ocorre porque, enquanto você estiver fazendo backup de dados de saudação e movê-lo tooAzure, o Azure simultaneamente é catalogação seus arquivos. Em algumas situações raras, a operação de catálogo de saudação pode demorar mais do que o esperado.

Olá indicadores a seguir pode ajudar a entender o afunilamento hello e adequadamente sobre as próximas etapas hello:

* **Interface do usuário é mostrando o andamento de transferência de dados de saudação**. dados de saudação ainda estão sendo transferidos. largura de banda de rede Hello ou tamanho de saudação de dados pode estar causando atrasos.
* **Interface do usuário não está mostrando o andamento da saudação para transferência de dados**. Olá abrir logs localizado em C:\Microsoft Azure Recovery Services Agent\Temp e, em seguida, verifique Olá FileProvider::EndData entrada nos logs de saudação. Essa entrada significa que terminar de transferência de dados hello e operação de catálogo hello está acontecendo. Não cancele os trabalhos de backup hello. Em vez disso, aguarde um pouco mais para Olá toofinish de operação de catálogo. Se Olá problema persistir, entre em contato com [suporte do Azure](https://portal.azure.com/#create/Microsoft.Support).
