---
title: aaaRun qualquer aplicativo do Windows em qualquer dispositivo com o Azure RemoteApp | Microsoft Docs
description: "Saiba como tooshare qualquer aplicativo do Windows com os usuários usando o Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: 961d40ca-9673-4977-aa54-d6b22fc61ce1
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 750f3b881e0cb671ff6e8f3e851bccdf2262d156
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-any-windows-app-on-any-device-with-azure-remoteapp"></a>Execute qualquer aplicativo do Windows em qualquer dispositivo com o Azure RemoteApp
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

Você pode executar um aplicativo do Windows em qualquer lugar e em qualquer dispositivo, agora, é sério: basta usar o Azure RemoteApp. Se ele é um aplicativo personalizado escrito há 10 anos, ou um aplicativo do Office, os usuários não tem mais toobe ligado tooa específica do sistema operacional (como o Windows XP) para os aplicativos alguns.

Com o Azure RemoteApp, os usuários também podem usar seu próprios Android ou get e dispositivos da Apple Olá a mesma experiência que tem no Windows (ou em dispositivos Windows Phone). Isso é realizado hospedando seus aplicativos do Windows em uma coleção de máquinas virtuais do Windows no Azure, em que os usuários podem acessá-los em qualquer lugar em que com conexão à Internet. 

Continue lendo para obter um exemplo de exatamente como toodo isso.

Neste artigo, vamos tooshare acesso com todos os seus usuários. No entanto, você pode usar QUALQUER aplicativo. Como você pode instalar o aplicativo em um computador Windows Server 2012 R2, você pode compartilhá-lo usando Olá etapas abaixo. Você pode examinar Olá [requisitos do aplicativo](remoteapp-appreqs.md) toomake-se de que seu aplicativo funcionará.

Observe que como o acesso é um banco de dados, e queremos que toobe de banco de dados úteis, realizaremos algumas etapas adicionais toolet usuários acesse o compartilhamento de dados do Access hello. Se seu aplicativo não é um banco de dados, ou você não precisa tooaccess capaz de seus usuários toobe um compartilhamento de arquivos, você poderá ignorar as etapas neste tutorial

> [!NOTE]
> <a name="note"></a>Você precisa de uma conta do Azure toocomplete neste tutorial:
> 
> * Você pode [abrir uma conta do Azure gratuitamente](https://azure.microsoft.com/free/?WT.mc_id=A261C142F): você obtém créditos você pode usar tootry out paga serviços do Azure e mesmo depois que eles são usados até você pode manter a conta de saudação e usar serviços do Azure, como sites de livre. Seu cartão de crédito nunca será cobrado a menos que você explicitamente alterar suas configurações e pergunte toobe cobrado.
> * Você pode [ativar benefícios para assinantes do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): todos os meses, sua assinatura do MSDN concede créditos que podem ser usados para serviços pagos do Azure.
> 
> 

## <a name="create-a-collection-in-remoteapp"></a>Criar uma coleção de RemoteApp
Comece pela criação de uma coleção. coleção de saudação serve como um contêiner para seus aplicativos e usuários. Cada coleção é baseada em uma imagem - você pode criar sua própria ou usar uma fornecida com sua assinatura. Para este tutorial, estamos usando a imagem de avaliação Olá Office 2013 - ele contém o aplicativo hello que desejamos tooshare.

1. No portal do Azure de Olá, role para baixo na árvore de navegação à esquerda Olá até que você veja o RemoteApp. Abra essa página.
2. Clique em **Criar uma coleção de RemoteApp**.
3. Clique em **Criação rápida** e digite um nome para a coleção.
4. Selecione a região de saudação deseja toouse toocreate sua coleção. Para melhor experiência de saudação, selecione região hello mais próximo geograficamente toohello local onde os usuários acessarão o aplicativo hello. Por exemplo, neste tutorial, os usuários de saudação serão localizados em Redmond, Washington. região do Azure mais próximo de saudação é **Oeste dos EUA**.
5. Selecione o plano de cobrança Olá que deseja toouse. plano de cobrança básico Olá coloca 16 usuários em uma VM do Azure grande, enquanto o plano de cobrança padrão Olá tem 10 usuários em uma VM do Azure grande. Como um exemplo geral, o plano básico Olá funciona bem para fluxo de trabalho de tipo de entrada de dados. Para um aplicativo de produtividade, como o Office, você desejaria plano padrão hello.
6. Por fim, selecione a imagem do Office 2013 Professional hello. Esta imagem contém aplicativos do Office 2013. Um lembrete: essa imagem é válida somente para coleções de avaliação e POCs. Você não pode usar essa imagem em uma coleção de produção.
7. Clique em **Criar coleção do RemoteApp**.

![Criar uma coleção de nuvem no RemoteApp](./media/remoteapp-anyapp/ra-anyappcreatecollection.png)

Isso inicia a criação de sua coleção, mas pode demorar até tooan horas.

Agora você está pronto tooadd seus usuários.

## <a name="share-hello-app-with-users"></a>Aplicativo de saudação do compartilhamento com usuários
Depois que a coleção foi criada com êxito, é hora toopublish acesso toousers e adicionar usuários de saudação que devem ter acesso tooit.

Se você navegou para fora do nó do Azure RemoteApp Olá enquanto estava sendo criada coleção hello, comece abrindo caminho fazer tooit de saudação home page do Azure.

1. Clique em coleção Olá criado anteriormente tooaccess opções adicionais e configurar a coleta de saudação.
   ![Uma nova coleção de nuvem no RemoteApp](./media/remoteapp-anyapp/ra-anyappcollection.png)
2. Em Olá **publicação** , clique em **publicar** na parte inferior da saudação de tela hello e clique **programas do menu Iniciar publicar**.
   ![Publicar o programa do RemoteApp](./media/remoteapp-anyapp/ra-anyapppublish.png)
3. Selecione os aplicativos Olá deseja toopublish da lista de saudação. Para nossa finalidade, escolhemos o Access. Clique em **Concluído**. Aguarde até que a publicação Olá aplicativos toofinish.
   ![Publicação do Access no RemoteApp](./media/remoteapp-anyapp/ra-anyapppublishaccess.png)
4. Depois que o aplicativo hello terminou de publicação, vá direto toohello **acesso de usuário** guia tooadd todos os usuários de saudação que precisam acessar os aplicativos de tooyour. Insira nomes de usuário (endereço de email) para seus usuários e, em seguida, clique em **Salvar**.

![Adicionar usuários tooRemoteApp](./media/remoteapp-anyapp/ra-anyappaddusers.png)

1. Agora, é hora tootell os usuários sobre esses novos aplicativos e como tooaccess-los. toodo isso, envie um email apontá-los toohello URL de download de cliente de área de trabalho remota.
   ![URL de download de cliente de saudação do RemoteApp](./media/remoteapp-anyapp/ra-anyappurl.png)

## <a name="configure-access-tooaccess"></a>Configurar acesso tooAccess
Alguns aplicativos precisam de configuração adicional após você implantá-los por meio do RemoteApp. Em particular, para acessar, estamos toocreate será um compartilhamento de arquivos no Azure que qualquer usuário pode acessar. (Se você não quiser toodo, você pode criar um [coleção híbrida](remoteapp-create-hybrid-deployment.md) [em vez de nosso conjunto de nuvem] que permite aos usuários acessar os arquivos e as informações em sua rede local.) Em seguida, vamos precisar tootell toomap nossos usuários uma unidade local no seu computador de toohello sistema de arquivos do Azure.

Olá primeira parte como Olá administrador fazer. Em seguida, temos algumas etapas para seus usuários.

1. Iniciar publicação interface de linha de comando hello (cmd.exe). Em Olá **publicação** guia, selecione **cmd**e, em seguida, clique em **publicar > publicar o programa usando o caminho**.
2. Insira o nome de saudação do aplicativo hello e caminho hello. Para nosso propósito, use "Explorador de arquivos" como nome hello e "% SYSTEMDRIVE%\windows\explorer.exe" como caminho de saudação.
   ![Olá cmd.exe arquivo de publicação.](./media/remoteapp-anyapp/ra-publishcmd.png)
3. Agora você precisa toocreate um Azure [conta de armazenamento](../storage/common/storage-create-storage-account.md). Nomeamos o nosso "accessstorage", portanto escolha um nome que seja significativo tooyou. (toomisquote Highlander, pode haver somente um "accessstorage".) ![Conta de armazenamento do Azure nosso](./media/remoteapp-anyapp/ra-anyappazurestorage.png)
4. Agora volte tooyour painel para que você possa obter armazenamento tooyour de caminho hello (local do ponto de extremidade). Você usará isso daqui a pouco, portanto certifique-se de copiá-lo em algum lugar.
   ![caminho de conta de armazenamento Olá](./media/remoteapp-anyapp/ra-anyappstoragelocation.png)
5. Em seguida, quando tiver sido criada a conta de armazenamento Olá, terá uma chave de acesso primária hello. Clique em **gerenciar chaves de acesso**e, em seguida, copie Olá chave de acesso primária.
6. Agora, definir contexto Olá Olá da conta de armazenamento e criar um novo compartilhamento de arquivo para acesso. Execute Olá cmdlets em uma janela elevada do Windows PowerShell a seguir:
   
        $ctx=New-AzureStorageContext <account name> <account key>
        $s = New-AzureStorageShare <share name> -Context $ctx
   
    Portanto para nossa participação, esses são os cmdlets de Olá executada:
   
        $ctx=New-AzureStorageContext accessstorage <key>
        $s = New-AzureStorageShare <share name> -Context $ctx

Agora, vez do usuário Olá-lo do. Primeiro, faça com que os usuários instalem um [cliente RemoteApp](remoteapp-clients.md). Em seguida, os usuários de saudação necessário toomap compartilhar uma unidade de toothat sua conta do Azure arquivo criado e adicione seus arquivos de acesso. É desse jeito que eles fazem isso:

1. No cliente, o RemoteApp Olá Olá acesso aplicativos publicados. Inicie o programa de cmd.exe hello.
2. Execute Olá toomap de comando a seguir uma unidade de compartilhamento de arquivos de toohello seu computador:
   
        net use z: \\<accountname>.file.core.windows.net\<share name> /u:<user name> <account key>
   
    Se você definir Olá **/ persistente** tooyes de parâmetro hello unidade mapeada persistirá entre sessões.
3. Agora, inicie o aplicativo do Explorador de arquivos de saudação do RemoteApp. Copie os arquivos de acesso que você deseja toouse no compartilhamento de arquivos de toohello de aplicativo compartilhado hello.
   ![Colocar arquivos do Access em um compartilhamento do Azure](./media/remoteapp-anyapp/ra-anyappuseraccess.png)
4. Finalmente, abrir o acesso e, em seguida, abra o banco de dados de saudação que você acabou de ser compartilhado. Você deve ver os dados no Access em execução na nuvem hello.
   ![Um banco de dados real em execução na nuvem Olá](./media/remoteapp-anyapp/ra-anyapprunningaccess.png)

Agora você pode usar o Access em qualquer um dos seus dispositivos - certifique-se de instalar um cliente RemoteApp.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Próximas etapas
Agora que você já dominou a criação de uma coleção, tente criar uma [coleção que use o Office 365](remoteapp-tutorial-o365anywhere.md). Ou você pode criar uma [coleção híbrida ](remoteapp-create-hybrid-deployment.md)que possa acessar sua rede local.

<!--Image references-->

