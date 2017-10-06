---
title: "aaaTasks permitido em diferentes estados ou status nos Serviços BizTalk | Microsoft Docs"
description: "Olá ações/operações permitidas no status diferente de MABS: parar, iniciar, reiniciar, suspender, continuar, excluir, dimensionar e atualizar configuração e fazendo backup"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: aea738f3-ec76-4099-a41b-e17fea9e252f
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/08/2016
ms.author: mandia
ms.openlocfilehash: 643307ba6fa9b05c82b867912feab249c42b65dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-you-can-and-cant-do-using-hello-biztalk-service-state"></a>O que você pode e não pode fazer usando Olá estado BizTalk Service

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Dependendo do estado atual de saudação do hello serviço BizTalk, há operações que você pode ou não pode executar em Olá serviço BizTalk.

Por exemplo, você pode provisionar um novo serviço BizTalk no hello portal clássico do Azure. Quando ele for concluído com êxito, Olá serviço BizTalk está em `active` estado. No estado ativo do hello, parar, suspender e excluir o serviço de BizTalk hello. Se você parar o serviço de BizTalk Olá e parar falhar, Olá serviço BizTalk vai tooa `StopFailed` estado. Em Olá `StopFailed` estado, você pode reiniciar o serviço de BizTalk hello. Se você tentar uma operação que não é permitida, como retomar Olá erro a seguir ocorre:

`Operation not allowed`

## <a name="view-hello-possible-states"></a>Exibição Olá possíveis estados

a seguir Olá tabelas liste as operações de saudação ou ações que podem ser feitas quando Olá BizTalk Service está em um estado específico. Um ✔ significa Olá operação é permitida enquanto estiver nesse estado. Uma entrada em branco significa Olá operação não pode ser executada enquanto estiver nesse estado.

| Estado do serviço | Iniciar | Parar | Reiniciar | Suspender | Continuar | Excluir | Escala | Atualização <br/> Configuração | Backup |
| --- | --- | --- | --- | --- | --- | --- |--- | --- | --- |
| Ativo |  | ✔ | ✔ | ✔ |  | ✔ |✔ |✔ |✔ |
| Desabilitado |  |  |  |  |  | ✔ | |  |  | 
| Suspenso |  |  |  |  | ✔ | ✔ | |  | ✔ |
| Parada | ✔ |  | ✔ |  |  | ✔ | |  | ✔ |
| Falha na atualização do serviço |  |  |  |  |  | ✔ | |  |  | 
| DisableFailed |  |  |  |  |  | ✔ | |  |  | 
| EnableFailed |  |  |  |  |  | ✔ | |  |  | 
| StartFailed <br/> StopFailed <br/> RestartFailed | ✔ | ✔ | ✔ |  |  | ✔ | | ✔ | |
| SuspendedFailed <br/> ResumeFailed|  |  |  | ✔ | ✔ | ✔ | |  |  | 
| CreatedFailed <br/> RestoreFailed |  |  |  |  |  | ✔ | |  |  | 
| ConfigUpdateFailed  |  |  | ✔ |  |  | ✔ | |✔ | |
| ScaleFailed |  |  |  |  |  | ✔ |✔ | |  |  | 



## <a name="see-also"></a>Consulte também
* [Criar um BizTalk Service usando Olá portal clássico do Azure](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [O que você pode fazer nas guias painel, monitorar e escala de saudação nos Serviços BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [O que você obterá com as edições Developer, Basic, Standard e Premium Olá nos Serviços BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [Como tooback de backup e restauração de um BizTalk Service](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [Limitação explicada nos Serviços BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=302282)<br/>
* [Recuperar hello controle de acesso e barramento de serviço do nome e o emissor valores chave do emissor para o BizTalk Service](http://go.microsoft.com/fwlink/p/?LinkID=303941)<br/>
* [Como posso começar a usar Olá SDK dos Serviços BizTalk do Azure](http://go.microsoft.com/fwlink/p/?LinkID=302335)

