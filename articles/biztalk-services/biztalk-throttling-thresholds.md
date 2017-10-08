---
title: "aaaLearn sobre limitação nos Serviços BizTalk | Microsoft Docs"
description: "Saiba mais sobre os limites de limitação e comportamentos de tempo de execução resultantes para os serviços BizTalk. A limitação é baseada no uso de memória e número de mensagens. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: f6663cf2-cda4-4bac-855e-27d2ad5c4fa4
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 46c8806c3a1f4eeb793f721f849771e0ec155197
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-throttling"></a>Serviços BizTalk: limitação

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Serviços BizTalk do Azure implementa o serviço com base em duas condições de limitação: número de hello e uso de memória de processamento de mensagens simultâneas. Este tópico lista Olá limitação limites e descreve o comportamento de tempo de execução de saudação quando ocorre uma condição de limitação.

## <a name="throttling-thresholds"></a>Limites da limitação
Olá a tabela a seguir lista Olá limitação de origem e de limites:

|  | Descrição | Limite baixo | Limite alto |
| --- | --- | --- | --- |
| Memória |% de memória total de sistema disponível/PageFileBytes. <p><p>Total PageFileBytes disponível é de aproximadamente 2 vezes Olá RAM do sistema hello. |60% |70% |
| Processamento de mensagem |Número de processamento de mensagens simultaneamente |40 vezes o número de núcleos |100 vezes o número de núcleos |

Quando um limite máximo for atingido, os Serviços BizTalk do Azure inicia toothrottle. Limitação será interrompido quando o limite mínimo de saudação é atingido. Por exemplo, seu serviço estiver usando 65% da memória do sistema. Nessa situação, o serviço de saudação não acelerador. Seu serviço começa usando 70% da memória do sistema. Nessa situação, o serviço Olá limita e continua toothrottle até que o serviço de saudação usa a memória do sistema 60% (limite inferior).

Serviços BizTalk do Azure controla Olá limitação status (estado normal versus estado limitado) e hello limitação duração.

## <a name="runtime-behavior"></a>Comportamento do tempo de execução
Quando os Serviços BizTalk do Azure entrará em um estado de limitação, ocorre a seguinte de saudação:

* A limitação ocorre por instância de função. Por exemplo:<br/>
  A InstânciadeFunçãoA está limitada. A InstânciadeFunçãoB não está limitada. Nesta situação, as mensagens da InstânciadeFunçãoB são processadas conforme o esperado. Mensagens de RoleInstanceA são descartadas e falharem com hello erro a seguir:<br/><br/>
  **O servidor está ocupado. Tente novamente.**<br/><br/>
* Nenhuma origem de pull pode pesquisar ou baixar uma mensagem. Por exemplo:<br/>
  um pipeline puxa as mensagens de uma origem de FTP externa. instância de função Hello fazer pull Olá obtém em um estado de limitação. Nessa situação, pipeline Olá para baixar mensagens adicionais até que a instância de função hello para de limitação.
* Uma resposta é enviada toohello cliente cliente Olá pode enviar novamente a mensagem de saudação.
* Você deve aguardar até que a limitação de saudação seja resolvido. Especificamente, você deve aguardar até que o limite mínimo de saudação é atingido.

## <a name="important-notes"></a>Observações importantes
* A limitação não pode ser desabilitada.
* Os limites de limitação não podem ser modificados.
* A limitação é implementada em todo o sistema.
* Olá servidor de banco de dados do SQL Azure também tem uma limitação interna.

## <a name="additional-azure-biztalk-services-topics"></a>Tópicos adicionais dos Serviços BizTalk do Azure
* [Instalando Olá SDK dos Serviços BizTalk do Azure](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [Tutoriais: Serviços BizTalk do Azure](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [Como posso começar a usar Olá SDK dos Serviços BizTalk do Azure](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [Serviços BizTalk do Azure](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a>Consulte também
* [Serviços BizTalk: gráfico das edições Developer, Basic, Standard e Premium](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [Serviços BizTalk: provisionamento usando o portal clássico do Azure](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [Serviços BizTalk: gráfico do status do provisionamento](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [Serviços BizTalk: guias Painel, Monitor e Escala](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [Serviços BizTalk: backup e restauração](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [Serviços BizTalk: nome e chave do emissor](http://go.microsoft.com/fwlink/p/?LinkID=303941)<br/>

