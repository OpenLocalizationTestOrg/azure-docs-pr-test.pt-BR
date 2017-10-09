---
title: aaaPrepare toopublish ou implantar um aplicativo do Azure do Visual Studio | Microsoft Docs
description: "Saiba Olá procedimentos tooset os serviços de conta de armazenamento e de nuvem e configurar seu aplicativo do Azure."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 92ee2f9e-ec49-4c7a-900d-620abe5e9d8a
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: b5231d400e2ad9e20c3f21bad48a77c328b1f7a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-toopublish-or-deploy-an-azure-application-from-visual-studio"></a>Preparar tooPublish ou implantar um aplicativo do Azure do Visual Studio
## <a name="overview"></a>Visão geral
Antes de publicar um projeto de serviço de nuvem, você deve configurar Olá serviços a seguir:

* Um **serviço de nuvem** toorun as funções do hello ambiente do Azure
* Um **conta de armazenamento** que fornece acesso a serviços de Blob, fila e tabela toohello.

Use Olá seguindo os procedimentos tooset esses serviços e configurar seu aplicativo

## <a name="create-a-cloud-service"></a>Criar um Serviço de Nuvem
toopublish um tooAzure de serviço de nuvem, você deve primeiro criar um serviço de nuvem, que executa suas funções no ambiente do Azure de saudação. Você pode criar um serviço de nuvem no hello [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885), conforme descrito na seção Olá **toocreate um serviço de nuvem usando Olá portal clássico do Azure**, mais adiante neste tópico. Você também pode criar um serviço de nuvem no Visual Studio usando o Assistente de publicação de saudação.

### <a name="toocreate-a-cloud-service-by-using-visual-studio"></a>toocreate um serviço de nuvem usando o Visual Studio
1. Abra o menu de atalho de saudação de saudação projeto do Azure e escolha **publicar**.

    ![VST_PublishMenu](./media/vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio/vst-publish-menu.png)
2. Se você ainda não tiver entrado, entrar com seu nome de usuário e senha para a conta da Microsoft hello ou conta organizacional associada à sua assinatura do Azure.
3. Escolha Olá **próximo** botão tooadvance toohello **configurações** página.

    ![Configurações comuns de assistente de publicação](./media/vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio/publish-settings-page.png)
4. Em Olá **serviços de nuvem** , escolha **criar novo**. Olá **criar serviços do Azure** caixa de diálogo é exibida.
5. Digite o nome de saudação do seu serviço de nuvem. nome de saudação faz parte do URL Olá para o serviço e, portanto, deve ser globalmente exclusivo. Olá não diferencia maiusculas de minúsculas.

### <a name="toocreate-a-cloud-service-by-using-hello-azure-classic-portal"></a>toocreate um serviço de nuvem usando Olá portal clássico do Azure
1. Entrar toohello [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkId=253103) no site da Microsoft hello.
2. toodisplay (opcional) uma lista de serviços de nuvem que você já criou, escolha o link de serviços de nuvem de saudação no lado esquerdo de saudação da página de saudação.
3. Escolha Olá  **+**  ícone em Olá inferior esquerdo de canto e, em seguida, escolha **serviço de nuvem** no menu de saudação que aparece. Outra tela com duas opções, **Criação rápida** e **Criação personalizada**, é exibida. Se você escolher **criação rápida**, você pode criar um serviço de nuvem apenas especificando sua URL e Olá região onde ele será fisicamente hospedado. Se você escolher **Criação personalizada**, você pode imediatamente publicar um serviço de nuvem, especificando um pacote (arquivo .cspkg), um arquivo de configuração (.cscfg), e um certificado. Criação personalizada não é necessária se você pretende toopublish seu serviço de nuvem usando Olá **publicar** comando em um projeto do Azure. Olá **publicar** comando está disponível no menu de atalho Olá para um projeto do Azure.
4. Escolha **criação rápida** toolater publicar seu serviço de nuvem usando o Visual Studio.
5. Especifique um nome para seu serviço de nuvem. URL completa Olá aparece próximo nome toohello.
6. Na lista de saudação, escolha a região Olá onde se encontram a maioria dos usuários.
7. Na parte inferior de saudação da janela hello, escolha Olá **criar serviço de nuvem** link.

## <a name="create-a-storage-account"></a>Criar uma conta de armazenamento
Uma conta de armazenamento fornece acesso a serviços de Blob, fila e tabela toohello. Você pode criar uma conta de armazenamento usando o Visual Studio ou hello [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkId=253103).

### <a name="toocreate-a-storage-account-by-using-visual-studio"></a>toocreate uma conta de armazenamento usando o Visual Studio
1. Em **Gerenciador de soluções**, abrir menu de atalho de saudação de saudação **armazenamento** nó e, em seguida, escolha **criar conta de armazenamento**.

    ![Criar uma nova conta de armazenamento do Azure](./media/vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio/IC744166.png)
2. Selecione ou digite Olá seguintes informações Olá nova conta de armazenamento no hello **criar conta de armazenamento** caixa de diálogo.

   * Olá toowhich de assinatura do Azure que você deseja tooadd conta de armazenamento de saudação.
   * Olá nome toouse para a nova conta de armazenamento hello.
   * região de saudação ou grupo de afinidade (como Oeste dos EUA ou Ásia Oriental).
   * Olá tipo de replicação você deseja toouse Olá conta de armazenamento, como com redundância geográfica.
3. Quando terminar, escolha **criar**.hello nova conta de armazenamento aparece no hello **armazenamento** lista **Server Explorer**.

### <a name="toocreate-a-storage-account-by-using-hello-azure-classic-portal"></a>toocreate uma conta de armazenamento usando Olá portal clássico do Azure
1. Entrar toohello [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkId=253103) no site da Microsoft hello.
2. (Opcional) tooview suas contas de armazenamento, escolha Olá **armazenamento** link no painel Olá Olá lado esquerdo da página de saudação.
3. No canto inferior esquerdo de saudação da página Olá, escolha Olá  **+**  ícone.
4. No menu de saudação que aparece, escolha **armazenamento**e, em seguida, escolha **criação rápida**.
5. Dê um nome que resulta em uma url exclusiva de conta de armazenamento hello.
6. Dê um nome ao serviço de nuvem. URL completa Olá aparece próximo nome toohello.
7. Na lista de saudação de regiões, escolha uma região onde a maioria dos usuários está localizada.
8. Especifique se deseja que a replicação geográfica tooenable. Se você habilitar a replicação geográfica, seus dados serão salvos em vários chance de saudação tooreduce locais físicos de perda. Esse recurso facilita o armazenamento mais caro, mas você pode reduzir o custo de hello, permitindo a localização geográfica ao criar conta de armazenamento Olá em vez de adicionar o recurso de hello mais tarde. Para obter mais informações, consulte [Replicação geográfica](http://go.microsoft.com/fwlink/?LinkId=253108).
9. Na parte inferior de saudação da janela hello, escolha Olá **criar conta de armazenamento** link.

Depois de criar sua conta de armazenamento, você verá Olá URLs que você pode usar recursos tooaccess em cada um dos serviços de armazenamento do Azure hello e também hello chaves de acesso primárias e secundárias para sua conta. Você usa essas chaves tooauthenticate solicitações feitas em relação aos serviços de armazenamento de saudação.

> [!NOTE]
> chave de acesso secundária Olá fornece Olá mesmo acessar a conta de armazenamento tooyour como chave de acesso primária Olá e é gerado como um backup de sua chave de acesso primário deve ser comprometida. Além disso, é recomendável que você gere novamente e regularmente suas chaves de acesso. Você pode modificar uma chave secundária conexão cadeia de caracteres configuração toouse Olá enquanto você regenera a chave primária de Olá, em seguida, você pode modificar-toouse Olá regenerada chave primária enquanto você regenera a chave secundária hello.
>
>

## <a name="configure-your-app-toouse-services-provided-by-hello-storage-account"></a>Configurar os serviços de toouse de aplicativo fornecidos pela conta de armazenamento Olá
Você deve configurar qualquer função que acessa serviços toouse Olá armazenamento do Azure serviços de armazenamento que você criou. toodo isso, você pode usar várias configurações de serviço para seu projeto do Azure. Por padrão, duas são criadas no projeto do Azure. Usando várias configurações de serviço, você pode usar o hello conexão mesma cadeia de caracteres em seu código, mas tem um valor diferente para uma cadeia de caracteres de conexão em cada configuração de serviço. Por exemplo, você pode usar um toorun de configuração de serviço e depurar seu aplicativo localmente usando o emulador de armazenamento do Azure hello e um toopublish de configuração de serviço diferentes tooAzure seu aplicativo. Para obter mais informações sobre configurações de serviço, consulte [Configurando o Projeto do Azure usando várias configurações de serviço](vs-azure-tools-multiple-services-project-configurations.md).

### <a name="tooconfigure-your-application-toouse-services-that-hello-storage-account-provides"></a>tooconfigure os serviços do aplicativo toouse que Olá conta de armazenamento fornece
1. Abra sua solução Azure no Visual Studio. No Gerenciador de soluções, abra o menu de atalho de saudação para cada função em seu projeto do Azure que acessa os serviços de armazenamento hello e escolha **propriedades**. Uma página com o nome de saudação da função de saudação é exibida no editor do Visual Studio hello. página de saudação exibe campos Olá Olá **configuração** guia.
2. Nas páginas de propriedade Olá para função hello, escolha **configurações**.
3. Em Olá **configuração do serviço** , escolha o nome de saudação da configuração do serviço de saudação que você deseja tooedit. Se você quiser toomake tooall de alterações das configurações de serviço Olá para essa função, você pode escolher **todas as configurações de**.  Para obter mais informações sobre como tooupdate as configurações de serviço, consulte a seção de saudação **gerenciar cadeias de caracteres de Conexão para contas de armazenamento** tópico Olá [configurar funções de saudação para um serviço de nuvem do Azure com o Visual Studio ](vs-azure-tools-configure-roles-for-cloud-service.md).
4. toomodify quaisquer configurações de cadeia de caracteres de conexão, escolha Olá **...** botão de próxima configuração toohello. Olá **criar cadeia de Conexão de armazenamento** caixa de diálogo é exibida.
5. Em **se conectar usando**, escolha Olá **sua assinatura** opção.
6. Em Olá **assinatura** , escolha sua assinatura. Se a lista Olá de assinaturas não incluem hello que você deseja, escolha Olá **baixar configurações de publicação** link.
7. Em Olá **nome da conta** , escolha o nome da sua conta de armazenamento. Ferramentas do Azure obtêm credenciais da conta de armazenamento automaticamente usando o arquivo. publishsettings de saudação. toospecify credenciais de sua conta de armazenamento manualmente, escolha Olá **credenciais inseridas manualmente** opção e, em seguida, continue com este procedimento. Você pode obter o nome da conta de armazenamento e a chave primária da saudação [portal clássico do Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885). Se você não quiser toospecify suas configurações de conta de armazenamento manualmente, escolha Olá **Okey** caixa de diálogo do botão tooclose hello.
8. Escolha Olá **insira a conta de armazenamento** link de credenciais.
9. Em Olá **nome da conta** , digite o nome da saudação da sua conta de armazenamento.

   > [!NOTE]
   > Faça logon no hello [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885)e, em seguida, escolha Olá **armazenamento** botão. portal de saudação mostra uma lista de contas de armazenamento. Se você escolher uma conta, uma página será aberta para ela. Você pode copiar nome Olá Olá da conta de armazenamento nesta página. Se você estiver usando uma versão anterior do portal clássico do hello, nome de saudação da sua conta de armazenamento aparece no hello **contas de armazenamento** exibição. toocopy nome, realçá-lo no hello **propriedades** janela deste exibir e, em seguida, escolha chaves Olá Ctrl-C. nome de saudação toopaste no Visual Studio, escolha Olá **nome da conta** texto caixa e, em seguida, escolha as teclas Ctrl + V de saudação.
   >
   >
10. Em Olá **chave de conta** caixa, digite sua chave primária ou copie e cole-o da saudação [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885).
     toocopy esta tecla:

    1. Na parte inferior de saudação da página Olá Olá apropriado conta de armazenamento, escolha Olá **gerenciar chaves** botão.
    2. Em Olá **gerenciar chaves de acesso** página, selecione o texto de saudação da chave de acesso primária hello e em seguida, escolha as teclas Ctrl + C de saudação.
    3. Em ferramentas do Azure, cole na chave Olá Olá **chave de conta** caixa.
    4. Você deve selecionar uma saudação toodetermine opções a seguir como serviço de saudação acessará a conta de armazenamento hello:

       * **Usar HTTP**. Essa é a opção de padrão de saudação. Por exemplo: `http://<account name>.blob.core.windows.net`.
       * **Use HTTPS** para uma conexão segura. Por exemplo: `https://<accountname>.blob.core.windows.net`.
       * **Especificar pontos de extremidade personalizados** para cada Olá três serviços. Você pode digitar esses pontos de extremidade no campo Olá para serviço específico hello.

         > [!NOTE]
         > Se você criar pontos de extremidade personalizados, poderá criar uma cadeia de conexão mais complexa. Quando você usar esse formato de cadeia de caracteres, você pode especificar pontos de extremidade de serviço de armazenamento que incluem um nome de domínio personalizado que você registrou para sua conta de armazenamento com hello serviço Blob. Também você pode conceder acesso apenas tooblob recursos em um único contêiner por meio de uma assinatura de acesso compartilhado. Para obter mais informações sobre como toocreate pontos de extremidade personalizados, consulte [configurar cadeias de Conexão de armazenamento do Azure](storage/common/storage-configure-connection-string.md).
         >
         >
11. toosave essas alterações de cadeia de caracteres de conexão, escolha Olá **Okey** botão e, em seguida, escolha Olá **salvar** botão na barra de ferramentas de saudação. Depois que você salva essas alterações, você pode obter o valor de saudação dessa cadeia de caracteres de conexão no seu código usando [GetConfigurationSettingValue](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getconfigurationsettingvalue.aspx). Quando você publica seu aplicativo tooAzure, escolha a configuração de serviço de saudação que contém a conta de armazenamento do Azure Olá para cadeia de caracteres de conexão de saudação. Depois que o aplicativo é publicado, verifique se o aplicativo hello funciona conforme o esperado em relação aos serviços de armazenamento do Azure Olá

## <a name="next-steps"></a>Próximas etapas
toolearn mais sobre como publicar aplicativos tooAzure do Visual Studio, consulte [publicando um serviço de nuvem usando ferramentas do Azure Olá](vs-azure-tools-publishing-a-cloud-service.md).
