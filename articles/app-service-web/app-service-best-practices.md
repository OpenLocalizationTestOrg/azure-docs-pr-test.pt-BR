---
title: "práticas recomendadas de aaaBest para o serviço de aplicativo do Azure"
description: "Aprenda as práticas recomendadas e solução de problemas do Serviço de Aplicativo do Azure."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: f3359464-fa44-4f4a-9ea6-7821060e8d0d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2016
ms.author: dariagrigoriu
ms.openlocfilehash: a1d3127f5a746aa43f7b56b45f17c45df9087bee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-azure-app-service"></a>Práticas Recomendadas para o Serviço de Aplicativo do Azure
Este artigo resume as práticas recomendadas para usar o [Serviço de Aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714). 

## <a name="colocation"></a>Colocação
Quando a composição de uma solução como um aplicativo web e um banco de dados de recursos do Azure estão localizados em efeitos de saudação de regiões diferentes podem incluir o seguinte de saudação:

* Maior latência na comunicação entre recursos
* Encargos monetários para dados de saída transferir entre regiões conforme observado no hello [do Azure de página de preços](https://azure.microsoft.com/pricing/details/data-transfers).

A colocação em Olá mesma região é melhor para compor uma solução como um aplicativo web de recursos do Azure e uma conta de armazenamento ou banco de dados usado toohold conteúdo ou dados. Ao criar recursos, você deve verificar se que eles estão em Olá mesma região do Azure, a menos que você tem comercial específica ou projetar o motivo para que eles não toobe. Você pode mover um toohello do aplicativo de serviço de aplicativo mesma região do seu banco de dados, aproveitando Olá [recurso de clonagem do serviço de aplicativo](app-service-web-app-cloning-portal.md) atualmente disponíveis para aplicativos de plano de serviço de aplicativo Premium.   

## <a name="memoryresources"></a>Quando aplicativos consomem mais memória do que o esperado
Quando você observar um aplicativo consome mais memória do que o esperado, conforme indicado por meio de monitoramento ou recomendações sobre serviço considere Olá [recurso de reparo automático de serviço de aplicativo](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites). Uma das opções de saudação do recurso de reparo automático de saudação está demorando ações personalizadas com base em um limite de memória. Ações abrangem o espectro de saudação do tooinvestigation de notificações de email por meio da redução de tooon especiais de despejo de memória pela reciclagem de processo do operador hello. Recuperação automática pode ser configurado por meio do Web. config e por meio de uma interface de usuário amigável conforme descrito nesta postagem de blog Olá [extensão de Site de suporte de serviço de aplicativo](https://azure.microsoft.com/blog/additional-updates-to-support-site-extension-for-azure-app-service-web-apps).   

## <a name="CPUresources"></a>Quando aplicativos consomem mais CPU do que o esperado
Quando você observar que um aplicativo consumindo mais recursos da CPU que o esperado ou passa por repetido picos de CPU, conforme indicado por meio de monitoramento ou recomendações sobre serviço considere escalabilidade vertical ou expansão Olá plano de serviço de aplicativo. Se seu aplicativo é o estado, aumento de escala é única opção de hello, enquanto se seu aplicativo estiver fora de escala, sem monitoração de estado lhe dará mais flexibilidade e maior potencial de escala. 

Para saber mais sobre aplicativos "com estado" versus "sem estado", assista a este vídeo: [Planejando um aplicativo de várias camadas ponta a ponta escalonável no aplicativo Web do Microsoft Azure](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2014/DEV-B414#fbid=?hashlink=fbid). Para saber mais sobre como as opções de colocação em escala e dimensionamento automático, leia: [Dimensionar um aplicativo Web no Serviço de Aplicativo do Azure](web-sites-scale.md).  

## <a name="socketresources"></a>Quando os recursos de soquete são exauridos
Um motivo comum para esgotando conexões TCP de saída é o uso de saudação das bibliotecas de cliente que não são implementados tooreuse conexões de TCP, ou no caso de saudação de um protocolo de nível superior, como HTTP - Keep-Alive não está sendo utilizado. Examine a documentação Olá para cada uma das bibliotecas de saudação referenciadas pelo Olá aplicativos no seu tooensure plano do serviço de aplicativo são configuradas ou acessados em seu código para reutilização eficiente de conexões de saída. Também siga as diretrizes de documentação de biblioteca Olá para criação correta e a versão ou limpeza tooavoid vazamento de conexões. Enquanto essas investigações de bibliotecas de cliente estão em impacto de progresso pode ser reduzido com expansão toomultiple instâncias.  

## <a name="appbackup"></a>Quando o backup de seu aplicativo começa a falhar
Olá duas razões mais comuns por que a falha do backup de aplicativo é: configurações de armazenamento inválido e a configuração de banco de dados inválido. Essas falhas geralmente acontecem quando há alterações toostorage ou recursos de banco de dados ou alterações como tooaccess esses recursos (por exemplo, credenciais atualizadas Olá banco de dados selecionado nas configurações de backup Olá). Backups normalmente executam em um agendamento e exigem acesso toostorage (para a saída do hello backup dos arquivos) e bancos de dados (para copiar e ler conteúdo toobe incluído no backup de saudação). Olá resultado da falha tooaccess qualquer um desses recursos seria falha de backup consistente. 

Quando ocorrem falhas de backup, consulte toounderstand de resultados mais recente que tipo de falha está ocorrendo. No caso de saudação de falhas de acesso de armazenamento, revisar e atualizar as configurações de armazenamento de saudação usadas na configuração de backup hello. No caso de saudação de falhas de acesso de banco de dados, analisar e atualizar suas cadeias de conexão como parte das configurações de aplicativo; Continue tooupdate tooproperly sua configuração de backup incluem bancos de dados de saudação necessário. Para obter mais informações sobre backup do aplicativo, consulte Olá [backup de um aplicativo web no serviço de aplicativo do Azure](web-sites-backup.md) documentação.

## <a name="nodejs"></a>Quando novos aplicativos Node. js são implantado tooAzure do serviço de aplicativo
Configuração de padrão de serviço de aplicativo do Azure para aplicativos Node. js é pretendido toobest naipe Olá necessidades dos aplicativos mais comuns. Se a configuração do seu aplicativo Node. js poderia se beneficiar de ajuste de desempenho tooimprove ou otimizar o uso de recursos para recursos de memória/CPU/rede, você pode revisar nossas práticas recomendadas e as etapas de solução de problemas. Este artigo de documentação descreve configurações de iisnode de saudação, talvez seja necessário tooconfigure para seu aplicativo Node. js, descreve Olá vários cenários ou problemas que seu aplicativo pode enfrentar e mostra como tooaddress esses problemas: [práticas recomendadas e Guia de solução de problemas para aplicativos de nó no serviço de aplicativo do Azure](app-service-web-nodejs-best-practices-and-troubleshoot-guide.md).   

