---
title: "aaaSet a integração contínua para microservices do Azure | Microsoft Docs"
description: "Obtenha uma visão geral de como tooset integração contínua e implantação para um aplicativo de malha do serviço usando o Visual Studio Team Services (VSTS)."
services: service-fabric
documentationcenter: na
author: mthalman-msft
manager: timlt
editor: 
ms.assetid: 3e8c2290-9e7a-456a-9b2c-db44d1b3988d
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 12/06/2016
ms.author: mthalman;mikhegn
ms.openlocfilehash: 041e081f4a42f379394f2d21f07db4f6de045b24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-service-fabric-continuous-integration-and-deployment-with-visual-studio-team-services"></a>Configurar a implantação e integração contínua do Service Fabric com o Visual Studio Team Services
Este artigo descreve Olá etapas tooset integração contínua e implantação de um aplicativo do Azure Service Fabric usando o Visual Studio Team Services (VSTS).

Este documento reflete o procedimento atual hello e é esperado toochange ao longo do tempo.

## <a name="prerequisites"></a>Pré-requisitos
tooget iniciado, siga estas etapas:

1. Certifique-se de que você tenha acesso tooa Team Services conta ou [criar um](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services) por conta própria.
2. Verifique se você tem o projeto de equipe do Team Services do access tooa ou [criar um](https://www.visualstudio.com/docs/setup-admin/create-team-project) por conta própria.
3. Certifique-se de que você tenha um toowhich de cluster do Service Fabric você pode implantar seu aplicativo ou criar um usando Olá [portal do Azure](service-fabric-cluster-creation-via-portal.md), uma [modelo do Azure Resource Manager](service-fabric-cluster-creation-via-arm.md), ou [Visual Studio ](service-fabric-cluster-creation-via-visual-studio.md).
4. Certifique-se de que você já tenha criado um projeto do Aplicativo do Service Fabric (.sfproj). Você deve ter um projeto que foi criado ou atualizado com o serviço de malha SDK 2.1 ou posterior (arquivo de .sfproj Olá deve conter um valor de propriedade ProjectVersion 1.1 ou superior).

> [!NOTE]
> Agentes de build personalizado não são mais necessários. Os agentes hospedados do Team Services agora têm o software de gerenciamento de cluster do Service Fabric pré-instalado, permitindo a implantação de seus aplicativos diretamente de agentes.
> 
> 

## <a name="configure-and-share-your-source-files"></a>Configurar e compartilhar seus arquivos de origem
primeira coisa que Olá desejar toodo é preparar um perfil de publicação para uso pelo processo de implantação de saudação que é executado no Team Services.  saudação de perfil de publicação deve ser o cluster de saudação tootarget configurado que você preparou anteriormente:

1. Escolha um perfil de publicação em seu projeto de aplicativo que você deseja toouse para seu fluxo de trabalho de integração contínua. Siga Olá [publicar instruções](service-fabric-publish-app-remote-cluster.md) sobre como toopublish um cluster remoto de tooa do aplicativo. Você não precisa realmente toopublish seu aplicativo embora. Você pode clicar em Olá **salvar** hiperlink no hello caixa de diálogo de publicação depois que você configurou as coisas corretamente.
2. Se você quiser que sua toobe de aplicativo atualizado para cada implantação que ocorre dentro do Team Services, você deseja tooconfigure Olá atualização tooenable do perfil de publicação. Em Olá mesmo publicar diálogo usado na etapa 1, certifique-se de que Olá **atualização Olá aplicativo** caixa de seleção é marcada.  Saiba mais sobre como [definir configurações de atualização adicionais](service-fabric-visualstudio-configure-upgrade.md). Clique em Olá **salvar** hiperlink toosave Olá configurações toohello perfil de publicação.
3. Certifique-se de que você salvou as alterações toohello publicar perfil e Cancelar Olá caixa de diálogo Publicar.
4. Agora é muito tempo[compartilhar seus arquivos de origem do projeto de aplicativo](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services#vs) com Team Services. Depois que os arquivos de origem são acessíveis no Team Services, agora você pode mover na próxima etapa toohello de geração de compilações. 

## <a name="create-a-build-definition"></a>Criar a definição de build
Uma definição de build do Team Services descreve um fluxo de trabalho composto por um conjunto de etapas de compilação que são executadas sequencialmente. meta de saudação da definição de compilação de saudação que você está criando é tooproduce um pacote de aplicativo de malha do serviço e outros artefatos, que podem ser usado toodeploy Olá aplicativo. Saiba mais sobre as [definições de build](https://www.visualstudio.com/docs/build/define/create)do Team Services.

### <a name="create-a-definition-from-hello-build-template"></a>Criar uma definição de modelo de compilação de saudação
1. Abra o projeto de equipe no Visual Studio Team Services.
2. Selecione Olá **criar** guia.
3. Verde Olá selecione  **+**  entrar toocreate uma nova definição de compilação.
4. Olá caixa de diálogo que é aberta, selecione **aplicativo do Azure Service Fabric** em Olá **criar** categoria de modelo.
5. Selecione **Avançar**.
6. Selecione repositório hello e ramificação associado ao seu aplicativo de malha do serviço.
7. Selecione a fila de agente de saudação desejar toouse. Há suporte para agentes hospedados.
8. Selecione **Criar**.
9. Salvar a definição de compilação hello e forneça um nome.
10. Olá, parágrafo a seguir é uma descrição das etapas de compilação Olá gerados pelo modelo hello:

| Etapa de build | Descrição |
| --- | --- |
| Restauração do NuGet |Restaura os pacotes do NuGet Olá para solução de saudação. |
| Compilar solução \*.sln |Compila a solução inteira hello. |
| Compilar solução \*.sfproj |Gera o pacote de aplicativo do Service Fabric Olá é usado toodeploy Olá aplicativo. local do pacote de aplicativo Hello é toobe especificado no diretório de artefato do build hello. |
| Atualizar Versões de Aplicativo do Service Fabric |Atualiza valores de versão de hello contidos em tooallow de arquivos de manifesto do pacote de aplicativo hello para suporte à atualização. Consulte Olá [página de documentação de tarefa](https://go.microsoft.com/fwlink/?LinkId=820529) para obter mais informações. |
| Copiar Arquivos |Olá cópias publicar perfil e toobe de artefatos de compilação do aplicativo parâmetros arquivos toohello consumido para a implantação. |
| Publicar o Artefato |Publica os artefatos de saudação da compilação. Permite que uma definição de versão artefatos da versão do tooconsume hello. |

### <a name="verify-hello-default-set-of-tasks"></a>Verifique se o conjunto padrão de saudação de tarefas
1. Verifique se Olá **solução** campo de entrada para Olá **restauração do NuGet** e **compilar solução** etapas de compilação.  Por padrão, essas etapas de compilação executar em todos os arquivos de solução que estão contidos no repositório de saudação associado.  Se você desejar somente Olá toooperate de definição de compilação em um desses arquivos de solução, você precisará de tooexplicitly atualização Olá caminho toothat arquivo.
2. Verifique se Olá **solução** campo de entrada para Olá **empacotar aplicativo** passo de compilação.  Por padrão, essa etapa de compilação presume que existe apenas um projeto de aplicativo do Service Fabric (.sfproj) no repositório de saudação.  Se você tiver vários esses arquivos em seu repositório e deseja tootarget apenas uma para esta definição de compilação, você precisará de tooexplicitly atualização Olá caminho toothat arquivo.  Se você quiser toopackage de projetos de vários aplicativos em seu repositório, você precisa toocreate adicionais **compilar do Visual Studio** etapas na definição de compilação de saudação que cada um projeto de aplicativo de destino.  Também, em seguida, seria necessário Olá tooupdate **argumentos de MSBuild** campo para cada uma das etapas de compilação para que o local do pacote de saudação é exclusivo para cada um deles.
3. Verificar o comportamento do controle de versão Olá definido no hello **versões de aplicativo de malha de serviço de atualização** passo de compilação.  Por padrão, essa etapa de compilação acrescenta Olá compilação tooall versão valores numéricos nos arquivos de manifesto do pacote de aplicativo hello. Consulte Olá [página de documentação de tarefa](https://go.microsoft.com/fwlink/?LinkId=820529) para obter mais informações. Isso é útil para dar suporte a atualização do aplicativo pois cada implantação de atualização requer valores de versão diferente de implantação anterior hello. Se você não estiver pretendendo toouse atualização do aplicativo no seu fluxo de trabalho, você pode considerar a desabilitação desta etapa de compilação. Ele deve ser desabilitado se sua intenção for tooproduce uma compilação que pode ser usado toooverwrite um aplicativo existente do Service Fabric. implantação Olá falhará se a versão de saudação do aplicativo hello produzido pela compilação Olá não corresponde a versão saudação do aplicativo hello cluster hello.
4. Se sua solução contiver um projeto .NET Core, certifique-se de que sua definição de compilação contém uma etapa de compilação que restaura dependências hello:
   1. Selecione **Adicionar etapa de build...**.
   2. Localizar Olá **de linha de comando** no guia de utilitário de saudação de tarefas e clique no botão Adicionar.
   3. Para campos de entrada da tarefa hello, use Olá valores a seguir:
   4. Ferramenta: dotnet
   5. Argumentos: restore
   6. Arraste tarefas Olá para que ele seja imediatamente após Olá **restauração do NuGet** etapa.
5. Salvar as alterações feitas toohello definição de compilação.

### <a name="try-it"></a>Experimente
Selecione **Enfileirar compilação** toomanually iniciar uma compilação. A compilação também é disparada durante o push ou check-in. Depois que você verificou a compilação hello está sendo executado com êxito, agora você pode mover em toodefining uma definição de versão que implanta o cluster de tooa do aplicativo.

## <a name="create-a-release-definition"></a>Criar uma definição de versão
Uma definição de versão do Team Services descreve um fluxo de trabalho composto por um conjunto de tarefas que são executadas sequencialmente. meta de saudação da definição de versão de saudação que você está criando é tootake um pacote de aplicativos e implantá-lo tooa cluster. Quando usados juntos, a definição de compilação hello e definição de versão pode executar o fluxo de trabalho inteiro Olá iniciem com tooending de arquivos de origem com um aplicativo em execução no cluster. Saiba mais sobre as [definições de versão](https://www.visualstudio.com/docs/release/author-release-definition/more-release-definition)do Team Services.

### <a name="create-a-definition-from-hello-release-template"></a>Criar uma definição de modelo de saudação de liberação
1. Abra o projeto no Visual Studio Team Services.
2. Selecione Olá **versão** guia.
3. Selecione Olá verde  **+**  toocreate uma nova definição de versão e selecione **criar versão definição** no menu de saudação.
4. Olá caixa de diálogo que é aberta, selecione **implantação de malha do serviço Azure** em Olá **implantação** categoria de modelo.
5. Selecione **Avançar**.
6. Selecione o que deseja toouse como origem Olá desta definição de versão de definição de compilação hello.  definição de compilação Olá versão definição referências Olá artefatos que foram produzidos pelo Olá selecionado.
7. Verificar Olá **implantação contínua** caixa de seleção se desejar toohave Team Services automaticamente cria uma nova versão e implantar o aplicativo de serviço de malha hello sempre que uma compilação é concluída.
8. Selecione a fila de agente de saudação desejar toouse. Há suporte para agentes hospedados.
9. Selecione **Criar**.
10. Edite nome de definição de Olá Olá ícone de lápis na parte superior de saudação da página de saudação.
11. Selecione Olá cluster toowhich seu aplicativo deve ser implantado no hello **Conexão Cluster** campo de entrada de tarefa hello. conexão de cluster Olá fornece informações Olá necessário permite Olá implantação tarefa tooconnect toohello cluster. Se você ainda não tiver uma conexão de cluster para o cluster, selecione Olá **gerenciar** hiperlink próxima toohello campo tooadd um. Na página de saudação que é aberta, execute Olá etapas a seguir:
    1. Selecione **novo ponto de extremidade de serviço** e, em seguida, selecione **Azure Service Fabric** menu hello.
    2. Selecione o tipo de saudação de autenticação usado pelo cluster Olá afetado por esse ponto de extremidade.
    3. Defina um nome para sua conexão em Olá **nome de Conexão** campo.  Normalmente, você poderia usar o nome de saudação do cluster.
    4. Definir a URL de ponto de extremidade de conexão de cliente Olá em Olá **ponto de extremidade do Cluster** campo.  Exemplo: tcp://contoso.westus.cloudapp.azure.com:19000.
    5. As credenciais do Active Directory do Azure, definir credenciais de saudação deseja toouse tooconnect toohello cluster Olá **Username** e **senha** campos.
    6. Para a autenticação baseada em certificado, defina Olá Base64 codificação do arquivo de certificado de cliente Olá no hello **certificado de cliente** campo.  Consulte a Ajuda pop-up a saudação nesse campo para obter informações sobre como tooget esse valor.  Se o certificado for protegido por senha, definir senha de saudação em Olá **senha** campo.
    7. Confirme suas alterações clicando em **OK**. Depois de navegar tooyour back definição de versão, clique em ícone de atualização de Olá Olá **Conexão Cluster** campo toosee Olá ponto de extremidade que acabou de adicionar.
12. Salve a definição de versão de saudação.

> [!NOTE]
> Contas da Microsoft (por exemplo, não há suporte para @hotmail.com ou @outlook.com) na autenticação do Azure Active Directory.
> 
> 

definição de saudação criado consiste em uma tarefa do tipo **implantação de aplicativo de malha do serviço**. Consulte Olá [página de documentação de tarefa](https://go.microsoft.com/fwlink/?LinkId=820528) para obter mais informações sobre essa tarefa.

### <a name="verify-hello-template-defaults"></a>Verifique se os padrões de modelo de saudação
1. Verificar Olá **perfil de publicação** campo de entrada para Olá **implantar o aplicativo do Service Fabric** tarefa. Por padrão, este campo faz referência a um perfil de publicação denominado Cloud.xml contidos em artefatos de saudação da compilação. Se você quiser tooreference um perfil de publicação diferente ou compilação Olá contém vários pacotes de aplicativos em seus artefatos, você precisa tooupdate Olá caminho adequadamente.
2. Verificar Olá **pacote de aplicativo** campo de entrada para Olá **implantar o aplicativo do Service Fabric** tarefa. Por padrão, este campo faz referência a caminho de pacote saudação padrão aplicativo usado no modelo de definição de compilação de saudação.  Se você modificou o caminho do pacote de aplicativo saudação padrão em Olá definição de compilação, você precisa tooupdate Olá caminho adequadamente aqui também.

### <a name="try-it"></a>Experimente
Selecione **criar versão** de saudação **versão** toomanually de menu do botão Criar uma versão. Olá caixa de diálogo que é aberta, selecione build Olá que você deseja toobase versão de saudação em e, em seguida, clique em **criar**. Se você tiver habilitado a implantação contínua, versões serão criadas automaticamente quando uma compilação conclusão da definição de compilação Olá associado.

## <a name="next-steps"></a>Próximas etapas
toolearn mais sobre a integração contínua com aplicativos do Service Fabric, ler Olá artigos a seguir:

* [Início da documentação do Team Services](https://www.visualstudio.com/docs/overview)
* [Gerenciamento de build no Team Services](https://www.visualstudio.com/docs/build/overview)
* [Gerenciamento de versão no Team Services](https://www.visualstudio.com/docs/release/overview)

