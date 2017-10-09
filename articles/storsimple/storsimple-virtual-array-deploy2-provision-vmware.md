---
title: aaaProvision Array Virtual do StorSimple no VMware | Microsoft Docs
description: "Esse segundo tutorial sobre a série de implantação da StorSimple Virtual Array envolve o provisionamento de um dispositivo virtual no VMware."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 0425b2a9-d36f-433d-8131-ee0cacef95f8
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/15/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0912c1c315a04ea46b6373a8fcd5554ecae14e61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---provision-in-vmware"></a>Implantar a StorSimple Virtual Array - Provisionar no VMware
![](./media/storsimple-virtual-array-deploy2-provision-vmware/vmware4.png)

## <a name="overview"></a>Visão geral
Este tutorial descreve como tooprovision e conecte-se tooa matriz Virtual do StorSimple em um sistema de host executando o VMware ESXi 5.5 e acima. Este artigo se aplica a implantação de toohello de matrizes de Virtual do StorSimple no portal do Azure e hello nuvem do Microsoft Azure Government.

Você precisa tooprovision de privilégios de administrador e conecte o dispositivo virtual tooa. a instalação inicial e provisionamento Olá pode levar toocomplete de cerca de 10 minutos.

## <a name="provisioning-prerequisites"></a>Pré-requisitos de provisionamento
Olá pré-requisitos tooprovision um dispositivo virtual em um sistema de host executando o VMware ESXi 5.5 e acima, é o seguinte.

### <a name="for-hello-storsimple-device-manager-service"></a>Para Olá serviço do Gerenciador de dispositivos de StorSimple
Antes de começar, verifique se:

* Você concluiu todas as etapas Olá [portal de saudação preparar para matriz Virtual StorSimple](storsimple-virtual-array-deploy1-portal-prep.md).
* Você baixou a imagem de dispositivo virtual Olá para VMware da saudação portal do Azure. Para obter mais informações, consulte **etapa 3: imagem de dispositivo virtual Olá Download** de [portal de Olá preparação para a guia de matriz Virtual StorSimple](storsimple-virtual-array-deploy1-portal-prep.md).

### <a name="for-hello-storsimple-virtual-device"></a>Para o dispositivo virtual StorSimple Olá
Antes de implantar um dispositivo virtual, verifique se:

* Você tem acesso tooa host sistema executando o Hyper-V (2008 R2 ou posterior) que pode ser usado tooa provisionar um dispositivo.
* sistema de host de saudação é capaz de toodedicate Olá tooprovision recursos a seguir em seu dispositivo virtual:

  * Um mínimo de quatro núcleos.
  * Pelo menos 8 GB de RAM. Se você planejar a matriz de virtual tooconfigure hello como servidor de arquivos, 8 GB dá suporte a menos de 2 milhões de arquivos. Você precisa de 2-4 milhões de arquivos de 16 GB RAM toosupport.
  * Uma interface de rede.
  * Um disco virtual de 500 GB para dados do sistema.

### <a name="for-hello-network-in-datacenter"></a>Para a rede Olá no datacenter
Antes de começar, verifique se:

* Você revisou Olá de rede requisitos toodeploy um dispositivo virtual StorSimple e rede de datacenter saudação configurado de acordo com os requisitos de saudação. 

## <a name="step-by-step-provisioning"></a>Provisionamento passo a passo
tooprovision e conecte-se o dispositivo virtual tooa, é necessário tooperform Olá etapas a seguir:

1. Verifique se o sistema de host Olá tem suficiente toomeet Olá mínima do dispositivo virtual os requisitos de recursos.
2. Provisionar um dispositivo virtual no seu hipervisor.
3. Inicie o dispositivo virtual hello e obter o endereço IP de saudação.

## <a name="step-1-ensure-host-system-meets-minimum-virtual-device-requirements"></a>Etapa 1: verificar se o sistema de host cumpre os requisitos mínimos de dispositivo virtual
toocreate um dispositivo virtual, você precisará:

* Sistema de host tooa acesso executando o VMware ESXi Server 5.5 e acima.
* VMware vSphere client, no host de ESXi do sistema toomanage hello.

  * Um mínimo de quatro núcleos.
  * Pelo menos 8 GB de RAM. Se você planejar a matriz de virtual tooconfigure hello como servidor de arquivos, 8 GB dá suporte a menos de 2 milhões de arquivos. Você precisa de 2-4 milhões de arquivos de 16 GB RAM toosupport.
  * Uma interface de rede conectado toohello rede capaz de tooInternet roteamento de tráfego. largura de banda de Internet mínima Olá deve ser 5 tooallow Mbps para trabalhar melhor de dispositivo de saudação.
  * Um disco virtual de 500 GB para dados.

## <a name="step-2-provision-a-virtual-device-in-hypervisor"></a>Etapa 2: provisionar um dispositivo virtual no hipervisor
Execute Olá seguindo as etapas tooprovision um dispositivo virtual em seu hipervisor.

1. Copie imagem de dispositivo virtual Olá em seu sistema. Você baixou esta imagem virtual por meio de saudação portal do Azure.

   1. Certifique-se de que você baixou o arquivo de imagem hello mais recente. Se você baixou anteriormente imagem hello, baixá-lo novamente tooensure imagem mais recente da saudação. imagem mais recente Olá tem dois arquivos (em vez de um).
   2. Anote Olá local onde você copiou a imagem hello como você está usando esta imagem posteriormente no procedimento Olá.

2. Faça logon no toohello server ESXi usando Olá vSphere cliente. É necessário toocreate privilégios de administrador toohave uma máquina virtual.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image1.png)
3. No cliente do vSphere hello, na seção de inventário de saudação no painel esquerdo do hello, selecione Olá ESX.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image2.png)
4. Carregar o servidor de ESXi Olá VMDK toohello. Navegue toohello **configuração** guia no painel direito da saudação. Em **Hardware**, selecione **Armazenamento**.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image3.png)
5. Em Olá direita painel, em **armazenamentos de dados**, selecione Olá onde você deseja Olá tooupload VMDK do repositório de dados. saudação de repositório de dados deve ter suficiente espaço livre para Olá SO e discos de dados.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image4.png)
6. Clique com o botão direito do mouse e selecione **Procurar no Repositório de Dados**.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image5.png)
7. Uma janela **Navegador de Repositório de Dados** é exibida.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image6.png)
8. Na barra de ferramentas de saudação, clique em ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image7.png) ícone toocreate uma nova pasta. Especifique o nome da pasta hello e anote-lo. Você usará posteriormente este nome de pasta ao criar uma máquina virtual (melhor prática recomendada). Clique em **OK**.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image8.png)
9. Olá nova pasta é exibida no painel esquerdo de saudação do hello **navegador de repositório de dados**.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image9.png)
10. Clique ícone de carregamento de saudação ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image10.png) e selecione **carregar arquivo**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image11.png)
11. Procurar e ponto toohello arquivos VMDK que você baixou. Existem dois itens. Selecione tooupload um arquivo.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image12m.png)
12. Clique em **Abrir**. carregamento Olá Olá VMDK arquivo toohello especificado começa do repositório de dados. Ele pode levar vários minutos para tooupload do arquivo hello.
13. Após Olá carregamento for concluído, você verá arquivo hello no armazenamento de dados de saudação na pasta Olá que você criou.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image14.png)

    Carregar agora Olá segundo VMDK arquivo toohello mesmo repositório de dados.
14. Janela de cliente do vSphere toohello retorno. Com o servidor ESXi selecionado, clique com botão direito do mouse e selecione **Nova Máquina Virtual**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image15.png)
15. Uma janela **Criar nova máquina Virtual** será exibida. Em Olá **configuração** página, selecione Olá **personalizado** opção. Clique em **Avançar**.
    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image16.png)
16. Em Olá **nome e local** , especifique o nome de saudação de sua máquina virtual. Esse nome deve corresponder o nome de pasta de saudação (prática recomendada) especificado anteriormente na etapa 8.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image17.png)
17. Em Olá **armazenamento** , selecione um repositório de dados que você deseja toouse tooprovision sua VM.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image18.png)
18. Em Olá **versão da máquina Virtual** página, selecione **versão da máquina Virtual: 8**. Versões 8 too11 todos têm suporte.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image19.png)
19. Em Olá **sistema operacional convidado** página, selecione Olá **sistema operacional convidado** como **Windows**. Para **versão**, na lista suspensa hello, selecione **Microsoft Windows Server 2012 (64 bits)**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image20.png)
20. Em Olá **CPUs** página, ajuste Olá **número de soquetes virtuais** e **número de núcleos por soquete virtual** para que Olá **Número Total de núcleos**é 4 (ou mais). Clique em **Avançar**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image21.png)
21. Em Olá **memória** especifique 8 GB (ou mais) de RAM. Clique em **Avançar**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image22.png)
22. Em Olá **rede** , especifique o número de Olá Olá de interfaces de rede. requisito mínimo de saudação é uma interface de rede.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image23.png)
23. Em Olá **controlador SCSI** página, aceite o padrão de saudação **controlador LSI lógica SAS**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image24.png)
24. Em Olá **selecione um disco** escolha **usar um disco virtual existente**. Clique em **Avançar**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image25.png)
25. Em Olá **Selecionar disco existente** página em **caminho do arquivo de disco**, clique em **procurar**. Isso abre uma caixa de diálogo **Procurar em Repositórios de Dados** . Navegue toohello local em que você carregou Olá VMDK. Você verá somente um arquivo no armazenamento de dados hello como dois arquivos de saudação que você carregou inicialmente foram mesclados. Selecione o arquivo hello e clique em **Okey**. Clique em **Avançar**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image26.png)
26. Em Olá **opções avançadas de** , aceite o padrão de saudação e em **próximo**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image27.png)
27. Em Olá **tooComplete pronto** , examine todas as configurações de saudação associadas à máquina virtual da nova hello. Verificar **editar configurações de máquina virtual de saudação antes da conclusão**. Clique em **Continuar**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image28.png)
28. Em Olá **propriedades de máquinas virtuais** página Olá **Hardware** guia, localize o hardware do dispositivo hello. Selecione **Novo Disco Rígido**. Clique em **Adicionar**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image29.png)
29. Você verá uma janela **Adicionar Hardware**. Em Olá **tipo de dispositivo** página em **Escolher tipo de saudação do dispositivo que você deseja tooadd**, selecione **disco rígido**e clique em **próximo**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image30.png)
30. Em Olá **selecione um disco** escolha **criar um novo disco virtual**. Clique em **Avançar**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image31.png)
31. Em Olá **criar um disco** página, altere Olá **tamanho do disco** too500 GB (ou mais). Enquanto 500 GB é o requisito mínimo de saudação, você sempre pode provisionar um disco maior. Observe que você não pode expandir ou reduzir Olá disco provisionado de uma vez. Para obter mais informações sobre tamanho Olá tooprovision de disco, examine a seção dimensionamento Olá Olá [documento de práticas recomendadas](storsimple-ova-best-practices.md). Em **Provisionamento de Disco**, selecione **Provisionamento Dinâmico**. Clique em **Avançar**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image32.png)
32. Em Olá **opções avançadas** página, aceite o padrão de saudação.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image33.png)
33. Em Olá **tooComplete pronto** , examine as opções de disco de saudação. Clique em **Concluir**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image34.png)
34. Retorne toohello página de propriedades da máquina Virtual. Um novo disco rígido é adicionado a máquina virtual de tooyour. Clique em **Concluir**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image35.png)
35. Com sua máquina virtual selecionada no painel direito da saudação, navegar toohello **resumo** guia. Examine as configurações de saudação para sua máquina virtual.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image36.png)

Sua máquina virtual está agora provisionada. Olá próxima etapa é toopower nesta máquina e obter o endereço IP hello.

## <a name="step-3-start-hello-virtual-device-and-get-hello-ip"></a>Etapa 3: Iniciar o dispositivo virtual hello e obter IP Olá
Executar Olá toostart as etapas a seguir em seu dispositivo virtual e conecte-se tooit.

#### <a name="toostart-hello-virtual-device"></a>dispositivo virtual do toostart Olá
1. Inicie o dispositivo virtual hello. No vSphere Olá Configuration Manager, no painel esquerdo do hello, selecione seu dispositivo e clique toobring menu de contexto de saudação. Selecione **Ligar/Desligar** e, em seguida, selecione **Ligar**. Isso deve ligar sua máquina virtual. Você pode exibir o status de saudação na parte inferior da saudação **tarefas recentes** painel do cliente do vSphere hello.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image37.png)
2. tarefas de configuração de saudação levará toocomplete de alguns minutos. Depois que o dispositivo Olá estiver em execução, navegar toohello **Console** guia. Envie Ctrl + Alt + Delete toolog no dispositivo toohello. Como alternativa, você pode aponte Olá cursor na janela do console hello e pressione Ctrl + Alt + Insert. saudação padrão usuário é *StorSimpleAdmin* e a senha padrão Olá é *Password1*.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image38.png)
3. Por motivos de segurança, senha de administrador de dispositivo de saudação expira no primeiro logon de saudação. Você é solicitadas toochange Olá por senha.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image39.png)
4. Insira uma senha que contenha pelo menos oito caracteres. senha de saudação deve conter 3 dos 4 esses requisitos: caracteres maiusculo, minúsculo, numérico e especial. Reinsira Olá senha tooconfirm-lo. Você será notificado que Olá senha foi alterada.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image40.png)
5. Depois de senha de saudação é alterada com êxito, dispositivo virtual Olá pode reinicializar. Aguarde Olá toocomplete de reinicialização. console do Windows PowerShell de saudação do dispositivo Olá pode ser exibido juntamente com uma barra de progresso.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image41.png)
6. As etapas 6 a 8 se aplicam somente na inicialização de um ambiente não DHCP. Se você estiver em um ambiente de DHCP, em seguida, ignorar essas etapas e vá toostep 9. Se o seu dispositivo no ambiente de não-DHCP, você verá Olá tela a seguir.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image42m.png)

   Em seguida, configure a rede de saudação.
7. Saudação de uso `Get-HcsIpAddress` comando interfaces de rede de saudação toolist habilitados em seu dispositivo virtual. Se o dispositivo tem uma interface de rede habilitada, a saudação padrão nome atribuído toothis interface é `Ethernet`.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image43m.png)
8. Saudação de uso `Set-HcsIpAddress` rede de saudação do cmdlet tooconfigure. Um exemplo é mostrado abaixo:

    `Set-HcsIpAddress –Name Ethernet –IpAddress 10.161.22.90 –Netmask 255.255.255.0 –Gateway 10.161.22.1`

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image44.png)
9. Após a instalação de saudação inicial for concluída e dispositivo Olá tiver iniciado, você verá texto da faixa de dispositivo hello. Anote um endereço IP hello e Olá URL exibida no dispositivo de Olá Olá faixa texto toomanage. Você usará esse IP endereço tooconnect toohello interface da web do seu dispositivo virtual e a instalação local do hello completa e o registro.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image45.png)
10. (Opcional) Execute esta etapa apenas se você estiver implantando seu dispositivo no hello nuvem do governo. Agora você habilitará o modo de Estados Unidos Federal Information Processing Standard (FIPS) hello em seu dispositivo. padrão Olá FIPS 140 define algoritmo de criptografia aprovado para uso pelos sistemas de computador do Governo Federal dos EUA para proteção de saudação de dados confidenciais.

    1. modo FIPS em Olá tooenable, execute Olá cmdlet a seguir:

        `Enable-HcsFIPSMode`
    2. Reinicialize o dispositivo depois de habilitar o modo FIPS Olá para que as validações de criptografia Olá entrem em vigor.

       > [!NOTE]
       > Você pode habilitar ou desabilitar o modo FIPS em seu dispositivo. Não há suporte para o dispositivo de saudação alternadas entre o modo FIPS e FIPS não.
       >
       >

Se seu dispositivo não atende aos requisitos mínimos de configuração de saudação, você verá um erro no texto da faixa de saudação (mostrado abaixo). Você precisará toomodify a configuração do dispositivo Olá para que ela tem recursos adequados toomeet Olá mínimo requisitos. Você pode, em seguida, reiniciar e conectar-se o dispositivo toohello. Consulte os requisitos mínimos de configuração toohello [etapa 1: Certifique-se de que o sistema de host de saudação atende aos requisitos mínimos de dispositivo virtual](#step-1-ensure-host-system-meets-minimum-virtual-device-requirements).

![](./media/storsimple-virtual-array-deploy2-provision-vmware/image46.png)

Se você enfrentar qualquer outro erro durante a configuração inicial hello usando a interface da web local hello, consulte toohello fluxos de trabalho a seguir:

* Executar testes de diagnóstico muito[solucionar problemas de instalação de interface do usuário da web](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors).
* [Gere um pacote de log e exiba os arquivos de log](storsimple-ova-web-ui-admin.md#generate-a-log-package).

## <a name="next-steps"></a>Próximas etapas
* [Configurar sua StorSimple Virtual Array como um servidor de arquivos](storsimple-virtual-array-deploy3-fs-setup.md)
* [Configurar sua StorSimple Virtual Array como um servidor iSCSI](storsimple-virtual-array-deploy3-iscsi-setup.md)
