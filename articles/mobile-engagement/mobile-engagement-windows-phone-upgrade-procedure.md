---
title: "aaaWindows procedimentos de atualização do SDK Phone Silverlight"
description: "Procedimentos de atualização do SDK do Windows Phone Silverlight para o Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 87130026-9759-4659-9184-788a3627a165
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: d72e7b8a59ef2c0a95b22efbf1e5257271399ddc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-sdk-upgrade-procedures"></a>Procedimentos de atualização do SDK do Windows Phone Silverlight
Se você já tiver integrado uma versão mais antiga do nosso SDK em seu aplicativo, você tem Olá tooconsider pontos a seguir ao atualizar Olá SDK.

Você pode ter vários procedimentos de toofollow se perdidas várias versões do SDK de saudação. Por exemplo, se você migrar de 0.10.1 too0.11.0 ter toofirst siga hello "de 0.9.0 too0.10.1" procedimento e hello "de 0.10.1 too0.11.0" procedimento.

## <a name="from-200-too330"></a>De 2.0.0 too3.3.0
### <a name="test-logs"></a>Logs de teste
Logs do console produzidos pelo Olá SDK agora podem ser habilitado/desabilitado/filtradas. toocustomize, propriedade de saudação update `EngagementAgent.Instance.TestLogEnabled` tooone do valor de saudação disponível de saudação `EngagementTestLogLevel` enumeração, por exemplo:

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

## <a name="from-111-too200"></a>De 1.1.1 too2.0.0
Olá a seguir descrevem como toomigrate uma integração SDK da saudação Capptain serviço oferecido pelo Capptain SAS em um aplicativo da plataforma do Azure Mobile Engagement. 

> [!IMPORTANT]
> Capptain e o compromisso de mobilidade não são Olá mesmos serviços e procedimento Olá indicado abaixo só destaca como toomigrate Olá aplicativo cliente. Migrando Olá SDK no aplicativo hello não vai migrar seus dados do hello Capptain toohello Mobile Engagement de servidores
> 
> 

Se você estiver migrando de uma versão anterior, consulte Olá Capptain site da web toomigrate too1.1.1 primeiro e aplicar Olá procedimento

### <a name="nuget-package"></a>Pacote NuGet
Substitua **Capptain.WindowsPhone** pelo pacote Nuget **MicrosoftAzure.MobileEngagement**.

### <a name="applying-mobile-engagement"></a>Aplicando o Mobile Engagement
Olá SDK usa o termo Olá `Engagement`. Você precisa tooupdate toomatch seu projeto essa alteração.

É necessário toouninstall seu pacote do nuget Capptain atual. Considere que todas as alterações na pasta de recursos Capptain serão removidas. Se você quiser tookeep esses arquivos, em seguida, faça uma cópia deles.

Depois disso, instale o novo pacote de nuget de contrato do Microsoft Azure Olá no seu projeto. Você pode encontrá-lo diretamente no [Nuget](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement). Substitui essa ação, todos os arquivos de recursos usado pelo contrato e adiciona Olá novo contrato DLL tooyour referências de projeto.

Você tem as referências do projeto tooclean excluindo referências Capptain DLL. Se você não fizer isso, versão de saudação do Capptain entrarão em conflito e ocorrerão erros.

Se você tiver personalizado Capptain recursos, copie o conteúdo de arquivos antigos e colá-los em novos arquivos de contrato hello. Observe que os arquivos xaml e o cs toobe atualizado.

Quando essas etapas forem concluídas, você só tem referências antigas de Capptain tooreplace por novas referências de contrato hello.

1. Todos os namespaces Capptain ter toobe atualizado.
   
    Antes da migração:
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    Após a migração:
   
        using Microsoft.Azure.Engagement;
2. Todas as classes Capptain que contêm "Capptain" devem conter “Engagement".
   
    Antes da migração:
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    Após a migração:
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. Para os arquivos xaml o namespace e atributos Capptain também se alteram.
   
    Antes da migração:
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    Após a migração:
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. Para Olá a outros recursos, como imagens Capptain, observe que eles foram renomeado toouse "Contrato".

### <a name="application-id--sdk-key"></a>ID do aplicativo / chave do SDK
O Engagement usa uma cadeia de conexão. Você não tem toospecify uma ID de aplicativo e uma chave do SDK com o Mobile Engagement, tiver apenas toospecify uma cadeia de caracteres de conexão. Você pode configurá-la em seu arquivo EngagementConfiguration.

configuração do contrato Olá pode ser definida em sua `Resources\EngagementConfiguration.xml` arquivo do projeto.

Edite esse arquivo toospecify:

* A cadeia de conexão do aplicativo entre as marcas `<connectionString>` and `<\connectionString>`.

Se você quiser toospecify em tempo de execução em vez disso, você pode chamar a seguir Olá método antes da inicialização de agente do hello contrato:

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Initialize Engagement angent with above configuration. */
        EngagementAgent.Instance.Init(engagementConfiguration);

cadeia de caracteres de conexão de saudação para seu aplicativo é exibida no hello Portal clássico do Azure.

### <a name="items-name-change"></a>Alteração do nome de itens
Todos os itens chamados *capptain* foram nomeados como *engagement*. Da mesma forma para *Capptain* muito*contrato*.

Exemplos de itens do Capptain usados normalmente :

* CapptainConfiguration agora denominado EngagementConfiguration
* CapptainAgent agora denominado EngagementAgent
* CapptainReach agora denominado EngagementReach
* CapptainHttpConfig agora denominado EngagementHttpConfig
* GetCapptainPageName agora denominado GetEngagementPageName

Observe que renomear também afeta métodos substituídos.

