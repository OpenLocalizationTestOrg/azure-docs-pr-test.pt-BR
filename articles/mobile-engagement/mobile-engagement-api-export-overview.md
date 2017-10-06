---
title: "aaaMobile contrato exportar visão geral da API"
description: "Saiba mais sobre exportação dos dados brutos conceitos básicos de saudação gerado pelo tooleverage de dispositivos do usuário-lo em suas próprias ferramentas"
services: mobile-engagement
documentationcenter: mobile
author: kpiteira
manager: erikre
editor: 
ms.assetid: 9380d47b-d7fa-4d4c-888f-97e6482196bb
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 04/26/2016
ms.author: kapiteir
ms.openlocfilehash: f55be29a29878e74f6a33419f08a5574a07a7478
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="mobile-engagement-export-api-overview"></a>Visão geral da API de Exportação do Mobile Engagement
## <a name="introduction"></a>Introdução
Neste documento, você aprenderá sobre exportação dos dados brutos conceitos básicos de saudação gerado pelo tooleverage de dispositivos do usuário-lo em suas próprias ferramentas.

## <a name="pre-requisites"></a>Pré-requisitos
Exportar dados brutos de saudação do Mobile Engagement requer:

* Olá API autenticação instalação toobe toouse capaz de APIs (consulte [instalação manual de autenticação](mobile-engagement-api-authentication-manual.md)),
* Use Olá APIs REST ou hello [.net SDK](mobile-engagement-dotnet-sdk-service-api.md),
* Uma conta de armazenamento do Azure.

> [!NOTE]
> É recomendável também Olá excelente [Microsoft Azure Storage Explorer](http://storageexplorer.com/), pelo menos durante a fase de desenvolvimento hello como ele fornece uma fácil toouse da interface do usuário para interagir com o armazenamento do Azure.
> 
> 

## <a name="what-can-be-exported"></a>O que pode ser exportado?
Mobile Engagement permite que seus usuários toocollect muitos tipos de dados e, portanto, tem vários tipos de exportação adequado toothese diferentes tipos de dados.
Há dois tipos essenciais de exportação:

* Instantâneo: geralmente usados tooexport dados que representa um estado e para os quais o Mobile Engagement não tem um histórico. Isso inclui Marcações (informações do aplicativo), tokens ou comentários de campanha de envio por push, por exemplo. Como consequência esses tipos de exportação não são relacionadas tooa Data.
* histórica: esse tipo de exportação é usado para dados acumulados ao longo do tempo, como Eventos ou Atividades, por exemplo.

Olá tabela a seguir descreve exaustivamente todas as Olá possíveis exportações:

| Tipo de Exportação | Tipo de Dados | Descrição |
| --- | --- | --- |
| Instantâneo |Empurrar |Gera uma exportação de comentários de Campanhas de Envio por Push em uma base de deviceid/userid |
| Instantâneo |Marca |Gera uma exportação de saudação marcas (app-info) associados tooeach dispositivos |
| Instantâneo |Dispositivo |Gera uma exportação de maioria dos dados Olá sobre dispositivos como technicals hello (modelo, localidade, fuso horário,...), marcas de hello, primeira vez visto,... |
| Instantâneo |Token |Gera uma exportação de todos os tokens de saudação válido |
| Histórica |Atividade |Gera uma exportação de todas as atividades de saudação de cada dispositivo em um determinado período de tempo |
| Histórica |Evento |Gera uma exportação de todas as atividades de saudação de cada dispositivo em um determinado período de tempo |
| Histórica |Trabalho |Gera uma exportação de todos os trabalhos de saudação para cada dispositivo em um determinado período de tempo |
| Histórica |Erro |Gera uma exportação de todos os erros de saudação de cada dispositivo em um determinado período de tempo |

## <a name="how-does-it-work"></a>Como ele funciona?
Exportações são tarefas de longa execução que podem produzir arquivos de dados grandes. Por esse motivo, eles não podem ser invocado tooreturn imediatamente um toodownload do arquivo.
Dados de pedidos tooexport do Mobile Engagement, você terá toocreate um **trabalho de exportação** por meio da API em que você especificar geralmente:

* tipo de saudação da exportação (instantâneo ou histórico)
* tipo de dados de saudação
* Olá **contêiner de armazenamento do Azure** (incluindo uma SAS válida com acesso de gravação) onde resultado Olá da exportação hello será gravado.
* Por exemplo, o parâmetro de URL de Contêiner de Exemplo seria https://[StorageAccountName].blob.core.windows.net/[ContainerName]?[SASWritePermissionsToken]  

Aqui está um exemplo do mundo real. https://testazmeexport.blob.core.windows.net/test1234azme?sv=2015-12-11&ss=b&srt=sco&sp=rwdlac&se=2016-12-17T04:59:26Z&st=2016-12-16T20:59:26Z&spr=https&sig=KRF3aVWjp2NEJDzjlmoplmu0M9HHlLdkBWRPAFmw90Q%3D

Observe que pode levar alguns minutos para que seu toobe trabalho iniciado e, em seguida, ela poderá ser executada de alguns segundos para o horário de tooseveral pequenos aplicativos para aplicativos com muitos usuários ou atividade.

Depois de saudação trabalho é criado, é possível toocheck toosee seu status, se ainda está em execução ou se ele for concluído.

Depois que o trabalho de saudação é bem-sucedida, o arquivo de dados resultante hello está disponível no hello fornecido o contêiner de armazenamento.

