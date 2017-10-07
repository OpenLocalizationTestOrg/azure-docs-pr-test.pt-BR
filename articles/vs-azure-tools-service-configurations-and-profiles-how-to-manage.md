---
title: "perfis e configurações de serviço aaaHow toomanage | Microsoft Docs"
description: "Saiba como toowork com arquivos de configuração de perfis e configurações de serviço | que armazenam configurações para ambientes de implantação hello e configurações de publicação para os serviços de nuvem."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 7da8c551-fb06-4057-b5c7-c77f4b39d803
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/11/2017
ms.author: kraigb
ms.openlocfilehash: 1dba9df2fa57fe94dacc90ae74b05ccdc28270c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-service-configurations-and-profiles"></a>Como toomanage serviço perfis e configurações
## <a name="overview"></a>Visão geral
Quando você publica um serviço de nuvem, o Visual Studio armazena informações de configuração em dois tipos de arquivos de configuração: perfis e configurações de serviço. Configurações de serviço (arquivos. cscfg) armazenam configurações para ambientes de implantação de saudação para um serviço de nuvem do Azure. O Azure usa esses arquivos de configuração ao gerenciar seus serviços de nuvem. Em Olá outro lado, as configurações de serviços de nuvem de publicação do repositório de perfis (arquivos. azurePubxml). Essas configurações são um registro de que você escolher quando usar Olá Assistente de publicação e são usados localmente pelo Visual Studio. Este tópico explica como toowork com ambos os tipos de arquivos de configuração.

## <a name="service-configurations"></a>Configurações de Serviço
Você pode criar várias toouse de configurações de serviço para cada um de seus ambientes de implantação. Por exemplo, você pode criar uma configuração de serviço para o ambiente de saudação local que você use toorun e testar um aplicativo do Azure e outra configuração de serviço para o seu ambiente de produção.

Você pode adicionar, excluir, renomear e modificar essas configurações de serviço com base em suas necessidades. Você pode gerenciar essas configurações de serviço do Visual Studio, conforme mostrado na ilustração a seguir de saudação.

![Gerenciar Configurações de Serviço](./media/vs-azure-tools-service-configurations-and-profiles-how-to-manage/manage-service-config.png)

Você também pode abrir Olá **gerenciar configurações** caixa de diálogo de páginas de propriedades da função hello. Propriedades de Olá tooopen para uma função em seu projeto do Azure, abra Olá menu de atalho para a função e, em seguida, escolha **propriedades**. Em Olá **configurações** guia, expanda Olá **configuração do serviço** e, em seguida, selecione **gerenciar** tooopen Olá **gerenciar configurações**caixa de diálogo.

### <a name="tooadd-a-service-configuration"></a>tooadd uma configuração de serviço
1. No Solution Explorer, abra o menu de atalho de saudação para Olá projeto do Azure e, em seguida, selecione **gerenciar configurações**.
   
    Olá **gerenciar configurações de serviço** caixa de diálogo é exibida.
2. tooadd uma configuração de serviço, você deve criar uma cópia de uma configuração existente. toodo isso, escolha Olá configuração que você deseja toocopy da lista de nomes de saudação e, em seguida, selecione **criar cópia**.
3. Configuração do serviço Olá toogive (opcional) um nome diferente, escolha a nova configuração de serviço Olá Olá nome lista e, em seguida, selecione **Renomear**. Em Olá **nome** caixa de texto, digite o nome de saudação que você deseja toouse para essa configuração de serviço e, em seguida, selecione **Okey**.
   
    Um novo arquivo de configuração de serviço chamado ServiceConfiguration. [Nome do novo]. cscfg é adicionado toohello projeto do Azure no Gerenciador de soluções.

### <a name="toodelete-a-service-configuration"></a>toodelete uma configuração de serviço
1. No Solution Explorer, abra o menu de atalho de saudação para Olá projeto do Azure e, em seguida, selecione **gerenciar configurações**.
   
    Olá **gerenciar configurações de serviço** caixa de diálogo é exibida.
2. toodelete uma configuração de serviço, escolha a configuração de saudação que você deseja toodelete de saudação **nome** e, em seguida, selecione **remover**. Uma caixa de diálogo é exibida tooverify que você deseja toodelete essa configuração.
3. Selecione **Excluir**.
   
     arquivo de configuração do serviço de saudação é removido do hello projeto do Azure no Gerenciador de soluções.

### <a name="toorename-a-service-configuration"></a>toorename uma configuração de serviço
1. No Gerenciador de soluções, abrir menu de atalho Olá para Olá projeto do Azure e, em seguida, selecione **gerenciar configurações**.
   
    Olá **gerenciar configurações de serviço** caixa de diálogo é exibida.
2. toorename uma configuração de serviço, escolha a nova configuração de serviço Olá Olá **nome** e, em seguida, selecione **Renomear**. Em Olá **nome** caixa de texto, digite o nome de saudação que você deseja toouse para essa configuração de serviço e, em seguida, selecione **Okey**.
   
    nome de saudação do arquivo de configuração do serviço de saudação é alterado no hello projeto do Azure no Gerenciador de soluções.

### <a name="toochange-a-service-configuration"></a>toochange uma configuração de serviço
* Se você quiser toochange uma configuração de serviço, abra o menu de atalho de saudação para função específica de saudação desejado toochange em Olá projeto do Azure e, em seguida, selecione **propriedades**. Consulte [como: configurar funções de saudação para um serviço de nuvem do Azure com o Visual Studio](https://docs.microsoft.com/azure/vs-azure-tools-configure-roles-for-cloud-service) para obter mais informações.

## <a name="make-different-setting-combinations-by-using-profiles"></a>Fazer diferentes combinações de configurações usando perfis
Usando um perfil, você pode preencher automaticamente Olá **Assistente de publicação** com diferentes combinações de configurações para finalidades diferentes. Por exemplo, você pode ter um perfil para depuração e outro para compilações de versão. Nesse caso, o **depurar** perfil teria **IntelliTrace** habilitado e Olá **depurar** configuração selecionada e o **versão** perfil teria **IntelliTrace** desabilitado e hello **versão** configuração selecionada. Você também pode usar um serviço usando uma conta de armazenamento diferentes toodeploy perfis diferentes.

Quando você executa o Assistente de saudação para Olá primeira vez, é criado um perfil padrão. O Visual Studio armazena perfil Olá em um arquivo que tem uma extensão. azurePubxml, que é adicionada tooyour projeto do Azure em Olá **perfis** pasta. Se você especificar diferentes opções manualmente quando você executa o Assistente de hello mais tarde, o arquivo hello atualiza automaticamente. Antes de executar Olá procedimento a seguir, você deve já publicou seu serviço de nuvem pelo menos uma vez.

### <a name="tooadd-a-profile"></a>tooadd um perfil
1. Abrir o menu de atalho de saudação de seu projeto do Azure e, em seguida, selecione **publicar**.
2. Próxima toohello **perfil de destino** lista, selecione Olá **Salvar perfil** botão como Olá na ilustração a seguir. Isso cria um perfil para você.
   
    ![Criar um novo perfil](./media/vs-azure-tools-service-configurations-and-profiles-how-to-manage/create-new-profile.png)
3. Após a criação de perfil de saudação, selecione **< Gerenciar … >** em Olá **perfil de destino** lista.
   
    Olá **gerenciar perfis** caixa de diálogo aparece como Olá na ilustração a seguir.
   
    ![Caixa de Diálogo Gerenciar Perfis](./media/vs-azure-tools-service-configurations-and-profiles-how-to-manage/manage-profiles.png)
4. Em Olá **nome** lista, escolha um perfil e, em seguida, selecione **criar cópia**.
5. Escolha Olá **fechar** botão.
   
    novo perfil de saudação aparece na lista de perfis de destino hello.
6. Em Olá **perfil de destino** lista perfil Olá selecione que você acabou de criar. configurações do Assistente de publicação Olá são preenchidas com opções de saudação do perfil de saudação selecionado.
7. Selecione Olá **anterior** e **próximo** botões toodisplay cada página do Assistente de publicação do hello e, em seguida, personalizar as configurações de saudação para este perfil. Confira [Assistente de Publicação de Aplicativo do Azure](http://go.microsoft.com/fwlink/p/?LinkID=623085) .
8. Quando terminar de personalizar configurações de saudação, selecione **próximo** toogo página de configurações de backup toohello. perfil de saudação é salvo quando você publicar o serviço hello usando essas configurações ou se você selecionar **salvar** próxima toohello lista de perfis.

### <a name="toorename-or-delete-a-profile"></a>toorename ou excluir um perfil
1. Abrir o menu de atalho de saudação de seu projeto do Azure e, em seguida, selecione **publicar**.
2. Em Olá **perfil de destino** lista, selecione **gerenciar**.
3. Em Olá **gerenciar perfis** caixa de diálogo, o perfil de saudação selecione que você deseja toodelete e, em seguida, selecione **remover**.
4. Na saudação caixa de diálogo de confirmação que aparece, selecione **Okey**.
5. Selecione **Fechar**.

### <a name="toochange-a-profile"></a>toochange um perfil
1. Abrir o menu de atalho de saudação de seu projeto do Azure e, em seguida, selecione **publicar**.
2. Em Olá **perfil de destino** lista perfil Olá selecione que você deseja toochange.
3. Selecione Olá **anterior** e **próximo** botões toodisplay Olá de cada página do Assistente de publicação e, em seguida, alterar as configurações de saudação desejado. Confira [Assistente de Publicação de Aplicativo do Azure](http://go.microsoft.com/fwlink/p/?LinkID=623085) .
4. Depois de terminar de alterar as configurações de saudação, selecione **próximo** toohello back toogo **configurações** página.
5. (Opcional) selecione **publicar** toopublish serviço em nuvem hello usando Olá novas configurações. Se você não quiser toopublish seu serviço de nuvem no momento e você fechar Olá Assistente de publicação, o Visual Studio perguntar se você deseja toosave Olá alterações toohello perfil.

## <a name="next-steps"></a>Próximas etapas
toolearn sobre a configuração de outras partes do seu projeto do Azure no Visual Studio, consulte [Configurando um projeto do Azure](http://go.microsoft.com/fwlink/p/?LinkID=623075)

