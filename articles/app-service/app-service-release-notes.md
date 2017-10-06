---
title: "Notas de versão aaaAzure SDK para .NET 2.5.1"
description: "Notas de versão SDK do Azure para .NET 2.5.1"
services: app-service
documentationcenter: .net,nodejs,java
author: Juliako
manager: erikre
editor: 
ms.assetid: 8d3d815f-bb58-447e-8ff0-f9b9603c7b00
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/10/2016
ms.author: juliako
ms.openlocfilehash: 5ee7688617c966baa409045881c172bbbc55ff63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-251-release-notes"></a>Notas de versão SDK do Azure para .NET 2.5.1
Este documento contém notas de versão de saudação do hello Azure SDK para .NET 2.5.1 de versão. 

## <a name="azure-sdk-for-net-251-release-notes"></a>Notas de versão SDK do Azure para .NET 2.5.1
Olá seguem novos recursos e atualizações no hello Azure SDK para .NET 2.5.1.

* Novos recursos/cenários relacionados muito**extensões de ferramentas do Web**. 
  
  * Sites do Azure foi renomeado tooAzure do serviço de aplicativo. Para obter mais informações, consulte [Serviço de Aplicativo do Azure e Serviços do Azure existentes](../app-service-web/app-service-changes-existing-services.md).
  * Foi adicionado suporte a aplicativos de API (visualização) do Azure para que os clientes podem publicar projetos do ASP.NET como aplicativos de API e, em seguida, usar Olá Adicionar > gesto de cliente de aplicativo de API do Azure em projetos toogenerate código c# com base na estrutura de saudação do hello implantado API App. 
  * nó de sites Olá no Gerenciador de servidores foi preterido no lugar do nó de serviço de aplicativo do Azure hello, que contém suporte para agrupamento de aplicativos de API do Azure, aplicativos móveis e aplicativos Web com base em grupo de recursos.
  * Foi adicionado suporte de aplicativos móveis (visualização) do Azure para que os clientes podem criar novos projetos de aplicativos móveis, adicionar controladores de aplicativos móveis, publicar projetos hello e depurar remotamente os aplicativos.
  * Adicionar > gesto de cliente de aplicativo de API do Azure agora dá suporte a arquivos JSON Swagger locais, para que os desenvolvedores de API da Web podem usar NuGets de terceiros como Swashbuckle toogenerate Swagger ou criá-lo manualmente. Dessa forma, os desenvolvedores de cliente podem usar tooconsume de recursos de geração de código Olá qualquer ponto de extremidade de Swagger em projetos c#. 
  * Aplicativo Web e API App caixas de diálogo de publicação foram conceito de Portal do Azure Olá toosupport aprimorado do recurso de agrupamento e seleção de/criação de grupos de recursos do Azure e planos de serviço de aplicativo são representados em Olá Web App e API App provisionamento caixa de diálogo Nova. 
  * Nós do Gerenciador de servidores de aplicativo de API do Azure fornecem links toohello que aplicativos de API profunda link no hello Portal do Azure, bem como outros recursos, como Log de Streaming e depuração remota.
    
    Para problemas conhecidos e limitações atuais no SDK do Azure .NET 2.5.1 [esta](app-service-release-notes.md#known_issues_2_5_1) seção abaixo.
* Novos recursos/cenários relacionados muito**ferramentas HDInsight** no Visual Studio estão habilitados nesta versão. 
  
  * Validação local de scripts do hive. Clique botão de script de validação de Olá no toosee da barra de ferramentas de saudação se há erros no script. 
  * Depuração de trabalhos de Hive aprimorada. Você pode depurar trabalhos de Hive acessando os logs de Yarn no Visual Studio. Se seu aplicativo tiver problemas de desempenho, investigar os logs YARN fornecerá informações úteis.
  * (Visualização pública) Preenchimento automático de palavra-chave e suporte IntelliSense para Hive. toohelp criar scripts de Hive, ferramentas de HDInsight para Visual Studio adicionou preenchimento automático de palavra-chave e suporte ao IntelliSense para o Hive.
  * Suporte para Storm. Agora você pode usar as ferramentas do HDInsight para Visual Studio toodevelop Storm topologias/Spouts/parafusos em c#. Você pode enviar hello desenvolvido cluster de Storm tooa topologia e ver o status de topologia/brilhante/spout hello. Você pode usar os logs de sistema e cliente registra tootroubleshoot seu Storm parafusos/topologias/Spouts. Você também pode usar os ativos JAVA existentes no Storm no HDInsight.
    
    Para obter mais informações, consulte [Introdução ao uso das ferramentas do HDInsight Hadoop para Visual Studio](../hdinsight/hdinsight-hadoop-visual-studio-tools-get-started.md).

## <a id="known_issues_2_5_1"></a>Limitações e problemas conhecidos do SDK do Azure para .NET 2.5.1
* O recurso de Aplicativos de API do Azure está visível como um destino de implantação para Aplicativos Móveis. Os aplicativos Web deve ser o destino de saudação apenas para aplicativos móveis até uma versão subsequente. 
* Azure App API de provisionamento pode resultar em êxito mas intermitentemente falha tooupdate Olá progresso na janela de atividade de serviço de aplicativo do Azure hello. Solução alternativa é o status de toocheck da API do Azure novo aplicativo hello em Olá Portal do Azure. 
* A experiência Arquivo > Novo Projeto > Aplicativo de API > F5 resulta em um erro de HTTP porque não há nenhum default/index.html. Solução alternativa é toomanually procurar toohello/api/valores URL. 
* Intermitentemente, ícones do Gerenciador de Servidores são exibidos na forma bidimensional. Reiniciar o VS resolve esse problema. 
* Se uma exceção for lançada durante o provisionamento de aplicativo Web ou API App (como erros de cota excedida ou o nome duplicado de gateway de aplicativo de API do Azure), erros de saudação mostram algum texto JSON bruto. 
* Problemas intermitentes de criação do projeto quando o Application Insights é verificado na hora da criação do projeto.
* Ocasionalmente, código de cliente de aplicativo de API do Azure Olá gerado está faltando namespaces, eles precisam toobe manualmente incluído (ou importados automaticamente por meio do Visual Studio indicações) para toocompile de código. 
* Projetos de aplicativo móvel devem ser publicado tooweb aplicativos, mas você deve escolher um site criado como um aplicativo móvel no hello Portal do Azure, como projetos de aplicativo móvel exigem um banco de dados. 
* página inicial de saudação para aplicativos móveis usa o termo hello "serviço móvel" em vez de "aplicativos móveis" 
* Criação do projeto de aplicativo móvel pode exigir até tooa toocreate de minuto. 
* Durante a API App provisionamento (em alguns casos), um erro é retornada pelo refletir o API do Azure Olá que permissões Olá não podem ser configuradas corretamente, durante a saudação API App foi provisionado corretamente e está pronto para uso. Você pode definir manualmente as permissões usando Olá Portal do Azure.
* Não há suporte para o Application Insights em modelos do Aplicativo de API e Aplicativos Móveis.
* Projetos de Aplicativo de API não podem ser usados em conjunto com os projetos de Serviço de Nuvem.
* Modelos de projeto de Aplicativo de API só estão disponíveis em C#.
* Consumo da API App por meio do menu de contexto de "Adicionar cliente de aplicativo de API do Azure" hello só tem suporte em c#.

