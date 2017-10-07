---
title: aaaProvision StorSimple a matriz Virtual no Hyper-V | Microsoft Docs
description: "Esse segundo tutorial sobre a implantação da Matriz Virtual StorSimple envolve o provisionamento de uma matriz virtual no Hyper-V."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 4354963c-e09d-41ac-9c8b-f21abeae9913
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/15/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f47d642f740827ae1440b819e07067c6a183527f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---provision-in-hyper-v"></a>Implantar o StorSimple Virtual Array - Provisionar no Hyper-V
![](./media/storsimple-virtual-array-deploy2-provision-hyperv/hyperv4.png)

## <a name="overview"></a>Visão geral
Este tutorial descreve como tooprovision uma StorSimple Virtual Array em um sistema de host executando o Hyper-V no Windows Server 2012 R2, Windows Server 2012 ou Windows Server 2008 R2. Este artigo se aplica a implantação de toohello de matrizes de Virtual do StorSimple no portal do Azure e a nuvem do Microsoft Azure Government.

Você precisa tooprovision de privilégios de administrador e configurar uma matriz virtual. a instalação inicial e provisionamento Olá pode levar toocomplete de cerca de 10 minutos.

## <a name="provisioning-prerequisites"></a>Pré-requisitos de provisionamento
Aqui você encontrará Olá pré-requisitos tooprovision uma matriz virtual em um sistema de host executando o Hyper-V no Windows Server 2012 R2, Windows Server 2012 ou Windows Server 2008 R2.

### <a name="for-hello-storsimple-device-manager-service"></a>Para Olá serviço do Gerenciador de dispositivos de StorSimple
Antes de começar, verifique se:

* Você concluiu todas as etapas Olá [portal de saudação preparar para matriz Virtual StorSimple](storsimple-virtual-array-deploy1-portal-prep.md).
* Você baixou imagem de matriz virtual Olá para o Hyper-V de saudação portal do Azure. Para obter mais informações, consulte **etapa 3: imagem de matriz virtual Olá Download** de [portal de Olá preparação para a guia de matriz Virtual StorSimple](storsimple-virtual-array-deploy1-portal-prep.md).

  > [!IMPORTANT]
  > software de saudação em execução no hello matriz Virtual StorSimple só pode ser usado com Olá serviço do Gerenciador de dispositivos do StorSimple.
  >
  >

### <a name="for-hello-storsimple-virtual-array"></a>Para Olá matriz Virtual StorSimple
Antes de implantar um dispositivo virtual, verifique se:

* Você tem acesso tooa host sistema que executa o Hyper-V no Windows Server 2008 R2 ou posterior que pode ser usado tooa provisionar um dispositivo.
* sistema de host de saudação é capaz de toodedicate Olá seguintes recursos tooprovision sua matriz virtual:

  * Um mínimo de quatro núcleos.
  * Pelo menos 8 GB de RAM. Se você planejar a matriz de virtual tooconfigure hello como servidor de arquivos, 8 GB dá suporte a menos de 2 milhões de arquivos. Você precisa de 2-4 milhões de arquivos de 16 GB RAM toosupport.
  * Uma interface de rede.
  * Um disco virtual de 500 GB para dados.

### <a name="for-hello-network-in-hello-datacenter"></a>Para a rede Olá Olá Datacenter
Antes de começar, examine Olá requisitos toodeploy uma matriz Virtual StorSimple do sistema de rede e configurar a rede de datacenter Olá adequadamente. Para obter mais informações, consulte [Requisitos de rede do StorSimple Virtual Array](storsimple-ova-system-requirements.md#networking-requirements).

## <a name="step-by-step-provisioning"></a>Provisionamento passo a passo
tooprovision e conectar-se a matriz virtual tooa, é necessário tooperform Olá etapas a seguir:

1. Verifique se o sistema de host Olá tem suficiente toomeet Olá mínimo matriz virtual os requisitos de recursos.
2. Provisionar uma matriz virtual no seu hipervisor.
3. Iniciar matriz virtual hello e obter o endereço IP hello.

Cada uma dessas etapas é explicada em Olá seções a seguir.

## <a name="step-1-ensure-that-hello-host-system-meets-minimum-virtual-array-requirements"></a>Etapa 1: Certifique-se de que o sistema de host de Olá atende aos requisitos mínimos de matriz virtual
toocreate uma matriz virtual, você precisa:

* função Hello Hyper-V instalada no Windows Server 2012 R2, Windows Server 2012 ou Windows Server 2008 R2 SP1.
* Microsoft Hyper-V Manager em um cliente do Microsoft Windows conectado toohello host.

Certifique-se de que Olá hardware (sistema de host) em que você está criando matriz virtual Olá subjacente é capaz de toodedicate Olá array virtual de tooyour de recursos a seguir:

* Um mínimo de quatro núcleos.
* Pelo menos 8 GB de RAM. Se você planejar a matriz de virtual tooconfigure hello como servidor de arquivos, 8 GB dá suporte a menos de 2 milhões de arquivos. Você precisa de 2-4 milhões de arquivos de 16 GB RAM toosupport.
* Uma interface de rede.
* Um disco virtual de 500 GB para dados do sistema.

## <a name="step-2-provision-a-virtual-array-in-hypervisor"></a>Etapa 2: provisionar uma matriz virtual no hipervisor
Execute Olá seguindo as etapas tooprovision um dispositivo no seu hipervisor.

#### <a name="tooprovision-a-virtual-array"></a>tooprovision uma matriz virtual
1. No host do Windows Server, copie unidade local do tooa Olá array virtual imagem. Você baixou essa imagem (VHD ou VHDX) por meio de saudação portal do Azure. Anote Olá local onde você copiou a imagem hello como você está usando esta imagem posteriormente no procedimento Olá.
2. Abra o **Gerenciador do Servidor**. No canto direito superior de saudação, clique em **ferramentas** e selecione **Gerenciador Hyper-V**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image1.png)  

   Se você estiver executando o Windows Server 2008 R2, abra Olá Gerenciador Hyper-V. No Gerenciador do Servidor, clique em **Funções > Hyper-V > Gerenciador do Hyper-V**.
3. Em **Gerenciador Hyper-V**, no painel de escopo hello, clique o menu de contexto do sistema nó tooopen hello e, em seguida, clique em **novo** > **Máquina Virtual**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image2.png)
4. Em Olá **antes de começar a** página de saudação Assistente de nova máquina Virtual, clique em **próximo**.
5. Em Olá **especificar nome e local** , forneça um **nome** para sua matriz virtual. Clique em **Avançar**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image4.png)
6. Em Olá **especificar geração** página, escolha o tipo de imagem de dispositivo de saudação e, em seguida, clique em **próximo**. Esta página não aparecerá se você estiver usando o Windows Server 2008 R2.

   * Escolha **Geração 2** se você baixou uma imagem .vhdx para o Windows Server 2012 ou posterior.
   * Escolha **Geração 1** se você baixou uma imagem .vhdx para o Windows Server 2008 R2 ou posterior.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image5.png)
7. Em Olá **atribuir memória** página, especifique um **memória de inicialização** pelo menos **8192 MB**, não habilite a memória dinâmica e, em seguida, clique em **próximo**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image6.png)  
8. Em Olá **configurar rede** página, especifique Olá comutador virtual toohello conectado à Internet e, em seguida, clique em **próximo**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image7.png)
9. Em Olá **conectar disco rígido virtual** escolha **usar um disco rígido virtual existente**, especifique o local de saudação da imagem de matriz virtual hello (. vhdx ou. vhd) e, em seguida, clique em **próximo**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image8m.png)
10. Saudação de revisão **resumo** e, em seguida, clique em **concluir** toocreate Olá VM.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image9.png)
11. requisitos mínimos do toomeet hello, você precisa de 4 núcleos. tooadd 4 de processadores virtuais, selecione o sistema de host no hello **Gerenciador Hyper-V** janela. No painel direito Olá na lista de saudação do **máquinas virtuais**, localize a máquina virtual de saudação você acabou de criar. Selecione e clique o nome da máquina hello e selecione **configurações**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image10.png)
12. Em Olá **configurações** página, no painel esquerdo do hello, clique em **processador**. No painel direito de hello, defina **número de processadores virtuais** too4 (ou mais). Clique em **Aplicar**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image11.png)
13. requisitos mínimos do toomeet hello, você também precisa tooadd um disco de dados virtual de 500 GB. Em Olá **configurações** página:

    1. No painel esquerdo do hello, selecione **controlador SCSI**.
    2. No painel direito da saudação, selecione **rígido,** e clique em **adicionar**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image12.png)
14. Em Olá **disco rígido** página, selecione Olá **disco rígido Virtual** opção e clique em **novo**. Olá **novo Assistente de disco rígido Virtual** inicia.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image13.png)
15. Em Olá **antes de começar a** página de saudação novo Assistente de disco rígido Virtual, clique em **próximo**.
16. Em Olá **página Escolher formato de disco**, aceite a opção padrão Olá **VHDX** formato. Clique em **Avançar**. Esta tela não é apresentada se o Windows Server 2008 R2 está em execução.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image15.png)
17. Em Olá **página Escolher tipo de disco**, defina o tipo de disco rígido virtual como **expansão dinâmica** (recomendado). **Tamanho fixo** disco funcionaria, mas talvez seja necessário toowait muito tempo. É recomendável que você não use Olá **diferenciação** opção. Clique em **Avançar**. No Windows Server 2012 R2 e Windows Server 2012, **expansão dinâmica** é a opção de padrão de saudação enquanto no Windows Server 2008 R2, o padrão de saudação é **tamanho fixo**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image16.png)
18. Em Olá **especificar nome e local** , forneça um **nome** , bem como **local** (você pode procurar tooone) para o disco de dados hello. Clique em **Avançar**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image17.png)
19. Em Olá **configurar disco** página opção select Olá **criar um novo disco virtual em branco** e especifique o tamanho de saudação como **500 GB** (ou mais). Enquanto 500 GB é o requisito mínimo de saudação, você sempre pode provisionar um disco maior. Observe que você não pode expandir ou reduzir Olá disco provisionado de uma vez. Para obter mais informações sobre tamanho Olá tooprovision de disco, examine a seção dimensionamento Olá Olá [documento de práticas recomendadas](storsimple-ova-best-practices.md). Clique em **Avançar**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image18.png)
20. Em Olá **resumo** página, examine os detalhes de saudação do disco virtual de dados e se estiver satisfeito, clique em **concluir** toocreate disco de saudação. Olá assistente for fechado e um disco rígido virtual é adicionado tooyour máquina.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image19.png)
21. Retornar toohello **configurações** página. Clique em **Okey** tooclose Olá **configurações** página e retornar a janela do Gerenciador de tooHyper-V.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image20.png)

## <a name="step-3-start-hello-virtual-array-and-get-hello-ip"></a>Etapa 3: Iniciar matriz virtual hello e obter IP Olá
Executar Olá seguindo as etapas toostart sua matriz virtual e conecte-se tooit.

#### <a name="toostart-hello-virtual-array"></a>matriz de virtual de saudação toostart
1. Inicie matriz virtual hello.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image21.png)
2. Depois que o dispositivo Olá estiver em execução, selecione dispositivo hello, clique com botão direito e selecione **conectar**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image22.png)
3. Você pode ter toowait 5 a 10 minutos para Olá dispositivo toobe pronto. Será exibida uma mensagem de status em andamento de Olá Olá console tooindicate. Depois que o dispositivo Olá estiver pronto, vá muito**ação**. Pressione `Ctrl + Alt + Delete` toolog na matriz virtual toohello. saudação padrão usuário é *StorSimpleAdmin* e a senha padrão Olá é *Password1*.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image23.png)
4. Por motivos de segurança, senha de administrador de dispositivo de saudação expira no primeiro logon de saudação. Você é solicitadas toochange Olá por senha.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image24.png)

   Insira uma senha que contenha pelo menos oito caracteres. Olá senha deve ter pelo menos 3 das Olá 4 requisitos a seguir: caracteres maiusculo, minúsculo, numérico e especial. Reinsira Olá senha tooconfirm-lo. Você será notificado que Olá senha foi alterada.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image25.png)
5. Depois de senha de saudação é alterada com êxito, array virtual Olá pode reiniciar. Aguarde Olá dispositivo toostart.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image26.png)

    console do Windows PowerShell de saudação do dispositivo Olá é exibido junto com uma barra de progresso.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image27.png)
6. As etapas 6 a 8 se aplicam somente na inicialização de um ambiente não DHCP. Se você estiver em um ambiente de DHCP, em seguida, ignorar essas etapas e vá toostep 9. Se o seu dispositivo no ambiente de não-DHCP, você verá Olá tela a seguir.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image28m.png)

    Em seguida, configure a rede de saudação.
7. Saudação de uso `Get-HcsIpAddress` comando interfaces de rede de saudação toolist habilitados em sua matriz virtual. Se o dispositivo tem uma interface de rede habilitada, a saudação padrão nome atribuído toothis interface é `Ethernet`.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image29m.png)
8. Saudação de uso `Set-HcsIpAddress` rede de saudação do cmdlet tooconfigure. Consulte Olá exemplo a seguir:

    `Set-HcsIpAddress –Name Ethernet –IpAddress 10.161.22.90 –Netmask 255.255.255.0 –Gateway 10.161.22.1`

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image30.png)
9. Após a instalação de saudação inicial for concluída e dispositivo Olá tiver iniciado, você verá texto da faixa de dispositivo hello. Anote um endereço IP hello e Olá URL exibida no dispositivo de Olá Olá faixa texto toomanage. Use esse IP endereço tooconnect toohello interface da web da sua matriz virtual e a instalação local do Olá completa e o registro.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image31m.png)
10. (Opcional) Execute esta etapa apenas se você estiver implantando seu dispositivo no hello nuvem do governo. Agora você habilitará o modo de Estados Unidos Federal Information Processing Standard (FIPS) hello em seu dispositivo. padrão Olá FIPS 140 define algoritmo de criptografia aprovado para uso pelos sistemas de computador do Governo Federal dos EUA para proteção de saudação de dados confidenciais.

    1. modo FIPS em Olá tooenable, execute Olá cmdlet a seguir:

        `Enable-HcsFIPSMode`
    2. Reinicialize o dispositivo depois de habilitar o modo FIPS Olá para que as validações de criptografia Olá entrem em vigor.

       > [!NOTE]
       > Você pode habilitar ou desabilitar o modo FIPS em seu dispositivo. Não há suporte para o dispositivo de saudação alternadas entre o modo FIPS e FIPS não.
       >
       >

Se seu dispositivo não atende aos requisitos mínimos de configuração de saudação, você verá Olá seguinte erro no texto da faixa de saudação (mostrado abaixo). Modificar configuração do dispositivo Olá para que hello máquina tem recursos adequados toomeet Olá requisitos mínimos. Você pode, em seguida, reiniciar e conectar-se o dispositivo toohello. Consulte os requisitos mínimos de configuração toohello [etapa 1: Certifique-se de que o sistema de host de Olá atende aos requisitos mínimos de matriz virtual](#step-1-ensure-that-the-host-system-meets-minimum-virtual-device-requirements).

![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image32.png)

Se você enfrentar qualquer outro erro durante a configuração inicial hello usando a interface da web local hello, consulte toohello fluxos de trabalho a seguir:

* Executar testes de diagnóstico muito[solucionar problemas de instalação de interface do usuário da web](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors).
* [Gere um pacote de log e exiba os arquivos de log](storsimple-ova-web-ui-admin.md#generate-a-log-package).

## <a name="next-steps"></a>Próximas etapas
* [Configurar sua StorSimple Virtual Array como um servidor de arquivos](storsimple-virtual-array-deploy3-fs-setup.md)
* [Configurar sua StorSimple Virtual Array como um servidor iSCSI](storsimple-virtual-array-deploy3-iscsi-setup.md)
