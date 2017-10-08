---
title: "aaaHow toocreate e implantar um serviço de nuvem | Microsoft Docs"
description: "Saiba como toocreate e implantar um serviço de nuvem usando o método de criação rápida hello no Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 0ea78ccc-5e7d-40f8-bdb6-478c0eb0e265
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 09f889f81ccee6e8a7657116183aa4100410214c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-deploy-a-cloud-service"></a>Como tooCreate e implantar um serviço de nuvem
> [!div class="op_single_selector"]
> * [Portal do Azure](cloud-services-how-to-create-deploy-portal.md)
> * [Portal clássico do Azure](cloud-services-how-to-create-deploy.md)
> 
> 

Olá portal clássico do Azure fornece duas maneiras para você toocreate e implantar um serviço de nuvem: **criação rápida** e **criação personalizada**.

Este tópico explica como toouse Olá toocreate de método rápido criar um novo serviço de nuvem e, em seguida, usar **carregar** tooupload e implantar um pacote de serviço de nuvem no Azure. Quando você usar esse método, Olá portal clássico do Azure torna disponível links convenientes para a conclusão de todos os requisitos conforme você avança. Se você estiver pronto toodeploy sua nuvem de serviço quando você criá-lo, você pode fazer ao Olá mesmo tempo usando **criação personalizada**.

> [!NOTE]
> Se você planejar toopublish seu serviço de nuvem do Visual Studio Team Services (VSTS), use **criação rápida**e, em seguida, configurar a publicação do VSTS de **início rápido** ou painel hello.
> 
> 

## <a name="concepts"></a>Conceitos
Três componentes são necessários na ordem toodeploy um aplicativo como uma nuvem de serviço no Azure:

* **Definição de serviço**  
  arquivo de definição de serviço de nuvem da saudação (. csdef) define o modelo de serviço hello, incluindo o número de funções hello.
* **Configuração de serviço**  
  arquivo de configuração de serviço de nuvem da saudação (. cscfg) fornece definições de configuração para o serviço de nuvem hello e funções individuais, incluindo Olá número de instâncias de função.
* **Pacote de serviço**  
  pacote de serviço da saudação (. cspkg) contém o código do aplicativo hello e configurações e o arquivo de definição de serviço hello.

Você pode aprender mais sobre essas e como um pacote de toocreate [aqui](cloud-services-model-and-package.md).

## <a name="prepare-your-app"></a>Preparação do aplicativo
Antes de implantar um serviço de nuvem, você deve criar o pacote de serviço de nuvem hello (. cspkg) do seu código de aplicativo e um arquivo de configuração de serviço de nuvem (. cscfg). Olá SDK do Azure fornece ferramentas para preparar a esses arquivos de implantação necessária. Você pode instalar o SDK de saudação do hello [Downloads do Azure](https://azure.microsoft.com/downloads/) página, na linguagem de saudação em que você preferir toodevelop seu código de aplicativo.

Três recursos de serviço de nuvem precisam de configurações especiais antes que você exporte um pacote de serviço:

* Se você quiser toodeploy um serviço de nuvem que usa o protocolo (SSL) para criptografia de dados, [configurar seu aplicativo](cloud-services-configure-ssl-certificate.md#step-2-modify-the-service-definition-and-configuration-files) para SSL.
* Se você quiser instâncias de toorole de conexões de área de trabalho remota tooconfigure, [configurar funções hello](cloud-services-role-enable-remote-desktop.md) para área de trabalho remota.
* Se você quiser tooconfigure detalhado de monitoramento para seu serviço de nuvem, habilite o diagnóstico do Azure para serviço de nuvem hello. *Monitoramento mínimo* (Olá nível padrão de monitoração) usa contadores de desempenho coletados a partir de sistemas operacionais do hello host para instâncias de função (máquinas virtuais). "O monitoramento detalhado * coleta métricas adicionais com base nos dados de desempenho em Olá função instâncias tooenable uma análise mais próxima dos problemas que ocorrem durante o processamento do aplicativo. toofind como tooenable diagnóstico do Azure, consulte [habilitando o diagnóstico no Azure](cloud-services-dotnet-diagnostics.md).

toocreate um serviço de nuvem com implantações de funções web ou funções de trabalho, você deve [criar pacote de serviço Olá](cloud-services-model-and-package.md#servicepackagecspkg).

## <a name="before-you-begin"></a>Antes de começar
* Se você ainda não instalou Olá SDK do Azure, clique em **instalar SDK do Azure** tooopen Olá [página Downloads do Azure](https://azure.microsoft.com/downloads/)e, em seguida, baixe Olá SDK para o idioma de saudação em que você preferir toodevelop seu código. (Você terá uma oportunidade toodo isso mais tarde.)
* Se quaisquer instâncias de função exigem um certificado, crie certificados hello. Os serviços de nuvem requerem um arquivo .pfx e uma chave privada. Você pode [carregar Olá certificados tooAzure](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) como criar e implantar o serviço de nuvem hello.
* Se desejar que o grupo de afinidade tooan do serviço de nuvem de saudação toodeploy, crie grupo de afinidade de saudação. Você pode usar um grupo de afinidade toodeploy seu serviço de nuvem e outros serviços do Azure toohello mesmo local em uma região. Você pode criar o grupo de afinidade Olá no hello **redes** área da saudação portal clássico do Azure, em Olá **grupos de afinidade** página.

## <a name="how-to-create-a-cloud-service-using-quick-create"></a>Tutorial: Criar um serviço de nuvem com a Criação Rápida
1. Em Olá [portal clássico do Azure](http://manage.windowsazure.com/), clique em **novo**>**de computação**>**serviço de nuvem** > **Criação rápida**.
   
    ![CloudServices_QuickCreate](./media/cloud-services-how-to-create-deploy/CloudServices_QuickCreate.png)
2. Em **URL**, insira um toouse de nome de subdomínio na URL pública Olá para acessar seu serviço de nuvem em implantações de produção. saudação de formato de URL para implantações de produção é: http://*myURL*. cloudapp.net.
3. Em **região ou grupo de afinidade**, selecione Olá geográfica região ou grupo de afinidade toodeploy Olá serviço de nuvem. Selecione um grupo de afinidade, se desejar toodeploy seu toohello de serviço de nuvem mesmo local que outros serviços do Azure dentro de uma região.
4. Clique em **Criar Serviço de Nuvem**.
   
    ![CloudServices_Region](./media/cloud-services-how-to-create-deploy/CloudServices_Regionlist.png)
   
    Você pode monitorar o status de saudação do processo de saudação na área de mensagem de saudação na parte inferior da saudação da janela de saudação.
   
    Olá **serviços de nuvem** área é aberto com hello novo serviço de nuvem exibido. Quando o status de saudação alterado tooCreated, criação de serviço de nuvem foi concluída com êxito.
   
    ![CloudServices_CloudServicesPage](./media/cloud-services-how-to-create-deploy/CloudServices_CloudServicesPage.png)

## <a name="how-to-upload-a-certificate-for-a-cloud-service"></a>Tutorial: Carregar um certificado para um serviço de nuvem
1. Em Olá [portal clássico do Azure](http://manage.windowsazure.com/), clique em **serviços de nuvem**, clique em nome de Olá Olá do serviço de nuvem e, em seguida, clique em **certificados**.
   
    ![CloudServices_QuickCreate](./media/cloud-services-how-to-create-deploy/CloudServices_EmptyDashboard.png)
2. Clique em **Carregar um certificado** ou **Carregar**.
3. Em **arquivo**, use **procurar** tooselect certificado de saudação (arquivo. pfx).
4. Em **senha**, insira a chave privada Olá certificado hello.
5. Clique em **OK** (marca de seleção).
   
    ![CloudServices_AddaCertificate](./media/cloud-services-how-to-create-deploy/CloudServices_AddaCertificate.png)
   
    Você pode assistir o progresso de saudação do carregamento de saudação na área de mensagem de saudação, mostrado abaixo. Quando o carregamento de saudação for concluído, o certificado de saudação é adicionado toohello tabela. Na área de mensagem de saudação, clique em mensagem de saudação tooclose Okey.
   
    ![CloudServices_CertificateProgress](./media/cloud-services-how-to-create-deploy/CloudServices_CertificateProgress.png)

## <a name="how-to-deploy-a-cloud-service"></a>Tutorial: Implantar um serviço de nuvem
1. Em Olá [portal clássico do Azure](http://manage.windowsazure.com/), clique em **serviços de nuvem**, clique em nome de Olá Olá do serviço de nuvem e, em seguida, clique em **painel**.
2. Clique em **Carregar uma nova implantação de produção** ou em **Carregar**.
3. Em **rótulo de implantação**, insira um nome para a nova implantação Olá - por exemplo, MyCloudServicev4.
4. Em **pacote**, use **procurar** tooselect Olá serviço pacote arquivo (. cspkg) toouse.
5. Em **configuração**, use **procurar** toouse (. cscfg) do arquivo de configuração do serviço de saudação tooselect.
6. Se o serviço de nuvem Olá incluirá todas as funções com apenas uma instância, selecione Olá **implantar mesmo se uma ou mais funções contiverem uma única instância** caixa de seleção tooenable Olá implantação tooproceed.
   
    Azure somente pode garante 99,95% acesso toohello serviço em nuvem durante as atualizações de serviço e manutenção se cada função tem pelo menos duas instâncias. Se necessário, você pode adicionar instâncias de função adicionais em Olá **escala** página depois de implantar o serviço de nuvem hello. Para obter mais informações, consulte [Contratos de Nível de Serviço](https://azure.microsoft.com/support/legal/sla/).
7. Clique em **Okey** implantação de serviço de nuvem (marca de seleção) toobegin hello.
   
    ![CloudServices_UploadaPackage](./media/cloud-services-how-to-create-deploy/CloudServices_UploadaPackage.png)
   
    Você pode monitorar o status de saudação da implantação de saudação na área de mensagem de saudação. Clique em mensagem de saudação toohide Okey.
   
    ![CloudServices_UploadProgress](./media/cloud-services-how-to-create-deploy/CloudServices_UploadProgress.png)

## <a name="verify-your-deployment-completed-successfully"></a>Verifique se a implantação foi concluída com êxito
1. Clique em **Painel**.
   
    Hello status deve mostrar que o serviço de saudação **executando**.
2. Em **visão rápida**, clique em Olá site URL tooopen seu serviço de nuvem em um navegador da web.
   
    ![CloudServices_QuickGlance](./media/cloud-services-how-to-create-deploy/CloudServices_QuickGlance.png)


## <a name="next-steps"></a>Próximas etapas
* [Configuração geral do serviço de nuvem](cloud-services-how-to-configure.md).
* Configurar um [nome de domínio personalizado](cloud-services-custom-domain-name.md).
* [Gerenciar seu serviço de nuvem](cloud-services-how-to-manage.md).
* Configurar [certificados SSL](cloud-services-configure-ssl-certificate.md).

