---
title: "Habilitando o Acesso Remoto para implantações do Azure no Eclipse"
description: "Saiba como habilitar o acesso remoto para implantações do Azure usando o Kit de Ferramentas do Azure para Eclipse."
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
ms.openlocfilehash: 654d511bd5a62341f87569317e97360c94a6f26c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="enabling-remote-access-for-azure-deployments-in-eclipse"></a>Habilitando o Acesso Remoto para implantações do Azure no Eclipse
Para ajudar a solucionar problemas em suas implantações, você pode habilitar e usar o Acesso Remoto a fim de conectar-se à máquina virtual que hospeda sua implantação. A funcionalidade Acesso Remoto baseia-se no protocolo RDP (Remote Desktop Protocol). Você pode configurar o Acesso Remoto para sua implantação após publicá-la no Azure ou, se você estiver usando o Eclipse com um sistema operacional Windows, poderá configurar o Acesso Remoto antes de publicar no Azure. Saiba que você precisará de um cliente de área de trabalho remota compatível com seu sistema operacional a fim de conectar-se à máquina virtual da implantação no Azure.

## <a name="how-to-enable-remote-access-before-you-deploy-to-azure"></a>Como habilitar o Acesso Remoto antes de implantar no Azure
> [!NOTE]
> Para habilitar o Acesso Remoto antes de implantar seu aplicativo no Azure, você precisará executar o Eclipse no Windows.
> 
> 

A imagem a seguir mostra a caixa de diálogo de propriedades do **Acesso Remoto** usada para habilitar o acesso remoto.

![][ic719494]

Há duas maneiras de exibir a caixa de diálogo de propriedades do **Acesso Remoto** :

* Clique no link **Avançado** na seção **Acesso Remoto** da caixa de diálogo **Publicar no Azure**.

* Abra a caixa de diálogo **Propriedades** de seu projeto do Azure.

Ao criar um novo projeto de implantação do Azure, o acesso remoto não estará habilitado por padrão. No entanto, você pode habilitá-lo com facilidade especificando o nome de usuário e a senha na caixa de diálogo **Publicar no Azure** . A senha do Acesso Remoto é criptografada usando certificados X.509. Se você não usar seu próprio certificado, a criptografia dependerá de um certificado autoassinado fornecido com o plug-in do Azure para Eclipse. Esse certificado autoassinado está na pasta **cert** de seu projeto do Azure, armazenado como um arquivo de certificado público (SampleRemoteAccessPublic.cer) e um arquivo de certificado PFX (Troca de Informações Pessoais) (SampleRemoteAccessPrivate.pfx). O segundo contém a chave privada do certificado e uma senha padrão, **Password1**. No entanto, como essa senha é de conhecimento público, o certificado padrão deve ser usado apenas para fins de aprendizado e não para uma implantação de produção. Assim, exceto para fins de aprendizado, quando você quiser habilitar as sessões remotas para suas implantações, deverá clicar no link **Avançado** na caixa de diálogo **Publicar no Azure** para especificar seu próprio certificado. Observe que você precisará carregar a versão PFX do certificado no serviço hospedado no Portal de Gerenciamento do Azure, para que o Azure possa descriptografar a senha do usuário.

O restante do tutorial mostra como habilitar o acesso remoto para um projeto de implantação do Azure criado inicialmente com o acesso remoto desabilitado. Para este tutorial, criaremos um novo certificado autoassinado e seu arquivo .pfx terá uma senha escolhida por você. Você também tem a opção de usar um certificado emitido por uma autoridade de certificação.

## <a name="how-to-enable-remote-access-after-you-have-deployed-to-azure"></a>Como habilitar o Acesso Remoto após a implantação no Azure
Para habilitar o acesso remoto após a implantação no Azure, execute as seguintes etapas:

1. Fazer logon no portal de gerenciamento do Azure usando sua conta do Azure

2. Na lista de **Serviços de Nuvem**, escolha o serviço de nuvem implantado

3. Na página da Web do serviço de nuvem, clique no link **Configurar**

4. Na parte inferior da página de configuração, clique no link **Remoto**

5. Quando a caixa de diálogo pop-up aparecer:
   
   * Especifique a Função para a qual você deseja habilitar o acesso remoto

   * Clique para marcar a caixa de seleção **Habilitar Área de Trabalho Remota**
   
   * Especifique um nome de usuário e senha que você deseja usar para o acesso remoto
   
   * Escolher o certificado a ser usado

6. Clique em **OK** 

Você verá uma mensagem informando que a alteração da configuração está em andamento, o que pode levar alguns minutos para ser concluído. Após a conclusão da alteração de configuração, execute as etapas na seção **Para fazer logon remotamente** posteriormente neste artigo.

## <a name="how-to-enable-remote-access-in-your-package"></a>Como habilitar o Acesso Remoto em seu pacote
1. No painel Gerenciador de Projetos do Eclipse, clique com o botão direito no projeto do Azure e clique em **Propriedades**.

2. Na caixa de diálogo **Propriedades**, expanda **Azure** no painel esquerdo e clique em **Acesso Remoto**.

3. Na caixa de diálogo **Acesso Remoto**, verifique se **Habilitar todas as funções para aceitar as Conexões da Área de Trabalho Remota com essas credenciais de logon** está marcada.

4. Especifique um nome de usuário para a conexão de Área de Trabalho Remota.

5. Especifique e confirme a senha para o usuário. Os valores de nome de usuário e senha definidos nesta caixa de diálogo serão usados quando você fizer uma conexão de Área de Trabalho Remota. (Observe que essa é uma senha separada da sua senha PFX).

6. Especifique a data de expiração da conta de usuário.

7. Clique em **Novo** para criar um novo certificado autoassinado. (Como alternativa, você pode selecionar um certificado de seu espaço de trabalho ou sistema de arquivos por meio dos botões **Espaço de Trabalho** ou **Sistema de Arquivos**, respectivamente, mas este tutorial, criaremos um novo certificado.)

   * Na caixa de diálogo **Novo Certificado** , especifique e confirme a senha que você usará para o arquivo PFX.

   * Aceite o valor fornecido para **Nome (CN)**ou use um nome personalizado.

   * Especifique o caminho e o nome de arquivo no qual o novo certificado, no formato .cer, será salvo. Para essa etapa e a próxima, você poderá usar a pasta **cert** de seu projeto do Azure, mas sinta-se à vontade para escolher outro local. Para este tutorial, usaremos **c:\mycert\mycert.cer**. (Crie a pasta **c:\mycert** antes de prosseguir ou use uma pasta existente, se desejado.)

   * Especifique o caminho e o nome de arquivo no qual o novo certificado e sua chave privada, no formato .pfx, serão salvos. Para este tutorial, usaremos **c:\mycert\mycert.pfx**. Sua caixa de diálogo **Novo Certificado** deve ser parecida com a seguinte (atualize os caminhos da pasta se você não usou **c:\mycert**):
     
      ![][ic712275]

   * Clique em **OK** para fechar a caixa de diálogo **Novo Certificado**.

8. A caixa de diálogo **Acesso Remoto** deve ser semelhante ao seguinte:</p>
   
   ![][ic719495]

9. Clique em **OK** para fechar a caixa de diálogo **cesso Remoto**.

Recrie seu aplicativo, com a compilação definida para implantação em nuvem.

## <a name="to-log-in-remotely"></a>Para fazer logon remotamente
Quando a sua instância de função estiver pronta, você poderá fazer logon remotamente na máquina virtual que está hospedando o aplicativo.

* Se você estiver usando o Eclipse no Windows e selecionou a opção **Iniciar área de trabalho remota na implantação** durante a implantação do Azure, receberá uma tela de logon para a Conexão de Área de Trabalho Remota quando a implantação for iniciada. Quando receber a solicitação de nome de usuário e senha, insira os valores que você especificou para o usuário remoto e assim conseguirá fazer logon.

* Outra maneira de fazer logon remotamente é por meio do <a href="http://go.microsoft.com/fwlink/?LinkID=512959">Portal de Gerenciamento do Azure</a>:
  
  * Na exibição **Serviços de Nuvem** do portal de Gerenciamento do Azure, clique em seu serviço de nuvem, clique em **Instâncias**, em uma instância específica, em seguida, clique no botão **Conectar**. O botão **Conectar** aparece da seguinte forma na barra de comandos:
    
      ![][ic659273]

  * Depois de clicar no botão **Conectar** , você receberá uma solicitação para abrir um arquivo RDP. Abra o arquivo e siga os prompts. (Você pode também salvar esse arquivo em seu computador local e depois executar o arquivo clicando duas vezes nele para fazer logon remoto em sua máquina virtual sem a necessidade de acessar primeiro o portal de gerenciamento).

  * Quando receber a solicitação de nome de usuário e senha, insira os valores que você especificou para o usuário remoto e assim conseguirá fazer logon.

> [!NOTE]
> Se você estiver em um sistema operacional que não seja o Windows, será necessário usar um cliente de Área de Trabalho Remota compatível com o sistema operacional e executar as etapas para definir esse cliente com as configurações no arquivo RDP baixado.
> 
> 

## <a name="see-also"></a>Consulte também
[Kit de Ferramentas do Azure para Eclipse][Azure Toolkit for Eclipse]

[Criar um aplicativo Hello World para Azure no Eclipse][Creating a Hello World Application for Azure in Eclipse]

[Instalar o Kit de Ferramentas do Azure para Eclipse][Installing the Azure Toolkit for Eclipse] 

Para saber mais sobre como usar o Azure com o Java, confira o [Centro de Desenvolvedores Java do Azure][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic712275]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic712275.png
[ic719495]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719495.png
[ic719494]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719494.png
[ic659273]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic659273.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690951.aspx -->
