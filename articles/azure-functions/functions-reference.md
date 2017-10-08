---
title: "aaaGuidance para o desenvolvimento de funções do Azure | Microsoft Docs"
description: "Saiba os conceitos de funções do Azure hello e técnicas que você precisa de funções de toodevelop no Azure, em todas as linguagens de programação e associações."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "guia do desenvolvedor, azure functions, funções, processamento de eventos, webhooks, computação dinâmica, arquitetura sem servidor"
ms.assetid: d8efe41a-bef8-4167-ba97-f3e016fcd39e
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/30/2017
ms.author: chrande
ms.openlocfilehash: 86d37dae5333f615faafc966e9da6e08e0a6354e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-developers-guide"></a>Guia do desenvolvedor do Azure Functions
Em funções do Azure, funções específicas compartilham alguns conceitos técnicos principais e componentes, independentemente do idioma de saudação ou associação usada. Antes de começar em detalhes tooa específico determinado idioma ou associação de aprendizado, ser tooread-se a esta visão geral que se aplica a tooall deles.

Este artigo pressupõe que você já leu Olá [visão geral de funções do Azure](functions-overview.md) e estiver familiarizado com [conceitos do SDK do WebJobs como gatilhos, associações e o tempo de execução do hello JobHost](../app-service-web/websites-dotnet-webjobs-sdk.md). As funções do Azure baseia-se em Olá SDK do WebJobs. 

## <a name="function-code"></a>Código de função
Um *função* Olá o conceito principal em funções do Azure. Escrever código para uma função em um idioma de sua escolha e salve o código de saudação e Olá de arquivos de configuração na mesma pasta. configuração de saudação é nomeada `function.json`, que contém dados de configuração JSON. Há suporte para vários idiomas, e cada um tem um toowork ligeiramente diferentes experiência otimizada recomendada para esse idioma. 

arquivo de function.json Olá define associações de função hello e outras definições de configuração. saudação de tempo de execução usa toomonitor de eventos neste arquivo toodetermine hello e como toopass dados e retornar dados de função execução. a seguir Olá é um exemplo de arquivo function.json.

```json
{
    "disabled":false,
    "bindings":[
        // ... bindings here
        {
            "type": "bindingType",
            "direction": "in",
            "name": "myParamName",
            // ... more depending on binding
        }
    ]
}
```

Saudação de conjunto `disabled` propriedade muito`true` tooprevent função de saudação do que está sendo executada.

Olá `bindings` propriedade é onde você configura os disparadores e associações. Cada associação compartilha algumas configurações comuns e algumas configurações, que são específicos tooa determinado tipo de associação. Cada associação requer Olá configurações a seguir:

| Propriedade | Valores/Tipos | Comentários |
| --- | --- | --- |
| `type` |string |Tipo de binding. Por exemplo: `queueTrigger`. |
| `direction` |'in', 'out' |Indica se a associação de saudação é para receber dados em função hello ou envio de dados de função hello. |
| `name` |string |nome de saudação que é usado para Olá dados associados na função hello. Para c#, este é o nome de um argumento; chave de saudação em uma lista de chave/valor-do para JavaScript. |

## <a name="function-app"></a>Aplicativo de funções
Um aplicativo de funções é composto por uma ou mais funções individuais que são gerenciadas em conjunto pelo Serviço de Aplicativo do Azure. Todas as funções hello em um compartilhamento de aplicativo de função hello mesmo preços do plano, a implantação contínua e a versão de tempo de execução. Funções escritas em pode de vários idiomas compartilham Olá mesma função de aplicativo. Pensar em um aplicativo de função como uma maneira tooorganize e coletivamente gerenciar suas funções. 

## <a name="runtime-script-host-and-web-host"></a>Tempo de execução (host de script e host Web)
tempo de execução de saudação ou host de script, é Olá subjacente SDK do WebJobs host que escuta eventos, coleta e envia dados e, por fim, executa o seu código. 

gatilhos de toofacilitate HTTP, também é um host da web que é projetado toosit na frente do host de script hello em cenários de produção. Ter dois hosts ajuda a host de script hello tooisolate do tráfego de front-end Olá gerenciado por Olá web host.

## <a name="folder-structure"></a>Estrutura de pastas
[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

Ao configurar um projeto para implantar o aplicativo de função tooa funções no serviço de aplicativo do Azure, você pode tratar essa estrutura de pastas como o código do site. Você pode usar ferramentas como implantação e integração contínuas ou scripts de implantação personalizados para implantar a instalação do pacote de tempo ou a transpilação do código.

> [!NOTE]
> Certifique-se de que toodeploy seu `host.json` pastas de arquivo e a função diretamente toohello `wwwroot` pasta. Não inclua Olá `wwwroot` pasta em implantações. Caso contrário, você acabará com pastas `wwwroot\wwwroot`. 
> 
> 

## <a id="fileupdate"></a>Como tooupdate função arquivos do aplicativo
editor de função Hello incorporado Olá portal do Azure permite que você atualize Olá *function.json* arquivo e o arquivo de código de saudação para uma função. tooupload ou atualização de outros arquivos como *Package. JSON* ou *Project* ou dependências, você tem toouse outros métodos de implantação.

Função aplicativos são criados no serviço de aplicativo, portanto todos Olá [opções de implantação de aplicativos da web de toostandard disponíveis](../app-service-web/web-sites-deploy.md) também estão disponíveis para aplicativos de função. Aqui estão alguns métodos, você pode usar tooupload ou atualizar os arquivos de aplicativo de função. 

#### <a name="toouse-app-service-editor"></a>toouse Editor de aplicativo de serviço
1. No portal do Azure funções hello, clique em **configurações do aplicativo de função**.
2. Em Olá **configurações avançadas** seção, clique em **ir configurações do serviço tooApp**.
3. Clique em **Editor do Serviço de Aplicativo** na navegação do Menu do aplicativo em **FERRAMENTAS DE DESENVOLVIMENTO**.
4. Clique em **Ir**.
   
   Depois que o Editor de serviço de aplicativo é carregado, você verá Olá *host.json* pastas de arquivo e a função em *wwwroot*. 
5. Arquivos abertos tooedit-los, ou arrastar e soltar de seus arquivos de tooupload de máquina de desenvolvimento.

#### <a name="toouse-hello-function-apps-scm-kudu-endpoint"></a>ponto de extremidade do aplicativo de função hello toouse SCM (Kudu)
1. Navegue até: `https://<function_app_name>.scm.azurewebsites.net`.
2. Clique em **Console de Depuração > CMD**.
3. Navegue muito`D:\home\site\wwwroot\` tooupdate *host.json* ou `D:\home\site\wwwroot\<function_name>` tooupdate arquivos de uma função.
4. Arrastar e soltar um arquivo que você deseja tooupload para a pasta apropriada Olá na grade de arquivo hello. Há duas áreas na grade de arquivo hello onde você pode remover um arquivo. Para *. zip* arquivos, aparecerá uma caixa com rótulo hello "arraste aqui tooupload e descompacte." Para outros tipos de arquivo, drop na grade de arquivo hello, mas fora da caixa "unzip" hello.

<!--NOTE: I've removed documentation on FTP, because it does not sync triggers on hello consumption plan --DonnaM -->

#### <a name="toouse-continuous-deployment"></a>implantação contínua toouse
Siga as instruções de saudação do tópico de saudação [implantação contínua para funções do Azure](functions-continuous-deployment.md).

## <a name="parallel-execution"></a>Execução paralela
Quando vários eventos de gatilho ocorrem mais rápido do que um tempo de execução da função de thread único pode processá-las, tempo de execução de saudação pode chamar a função hello várias vezes em paralelo.  Se um aplicativo de função está usando Olá [consumo de plano de hospedagem](functions-scale.md#how-the-consumption-plan-works), Olá função aplicativo pode ser expandida automaticamente.  Cada instância do aplicativo de função hello, se o aplicativo hello é executado em Olá consumo plano ou uma expressão de hospedagem [plano de hospedagem do serviço de aplicativo](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md), podem processar invocações simultâneas em paralelo usando vários threads.  número máximo de saudação de chamadas simultâneas de função em cada instância do aplicativo de função varia com base no tipo de saudação do gatilho que está sendo usado, bem como recursos de Olá usados por outras funções em um aplicativo de função hello.

## <a name="functions-runtime-versioning"></a>Controle de versão de tempo de execução de funções

Você pode configurar a versão de saudação do tempo de execução de funções hello usando Olá `FUNCTIONS_EXTENSION_VERSION` configuração do aplicativo. Por exemplo, o valor de hello "~ 1" indica que o seu aplicativo com a função usará 1 como sua versão principal. Aplicativos de função são atualizados tooeach nova versão secundária que elas são lançadas. Você pode exibir a versão exata de saudação do seu aplicativo de função no hello **configurações** guia Olá Portal do Azure.

## <a name="repositories"></a>Repositórios
código de saudação para funções do Azure é o código-fonte aberto e armazenadas em repositórios GitHub:

* [Tempo de execução do Azure Functions](https://github.com/Azure/azure-webjobs-sdk-script/)
* [Portal do Azure Functions](https://github.com/projectkudu/AzureFunctionsPortal)
* [Modelos do Azure Functions](https://github.com/Azure/azure-webjobs-sdk-templates/)
* [SDK WebJobs do Azure](https://github.com/Azure/azure-webjobs-sdk/)
* [Extensões do SDK WebJobs do Azure](https://github.com/Azure/azure-webjobs-sdk-extensions/)

## <a name="bindings"></a>Associações
Veja uma tabela de todas as associações com suporte.

[!INCLUDE [dynamic compute](../../includes/functions-bindings.md)]

## <a name="reporting-issues"></a>Problemas de relatórios
[!INCLUDE [Reporting Issues](../../includes/functions-reporting-issues.md)]

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações, consulte Olá recursos a seguir:

* [Práticas recomendadas para o Azure Functions](functions-best-practices.md)
* [Referência do desenvolvedor de C# do Azure Functions](functions-reference-csharp.md)
* [Referência do desenvolvedor em F# do Azure Functions](functions-reference-fsharp.md)
* [Referência do desenvolvedor de NodeJS do Azure Functions](functions-reference-node.md)
* [Gatilhos e de associações do Azure Functions](functions-triggers-bindings.md)
* [As funções do Azure: Olá jornada](https://blogs.msdn.microsoft.com/appserviceteam/2016/04/27/azure-functions-the-journey/) no blog da equipe saudação do serviço de aplicativo do Azure. Um histórico de como o Azure Functions foi desenvolvido.

