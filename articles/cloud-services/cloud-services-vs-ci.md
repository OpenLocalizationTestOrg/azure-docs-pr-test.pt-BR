---
title: "Serviços de aaaContinuous de entrega para a nuvem com o Visual Studio Online | Microsoft Docs"
description: "Saiba como tooset a entrega contínua para o Azure aplicativos de nuvem sem salvar arquivos de configuração do serviço de toohello chave de armazenamento de diagnóstico"
services: cloud-services
documentationcenter: 
author: cawa
manager: paulyuk
editor: 
ms.assetid: 148b2959-c5db-4e4a-a7e9-fccb252e7e8a
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 11/02/2016
ms.author: cawa
ms.openlocfilehash: dc87d049e46daf8b8a26ee4450ebd9b7910f287b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="securely-save-cloud-services-diagnostics-storage-key-and-setup-continuous-integration-and-deployment-tooazure-using-visual-studio-online"></a>Securely salvar serviços diagnóstico chave armazenamento em nuvem e tooAzure integração contínua de instalação e implantação usando o Visual Studio Online
 É um projeto de origem de tooopen prática comum hoje em dia. Salvar segredos do aplicativo nos arquivos de configuração não é mais uma prática segura, já que vulnerabilidades de segurança são expostas a partir de segredos vazados de controles de origem pública. Armazenar segredo como texto sem formatação em um arquivo em um pipeline de integração contínua não é seguro em como servidores de compilação podem ser compartilhada recursos no ambiente de nuvem hello. Este artigo explica como o Visual Studio e o Visual Studio Online reduz as preocupações de segurança Olá durante o desenvolvimento e o processo de integração contínua.

## <a name="remove-diagnostics-storage-key-secret-in-project-configuration-file"></a>Remover o segredo de chave de armazenamento de diagnóstico em arquivo de configuração de projeto
A extensão de diagnóstico dos Serviços de Nuvem requer o armazenamento do Azure para salvar os resultados do diagnóstico. Anteriormente a cadeia de conexão de armazenamento Olá é especificada nos arquivos de configuração (. cscfg) de serviços de nuvem hello e pode fazer check-in controle toosource. Na versão mais recente do SDK do Azure de saudação alteramos o repositório de tooonly comportamento Olá uma conexão parcial de cadeia de caracteres com chave Olá substituído por um token. Olá etapas a seguir descreve como novas ferramentas de serviços de nuvem Olá funciona:

### <a name="1-open-hello-role-designer"></a>1. Abra o designer de função hello
* Clique duas vezes ou clique com o botão direito em um designer de função de tooopen de função de serviços de nuvem

![Abrir o designer de função][0]

### <a name="2-under-diagnostics-section-a-new-check-box-dont-remove-storage-key-secret-from-project-is-added"></a>2. Na seção de diagnóstico, uma nova caixa de seleção "Não remover o segredo da chave de armazenamento projeto" é adicionada
* Se você estiver usando o emulador de armazenamento local hello, essa caixa de seleção está desabilitada porque não há nenhum segredo toomanage para cadeia de conexão local hello, que é UseDevelopmentStorage = true.

![A cadeia de conexão do emulador de armazenamento local não é um segredo][1]

* Se você estiver criando um novo projeto, por padrão, essa caixa de seleção estará desmarcada. Isso resulta na seção chave de armazenamento de saudação do Olá selecionado que está sendo substituída por um token de cadeia de conexão de armazenamento. Olá valor do token Olá será localizada na pasta AppData Roaming do usuário atual hello, por exemplo: C:\Users\contosouser\AppData\Roaming\Microsoft\CloudService

> Observe a pasta user\AppData Olá é acesso controlado pela entrada do usuário e é considerada segredos de desenvolvimento de toostore um local seguro.
> 
> 

![A chave de armazenamento é salva na pasta de perfil de usuário][2]

### <a name="3-select-a-diagnostics-storage-account"></a>3. Selecionar uma conta de armazenamento de diagnóstico
* Selecione uma conta de armazenamento da caixa de diálogo Olá iniciada clicando Olá "..." . Observe como cadeia de conexão de armazenamento Olá gerado não terá chave de conta de armazenamento hello.
* Por exemplo: DefaultEndpointsProtocol=https;AccountName=contosostorage;AccountKey=$(*clouddiagstrg.key*)

### <a name="4----debugging-hello-project"></a>4.    Depuração de projeto Olá
* F5 toostart de depuração no Visual Studio. Tudo deve funcionar na saudação que mesma maneira como antes.
  ![Iniciar a depuração no local][3]

### <a name="5-publish-project-from-visual-studio"></a>5. Publicar o projeto do Visual Studio
* Olá iniciar caixa de diálogo Publicar e prossiga com instruções entrar toopublish Olá aplicativo tooAzure.

### <a name="6-additional-information"></a>6. Informações adicionais
> Observação: painel de configurações de saudação no designer de função hello permanecerá como é agora. Se você quiser recursos de gerenciamento de informações secretas Olá toouse para diagnóstico, vá toohello guia de configurações.
> 
> 

![Adicionar configurações][4]

> Observação: Se habilitada, Olá Application Insights chave será armazenada como texto sem formatação. chave de saudação só é usada para carregar conteúdo para que não há dados confidenciais em risco de comprometimento.
> 
> 

## <a name="build-and-publish-a-cloud-services-project-using-visual-studio-online-task-templates"></a>Criar e publicar um projeto dos Serviços de Nuvem usando modelos de tarefa do Visual Studio Online
* Olá, as etapas a seguir ilustra como toosetup integração contínua para serviços de nuvem projeto usar tarefas do Visual Studio online:
  ### <a name="1----obtain-a-vso-account"></a>1.    Obter uma conta do VSO
* [Criar a conta do Visual Studio Online] [ Create Visual Studio Online account] se você não tiver um
* [Criar projeto de equipe] [ Create team project] na conta do Visual Studio online

### <a name="2----setup-source-control-in-visual-studio"></a>2.    Configurar o controle de origem no Visual Studio
* Conecte-se o projeto de equipe tooa

![Conectar projeto tooteam][5]

![Selecione tooconnect de projeto de equipe para][6]

* Adicionar o controle de toosource de projeto

![Adicionar projeto toosource controle][7]

![Pasta de controle de origem do mapa projeto tooa][8]

* Fazer check-in do seu projeto no Team Explorer

![Check-in de controle de toosource de projeto][9]

### <a name="3----configure-build-process"></a>3.    Configurar o processo de compilação
* Procurar um projeto de equipe tooyour e adicione um novo processo de compilação modelos

![Adicionar uma nova compilação][10]

* Selecionar tarefa de compilação

![Adicionar uma tarefa de compilação][11]

![Selecionar o modelo de tarefa Compilação do Visual Studio][12]

* Edite a entrada da tarefa de compilação. Personalize compilação Olá parâmetros de acordo com tooyour necessário

![Configurar a tarefa de compilação][13]

`/t:Publish /p:TargetProfile=$(targetProfile) /p:DebugType=None /p:SkipInvalidConfigurations=true /p:OutputPath=bin\ /p:PublishDir="$(build.artifactstagingdirectory)\\"`

* Configurar variáveis de compilação

![Configurar variáveis de compilação][14]

* Adicionar um destino de compilação tooupload tarefa

![Escolher publicar tarefa de local de compilação][15]

![Configurar publicar tarefa de compilação de local de publicação][16]

* Executar compilação Olá

![Enfileirar Nova Compilação][17]

![Exibir o resumo da compilação][18]

* Se a compilação de saudação for bem-sucedida, você verá um toobelow semelhante de resultado

![Resultado da compilação][19]

### <a name="4----configure-release-process"></a>4.    Configurar o processo de lançamento
* Criar uma nova versão

![Criar nova versão][20]

* Selecione a tarefa de implantação de serviços de nuvem do Azure Olá

![Selecionar a tarefa de implantação dos Serviços de Nuvem do Azure][21]

* Como a chave de conta de armazenamento Olá não está marcada no controle toosource, precisamos chave secreta do toospecify Olá para configurar extensões de diagnóstico. Expanda Olá **opções avançadas para criar novo serviço** seção e editar Olá **chaves de conta de armazenamento de diagnóstico** entrada de parâmetro. Essa entrada leva em várias linhas do par chave-valor no formato de saudação do **[RoleName]:$(StorageAccountKey)**

> Observação: se sua conta de armazenamento está sob de diagnóstico hello mesma assinatura em que você publicará o aplicativo de serviços de nuvem hello, você não tiver tooenter Olá chave na entrada de tarefa de implantação Olá; implantação Olá programaticamente Obtenha informações de armazenamento de saudação da sua assinatura
> 
> 

![Configurar a tarefa de implantação dos Serviços de Nuvem][22]

* Segredo do uso de compilação variáveis toosave chaves de armazenamento. toomask uma variável como um segredo clique no ícone de cadeado Olá Olá direita de saudação variáveis de entrada

![Salvar chaves de armazenamento em variáveis de compilação secretas][23]

* Criar uma versão e implantar seu projeto tooAzure

![Criar nova versão][24]

## <a name="next-steps"></a>Próximas etapas
toolearn mais sobre a configuração de extensões de diagnóstico para os serviços de nuvem do Azure, consulte [habilitar o diagnóstico nos serviços de nuvem do Azure usando o PowerShell][Enable diagnostics in Azure Cloud Services using PowerShell]

[Create Visual Studio Online account]:https://www.visualstudio.com/team-services/
[Create team project]: https://www.visualstudio.com/it-it/docs/setup-admin/team-services/connect-to-visual-studio-team-services
[Enable diagnostics in Azure Cloud Services using PowerShell]:https://azure.microsoft.com/en-us/documentation/articles/cloud-services-diagnostics-powershell/

[0]: ./media/cloud-services-vs-ci/vs-01.png
[1]: ./media/cloud-services-vs-ci/vs-02.png
[2]: ./media/cloud-services-vs-ci/file-01.png
[3]: ./media/cloud-services-vs-ci/vs-03.png
[4]: ./media/cloud-services-vs-ci/vs-04.png
[5]: ./media/cloud-services-vs-ci/vs-05.png
[6]: ./media/cloud-services-vs-ci/vs-06.png
[7]: ./media/cloud-services-vs-ci/vs-07.png
[8]: ./media/cloud-services-vs-ci/vs-08.png
[9]: ./media/cloud-services-vs-ci/vs-09.png
[10]: ./media/cloud-services-vs-ci/vso-01.png
[11]: ./media/cloud-services-vs-ci/vso-02.png
[12]: ./media/cloud-services-vs-ci/vso-03.png
[13]: ./media/cloud-services-vs-ci/vso-04.png
[14]: ./media/cloud-services-vs-ci/vso-05.png
[15]: ./media/cloud-services-vs-ci/vso-06.png
[16]: ./media/cloud-services-vs-ci/vso-07.png
[17]: ./media/cloud-services-vs-ci/vso-08.png
[18]: ./media/cloud-services-vs-ci/vso-09.png
[19]: ./media/cloud-services-vs-ci/vso-10.png
[20]: ./media/cloud-services-vs-ci/vso-11.png
[21]: ./media/cloud-services-vs-ci/vso-12.png
[22]: ./media/cloud-services-vs-ci/vso-13.png
[23]: ./media/cloud-services-vs-ci/vso-14.png
[24]: ./media/cloud-services-vs-ci/vso-15.png
