---
title: "aaaEnabling acesso remoto para implantações do Azure no Eclipse"
description: "Saiba como tooenable remoto acessa para implantações do Azure usando Olá Kit de ferramentas do Azure para Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: b6150006-9a7f-4d83-be18-d35ec780c7c5
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 00c2bf22c1f3ec792098f154f771c87506e87881
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-remote-access-for-azure-deployments-in-eclipse"></a>Habilitando o Acesso Remoto para implantações do Azure no Eclipse
toohelp solucionar problemas de suas implantações, você pode habilitar e usar o acesso remoto tooconnect toohello máquina virtual que hospeda sua implantação. Olá funcionalidade de acesso remoto depende Olá protocolo de área de trabalho remota (RDP). Você pode configurar o acesso remoto para sua implantação depois que você tenha publicado tooAzure, ou se você estiver usando o Eclipse com um sistema operacional Windows, você pode configurar o acesso remoto antes de publicar tooAzure. Observe que você precisará de um cliente de desktop remoto é compatível com o sistema operacional na máquina de virtual da implantação do pedido tooconnect tooyour no Azure.

## <a name="how-tooenable-remote-access-before-you-deploy-tooazure"></a>Como tooenable acesso remoto antes de implantar tooAzure
> [!NOTE]
> tooenable acesso remoto antes de implantar seu aplicativo tooAzure, você precisa toobe executando o Eclipse no Windows.
> 
> 

Olá, imagem a seguir mostra Olá **acesso remoto** caixa de diálogo de propriedades usada tooenable o acesso remoto.

![][ic719494]

Há dois Olá toodisplay de maneiras **acesso remoto** caixa de diálogo de propriedades:

* Clique em Olá **avançado** link no hello **acesso remoto** seção Olá **publicar tooAzure** caixa de diálogo.

* Olá abrir **propriedades** caixa de diálogo do projeto do Azure.

Quando você cria um novo projeto de implantação do Azure, o projeto de saudação não terá acesso remoto habilitado por padrão. No entanto, você pode facilmente habilitar acesso remoto especificando Olá nome de usuário e senha em Olá **publicar tooAzure** caixa de diálogo. senha de acesso remoto de saudação é criptografada usando certificados x. 509. Se você não usar fornecer seu próprio certificado, Olá criptografia baseia-se em um certificado autoassinado fornecido com hello plug-in do Azure para Eclipse. Este certificado autoassinado está Olá **cert** pasta do seu projeto do Azure, armazenado como um arquivo de certificado público (SampleRemoteAccessPublic.cer) e como um Personal Information Exchange (PFX) (arquivo de certificado SampleRemoteAccessPrivate.pfx). Olá último contém a chave particular Olá certificado hello e tem uma senha padrão, **Password1**. No entanto, desde que essa senha é de conhecimento público, certificado padrão de saudação deve ser usado apenas para fins de aprendizado, não para uma implantação de produção. Assim que para fins de aprendizado, quando você quiser tooenabled a sessões remotas para suas implantações, clique em Olá **avançado** link no hello **publicar tooAzure** toospecify da caixa de diálogo seu próprio certificado. Observe que você precisará tooupload Olá PFX versão Olá certificado tooyour hospedado do serviço de dentro Olá Portal de gerenciamento do Azure, para que o Azure possa descriptografar a senha do usuário hello.

restante de saudação do tutorial Olá mostra como acessar o tooenable remoto para um projeto de implantação do Azure que foi inicialmente criado com o acesso remoto desativado. Para este tutorial, criaremos um novo certificado autoassinado e seu arquivo .pfx terá uma senha escolhida por você. Você também tem a opção de saudação do uso de um certificado emitido por uma autoridade de certificação.

## <a name="how-tooenable-remote-access-after-you-have-deployed-tooazure"></a>Como tooenable acesso remoto depois que você implantou tooAzure
tooenable acesso remoto depois que você implantou tooAzure, Olá use as etapas a seguir:

1. Faça logon no portal de gerenciamento do Azure hello usando sua conta do Azure

2. Na lista de **Serviços de Nuvem**, escolha o serviço de nuvem implantado

3. Na página de web de serviço de nuvem hello, clique em Olá **configurar** link

4. Na parte inferior de saudação da página de configuração hello, clique em Olá **remoto** link

5. Quando for exibida a caixa de diálogo pop-up de saudação:
   
   * Especificar Olá função você para o qual você deseja acesso remoto tooenable

   * Clique em Olá tooselect **habilitar área de trabalho remota** caixa de seleção
   
   * Especifique um nome de usuário e senha que você deseja toouse para acesso remoto
   
   * Selecione Olá certificado toouse

6. Clique em **OK** 

Você verá uma mensagem informando que a alteração da configuração está em andamento, o que pode levar alguns toocomplete de minutos. Após a alteração de configuração hello, siga as etapas de Olá Olá **toolog em remotamente** seção mais adiante neste artigo.

## <a name="how-tooenable-remote-access-in-your-package"></a>Como tooenable de acesso remoto no pacote
1. No painel Gerenciador de Projetos do Eclipse, clique com o botão direito no projeto do Azure e clique em **Propriedades**.

2. Em Olá **propriedades** caixa de diálogo, expanda **Azure** no painel esquerdo do hello e clique em **acesso remoto**.

3. Em Olá **acesso remoto** caixa de diálogo, certifique-se de **habilitar todas as funções tooaccept conexões de área de trabalho remota com essas credenciais de logon** é verificada.

4. Especifique um nome de usuário para Olá conexão de área de trabalho remota.

5. Especifique e confirme a senha de saudação do usuário de saudação. produtos de valores de nome e a senha de usuário Olá definidos nesta caixa de diálogo serão usados quando você faz uma conexão de área de trabalho remota. (Observe que essa é uma senha separada da sua senha PFX).

6. Especifique a data de validade de Olá Olá conta de usuário.

7. Clique em **novo** toocreate um novo certificado autoassinado. (Como alternativa, você pode selecionar um certificado de seu espaço de trabalho ou sistema de arquivos por meio de saudação **espaço de trabalho** ou **FileSystem** botões, respectivamente, mas para fins deste tutorial, criaremos um novo certificado).

   * Em Olá **novo certificado** caixa de diálogo, especifique e confirme a senha de saudação que será usada para o arquivo PFX.

   * Aceite Olá valor fornecido para **nome (CN)**, ou use um nome personalizado.

   * Especifique Olá caminho e nome de arquivo onde Olá novo certificado, no formato. cer, será salvo. Para esta etapa e Olá próxima, você poderá usar Olá **cert** pasta do seu projeto do Azure, mas estiver livre toochoose outro local. Para este tutorial, usaremos **c:\mycert\mycert.cer**. (Criar hello **c:\mycert** tooproceeding anterior da pasta ou usar uma pasta existente, se desejado.)

   * Especifique Olá caminho e nome de arquivo onde Olá novo certificado e sua chave privada, no formato. pfx, serão salvos. Para este tutorial, usaremos **c:\mycert\mycert.pfx**. O **novo certificado** caixa de diálogo deve parecer semelhante seguinte de toohello (atualizar os caminhos de pasta Olá se você não usou **c:\mycert**):
     
      ![][ic712275]

   * Clique em **Okey** tooclose Olá **novo certificado** caixa de diálogo.

8. O **acesso remoto** caixa de diálogo deve ser a seguir toohello semelhante:</p>
   
   ![][ic719495]

9. Clique em **Okey** tooclose Olá **acesso remoto** caixa de diálogo.

Recrie seu aplicativo, com hello criar conjunto de toocloud de implantação.

## <a name="toolog-in-remotely"></a>toolog em remotamente
Quando sua instância de função estiver pronta, você poderá fazer logon remotamente na máquina virtual toohello que está hospedando o seu aplicativo.

* Se estiver usando o Eclipse no Windows e selecionado Olá **implantação de área de trabalho remota no início** opção durante tooAzure sua implantação, você verá uma tela de logon da Conexão de área de trabalho remota quando sua implantação for iniciada. Quando você for solicitado Olá nome de usuário e senha, insira valores hello que você especificou para o usuário remoto hello e será capaz de toolog no.

* Toolog de outra forma no remotamente é por meio de saudação <a href="http://go.microsoft.com/fwlink/?LinkID=512959">Portal de gerenciamento</a>:
  
  * Dentro de saudação **serviços de nuvem** exibição de saudação portal de gerenciamento do Azure, clique em seu serviço de nuvem, **instâncias**, clique em uma instância específica e, em seguida, clique em Olá **conectar**botão. Olá **conectar** botão aparece como a seguir na barra de comandos Olá Olá:
    
      ![][ic659273]

  * Depois de clicar em Olá **conectar** botão, você será solicitado tooopen um arquivo RDP. Abra o arquivo hello e siga os prompts de saudação. (Você pode também salvar este computador local do arquivo tooyour e executar arquivo hello clicando duas vezes nele log tooremote no tooyour máquina virtual sem a necessidade de toofirst acesse o portal de gerenciamento hello.)

  * Quando você for solicitado Olá nome de usuário e senha, insira valores hello que você especificou para o usuário remoto hello e será capaz de toolog no.

> [!NOTE]
> Se você estiver usando um sistema operacional Windows não, você precisa toouse um cliente de área de trabalho remota que é compatível com o sistema operacional e siga Olá etapas tooconfigure que o cliente com as configurações de saudação no arquivo RDP Olá que você baixou.
> 
> 

## <a name="see-also"></a>Consulte também
[Kit de Ferramentas do Azure para Eclipse][Azure Toolkit for Eclipse]

[Criar um aplicativo Hello World para Azure no Eclipse][Creating a Hello World Application for Azure in Eclipse]

[Saudação de instalar o Kit de ferramentas do Azure para Eclipse][Installing hello Azure Toolkit for Eclipse] 

Para obter mais informações sobre como usar o Azure com Java, consulte Olá [Centro de desenvolvedores de Java do Azure][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic712275]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic712275.png
[ic719495]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719495.png
[ic719494]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719494.png
[ic659273]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic659273.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690951.aspx -->
