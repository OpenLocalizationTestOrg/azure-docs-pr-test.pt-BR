---
title: 'Microsoft Genomics: Perguntas frequentes | Microsoft Docs'
titleSuffix: Azure
description: Respostas a perguntas frequentes que os clientes fazem sobre o Genomics Microsoft.
services: microsoft-genomics
author: grhuynh
manager: jhubbard
editor: jasonwhowell
ms.author: grhuynh
ms.service: microsoft-genomics
ms.workload: genomics
ms.topic: article
ms.date: 12/07/2017
ms.openlocfilehash: 2077eeb5177b07c458476ae900f81b72e35f0dc3
ms.sourcegitcommit: 922687d91838b77c038c68b415ab87d94729555e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2017
---
# <a name="microsoft-genomics-common-questions"></a>Microsoft Genomics: Perguntas frequentes

Este artigo lista as principais dúvidas que você pode ter relacionadas ao Microsoft Genomics. Para obter mais informações sobre o serviço do Microsoft Genomics, consulte [O que é Microsoft Genomics?](overview-what-is-genomics.md) 


## <a name="what-is-the-sla-for-microsoft-genomics"></a>O que é o SLA para Microsoft Genomics?
Garantimos que em 99,9% do tempo o serviço Microsoft Genomics estará disponível para receber solicitações de API de fluxo de trabalho. Para saber mais, veja [SLA](https://azure.microsoft.com/support/legal/sla/genomics/v1_0/).

## <a name="how-does-the-usage-of-microsoft-genomics-show-up-on-my-bill"></a>Como o uso do Microsoft Genomics aparece na minha fatura?
O Microsoft Genomics é faturado de acordo com o número de gigabases processados por fluxo de trabalho. Para saber mais, consulte [Preços](https://azure.microsoft.com/pricing/details/genomics/).


## <a name="where-can-i-find-a-list-of-all-possible-commands-and-arguments-for-the-msgen-client"></a>Onde encontrar uma lista de todos os comandos e argumentos possíveis para o `msgen` cliente?
Você pode obter uma lista completa dos comandos e argumentos disponíveis executando `msgen help`. Se nenhum argumento adicional é fornecido, ele mostra uma lista de seções de ajuda disponíveis, uma para cada um dos `submit`, `list`, `cancel`, e `status`. Para obter ajuda para um comando específico, digite `msgen help command`; por exemplo, `msgen help submit` lista todas as opções de envio.

## <a name="what-are-the-most-commonly-used-commands-for-the-msgen-client"></a>Quais são os comandos mais comuns usados para o `msgen` cliente?
Os comandos mais usados são argumentos para o `msgen` cliente incluem: 

 |**Comando**          |  **Descrição do campo** |
 |:--------------------|:-------------         |
 |`list`               |Retorna uma lista de trabalhos que você enviou. Para argumentos, consulte `msgen help list`.  |
 |`submit`             |Envia uma solicitação de fluxo de trabalho para o serviço. Para argumentos, consulte `msgen help submit`.|
 |`status`             |Retorna o status do fluxo de trabalho especificado por `--workflow-id`. Consulte também `msgen help status`. |
 |`cancel`             |Envia uma solicitação para cancelar o processamento do fluxo de trabalho especificado por `--workflow-id`. Consulte também `msgen help cancel`. |

## <a name="where-do-i-get-the-value-for---api-url-base"></a>Onde posso obter o valor de `--api-url-base`?
Vá ao portal do Azure e abra a página da sua conta do Genomics. No cabeçalho **Gerenciamento**, escolha **Chaves de acesso**. Lá, você encontra a URL de API e suas chaves de acesso.

## <a name="where-do-i-get-the-value-for---access-key"></a>Onde posso obter o valor de `--access-key`?
Vá ao portal do Azure e abra a página da sua conta do Genomics. No cabeçalho **Gerenciamento**, escolha **Chaves de acesso**. Lá, você encontra a URL de API e suas chaves de acesso.

## <a name="why-do-i-need-two-access-keys"></a>Por que preciso duas chaves de acesso?
São necessárias duas chaves de acesso no caso de você desejar atualizá-las (gerá-las novamente) sem interromper o uso do serviço. Por exemplo, você deseja atualizar a primeira chave. Nesse caso, você deve alternar todos os novos fluxos de trabalho para usar a segunda chave. Em seguida, aguarde até que os fluxos de trabalho já em execução que usam a primeira chave sejam concluídos. Somente então, atualize a chave.

## <a name="do-you-save-my-storage-account-keys"></a>Você salva minhas chaves de conta de armazenamento?
Sua chave de conta de armazenamento é usada para criar tokens de acesso de curto prazo para o serviço Microsoft Genomics ler os arquivos de entrada e gravar os arquivos de saída. A vida útil padrão do token é de 48 horas. A duração do token pode ser alterada com a `-sas/--sas-duration` opção do comando Enviar; o valor é em horas.

## <a name="what-genome-references-can-i-use"></a>Quais referências de genoma posso usar?

Há suporte para essas referências:
 |Referência              | Valor de `-pa/--process-args` |
 |:-------------         |:-------------                 |
 |b37                    | `R=b37m1`                     |
 |hg38                   | `R=hg38m1`                    |      
 |hg38 (nenhuma análise alt) | `R=hg38m1x`                   |  
 |hg19                   | `R=hg19m1`                    |    

## <a name="how-do-i-format-my-command-line-arguments-as-a-config-file"></a>Como formato meus argumentos de linha de comando como um arquivo de configuração? 

msgen compreende os arquivos de configuração no seguinte formato:
* Todas as opções são fornecidas como pares chave-valor com valores separados de chaves por dois-pontos.
Espaço em branco é ignorado.
* Linhas que começam com `#` serão ignoradas.
* Qualquer argumento de linha de comando no formato longo pode ser convertido a uma chave retirando seus principais traços e substituindo traços entre palavras com sublinhados. Aqui estão alguns exemplos de conversão:

 |Argumento de linha de comando            | Linha de arquivo de configuração |
 |:-------------                   |:-------------                 |
 |`-u/--api-url-base https://url`  | *api_url_base:https://url*    |
 |`-k/--access-key KEY`            | *access_key:KEY*              |      
 |`-pa/--process-args R=B37m1`     | *process_args:R-b37m1*        |  

## <a name="next-steps"></a>Próximas etapas

Use os seguintes recursos para começar com o Microsoft Genomics:
- Comece executando o seu primeiro fluxo de trabalho pelo serviço do Microsoft Genomics. [Execute um fluxo de trabalho através do serviço do Microsoft Genomics](quickstart-run-genomics-workflow-portal.md)
- Envie seus próprios dados para processamento pelo serviço do Microsoft Genomics: [FASTQ emparelhado](quickstart-input-pair-FASTQ.md) | [BAM](quickstart-input-BAM.md) | [FASTQ múltiplos ou BAM](quickstart-input-multiple.md) 

