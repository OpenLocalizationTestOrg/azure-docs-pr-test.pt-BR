---
title: "Notas de versão do SDK para .NET 2.7 e .NET 2.7.1 de aaaAzure"
description: "Notas de versão do SDK do Azure para .NET 2.7 e .NET 2.7.1"
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: 877d070a-9bd5-49b3-8fac-6bb5f65c3554
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: 8ec72b0f18702e6d811f0cbe4790685be7881d96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-27-and-net-271-release-notes"></a>Notas de versão do SDK do Azure para .NET 2.7 e .NET 2.7.1
## <a name="overview"></a>Visão geral
Este documento contém notas de versão de saudação do hello Azure SDK versão 2.7 .NET. 

documento Hello também contém notas de versão de saudação do hello Azure SDK para .NET 2.7.1 de versão.

O SDK 2.7 do Azure tem suporte apenas no Visual Studio 2015 e Visual Studio 2013. [Azure SDK 2.6](https://azure.microsoft.com/downloads/) é Olá suporte último SDK para o Visual Studio 2012.

Para obter informações detalhadas sobre esta versão, confira a [postagem de anúncio do SDK 2.7 do Azure](https://azure.microsoft.com/blog/2015/07/20/announcing-the-azure-sdk-2-7-for-net/) e a [postagem de anúncio do SDK 2.7.1 do Azure](http://go.microsoft.com/fwlink/?LinkId=623850).

## <a name="azure-sdk-for-net-27"></a>SDK do Azure para .NET 2.7
### <a name="sign-in-improvements-for-visual-studio-2015"></a>Aprimoramentos de inscrição do Visual Studio 2015
2.7 de SDK do Azure para Visual Studio 2015 oferece suporte a novos recursos de gerenciamento de identidade Olá no Visual Studio 2015.  Isso inclui suporte para contas que acessam o Azure por meio do controle de acesso com base em função, provedores de soluções de nuvem, DreamSpark e outros tipos de conta e assinatura.

Olá entrar melhorias incluídas com o Azure SDK 2.7 só estão disponíveis no Visual Studio 2015. O suporte para Visual Studio 2013 está incluído no SDK do Azure 2.7.1.

### <a name="mobile-sdk"></a>SDK móvel
Atualizado **aplicativos móveis** tooreflect de modelos mais recente [pacote NuGet](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) e o processo de instalação.

### <a name="service-bus"></a>Barramento de Serviço
Correções de bugs e aprimoramentos gerais. Para obter detalhes sobre os recursos e atualizações, consulte toohello notas de versão mais recente Olá [NuGet do barramento de serviço](http://www.nuget.org/packages/WindowsAzure.ServiceBus/).

### <a name="hdinsight-tools"></a>Ferramentas do HDInsight
Em Olá essa versão seguintes atualizações foram feitas. Essas atualizações estão no modo de visualização. Para saber mais, confira [este blog](http://go.microsoft.com/fwlink/?LinkId=619108).

* Gráficos de hive para Hive em trabalhos Tez
* Suporte total para IntelliSense do DML do Hive
* Suporte de modelo do pig
* Modelos de Storm para serviços do Azure

#### <a name="breaking-changes"></a>Alterações de última hora
* Antigo **Storm** projeto deve ser atualizado quando esta versão das ferramentas de saudação. Para saber mais, confira [este blog](http://go.microsoft.com/fwlink/?LinkId=619108).
* Não há mais suporte para o Visual Studio Web Express. Para saber mais, confira [este blog](http://go.microsoft.com/fwlink/?LinkId=619108).

### <a name="azure-app-service-tools"></a>Ferramentas do Serviço de Aplicativo do Azure
Em Olá essa versão seguintes atualizações foram feitas tooWeb extensões de ferramentas. Para saber mais, confira [este](https://azure.microsoft.com/blog/2015/07/20/announcing-the-azure-sdk-2-7-for-net/) blog. 

* Suporte para contas do DreamSpark adicionado
* Alterar completo tooAzure ferramentas feitas toosupport Olá novas APIs de gerenciamento de recursos do Azure
* Suporte para o serviço de aplicativo do Azure adicionada muito[Cloud Explorer](#cloud_explorer)

#### <a name="known-issues"></a>Problemas conhecidos
Nós de slot de implantação de aplicativo Web não aparecem no nó de Slots Olá no Gerenciador de servidores, e nós de filho de slot de implantação de aplicativo Web não carregarão em soluções de nuvem. Esse problema foi resolvido e preparado para a próxima versão SDK hello. 

### <a name="cloud_explorer"></a>Gerenciador de nuvem para Visual Studio 2015
2.7 do SDK do Azure inclui Cloud Explorer para Visual Studio 2015 que permite que você tooview os recursos do Azure, inspecionar suas propriedades e executar ações de chave do desenvolvedor de dentro do Visual Studio. 

Soluções de nuvem oferece suporte à seguinte hello:

* Exibições de grupo de recursos e tipo de recurso de seus recursos do Azure 
* Pesquisar recursos por nome (disponível no modo de exibição do tipo de recurso)
* Suporte para assinaturas e recursos que têm o controle de acesso com base em função (RBAC) aplicado 
* Painel de ação integrada que mostra os recursos de tooselected específico de ações para desenvolvedores. Por exemplo: anexar o depurador remoto para máquinas virtuais criadas usando Olá pilha do Gerenciador de recursos, exibir dados de diagnóstico para máquinas virtuais etc.
* Painel de propriedades integradas que mostra as propriedades voltadas para desenvolvedores comumente necessárias durante o desenvolvimento e teste 
* Troca rápida de saudação conta toouse ao enumerar os recursos (use o comando configurações na barra de ferramentas) 
* Filtragem de assinaturas toouse ao enumerar os recursos (use o comando configurações na barra de ferramentas) 
* Links profundos toohello Portal do Azure para gerenciamento de recursos e grupos de recursos 

### <a name="azure-resource-manager-tools"></a>Ferramentas do gerenciador de recursos do Azure
Ferramentas de Gerenciador de recursos do Azure Olá foram toowork atualizado com novos tipos de assinatura e controle de acesso com base da função (RBAC).  Está incluída com essas alterações Olá capacidade toouse novas contas de armazenamento, além de tooclassic armazenamento, artefatos toostore durante a implantação.  

Se você estiver usando um projeto do grupo de recursos do Azure de uma versão anterior do SDK de saudação com hello 2.7 SDK, um novo script de implantação é necessário toodeploy usando uma nova conta de armazenamento, em vez de armazenamento clássicos.  Você será solicitado antes que as alterações sejam feitas tooyour projeto tooadd Olá novo script.  script antigo Olá será renomeado e você precisará toomanually fazer modificações toohello novo script.

### <a name="storage-explorer-tools"></a>Ferramentas do Gerenciador de Armazenamento
* Suporte à exibição de Blobs acrescentados. Mais informações disponíveis [nesta postagem do blog](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/04/13/introducing-azure-storage-append-blob.aspx). 
* Suporte à exibição de contas de armazenamento Premium por meio do Gerenciador de Servidores. Gerenciador de servidores serão exibidas somente blobs de página para contas de armazenamento premium como eles são o tipo de saudação só tem suportada para contas de armazenamento premium.

### <a name="azure-data-factory-tools-for-visual-studio"></a>Ferramentas da Azure Data Factory para o Visual Studio
Introdução às **Ferramentas da Azure Data Factory** para o Visual Studio. Abaixo estão os recursos Olá habilitado. Para obter mais informações, confira [este blog](http://go.microsoft.com/fwlink/?LinkId=617530) .

* **Modelo com base em criação**: selecione de maiusculas e minúsculas use baseado em modelos, modelos de movimentação de dados ou modelos de processamento de dados toodeploy uma solução de integração de dados de ponta a ponta e começar práticos rapidamente com a fábrica de dados. 
* **Integração com o Gerenciador de Soluções para criar e implantar as entidades de Data Factory**: crie e implante pipelines e entidades relacionadas como projetos do Visual Studio. 
* **Integração com o modo de exibição de diagrama para interação com o visual durante a criação**: criar visualmente pipelines e conjuntos de dados com o auxílio do hello exibição de diagrama. 
* **Integração com o Gerenciador de servidores para navegação e interação com entidades já implantadas**: Aproveite Olá Server Explorer toobrowse já implantado fábricas de dados e entidades correspondentes. Importe um Data Factory implantado ou qualquer entidade (Pipeline, serviço vinculado, conjuntos de dados) no seu projeto. 
* **Edição de JSON com validação de esquema e IntelliSense avançado**: configure de forma eficiente e edite documentos JSON de entidades de Data Factory com IntelliSense avançado e validação de esquema 
* **Publicação com vários ambiente**: publicar toodev pipelines criados, teste ou ambiente de produção com a criação de arquivos de configuração separado para cada ambiente.
* **Suporte ao processamento de dados com base em Pig, Hive e .Net**: suporte para scripts Pig e Hive no projeto de Data Factory. Suporte para referenciar o Projeto C# para gerenciar atividade do .Net.

## <a name="azure-sdk-for-net-271"></a>SDK do Azure para .NET 2.7.1
Olá seção a seguir contém as atualizações que foram introduzidas com hello Azure SDK para .NET 2.7.1 de versão.

### <a name="hdinsight-tools"></a>Ferramentas do HDInsight
Para obter mais explicações sobre atualizações de ferramentas de HDInsight, consulte [Este blog](http://go.microsoft.com/fwlink/?LinkId=623831).

* Exibição de Operador de Trabalho do Hive (um novo recurso)
  
    toohelp compreender sua consulta de Hive melhor, recurso de exibição de operador Hive Olá foi adicionado. toosee todos os operadores de saudação dentro de um vértice, clique duas vezes em vértices Olá Olá do gráfico de trabalho. tooview mais detalhes sobre um operador específico, passe o mouse sobre esse operador.
* Marcador de Erro do Hive (um novo recurso)
  
    tooenable que tooview Olá erros gramaticais imediatamente, Olá recurso Hive marcador de erro foi adicionado. Além disso, as mensagens de erro foram aprimoradas e agora você pode ver erros gramaticais detalhadas instantaneamente (até nesta versão, você precisava toosubmit um cluster de toohello de script de Hive e aguarde algum tempo antes de obter detalhes sobre a mensagem de erro).  
* Gráfico de topologia Storm (um novo recurso)
  
    Visualizando é muito importante quando você deseja toosee se a topologia está funcionando conforme o esperado. Nesta versão, adicionamos visualização para gráficos Storm. Você pode visualizar as métricas importantes Olá para a sua topologia (por exemplo, uma cor indica se um determinado raio é "ocupado" ou não). Você pode também clicar duas vezes Olá brilhante/Spout tooview obter mais detalhes.
* Suporte para clusters de HDInsight que foram criados no hello Portal do Azure (uma correção de erros)
  
    Você pode usar o Visual Studio tooview e enviar trabalhos tooall o HDInsight clusters, independentemente de onde o cluster Olá foram criadas.
* Suporte ao IntelliSense mais e mais rápido metadados Hive carregar (uma melhoria)
  
    Aprimoramos Olá IntelliSense adicionando mais sugestões de usuário amigável. Por exemplo, o alias de tabela pode agora também ser sugerido no IntelliSense para que você possa escrever sua consulta mais facilmente. Além disso, aprimoramos Olá Hive metadados carregamento de modo que apenas levar vários segundos toolist todos os bancos de dados de saudação, tabelas e colunas de sua metastore Hive.

Para obter mais explicações sobre atualizações de ferramentas de HDInsight, consulte [Este blog](http://go.microsoft.com/fwlink/?LinkId=623831).

### <a name="improvements-in-visual-studio-2013"></a>Aprimoramentos no Visual Studio 2013
* 2.7.1 do SDK do Azure permite que o Visual Studio 2013 tooaccess contas do Azure e assinaturas por meio do controle de acesso baseado em função, provedores de soluções de nuvem e Dreamspark.
* Com o SDK do Azure 2.7.1, nova janela de ferramenta Cloud Explorer Olá agora também está disponível no Visual Studio 2013.

### <a name="known-issues"></a>Problemas conhecidos
Instalando Olá SDK 2.6 do Azure ou 2.7.1 para Visual Studio Community 2013 em uma não - em inglês OS exibirá um aviso que Olá inglês e recursos diferentes do inglês do Visual Studio podem ser incompatível. Esse aviso pode ser descartado com segurança. Ele ocorrerá apenas se máquina Olá não continha uma instalação anterior do Visual Studio Community 2013 e você estiver instalando em uma não - em inglês OS Olá SDK. Aviso de saudação é exibido depois que o pacote de idiomas Olá aplica Olá RTM recursos tooVisual Studio, mas antes de aplicar a atualização 4. Ignorando aviso Olá permitirá Olá language pack toocontinue e aplicando Olá atualização 4 versão completa o pacote de idiomas Olá conteúdo.

Projetos do LightSwitch não são compatíveis com esta versão. Esse problema será resolvido com hello SDK próxima versão.

## <a name="also-see"></a>Consulte também
[Postagem de anúncio do SDK 2.7.1 do Azure](http://go.microsoft.com/fwlink/?LinkId=623850)

[Postagem de anúncio do SDK 2.7 do Azure](https://azure.microsoft.com/blog/2015/07/20/announcing-the-azure-sdk-2-7-for-net/)

[Suporte e informações de desativação de saudação do Azure SDK para .NET e APIs](https://msdn.microsoft.com/library/azure/dn479282.aspx/)

