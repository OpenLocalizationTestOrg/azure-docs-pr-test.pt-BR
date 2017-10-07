---
title: "aaaPublishing um serviço de nuvem usando ferramentas do Azure Olá | Microsoft Docs"
description: "Saiba mais sobre como toopublish Azure nuvem projetos de serviço usando o Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1a07b6e4-3678-4cbf-b37e-4520b402a3d9
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/14/2017
ms.author: kraigb
ms.openlocfilehash: 31ede8308146de2bb128b768f23f64eb85bc7548
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="publishing-a-cloud-service-using-hello-azure-tools"></a>Publicando um serviço de nuvem usando ferramentas do Azure Olá
Usando ferramentas do Azure Olá para Microsoft Visual Studio, você pode publicar seu aplicativo do Azure diretamente do Visual Studio. Visual Studio oferece suporte a integrado publicação tooeither Olá preparação ou Olá o ambiente de produção de um serviço de nuvem.

Para publicar um aplicativo do Azure, você deve ter uma assinatura do Azure. Você também deve configurar uma nuvem de serviços e armazenamento conta toobe usado pelo seu aplicativo. Você pode configurar isso no hello [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885).

> [!IMPORTANT]
> Quando você publicar, você pode selecionar o ambiente de implantação de saudação para seu serviço de nuvem. Você também deve selecionar uma conta de armazenamento que é o pacote de aplicativo hello toostore usado para a implantação. Após a implantação, o pacote de aplicativo hello é removido da conta de armazenamento de saudação.
> 
> 

Quando você estiver desenvolvendo e testando um aplicativo do Azure, você pode usar o Web Deploy toopublish alterações incrementalmente para funções web. Depois de publicar o seu ambiente de implantação do aplicativo tooa, implantação da Web permite implantar alterações diretamente a máquina virtual de toohello que está executando a função de web de saudação. Você não tem toopackage e publicar seu aplicativo inteiro do Azure cada vez que você deseja tooupdate seu tootest de função web alterações hello. Com essa abordagem, você pode ter suas alterações de função da web disponíveis na nuvem Olá para seu ambiente de implantação do aplicativo publicado tooa de teste sem toohave de espera.

Use Olá toopublish procedimentos a seguir seu aplicativo do Azure e tooupdate uma função web usando a implantação da Web:

* Publicar ou empacotar um aplicativo do Azure do Visual Studio
* Atualizar uma função web como parte do ciclo de teste e desenvolvimento Olá

## <a name="publish-or-package-an-azure-application-from-visual-studio"></a>Publicar ou empacotar um aplicativo do Azure do Visual Studio
Quando você publica seu aplicativo do Azure, você pode fazer uma das seguintes tarefas de saudação:

* Criar um pacote de serviço: você pode usar este toopublish de arquivo de configuração de serviço de pacote e hello seu ambiente de implantação do aplicativo tooa de saudação [Portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885).
* Publicar seu projeto do Azure do Visual Studio: toopublish seu aplicativo diretamente tooAzure, use Olá Assistente de publicação. Para obter informações, consulte [Assistente de Publicação de Aplicativo do Azure](vs-azure-tools-publish-azure-application-wizard.md).

### <a name="toocreate-a-service-package-from-visual-studio"></a>toocreate um pacote de serviço do Visual Studio
1. Quando estiver pronto toopublish seu aplicativo, abra o Gerenciador de soluções, menu de atalho Olá aberto para Olá projeto do Azure que contém suas funções, e selecione publicar.
2. toocreate um pacote de serviço, siga estas etapas:  
   
   1. No menu de atalho de saudação de saudação do Azure do projeto, escolha **pacote**.
   2. Em Olá **empacotar aplicativo do Azure** caixa de diálogo, escolha um pacote de configuração do serviço Olá para o qual você deseja toocreate e, em seguida, escolha a configuração de compilação de hello.
   3. tooturn (opcional) na área de trabalho remota para o serviço de nuvem Olá após publicá-lo, selecione Olá **habilitar a área de trabalho remota para todas as funções** caixa de seleção e, em seguida, selecione **configurações** tooconfigure área de trabalho remota. Se desejar toodebug seu serviço de nuvem após publicá-lo, ative a depuração remota selecionando **habilitar depurador remoto para todas as funções**.
      
      Para saber mais, confira [Usando a Área de Trabalho Remota com as funções do Azure](vs-azure-tools-remote-desktop-roles.md).
   4. Olá toocreate do pacote, escolha Olá **pacote** link.
      
      Explorador de arquivos mostra o local do arquivo hello de saudação recentemente criado o pacote. Você pode copiar esse local para que você pode usá-lo de saudação [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885).
   5. toopublish nesse ambiente de implantação do pacote tooa, você deve usar esse local como Olá local do pacote quando você cria um serviço de nuvem e implanta esse ambiente tooan de pacote com hello [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885).
3. Processo de implantação de saudação toocancel (opcional), no menu de atalho de saudação de item de linha de saudação no log de atividades de saudação, escolha **Cancelar e remover**. Isso interrompe o processo de implantação de saudação e exclui o ambiente de implantação de saudação do Azure.
   
   > [!NOTE]
   > tooremove esse ambiente de implantação depois que ele tiver sido implantado, você deve usar Olá [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885).
   > 
   > 
4. (Opcional) Depois que suas instâncias de função forem iniciadas, o Visual Studio mostra automaticamente o ambiente de implantação Olá no hello **serviços de nuvem** nó no Gerenciador de servidores. A partir daqui, você pode ver o status de Olá Olá individuais de instâncias de função. Consulte [recursos de gerenciamento Azure com o Gerenciador de nuvem](vs-azure-tools-resources-managing-with-cloud-explorer.md).hello ilustração a seguir mostra as instâncias de função hello enquanto eles ainda estão no estado Inicializando da saudação:
   
    ![VST_DeployComputeNode](./media/vs-azure-tools-publishing-a-cloud-service/IC744134.png)

## <a name="update-a-web-role-as-part-of-hello-development-and-testing-cycle"></a>Atualizar uma função Web como parte do desenvolvimento de saudação e ciclo de testes
Se a infraestrutura de back-end do seu aplicativo estiver estável, mas as funções hello web precisam de atualização mais frequente, você pode usar a implantação da Web tooupdate apenas uma função web em seu projeto. Isso é útil quando você não deseja toorebuild e reimplantar as funções de trabalho de back-end hello, ou se você tiver várias funções web e quiser tooupdate apenas uma das funções de web hello.

### <a name="requirements"></a>Requisitos
Aqui está Olá requisitos toouse implantação da Web tooupdate sua função web:

* **Para desenvolvimento e teste fins:** Olá as alterações são feitas diretamente toohello máquina de virtual onde a função de web hello está sendo executado. Se essa máquina virtual tem toobe reciclado, alterações de hello são perdidas, pois o pacote original de saudação que você publicou é toorecreate usado Olá para a função hello. Você deve publicar novamente a função de web hello alterações mais recentes seu aplicativo tooget hello.
* **Apenas funções Web podem ser atualizadas:** funções de trabalho não podem ser atualizadas. Além disso, você não pode atualizar Olá RoleEntryPoint no web role.cs.
* **Só há suporte a uma única instância de uma função Web:** não pode haver várias instâncias da função Web em seu ambiente de implantação. No entanto, há suporte para várias funções Web, cada com apenas uma instância.
* **Você deve habilitar conexões de área de trabalho remota:** isso é necessário para que a implantação da Web pode usar Olá usuário e senha tooconnect toohello máquina virtual toodeploy Olá alterações toohello servidor que está executando o Internet Information Services (IIS). Além disso, talvez seja necessário tooconnect toohello máquina virtual tooadd tooIIS um certificado confiável nesta máquina virtual. (Isso assegura que a conexão remota Olá para IIS que é usada pela implantação da Web seja segura.)

Olá procedimento a seguir pressupõe que você esteja usando Olá **publicar aplicativo do Azure** assistente.

### <a name="tooenable-web-deploy-when-you-publish-your-application"></a>tooEnable implantar quando você publicar seu aplicativo Web
1. Olá tooenable **ativar implantação da Web** para todos os web caixa de seleção de funções, primeiro você deve configurar conexões de área de trabalho remota. Selecione **habilitar área de trabalho remota** para todas as funções e, em seguida, as credenciais de Olá de fonte que serão usado tooconnect remotamente no hello **configuração da área de trabalho remota** caixa que aparece. Consulte [Usando a Área de Trabalho Remota com funções do Azure](vs-azure-tools-remote-desktop-roles.md) para obter mais informações.
2. tooenable implantação da Web para todos os Olá funções da web em seu aplicativo, selecione **ativar implantação da Web para todas as funções web**.
   
    Um triângulo amarelo de aviso será exibido. A Implantação da Web usa um certificado não confiável, autoassinado por padrão, o que não é recomendado para carregar dados confidenciais. Se você precisar toosecure esse processo para dados confidenciais, você pode adicionar um toobe do certificado SSL usado para conexões de implantação da Web. Esse certificado precisa toobe um certificado confiável. Para obter informações sobre como toodo isso, consulte a seção Olá **tooMake Web implantar Secure** mais adiante neste tópico.
3. Escolha **próximo** tooshow Olá **resumo** tela e, em seguida, escolha **publicar** serviço de nuvem toodeploy hello.
   
    serviço de nuvem Olá é publicado. máquina virtual Olá criado tem conexões remotas habilitadas para o IIS para que a implantação da Web pode ser usado tooupdate suas funções web sem republicá-las.
   
   > [!NOTE]
   > Se você tiver mais de uma instância configurada para uma função web, uma mensagem de aviso será exibida, informando que cada função web será limitado tooone instância somente no pacote de saudação que criou toopublish seu aplicativo. Selecione **Okey** toocontinue. Conforme mencionado na seção de requisitos hello, você pode ter mais de uma função web, mas apenas uma instância de cada função.
   > 
   > 

### <a name="tooupdate-your-web-role-by-using-web-deploy"></a>tooUpdate sua função Web usando a implantação da Web
1. toouse implantação da Web, verifique o projeto de toohello de alterações de código para qualquer uma das funções web no Visual Studio que você deseja toopublish e, em seguida, clique com botão direito neste nó do projeto em sua solução e aponte muito**publicar**. Olá **Publicar Web** caixa de diálogo é exibida.
2. (Opcional) Se você adicionou um toouse de certificado SSL confiável para conexões remotas para o IIS, você pode desmarcar Olá **permitir certificado não confiável** caixa de seleção. Para obter informações sobre como tooadd uma toomake de certificado de implantação da Web seguro, consulte a seção de saudação **tooMake Web implantar seguro** mais adiante neste tópico.
3. toouse implantação da Web, Olá publicar mecanismo precisa Olá nome e a senha que você configurou para sua conexão de área de trabalho remota quando você publicou o pacote de saudação primeiro.
   
   1. Em **nome de usuário**, insira o nome de usuário de saudação.
   2. Em **senha**, digite a senha de saudação.
   3. (Opcional) Se você quiser toosave essa senha neste perfil, escolha **salvar senha**.
4. função de web do tooyour toopublish Olá alterações, escolha **publicar**.
   
    linha de status Olá exibe **publicação iniciada**. Quando a publicação Olá for concluída, **publicação bem-sucedida** é exibida. alterações de saudação foram função da web de toohello implantado na sua máquina virtual. Agora você pode iniciar o aplicativo do Azure no hello ambiente Azure tootest suas alterações.

### <a name="toomake-web-deploy-secure"></a>tooMake implantar segura da Web
1. A Implantação da Web usa um certificado não confiável, autoassinado por padrão, o que não é recomendado para carregar dados confidenciais. Se você precisar toosecure esse processo para dados confidenciais, você pode adicionar um toobe do certificado SSL usado para conexões de implantação da Web. Esse certificado precisa toobe um certificado confiável, o que você obtém de uma autoridade de certificação (CA).
   
    toomake de implantação da Web seguro para cada máquina virtual para cada uma das funções web, você deve carregar o certificado confiável de saudação que você deseja toouse para toohello de implantação da web [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885). Isso garante que o certificado Olá é adicionado a máquina virtual toohello que é criada para a função de web hello quando você publicar seu aplicativo.
2. tooadd um toouse de tooIIS de certificado SSL confiável para conexões remotas, siga estas etapas:
   
   1. máquina virtual do tooconnect toohello que está executando Olá web função, instância de saudação select de função da web de saudação em **Cloud Explorer** ou **Gerenciador de servidores**e, em seguida, escolha Olá **se conectar usando Área de trabalho remota** comando. Para obter etapas detalhadas sobre como tooconnect toohello virtual máquina, consulte [usando a área de trabalho remota com funções do Azure](vs-azure-tools-remote-desktop-roles.md).
      
      O navegador solicitará que você toodownload um. Arquivo RDP.
   2. tooadd um certificado SSL, o serviço de gerenciamento de saudação aberto no Gerenciador do IIS. No Gerenciador do IIS, habilitar o SSL por abrindo Olá **associações** link no hello **ação** painel. Olá **Adicionar associação do Site** caixa de diálogo é exibida. Escolha **adicionar**e, em seguida, escolha o HTTPS no hello **tipo** lista suspensa. Em Olá **certificado SSL** , escolha o certificado SSL de saudação que você assinou por uma autoridade de certificação e que você carregou toohello [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885). Para obter mais informações, consulte [definir configurações de Conexão para Olá serviço de gerenciamento](http://go.microsoft.com/fwlink/?LinkId=215824).
      
      > [!NOTE]
      > Se você adicionar um certificado SSL confiável, triângulo de aviso amarelo de saudação não aparece mais na Olá **Assistente de publicação**.
      > 
      > 

## <a name="include-files-in-hello-service-package"></a>Incluir arquivos no hello pacote de serviço
Talvez seja necessário tooinclude determinados arquivos em seu pacote de serviço para que eles estejam disponíveis na máquina virtual de saudação que é criada para uma função. Por exemplo, convém tooadd um .exe ou um arquivo. msi que é usado por um pacote de serviço de tooyour de script de inicialização. Ou, talvez seja necessário tooadd um assembly que requer um projeto de função de trabalho ou função da web. arquivos de tooinclude devem ser adicionados toohello solução para seu aplicativo do Azure.

### <a name="tooinclude-files-in-hello-service-package"></a>tooinclude arquivos no pacote de serviço Olá
1. tooadd um pacote de serviço do assembly tooa, Olá use as etapas a seguir:
   
   1. Em **Solution Explorer** Olá abrir nó Olá projeto que está faltando o assembly hello referenciado.
   2. tooadd Olá assembly toohello projeto, menu de atalho Olá aberto para Olá **referências** pasta e, em seguida, escolha **adicionar referência**. caixa de diálogo de adicionar referência de saudação aparece.
   3. Escolha Olá referência que você deseja tooadd e, em seguida, escolha Olá **Okey** botão.
      
      referência de Olá é adicionada a lista de toohello em hello **referências** pasta.
   4. Abra o menu de atalho Olá para assembly hello que você adicionou e escolha **propriedades**. Olá **propriedades** janela é exibida.
      
      tooinclude desse assembly no serviço de saudação do pacote, em Olá **lista cópia Local** escolha **True**.
2. Em **Solution Explorer** Olá abrir nó Olá projeto que está faltando o assembly hello referenciado.
3. tooadd Olá assembly toohello projeto, menu de atalho Olá aberto para Olá **referências** pasta e, em seguida, escolha **adicionar referência**. Olá **adicionar referência** caixa de diálogo é exibida.
4. Escolha Olá referência que você deseja tooadd e, em seguida, escolha Olá **Okey** botão.
   
    referência de Olá é adicionada a lista de toohello em hello **referências** pasta.
5. Abra o menu de atalho Olá para assembly hello que você adicionou e escolha **propriedades**. janela de propriedades de saudação é exibida.
6. tooinclude desse assembly no serviço de saudação do pacote, em Olá **Copy Local** , escolha **True**.
7. tooinclude arquivos no pacote de serviço Olá que foram adicionados tooyour projeto de função web, abra Olá menu de atalho para o arquivo hello e, em seguida, escolha **propriedades**. De saudação **propriedades** janela, escolha **conteúdo** de saudação **ação de compilação** caixa de listagem.
8. tooinclude arquivos no pacote de serviço Olá que foram adicionados tooyour projeto de função de trabalho, abra Olá menu de atalho para o arquivo hello e, em seguida, escolha **propriedades**. De saudação **propriedades** janela, escolha **copiar se mais recente** de saudação **diretório de toooutput cópia** caixa de listagem.

## <a name="next-steps"></a>Próximas etapas
toolearn mais informações sobre publicação tooAzure do Visual Studio, consulte [Assistente de aplicativo do Azure publicação](vs-azure-tools-publish-azure-application-wizard.md).

