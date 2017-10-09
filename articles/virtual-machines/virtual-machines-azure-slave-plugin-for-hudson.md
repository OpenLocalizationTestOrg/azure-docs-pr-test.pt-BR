---
title: "aaaHow toouse hello Azure escravo de plug-in com a integração contínua Hudson | Microsoft Docs"
description: "Descreve como toouse hello Azure slave plug-in com a integração contínua Hudson."
services: virtual-machines-linux
documentationcenter: 
author: rmcmurray
manager: wpickett
editor: 
ms.assetid: b2083d1c-4de8-4a19-a615-ccc9d9b6e1d9
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: cd6e67ad71c208aa56746aa8b70ba507da20bee9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-slave-plug-in-with-hudson-continuous-integration"></a>Como toouse hello Azure slave plug-in com a integração contínua Hudson
Hello Azure escravo de plug-in para Hudson permite que você tooprovision subordinado nós no Azure quando em execução distribuída cria.

## <a name="install-hello-azure-slave-plug-in"></a>Instalar hello Azure subordinado plug-in
1. No painel Hudson do hello, clique em **Hudson gerenciar**.
2. Em Olá **Hudson gerenciar** página, clique em **gerenciar plug-ins**.
3. Clique em Olá **disponível** guia.
4. Clique em **pesquisa** e tipo **Azure** toolimit Olá lista toorelevant plug-ins.
   
    Se você optar por tooscroll por meio da lista de saudação de plug-ins disponíveis, você encontrará hello Azure subordinado plug-in em Olá **distribuídas de compilação e de gerenciamento de Cluster** seção Olá **outros** guia.
5. Selecione caixa de seleção Olá para **plug-in do Azure subordinado**.
6. Clique em **Instalar**.
7. Reinicie o Hudson.

Agora que Olá plug-in estiver instalado, as próximas etapas Olá seria tooconfigure Olá plug-in com o perfil de assinatura do Azure e toocreate um modelo que será usado na criação de hello VM para o nó de escravo hello.

## <a name="configure-hello-azure-slave-plug-in-with-your-subscription-profile"></a>Configurar hello Azure subordinado plug-in com o seu perfil de inscrição
Um perfil de assinatura, também chamado de tooas configurações de publicação, é um arquivo XML que contém credenciais seguras e informações adicionais, você precisará toowork com o Azure no seu ambiente de desenvolvimento. tooconfigure hello Azure escravo de plug-in, você precisa:

* A ID de sua assinatura
* Um certificado de gerenciamento da sua assinatura

Eles podem ser encontrados em seu [perfil de assinatura]. Veja a seguir um exemplo de perfil de assinatura.

    <?xml version="1.0" encoding="utf-8"?>

        <PublishData>

          <PublishProfile SchemaVersion="2.0" PublishMethod="AzureServiceManagementAPI">

        <Subscription

              ServiceManagementUrl="https://management.core.windows.net"

              Id="<Subscription ID>"

              Name="Pay-As-You-Go"
            ManagementCertificate="<Management certificate value>" />

          </PublishProfile>

    </PublishData>

Uma vez que o perfil de assinatura, siga essas tooconfigure de etapas hello Azure escravo de plug-in.

1. No painel Hudson do hello, clique em **Hudson gerenciar**.
2. Clique em **Configure System**.
3. Role para baixo de saudação do hello página toofind **nuvem** seção.
4. Clique em **Adicionar nova nuvem > Microsoft Azure**.
   
    ![adicionar nova nuvem][add new cloud]
   
    Isso mostrará campos Olá em que você precisa tooenter detalhes da sua assinatura.
   
    ![configurar perfil][configure profile]
5. Copie o certificado de id e o gerenciamento de assinatura de saudação do seu perfil de inscrição e cole-os nos campos apropriados hello.
   
    Ao copiar Olá assinatura id e o gerenciamento de certificado, **não** incluir aspas Olá colocar valores hello.
6. Clique em **Verify configuration**.
7. Quando a configuração de saudação é verificada com êxito, clique em **salvar**.

## <a name="set-up-a-virtual-machine-template-for-hello-azure-slave-plug-in"></a>Configurar um modelo de máquina virtual para hello Azure subordinado plug-in
Um modelo de máquina virtual define parâmetros Olá Olá plug-in usará toocreate um nó subordinado no Azure. Em Olá etapas a seguir é estará criando o modelo para uma VM Ubuntu.

1. No painel Hudson do hello, clique em **Hudson gerenciar**.
2. Clique em **Configure System**.
3. Role para baixo de saudação do hello página toofind **nuvem** seção.
4. Dentro de saudação **nuvem** seção, localize **Adicionar modelo de máquina Virtual do Azure** e clique em Olá **adicionar** botão.
   
    ![adicionar modelo de vm][add vm template]
5. Especifique um nome de serviço de nuvem no hello **nome** campo. Se o nome hello especificado refere-se tooan existente de serviço de nuvem, Olá VM será provisionado no serviço. Caso contrário, o Azure criará um novo.
6. Em Olá **descrição** , digite o texto que descreve o modelo de saudação você está criando. Essas informações são apenas para fins de documentação e não são usadas no provisionamento de uma VM.
7. Em Olá **rótulos** , digite **linux**. Este rótulo é usado tooidentify Olá modelo que você está criando e é o modelo de saudação de tooreference subsequentemente usada ao criar um trabalho de Hudson.
8. Selecione uma região onde Olá VM será criado.
9. Selecione o tamanho da VM Olá apropriado.
10. Especifique uma conta de armazenamento onde Olá VM será criado. Certifique-se de que ela está em Olá mesma região que o serviço de nuvem Olá você está usando. Se desejar que o novo toobe de armazenamento criada, você pode deixar esse campo em branco.
11. Tempo de retenção Especifica o número de saudação de minutos antes de Hudson exclui um subordinado ocioso. Deixe este valor saudação padrão é 60.
12. Em **uso**, selecione Olá condição adequada quando esse nó subordinado será usado. Por enquanto, selecione **Utilize this node as much as possible**.
    
     Neste ponto, seu formulário seria toothis um pouco semelhante:
    
     ![configuração de modelo][template config]
13. Em **família de imagem ou Id** ter toospecify qual imagem do sistema será instalada na sua VM. Você pode selecionar em uma lista de famílias de imagens ou especificar uma imagem personalizada.
    
     Se você quiser tooselect em uma lista de famílias de imagem, digite Olá primeiro caractere (diferencia maiusculas de minúsculas) de nome de família de imagem hello. Por exemplo, se você digitar **U** , será exibida uma lista das famílias de servidores do Ubuntu. Depois que você seleciona na lista de hello, Jenkins usará a versão mais recente de saudação dessa imagem do sistema de família ao provisionar a VM.
    
     ![lista de famílias de SO][OS family list]
    
     Se você tiver uma imagem personalizada que você deseja toouse, digite o nome de saudação da imagem personalizada. Nomes de imagens personalizadas não são mostrados em uma lista para que você tenha tooensure que Olá nome foi digitado corretamente.    
    
     Para este tutorial, digite **U** toobring uma lista de imagens Ubuntu e selecione **Ubuntu Server 14.04 LTS**.
14. Em **Método de Inicialização**, selecione **SSH**.
15. Script de saudação abaixo de copiar e colar no hello **script Init** campo.
    
         # Install Java
    
         sudo apt-get -y update
    
         sudo apt-get install -y openjdk-7-jdk
    
         sudo apt-get -y update --fix-missing
    
         sudo apt-get install -y openjdk-7-jdk
    
         # Install git
    
         sudo apt-get install -y git
    
         #Install ant
    
         sudo apt-get install -y ant
    
         sudo apt-get -y update --fix-missing
    
         sudo apt-get install -y ant
    
     Olá **script Init** será executado depois de saudação VM é criada. Neste exemplo, o script hello instala ant, Java e git.
16. Em Olá **Username** e **senha** campos, insira valores de sua preferência para a conta de administrador hello será criada na sua VM.
17. Clique em **Verificar modelo** toocheck se Olá parâmetros especificados são válidos.
18. Clique em **Save**.

## <a name="create-a-hudson-job-that-runs-on-a-slave-node-on-azure"></a>Criar um trabalho do Hudson executado em um nó subordinado no Azure
Nesta seção, você criará uma tarefa do Hudson que será executada em um nó subordinado no Azure.

1. No painel Hudson do hello, clique em **novo trabalho**.
2. Insira um nome para o trabalho de saudação que você está criando.
3. Para o tipo de trabalho hello, selecione **criar um trabalho de software livre de estilo**.
4. Clique em **OK**.
5. Na página de configuração de trabalho hello, selecione **restringir onde este projeto pode ser executado**.
6. Selecione **nó e o rótulo do menu** e selecione **linux** (especificamos a este rótulo ao criar o modelo de máquina virtual de saudação na seção anterior Olá).
7. Em Olá **criar** seção, clique em **adicionar a etapa de compilação** e selecione **executar shell**.
8. Editar saudação script a seguir, substituindo **{seu nome de conta do github}**, **{o nome do projeto}**, e **{diretório do projeto}** com valores adequados e cole Olá Editar script na área de texto de saudação que aparece.
   
        # Clone from git repo
   
        currentDir="$PWD"
   
        if [ -e {your project directory} ]; then
   
              cd {your project directory}
   
              git pull origin master
   
        else
   
              git clone https://github.com/{your github account name}/{your project name}.git
   
        fi
   
        # change directory tooproject
   
        cd $currentDir/{your project directory}
   
        #Execute build task
   
        ant
9. Clique em **Save**.
10. Olá painel Hudson em, encontre o trabalho de saudação que você acabou de criar e clique em Olá **agendar uma compilação** ícone.

Hudson será, em seguida, criar um nó subordinado usando Olá modelo criado na seção anterior hello e executar script hello especificado na etapa de compilação Olá para esta tarefa.

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre como usar o Azure com Java, consulte Olá [Centro de desenvolvedores de Java do Azure].

<!-- URL List -->

[Centro de desenvolvedores de Java do Azure]: https://azure.microsoft.com/develop/java/
[perfil de assinatura]: http://go.microsoft.com/fwlink/?LinkID=396395

<!-- IMG List -->

[add new cloud]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addcloud.png
[configure profile]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-configureprofile.png
[add vm template]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addnewvmtemplate.png
[template config]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-templateconfig1-withdata.png
[OS family list]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-oslist.png

