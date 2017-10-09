---
title: aaaDeploy 4HANA/S de SAP ou BW/4HANA em uma VM do Azure | Microsoft Docs
description: Implantar o SAP S/4HANA ou o BW/4HANA em uma VM do Azure
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 44bbd2b6-a376-4b5c-b824-e76917117fa9
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 09/15/2016
ms.author: hermannd
ms.openlocfilehash: 7e57f7daa7667b7c7dbcb86f6892a54e4295b74c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-sap-s4hana-or-bw4hana-on-azure"></a>Implantar o SAP S/4HANA ou o BW/4HANA no Azure
Este artigo descreve como toodeploy S/4HANA no Azure usando Olá biblioteca de dispositivo de nuvem do SAP (SAP CAL) 3.0. toodeploy outras soluções baseadas em SAP HANA, como BW/4HANA, siga Olá mesmas etapas.

> [!NOTE]
Para obter mais informações sobre Olá CAL do SAP, vá toohello [biblioteca de dispositivo de nuvem do SAP](https://cal.sap.com/) site. SAP também tem um blog sobre Olá [SAP nuvem Appliance biblioteca 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).

> [!NOTE]
Além disso como de 29 de maio de 2017, você pode usar o modelo de implantação do Azure Resource Manager Olá implantação clássica menos preferencial toohello modelo toodeploy Olá CAL do SAP. É recomendável que você use o novo modelo de implantação de Gerenciador de recursos hello e ignorar o modelo de implantação clássico hello.

## <a name="step-by-step-process-toodeploy-hello-solution"></a>Solução de saudação toodeploy processo passo a passo

Olá sequência de capturas de tela a seguir mostra como toodeploy S/4HANA no Azure usando Olá CAL do SAP. processo de saudação funciona Olá mesma forma para outras soluções, como BW/4HANA.

Olá **soluções** página mostra alguns Olá soluções baseadas em SAP HANA de CAL disponíveis no Azure. **SAP S/4HANA 1610 FPS01, Fully-Activated dispositivo** está na linha intermediária hello:

![Soluções de SAP CAL](./media/cal-s4h/s4h-pic-1c.png)

### <a name="create-an-account-in-hello-sap-cal"></a>Criar uma conta no hello CAL do SAP
1. toosign em toohello CAL do SAP para hello primeira vez, use seu usuário SAP S ou outro usuário registrado com o SAP. Em seguida, defina uma conta de CAL do SAP que é usada por dispositivos de toodeploy Olá CAL do SAP no Azure. Na definição de conta hello, você precisa:

    a. Selecione o modelo de implantação de saudação no Azure (Gerenciador de recursos ou clássico).

    b. Inserir sua assinatura do Azure. Tooone assinatura só pode ser atribuída a uma conta de CAL do SAP. Se você precisar de mais de uma assinatura, você precisa toocreate outra conta de CAL do SAP.

    c. Dê Olá SAP CAL permissão toodeploy em sua assinatura do Azure.

    > [!NOTE]
    as próximas etapas Olá mostram como a conta toocreate um CAL do SAP para implantações do Gerenciador de recursos. Se você já tiver uma conta de CAL do SAP que é o modelo de implantação clássico toohello vinculado, você *necessário* toofollow toocreate essas etapas uma nova conta de CAL do SAP. nova conta de CAL SAP Olá precisa toodeploy no modelo do Gerenciador de recursos de saudação.

2. Crie uma nova conta do SAP CAL. Olá **contas** página mostra três opções para o Azure: 

    a. **Microsoft Azure (clássica)** é o modelo de implantação clássico hello e não está mais preferencial.

    b. **Microsoft Azure** é Olá novo modelo de implantação de Gerenciador de recursos.

    c. **Windows Azure operado pela 21Vianet** é uma opção na China que usa o modelo de implantação clássico hello.

    Selecione toodeploy no modelo do Gerenciador de recursos de hello, **Microsoft Azure**.

    ![Detalhes da conta da SAP CAL](./media/cal-s4h/s4h-pic-2a.png)

3. Digite hello Azure **ID da assinatura** que podem ser encontrados no hello portal do Azure.

   ![Contas da SAP CAL](./media/cal-s4h/s4h-pic3c.png)

4. tooauthorize Olá CAL SAP toodeploy em Olá assinatura do Azure que você definiu, clique em **autorizar**. saudação de página a seguir aparece na guia do navegador hello:

   ![Entrar nos serviços de nuvem do Internet Explorer](./media/cal-s4h/s4h-pic4c.png)

5. Se mais de um usuário estiver listado, escolha a conta da Microsoft hello que é vinculado toobe Olá coadministrator de saudação assinatura do Azure que você selecionou. saudação de página a seguir aparece na guia do navegador hello:

   ![Confirmação dos serviços de nuvem do Internet Explorer](./media/cal-s4h/s4h-pic5a.png)

6. Clique em **Aceitar**. Se a autorização Olá for bem-sucedida, Olá SAP CAL definição da conta será exibida novamente. Após um curto período de tempo, uma mensagem confirmará que o processo de autorização de saudação foi bem-sucedida.

7. Olá tooassign recém-criado CAL SAP tooyour de conta do usuário, insira seu **ID de usuário** no hello caixa de texto de saudação à direita e clique em **adicionar**.

   ![Associação de toouser de conta](./media/cal-s4h/s4h-pic8a.png)

8. clique de sua conta com usuário Olá que você use toosign em toohello CAL do SAP, tooassociate **revisão**. 
 
9. associação de saudação toocreate entre o usuário e conta de CAL SAP Olá recém-criado, clique em **criar**.

   ![Associação de conta do usuário tooSAP CAL](./media/cal-s4h/s4h-pic9b.png)

Você criou com êxito uma conta da SAP CAL que é capaz de:

- Use o modelo de implantação do Gerenciador de recursos de saudação.
- Implantar os sistemas SAP na sua assinatura do Azure.

Agora você pode iniciar toodeploy 4HANA/S em sua assinatura do usuário no Azure.

> [!NOTE]
Antes de continuar, determine se você tem cotas de núcleo do Azure para as VMs Série H do Azure. No momento de Olá Olá CAL do SAP usa toodeploy H-Series VMs do Azure algumas das soluções de saudação do SAP HANA. Sua assinatura do Azure talvez não tenha cotas de núcleo da Série H para a Série H. Nesse caso, talvez seja necessário toocontact suporte do Azure tooget uma cota de pelo menos 16 núcleos de série de H.

> [!NOTE]
Quando você implanta uma solução no Azure no hello CAL do SAP, talvez você descubra que você pode escolher apenas uma região do Azure. toodeploy em regiões do Azure diferentes Olá um sugeridas pelo Olá CAL do SAP, é necessário toopurchase uma assinatura de CAL do SAP. Também pode ser necessário tooopen uma mensagem com SAP toohave seu toodeliver de conta habilitada CAL em regiões do Azure diferentes Olá aqueles inicialmente sugeridos.

### <a name="deploy-a-solution"></a>Implantar uma solução

Permite implantar uma solução de saudação **soluções** página de saudação CAL do SAP. Olá CAL SAP tem dois toodeploy de sequências:

- Uma sequência básica que usa um toobe de sistema de saudação a toodefine do página implantado
- Uma sequência avançada que fornece certas opções sobre tamanhos de VM 

Demonstraremos Olá toodeployment de caminho básica aqui.

1. Em Olá **detalhes da conta** página, você precisa:

    a. Selecionar uma conta da SAP CAL. (Use uma conta que seja toodeploy associado com o modelo de implantação do Gerenciador de recursos de saudação).

    b. Inserir um **Nome** para a instância.

    c. Selecionar uma **Região** do Azure. Olá CAL do SAP sugere uma região. Se você precisar outra região do Azure e você não tiver uma assinatura de CAL do SAP, você precisa de assinatura de tooorder um CAL com o SAP.

    d. Insira um mestre **senha** para solução de saudação de oito ou nove caracteres. Olá senha é usada para administradores de saudação de diferentes componentes de saudação.

   ![Modo básico da SAP CAL: criar instância](./media/cal-s4h/s4h-pic10a.png)

2. Clique em **criar**e na caixa de mensagem de saudação que aparece, clique em **Okey**.

   ![Tamanhos de VM com suporte na SAP CAL](./media/cal-s4h/s4h-pic10b.png)

3. Em Olá **chave privada** caixa de diálogo, clique em **repositório** toostore Olá chave particular Olá CAL do SAP. Clique em toouse proteção por senha para a chave privada do hello, **baixar**. 

   ![Chave privada da SAP CAL](./media/cal-s4h/s4h-pic10c.png)

4. Saudação de leitura CAL SAP **aviso** da mensagem e, em seguida, clique em **Okey**.

   ![Aviso da SAP CAL](./media/cal-s4h/s4h-pic10d.png)

    Agora a implantação Olá ocorre. Depois de algum tempo, dependendo do tamanho de saudação e a complexidade da solução hello (Olá SAP CAL fornece uma estimativa), Olá status será exibido como ativa e pronta para uso.

5. máquinas de virtuais de saudação toofind coletadas com hello outros recursos associados em um grupo de recursos, consulte toohello portal do Azure: 

   ![Objetos de CAL SAP implantados no novo portal de saudação](./media/cal-s4h/sapcaldeplyment_portalview.png)

6. No portal do SAP CAL hello, status de saudação aparece como **Active**. solução de toohello tooconnect, clique em **conectar**. Opções diferentes tooconnect toohello diferentes componentes são implantados dentro dessa solução.

   ![Instâncias da SAP CAL](./media/cal-s4h/active_solution.png)

7. Antes de usar um dos sistemas de toohello implantado em tooconnect Olá opções, clique em **guia de Introdução**. 

   ![Conecte-se a instância de toohello](./media/cal-s4h/connect_to_solution.png)

    nomes de documentação Olá Olá usuários para cada um dos métodos de conectividade de saudação. as senhas de saudação para os usuários são definidas toohello senha mestra que você definiu no início do processo de implantação de saudação hello. Na documentação do hello, outros usuários mais funcionais são listados com suas senhas, o que você pode usar toosign no toohello implantado sistema. 

    Por exemplo, se você usar o hello SAP GUI que foi pré-instalado no computador de área de trabalho remota do Windows hello, Olá sistema S/4 pode parecer assim:

   ![SM50 em Olá pré-instalado SAP GUI](./media/cal-s4h/gui_sm50.png)

    Ou, se você usar Olá DBACockpit, instância Olá poderia se parecer com:

   ![SM50 em Olá DBACockpit SAP GUI](./media/cal-s4h/dbacockpit.png)

Em algumas horas, um dispositivo de SAP S/4 íntegro é implantado no Azure.

Se você comprou uma assinatura de CAL do SAP, SAP totalmente dá suporte a implantações por meio de saudação CAL do SAP no Azure. fila de suporte de saudação é BC-VCM-CAL.







