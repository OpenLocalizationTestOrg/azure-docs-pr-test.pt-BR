---
title: "Visão geral do Cache Local do serviço de aplicativo aaaAzure | Microsoft Docs"
description: "Este artigo descreve como tooenable, redimensionar e consulta Olá status do recurso de Cache Local de serviço de aplicativo do Azure Olá"
services: app-service
documentationcenter: app-service
author: SyntaxC4
manager: yochayk
editor: 
tags: optional
keywords: 
ms.assetid: e34d405e-c5d4-46ad-9b26-2a1eda86ce80
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/04/2016
ms.author: cfowler
ms.openlocfilehash: 220331ac7e15352a434d63266701071024d868c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-local-cache-overview"></a>Visão geral do cache local do Serviço de Aplicativo do Azure
O conteúdo dos aplicativos Web do Azure é armazenado no Armazenamento do Azure e exibido de forma duradoura como um compartilhamento de conteúdo. Esse design é pretendido toowork com uma variedade de aplicativos e tem Olá seguintes atributos:  

* Olá conteúdo é compartilhado entre várias instâncias de máquina virtual (VM) do aplicativo web de saudação.
* conteúdo de saudação é durável e pode ser modificado por aplicativos web em execução.
* Arquivos de log e arquivos de dados de diagnóstico estão disponíveis em Olá mesmo compartilhados pasta de conteúdo.
* Publicando o novo conteúdo diretamente atualizações Olá pasta de conteúdo. Você pode imediatamente Olá exibição mesmo conteúdo por meio do site SCM hello e Olá aplicativo web em execução (normalmente algumas tecnologias como ASP.NET iniciar uma reinicialização do aplicativo web em algum conteúdo mais recente do arquivo alterações tooget Olá).

Embora muitos aplicativos Web usem um ou todos esses recursos, outros precisam somente de um repositório de conteúdo de alto desempenho somente leitura de onde eles possam ser executados com alta disponibilidade. Esses aplicativos podem se beneficiar de uma instância de máquina virtual de um cache local específico.

recurso de Cache Local de serviço de aplicativo do Azure Olá fornece uma exibição de função da web do seu conteúdo. Esse conteúdo é um cache de write-but-discard do seu conteúdo de armazenamento que é criado de forma assíncrona na inicialização do site. Ao cache Olá estiver pronta, Olá é comutada toorun contra conteúdo Olá armazenado em cache. Aplicativos Web executados no Cache Local têm Olá benefícios a seguir:

* Eles são toolatencies imune que ocorrem quando eles acessarem o conteúdo no armazenamento do Azure.
* Eles são atualizações toohello imune planejado ou tempos de inatividade não planejados e outras interrupções com armazenamento do Azure que ocorrem em servidores que servem o compartilhamento de conteúdo de saudação.
* Eles têm menos reinicializações do aplicativo devido a alterações de compartilhamento de toostorage.

## <a name="how-local-cache-changes-hello-behavior-of-app-service"></a>Como o Cache Local altera o comportamento de saudação do serviço de aplicativo
* cache local Olá é uma cópia de pastas /site e /siteextensions Olá Olá web app. Ele é criado na instância VM local Olá na inicialização do aplicativo web. Olá tamanho do cache local do hello por aplicativo web é limitado too300 MB por padrão, mas você pode aumentar a too2 GB.
* cache local Olá é leitura / gravação. No entanto, as modificações serão descartadas quando o aplicativo da web de saudação move as máquinas virtuais ou obtém reiniciado. Você não deve usar o Cache Local para aplicativos que armazenam dados de missão crítica no repositório de conteúdo de saudação.
* Aplicativos Web podem continuar toowrite arquivos de log e dados de diagnóstico que tinham no momento. Arquivos de log e dados, no entanto, são armazenados localmente em Olá VM. Em seguida, eles são copiados periodicamente toohello repositório de conteúdo compartilhado. repositório de conteúdo compartilhado cópia toohello Hello é um esforço mais favorável – faz backup de gravação pode ser perdido devido a falhas repentinas tooa de uma instância VM.
* Há uma alteração na estrutura de pastas de saudação do hello arquivos de log e as pastas de dados para aplicativos web que usam o Cache Local. Agora há subpastas Olá arquivos de log e dados de pastas de armazenamento que seguem o padrão de nomenclatura hello "identificador exclusivo" + o carimbo de data / hora. Cada uma das subpastas Olá corresponde a instância VM tooa onde Olá web aplicativo está em execução ou foi executada.  
* Publicação alterações toohello web aplicativo por meio de qualquer um dos mecanismos de publicação Olá publicará toohello repositório de conteúdo compartilhado. Isso ocorre por design, porque queremos Olá publicado conteúdo toobe durável. cache local de saudação de toorefresh do aplicativo de web hello, ele precisa toobe reiniciado. Isso parece como uma etapa excessiva? ciclo de vida de saudação do toomake contínuo, consulte informações de saudação neste artigo.
* D:\home. apontará o cache local toohello. D:\Local continuará apontando o armazenamento temporário de específico de VM toohello.
* exibição de conteúdo saudação padrão do site SCM Olá continuará toobe que Olá repositório de conteúdo compartilhado.

## <a name="enable-local-cache-in-app-service"></a>Habilitar o Cache Local no Serviço de Aplicativo
Configure o Cache Local usando uma combinação de configurações de aplicativo reservadas. Você pode configurar essas configurações de aplicativo usando Olá métodos a seguir:

* [Portal do Azure](#Configure-Local-Cache-Portal)
* [Gerenciador de Recursos do Azure](#Configure-Local-Cache-ARM)

### <a name="configure-local-cache-by-using-hello-azure-portal"></a>Configurar o Cache Local usando Olá portal do Azure
<a name="Configure-Local-Cache-Portal"></a>

Habilitar o Cache Local com base em cada aplicativo Web usando esta configuração de aplicativo: `WEBSITE_LOCAL_CACHE_OPTION` = `Always`  

![Configurações de aplicativo do portal do Azure: cache local](media/app-service-local-cache/app-service-local-cache-configure-portal.png)

### <a name="configure-local-cache-by-using-azure-resource-manager"></a>Configurar o Cache Local usando o Azure Resource Manager
<a name="Configure-Local-Cache-ARM"></a>

```

...

{
    "apiVersion": "2015-08-01",
    "type": "config",
    "name": "appsettings",
    "dependsOn": [
        "[resourceId('Microsoft.Web/sites/', variables('siteName'))]"
    ],

"properties": {
        "WEBSITE_LOCAL_CACHE_OPTION": "Always",
        "WEBSITE_LOCAL_CACHE_SIZEINMB": "300"
    }
}

...
```

## <a name="change-hello-size-setting-in-local-cache"></a>Alterar a configuração de tamanho de saudação no Cache Local
Por padrão, o tamanho do cache local Olá é **300 MB**. Isso inclui /site hello e /siteextensions pastas que são copiadas do hello conteúdo de repositório, bem como quaisquer pastas de dados e logs criado localmente. tooincrease limite, use a configuração do aplicativo hello `WEBSITE_LOCAL_CACHE_SIZEINMB`. Você pode aumentar o tamanho de saudação até muito**2 GB** (2000 MB) por um aplicativo web.

## <a name="best-practices-for-using-app-service-local-cache"></a>Práticas recomendadas para usar o Cache Local do Serviço de Aplicativo
É recomendável que você use o Cache Local em conjunto com hello [ambientes de preparo](../app-service-web/web-sites-staged-publishing.md) recurso.

* Adicionar Olá *Autoadesivas* configuração do aplicativo `WEBSITE_LOCAL_CACHE_OPTION` com valor de saudação `Always` tooyour **produção** slot. Se você estiver usando `WEBSITE_LOCAL_CACHE_SIZEINMB`, também adicioná-lo como um slot de produção tooyour configuração temporária.
* Criar um **preparo** slot e publicar o slot de preparo tooyour. Normalmente, você não definir Olá slot toouse Cache Local tooenable um ciclo de vida de compilar-implantar-testar perfeito para se obter benefícios de saudação do Cache Local para o slot de produção de hello de preparo de preparo.
* Teste seu site no Slot de preparo.  
* Quando estiver pronto, execute uma [operação de permuta](../app-service-web/web-sites-staged-publishing.md#Swap) entre seus slots de Preparo e de Produção.  
* Configurações Autoadesivas incluem o nome e o slot tooa temporária. Assim ao slot de preparo Olá obtém trocada em produção, ele herdará as configurações de aplicativo de Cache Local hello. Olá permutado recentemente slot serão executadas no cache local Olá após alguns minutos e será aquecido como parte de aquecimento de slot após a troca de produção. Portanto quando a troca de slot Olá for concluída, o slot de produção serão executados no cache local hello.

## <a name="frequently-asked-questions-faq"></a>Perguntas frequentes (FAQ)
### <a name="how-can-i-tell-if-local-cache-applies-toomy-web-app"></a>Como saber se o Cache Local se aplica a toomy web aplicativo?
Se seu aplicativo web precisa de um repositório de conteúdo de alto desempenho e confiável, não usa dados críticos do toowrite Olá repositório de conteúdo em tempo de execução e é menor que 2 GB de tamanho total, Olá resposta é "Sim"! tamanho total de saudação de tooget das pastas /site e /siteextensions, você pode usar a extensão de site hello "Uso de disco de aplicativos de Web do Azure".  

### <a name="how-can-i-tell-if-my-site-has-switched-toousing-local-cache"></a>Como saber se meu site alternou toousing Cache Local?
Se você estiver usando o recurso de Cache Local Olá com ambientes de preparo, operação de permuta Olá não será concluída até que o Cache Local é aquecido. toocheck se seu site esteja em execução no Cache Local, você pode verificar a variável de ambiente do processo de trabalho de Olá `WEBSITE_LOCALCACHE_READY`. Use instruções de saudação em Olá [variável de ambiente do processo de trabalho](https://github.com/projectkudu/kudu/wiki/Process-Threads-list-and-minidump-gcdump-diagsession#process-environment-variable) tooaccess página Olá variável de ambiente de processo de trabalho em várias instâncias.  

### <a name="i-just-published-new-changes-but-my-web-app-does-not-seem-toohave-them-why"></a>Acabou de publicar novas alterações, mas o meu aplicativo web não tem toohave-los. Por quê?
Se seu aplicativo web usa o Cache Local, em seguida, será necessário toorestart suas alterações mais recentes do site tooget hello. Não quer o site de produção de tooa toopublish alterações? Consulte opções de slot Olá anterior seção de práticas recomendadas hello.

### <a name="where-are-my-logs"></a>Onde estão meus logs?
Com o cache local, as pastas de logs e de dados são um pouco diferentes. No entanto, hello estrutura de suas subpastas permaneça Olá mesmo, exceto pelo fato de subpastas de saudação são aninhadas em uma subpasta com hello formato "identificador exclusivo de VM" + o carimbo de data / hora.

### <a name="i-have-local-cache-enabled-but-my-web-app-still-gets-restarted-why-is-that-i-thought-local-cache-helped-with-frequent-app-restarts"></a>Meu Cache Local está habilitado, mas meu aplicativo Web ainda é reiniciado. Por que isso acontece? Pensei que o Cache Local ajudasse com reinicializações frequentes do aplicativo.
O Cache Local ajuda a evitar reinicializações de aplicativo Web relacionadas ao armazenamento. No entanto, seu aplicativo web ainda pode sofrer reinicializações durante as atualizações de infraestrutura planejada de saudação VM. Olá geral reinicializações de aplicativo com o Cache Local habilitado devem ser menos.

### <a name="does-local-cache-exclude-any-directories-from-being-copied-toohello-faster-local-drive"></a>Cache Local exclua as pastas sejam copiados unidade local mais rapidamente toohello?
Como parte da etapa de saudação que copia o conteúdo de armazenamento Olá qualquer pasta denominada repositório será excluída. Isso ajuda a cenários em que o conteúdo do site pode conter um repositório de controle de origem que não pode ser necessárias na operação de tooday dia do aplicativo web de saudação. 
