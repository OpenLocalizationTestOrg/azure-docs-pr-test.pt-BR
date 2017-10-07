---
title: "informações de estado aaaRetrieving para um trabalho de importação/exportação do Azure | Microsoft Docs"
description: "Saiba como tooobtain informações de estado de trabalhos do serviço de importação/exportação do Microsoft Azure."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 22d7e5f0-94da-49b4-a1ac-dd4c14a423c2
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: muralikk
ms.openlocfilehash: cbc35660519573d92f641924ac0025c9e577d69b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="retrieving-state-information-for-an-importexport-job"></a>Recuperação de informações de estado para um trabalho de Importação/Exportação
Você pode chamar hello [obter trabalho](/rest/api/storageimportexport/jobs#Jobs_Get) informações de tooretrieve operação sobre importar e exportar trabalhos. Olá informações retornadas incluem:

-   status atual de saudação do trabalho hello.

-   porcentagem aproximada de saudação que cada trabalho foi concluído.

-   estado atual de saudação de cada unidade.

-   URIs para blobs que contêm logs de erros e informações de log detalhadas (se habilitado).

Olá, seções a seguir explicam informações de hello retornadas por Olá `Get Job` operação.

## <a name="job-states"></a>Estados do trabalho
tabela de saudação e diagrama de estado Olá abaixo descrevem estados Olá transição de um trabalho durante seu ciclo de vida. estado atual de saudação do trabalho de saudação pode ser determinado por chamada hello `Get Job` operação.

![JobStates](./media/storage-import-export-retrieving-state-info-for-a-job/JobStates.png "JobStates")

Olá tabela a seguir descreve cada estado que um trabalho pode passar.

|Estado do trabalho|Descrição|
|---------------|-----------------|
|`Creating`|Depois de você chamar a operação Put Job de saudação, um trabalho é criado e seu estado é definido muito`Creating`. Durante a saudação trabalho Olá `Creating` estado, Olá serviço de importação/exportação supõe Olá unidades não foram enviadas toohello Datacenter. Um trabalho pode permanecer no hello `Creating` estado backup tootwo semanas, após o qual ele é excluído automaticamente pelo serviço de saudação.<br /><br /> Se você chamar a operação Update Job Properties de saudação durante trabalho Olá Olá `Creating` de estado, Olá trabalho permanece Olá `Creating` estado e Olá tempo limite de intervalo é redefinição tootwo semanas.|
|`Shipping`|Depois que você enviar seu pacote, você deve chamar hello Update Job Properties operação update Olá o estado do trabalho de saudação muito`Shipping`. Olá, estado de envio pode ser definido somente se hello `DeliveryPackage` (transportadora e o número de controle) e hello `ReturnAddress` propriedades definidas para o trabalho de saudação.<br /><br /> trabalho de saudação permanecerá no estado de envio Olá para backup tootwo semanas. Se duas semanas tiverem passado e Olá unidades não tiverem sido recebidas, operadores de serviço de importação/exportação Olá serão notificados.|
|`Received`|Depois que todas as unidades tiverem sido recebidas no data center de hello, estado do trabalho Olá será definido toohello estado recebido.|
|`Transferring`|Depois de saudação unidades tiverem sido recebidas no data center de saudação e pelo menos uma unidade tiver iniciado o processamento, estado do trabalho Olá será definido toohello `Transferring` estado. Consulte Olá `Drive States` seção abaixo para obter informações detalhadas.|
|`Packaging`|Depois que todas as unidades tiverem concluído o processamento, Olá trabalho será colocado no hello `Packaging` estado até que Olá unidades sejam enviadas toohello back cliente.|
|`Completed`|Depois que todas as unidades foram enviadas toohello back cliente, se Olá trabalho foi concluído sem erros, em seguida, Olá trabalho será definido toohello `Completed` estado. Olá trabalho será automaticamente excluído após 90 dias no hello `Completed` estado.|
|`Closed`|Depois que todas as unidades foram enviadas toohello back cliente, se houve erros durante o processamento de saudação do trabalho de saudação, em seguida, Olá trabalho será definido toohello `Closed` estado. Olá trabalho será automaticamente excluído após 90 dias no hello `Closed` estado.|

Você pode cancelar um trabalho somente em determinados estados. Um trabalho cancelado ignora a etapa de cópia de dados hello, porém segue Olá mesmo transições de estado como um trabalho que não foi cancelado.

Olá tabela a seguir descreve os erros que podem ocorrer para cada estado do trabalho, bem como efeito Olá no trabalho hello quando ocorre um erro.

|Estado do trabalho|Evento|Resolução/Próximas etapas|
|---------------|-----------|------------------------------|
|`Creating or Undefined`|Uma ou mais unidades para um trabalho chegaram, mas Olá trabalho não está em Olá `Shipping` estado ou há um registro de trabalho Olá no serviço de saudação.|equipe de operações do serviço de importação/exportação de Hello serão tentam toocontact Olá cliente toocreate ou atualizar o trabalho de saudação com o trabalho de saudação de toomove informações necessárias para a frente.<br /><br /> Se Olá equipe de operações não é possível toocontact Prezado cliente dentro de duas semanas, a equipe de operações de Olá tentará tooreturn Olá unidades.<br /><br /> No caso de Olá Olá unidades não podem ser retornadas e Olá cliente não pode ser contatado, Olá unidades serão destruídas em 90 dias com segurança.<br /><br /> Observe que um trabalho não pode ser processado até que seu estado é atualizado muito`Shipping`.|
|`Shipping`|pacote de saudação para um trabalho não foi recebido por mais de duas semanas.|equipe de operações de saudação notificará o cliente de saudação do pacote de saudação ausente. Com base na resposta do cliente Olá, equipe de operações de saudação serão estender Olá intervalo toowait para Olá pacote tooarrive, ou cancelar o trabalho de saudação.<br /><br /> No evento Olá cliente Olá não pode ser contatado ou não responder dentro de 30 dias, equipe de operações de saudação iniciará o trabalho de saudação toomove ação de saudação `Shipping` diretamente estado toohello `Closed` estado.|
|`Completed/Closed`|Olá unidades nunca atingiu o endereço do remetente hello ou foram danificadas na remessa (aplica-se o trabalho de exportação tooan somente).|Se Olá unidades não chegarem remetente hello, Prezado cliente deve primeiro chamada hello obter trabalho operação ou verificar o status do trabalho Olá no hello tooensure portal que Olá unidades foram enviadas. Se Olá unidades foram enviadas, cliente Olá deve contatar Olá envio provedor tootry e localize Olá unidades.<br /><br /> Se Olá unidades são danificadas durante a remessa, o cliente Olá talvez queira toorequest outro trabalho de exportação, ou blobs ausentes do download hello.|
|`Transferring/Packaging`|O trabalho tem um endereço de remetente incorreto ou ausente.|equipe de operações de saudação tentará alcançar toohello pessoa de contato para o endereço correto do Olá Olá trabalho tooobtain.<br /><br /> No evento Olá cliente Olá não pode ser alcançado, Olá unidades serão destruídas com segurança em 90 dias.|
|`Creating / Shipping/ Transferring`|Uma unidade que não aparecem na lista de saudação do toobe unidades importado está incluída no envio do pacote de saudação.|Hello unidades adicionais não serão processadas e serão retornadas toohello cliente quando Olá trabalho seja concluído.|

## <a name="drive-states"></a>Estados da unidade
tabela de saudação e diagrama de saudação abaixo descrevem Olá ciclo de vida de uma unidade individual como ela passa por um trabalho de importação ou exportação. Você pode recuperar o estado atual da unidade Olá Olá chamada `Get Job` operação e inspecionando Olá `State` elemento de saudação `DriveList` propriedade.

![DriveStates](./media/storage-import-export-retrieving-state-info-for-a-job/DriveStates.png "DriveStates")

Olá tabela a seguir descreve cada estado de uma unidade pode passar.

|Estado da unidade|Descrição|
|-----------------|-----------------|
|`Specified`|Para um trabalho de importação, quando Olá trabalho é criado com hello operação Put Job, estado de saudação inicial para uma unidade é hello `Specified` estado. Para um trabalho de exportação, desde que nenhuma unidade foi especificada quando o trabalho de saudação é criado, estado inicial de unidade de saudação é hello `Received` estado.|
|`Received`|unidade de saudação passa toohello `Received` estado quando hello operador do serviço de importação/exportação tiver processado unidades Olá recebidas do hello envio da empresa para um trabalho de importação. Para um trabalho de exportação, o estado inicial de unidade de saudação é hello `Received` estado.|
|`NeverReceived`|unidade de saudação moverá toohello `NeverReceived` estado quando hello chega de pacote para um trabalho, mas pacote hello não contém a unidade de saudação. Uma unidade também pode mover esse estado se foram duas semanas desde que o serviço de saudação recebeu informações de envio de saudação, mas o pacote hello ainda não tiver chegado no data center de saudação.|
|`Transferring`|Uma unidade moverá toohello `Transferring` estado quando hello serviço começa tootransfer dados Olá unidade tooWindows armazenamento do Azure.|
|`Completed`|Uma unidade moverá toohello `Completed` estado quando o serviço de saudação tiver transferido com êxito todos os dados de saudação sem erros.|
|`CompletedMoreInfo`|Uma unidade moverá toohello `CompletedMoreInfo` estado quando serviço Olá encontrou alguns problemas ao copiar dados de ou unidade de toohello. informações de saudação podem incluir erros, avisos ou mensagens informativas sobre substituição de blobs.|
|`ShippedBack`|unidade de saudação moverá toohello `ShippedBack` estado quando ela foi enviada do endereço do remetente de toohello Olá data center de volta.|

Olá tabela a seguir descreve Olá estados de falha de unidade e Olá ações executadas para cada estado.

|Estado da unidade|Evento|Resolução/Próxima etapa|
|-----------------|-----------|-----------------------------|
|`NeverReceived`|Uma unidade que está marcada como `NeverReceived` (porque ela não foi recebida como parte da remessa do trabalho Olá) chega em outra remessa.|equipe de operações de saudação moverá Olá unidade toohello `Received` estado.|
|`N/A`|Uma unidade que não faz parte de qualquer trabalho chega no data center de saudação como parte de outro trabalho.|unidade de saudação será marcada como uma unidade adicional e será retornada toohello cliente quando Olá trabalho associado com o pacote original Olá estiver concluído.|

## <a name="faulted-states"></a>Estados com falha
Quando um trabalho ou a unidade não tooprogress normalmente por meio de seu ciclo de vida esperado, Olá trabalho ou a unidade será movida para um `Faulted` estado. Nesse ponto, equipe de operações de saudação entrará em contato com o cliente Olá por email ou telefone. Uma vez Olá problema for resolvido, Olá falha de trabalho ou unidade será retirada Olá `Faulted` estado e movidos para Olá apropriada estado.

## <a name="next-steps"></a>Próximas etapas

* [Usando a API REST do serviço de importação/exportação Olá](storage-import-export-using-the-rest-api.md)
