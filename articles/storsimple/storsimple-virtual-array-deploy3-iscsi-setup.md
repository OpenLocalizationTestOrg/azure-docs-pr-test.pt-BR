---
title: "instalação do server aaaMicrosoft Azure StorSimple Virtual Array iSCSI | Microsoft Docs"
description: "Descreve como tooperform a configuração inicial, registrar o servidor do StorSimple iSCSI e concluir a instalação do dispositivo."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 4db116d1-978b-48e8-b572-a719a8425dbc
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.openlocfilehash: b4ff6391cb2af69d4e83dcdac5e027f8498005b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array--set-up-as-an-iscsi-server-via-azure-portal"></a>Implantar o StorSimple Virtual Array — configurar como um servidor iSCSI por meio do portal do Azure

![fluxo do processo de instalação iscsi](./media/storsimple-virtual-array-deploy3-iscsi-setup/iscsi4.png)

## <a name="overview"></a>Visão geral

Este tutorial de implantação se aplica a toohello Microsoft Azure StorSimple Virtual Array. Este tutorial descreve como instalação inicial do tooperform hello, registrar o servidor do iSCSI StorSimple, configuração de dispositivo concluída Olá e, em seguida, criar, montar, inicializar e formatar volumes no StorSimple Virtual Array configurado como um servidor iSCSI. 

procedimentos de saudação descritos aqui levar aproximadamente 30 minutos too1 horas toocomplete. informações de Olá publicadas neste artigo aplicam-se somente a matrizes Virtual tooStorSimple.

## <a name="setup-prerequisites"></a>Pré-requisitos de configuração

Antes de configurar e de instalar a Matriz Virtual StorSimple, verifique se:

* Ter provisionado uma matriz virtual e conectado tooit conforme descrito em [implantar StorSimple Virtual Array - provisionar uma matriz virtual no Hyper-V](storsimple-ova-deploy2-provision-hyperv.md) ou [implantar StorSimple Virtual Array - provisionar uma matriz virtual no VMware ](storsimple-virtual-array-deploy2-provision-vmware.md).
* Você tem a chave de registro do serviço de saudação do hello serviço Gerenciador de dispositivos do StorSimple que você criou toomanage suas matrizes de Virtual do StorSimple. Para obter mais informações, consulte **etapa 2: chave de registro de serviço Get hello** na [implantar StorSimple Virtual Array - preparar portal Olá](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key).
* Quando se trata de saudação outra matriz virtual que você está registrando com um serviço existente do Gerenciador de dispositivos de StorSimple, você deve ter o chave de criptografia de dados de serviço de saudação. Essa chave foi gerada quando o primeiro dispositivo de saudação foi registrado com êxito com esse serviço. Se você perdeu essa chave, consulte **chave de criptografia de dados de serviço do Get hello** na [Use Olá tooadminister de interface de usuário da Web sua matriz Virtual StorSimple](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key).

## <a name="step-by-step-setup"></a>Configuração passo a passo

Use Olá acompanhamento tooset instruções passo a passo e configurar sua matriz Virtual do StorSimple:

* [Etapa 1: Concluir instalação de interface do usuário da web local hello e registrar seu dispositivo](#step-1-complete-the-local-web-ui-setup-and-register-your-device)
* [Etapa 2: Olá completa necessária configuração do dispositivo](#step-2-complete-the-required-device-setup)
* [Etapa 3: adicionar um volume](#step-3-add-a-volume)
* [Etapa 4: montar, inicializar e formatar um volume](#step-4-mount-initialize-and-format-a-volume)

## <a name="step-1-complete-hello-local-web-ui-setup-and-register-your-device"></a>Etapa 1: Concluir instalação de interface do usuário da web local hello e registrar seu dispositivo

#### <a name="toocomplete-hello-setup-and-register-hello-device"></a>toocomplete Olá instalação e registrar dispositivo Olá

1. Abra uma janela do navegador. tooconnect toohello web tipo de interface do usuário:
   
    `https://<ip-address of network interface>`
   
    Use a URL de conexão de Olá anotado na etapa anterior hello. Você verá um erro informando que há um problema com o certificado de segurança do site hello. Clique em **continuar toothis web página**.
   
    ![erro de certificado de segurança](./media/storsimple-virtual-array-deploy3-iscsi-setup/image3.png)
2. Entrar toohello web da interface do usuário do seu dispositivo virtual como **StorSimpleAdmin**. Insira a senha de administrador de dispositivo de saudação alterada na etapa 3: Iniciar Olá dispositivo virtual [implantar StorSimple Virtual Array - provisionar um dispositivo virtual no Hyper-V](storsimple-virtual-array-deploy2-provision-hyperv.md) ou [implantar StorSimple Virtual Array - Provisione um dispositivo virtual no VMware](storsimple-virtual-array-deploy2-provision-vmware.md).
   
    ![Página de entrada](./media/storsimple-virtual-array-deploy3-iscsi-setup/image4.png)
3. Você será levado toohello **início** página. Esta página descreve Olá várias configurações necessárias tooconfigure e registrar Olá dispositivo virtual com o serviço do Gerenciador de dispositivos de StorSimple hello. Observe que Olá **as configurações de rede**, **configurações de proxy da Web**, e **configurações de tempo** são opcionais. Olá, somente as configurações exigidas são **configurações do dispositivo** e **configurações de nuvem**.
   
    ![Página inicial](./media/storsimple-virtual-array-deploy3-iscsi-setup/image5.png)
4. Em Olá **as configurações de rede** página em **interfaces de rede**, DATA 0 será configurado automaticamente para você. Cada interface de rede é definido pelo padrão tooget um endereço IP automaticamente (DHCP). Assim, um endereço IP, a sub-rede e gateway serão atribuídos automaticamente (tanto para IPv4 quanto para IPv6).
   
    Quando você planejar toodeploy seu dispositivo, como um servidor do iSCSI (armazenamento em bloco tooprovision), é recomendável que você desabilite Olá **obter endereços IP automaticamente** opção e configurar endereços IP estáticos.
   
    ![Página de configurações de rede](./media/storsimple-virtual-array-deploy3-iscsi-setup/image6.png)
   
    Se você adicionou mais de uma interface de rede durante o provisionamento de saudação do dispositivo hello, você pode configurá-los aqui. Observe que você pode configurar a interface de rede apenas como IPv4 ou como IPv4 e IPv6. Não há suporte para configurações somente IPv6.
5. Servidores DNS são necessários porque eles são usados quando o dispositivo tenta toocommunicate com seus provedores de serviço de armazenamento de nuvem ou tooresolve seu dispositivo por nome se ele está configurado como um servidor de arquivos. Em Olá **as configurações de rede** página em Olá **servidores DNS**:
   
   1. Um servidor DNS primário e um secundário serão configurados automaticamente. Se você escolher tooconfigure endereços IP estáticos, você pode especificar servidores DNS. Para alta disponibilidade, recomendamos que você configure um servidor DNS primário e um secundário.
   2. Clique em **Aplicar**. Isso se aplica e validar as configurações de rede de saudação.
6. Em Olá **configurações do dispositivo** página:
   
   1. Atribuir uma única **nome** tooyour dispositivo. Esse nome pode ter de 1 a 15 caracteres e pode conter letras, números e hifens.
   2. Clique em Olá **servidor iSCSI** ícone ![ícone do servidor iSCSI](./media/storsimple-virtual-array-deploy3-iscsi-setup/image7.png) para Olá **tipo** de dispositivo que você está criando. Um servidor iSCSI permitirá que você tooprovision armazenamento em bloco.
   3. Especifique se deseja toobe este dispositivo ingressado no domínio. Se o dispositivo for um servidor iSCSI, em seguida, ingressar em domínio Olá é opcional. Se você decidir junção toonot seu domínio de tooa iSCSI do servidor, clique em **aplicar**, aguarde Olá configurações toobe aplicada e, em seguida, ignorar toohello próxima etapa.
      
       Se desejar que o domínio de tooa toojoin Olá dispositivo. Insira um **Nome de domínio** e clique em **Aplicar**.
      
      > [!NOTE]
      > Se unir seu domínio de tooa do servidor iSCSI, certifique-se de que o virtual array está em sua própria unidade organizacional (UO) para o Microsoft Azure Active Directory e nenhum objeto de diretiva de grupo (GPO) são aplicada tooit.
      > 
      > 
   4. Uma caixa de diálogo aparecerá. Insira suas credenciais de domínio no formato especificado hello. Clique o ícone de verificação Olá ![ícone de verificação](./media/storsimple-virtual-array-deploy3-iscsi-setup/image15.png). as credenciais de domínio Hello serão verificadas. Você verá uma mensagem de erro se Olá credenciais estão incorretas.
      
       ![credenciais](./media/storsimple-virtual-array-deploy3-iscsi-setup/image8.png)
   5. Clique em **Aplicar**. Isso se aplica e validar as configurações de dispositivo de saudação.
7. Opcionalmente, configure seu servidor proxy da Web. Embora a configuração do proxy da Web seja opcional, saiba que se você usar um proxy da Web, só poderá configurá-lo aqui.
   
    ![configurar o proxy Web](./media/storsimple-virtual-array-deploy3-iscsi-setup/image9.png)
   
    Em Olá **proxy Web** página:
   
   1. Olá fonte **URL do proxy Web** neste formato: *http://host-IP endereço* ou *FDQN:Port número*. Observe que não há suporte para URLs HTTPS.
   2. Especifique a **Autenticação** como **Básica** ou **Nenhuma**.
   3. Se você estiver usando a autenticação, você também precisará tooprovide um **Username** e **senha**.
   4. Clique em **Aplicar**. Isso validar e aplicar configurações de proxy da web de saudação configurada.
8. (Opcionalmente) definir configurações de tempo de saudação para seu dispositivo, como o fuso horário e Olá servidores NTP primários e secundário. Os servidores NTP são necessários, pois seu dispositivo deve sincronizar a hora para que ele possa se autenticar com seus provedores de serviço de nuvem.
   
    ![Configurações de hora](./media/storsimple-virtual-array-deploy3-iscsi-setup/image10.png)
   
    Em Olá **configurações de tempo** página:
   
   1. Olá lista suspensa, selecione lista Olá **fuso horário** com base em localização geográfica hello, no qual Olá dispositivo está sendo implantado. Olá fuso horário padrão para o dispositivo é PST. Seu dispositivo usará esse fuso horário para todas as operações agendadas.
   2. Especifique um **servidor NTP primário** para seu dispositivo ou aceite o valor padrão Olá time.windows.com. Certifique-se de que sua rede permite toopass de tráfego NTP do toohello seu data center da Internet.
   3. Opcionalmente, especifique um **Servidor NTP secundário** para o dispositivo.
   4. Clique em **Aplicar**. Isso irá validar e aplicar as configurações de tempo de saudação configurada.
9. Defina as configurações de nuvem de saudação para seu dispositivo. Nesta etapa, você concluir a configuração de dispositivo local hello e, em seguida, registre o dispositivo de saudação com seu serviço de Gerenciador de dispositivos do StorSimple.
   
   1. Digite hello **chave de registro** que você obteve na **etapa 2: chave de registro de serviço Get hello** na [implantar StorSimple Virtual Array - preparar Olá Portal](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key).
   2. Se esse não for o primeiro dispositivo de saudação que você está registrando com esse serviço, você precisará Olá tooprovide **chave de criptografia de dados de serviço**. Essa chave é necessária com hello serviço Registro tooregister chave dispositivos adicionais com hello serviço do Gerenciador de dispositivos do StorSimple. Para obter mais informações, consulte muito[chave de criptografia de dados de serviço do Get hello](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key) no local da web da interface do usuário.
   3. Clique em **Registrar**. Isso reiniciará o dispositivo hello. Talvez seja necessário toowait 2 a 3 minutos antes de dispositivo de saudação for registrado com êxito. Após a reinicialização do dispositivo hello, você será levado toohello logon na página.
      
      ![Registrar dispositivo](./media/storsimple-virtual-array-deploy3-iscsi-setup/image11.png)
10. Retorne toohello portal do Azure.
11. Navegue toohello **dispositivos** folha do seu serviço. Se você tiver muitos recursos, clique em **Todos os recursos**, clique no nome do serviço (procure, se necessário) e clique em **Dispositivos**.
12. Em Olá **dispositivos** folha, verifique se esse dispositivo Olá conectou com êxito toohello serviço verificando o status de saudação. status de saudação do dispositivo deve ser **pronto tooset backup**.
    
    ![Registrar dispositivo](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis1m.png)

## <a name="step-2-configure-hello-device-as-iscsi-server"></a>Etapa 2: Configurar dispositivo hello como o servidor iSCSI

Execute Olá etapas Olá configuração do dispositivo Olá necessário toocomplete portal do Azure.

#### <a name="tooconfigure-hello-device-as-iscsi-server"></a>dispositivo de saudação tooconfigure como o servidor iSCSI

1. Serviço de Gerenciador de dispositivos de StorSimple tooyour go e, em seguida, vá muito**gerenciamento > dispositivos**. Em Olá **dispositivos** folha, dispositivo Olá selecione que você acabou de criar. Este dispositivo aparecerão como **pronto tooset backup**.
   
    ![Configurar dispositivo como servidor iSCSI](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis1m.png) 
2. Clique em dispositivo hello e você verá uma mensagem de cabeçalho indicando que o dispositivo Olá é toosetup pronto.
   
    ![Configurar dispositivo como servidor iSCSI](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis2m.png)  
3. Clique em **configurar** na barra de comandos de dispositivo hello. Isso abre a saudação **configurar** folha. Em Olá **configurar** folha, Olá a seguir:
   
   * nome do servidor iSCSI Olá é preenchida automaticamente.
   * Certifique-se de criptografia de armazenamento em nuvem hello está definida muito**habilitado**. Isso garante que os dados de saudação enviados do hello dispositivo toohello nuvem sejam criptografados.
   * Especifique uma chave de criptografia de 32 caracteres e grave-a em um aplicativo de gerenciamento de chaves para referência futura.
   * Selecione um toobe de conta de armazenamento usado com seu dispositivo. Nesta assinatura, você pode selecionar uma conta de armazenamento existente, ou você pode clicar em **adicionar** toochoose uma conta de uma assinatura diferente.
     
     ![Configurar dispositivo como servidor iSCSI](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis4m.png)
4. Clique em **configurar** toocomplete configurar servidor de saudação do iSCSI.
   
    ![Configurar dispositivo como servidor iSCSI](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis5m.png) 
5. Você será notificado de que a criação do servidor iSCSI hello está em andamento. Depois que o servidor iSCSI Olá é criado com êxito, Olá **dispositivos** folha é atualizada e status do dispositivo correspondente Olá **Online**.
   
    ![Configurar dispositivo como servidor iSCSI](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis9m.png)

## <a name="step-3-add-a-volume"></a>Etapa 3: adicionar um volume

1. Em Olá **dispositivos** folha, dispositivo Olá select que acabou de configurar um servidor do iSCSI. Clique em **...**  (como alternativa, clique na linha) e no menu de contexto hello, selecione **Adicionar volume**. Você também pode clicar em **+ Adicionar volume** na barra de comandos de saudação. Isso abre a saudação **Adicionar volume** folha.
   
    ![Adicionar um volume](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis10m.png)
2. Em Olá **Adicionar volume** folha, Olá a seguir:
   
   * Em Olá **nome do Volume** campo, digite um nome exclusivo para seu volume. nome da saudação deve ser uma cadeia de caracteres com 3 caracteres too127.
   * Em Olá **tipo** suspensa lista, especifique se toocreate um **em camadas** ou **localmente afixado** volume. Para as cargas de trabalho que exigem garantias locais, latências baixas e um melhor desempenho, selecione **volume** **Localmente afixado**. Para todos os outros dados, selecione **Volume** em **camadas**.
   * Em Olá **capacidade** , especifique o tamanho de saudação do volume de saudação. Um volume em camadas deve ter entre 500 GB e 5 TB e um volume fixado localmente deve ter entre 50 GB e 500 GB.
     
     Um volume localmente afixado é muito provisionado e garante que os dados primários de saudação no volume de saudação permanecem no dispositivo hello e não despejar toohello nuvem.
     
     Um volume em camadas em Olá outro lado escassamente provisionado. Quando você cria um volume em camadas, aproximadamente 10% do espaço de saudação é provisionado na camada local hello e 90% do espaço de saudação é provisionado na nuvem hello. Por exemplo, se você provisionar um volume de 1 TB, 100 GB reside no espaço local hello e 900 GB é usado na nuvem hello quando Olá camadas de dados. Isso implica por sua vez é que, se você ficar sem todo o espaço local Olá no dispositivo Olá, você não pode provisionar um compartilhamento em camadas (porque Olá 10% não está disponível).
     
     ![Adicionar um volume](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis12.png)
   * Clique em **conectado hosts**, selecione um acesso controle ACR (registro) correspondente toohello iniciador iSCSI que você deseja tooconnect toothis volume e, em seguida, clique em **selecione**. <br><br> 
3. tooadd um novo host conectado, clique em **adicionar novo**, insira um nome de host de saudação e o iSCSI IQN (nome qualificado) e depois clique em **adicionar**. Se você não tiver Olá IQN, vá muito[Olá apêndice a: obter o IQN de um host do Windows Server](#appendix-a-get-the-iqn-of-a-windows-server-host).
   
      ![Adicionar um volume](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis15m.png)
4. Ao concluir a configuração de seu volume, clique em **OK**. Um volume será criado com hello especificado as configurações e você verá uma notificação. Por padrão, monitoramento e o backup serão habilitados para o volume de saudação.
   
     ![Adicionar um volume](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis18m.png)
5. tooconfirm que Olá volume foi criado com êxito, vá toohello **Volumes** folha. Você deve ver o volume de saudação listado.
   
   ![Adicionar um volume](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis20m.png)

## <a name="step-4-mount-initialize-and-format-a-volume"></a>Etapa 4: montar, inicializar e formatar um volume

Executar Olá seguindo as etapas toomount, inicializar e formatar seus volumes do StorSimple em um host do Windows Server.

#### <a name="toomount-initialize-and-format-a-volume"></a>toomount, inicializar e formatar um volume

1. Olá abrir **iniciador iSCSI** aplicativo no servidor de saudação apropriado.
2. Em Olá **propriedades do iniciador iSCSI** janela Olá **descoberta** , clique em **descobrir Portal**.
   
    ![Descobrir Portal](./media/storsimple-virtual-array-deploy3-iscsi-setup/image22.png)
3. Em Olá **descobrir Portal de destino** caixa de diálogo, forneça Olá endereço IP de sua interface de rede habilitada com iSCSI e, em seguida, clique em **Okey**.
   
    ![Endereço IP](./media/storsimple-virtual-array-deploy3-iscsi-setup/image23.png)
4. Em Olá **propriedades do iniciador iSCSI** janela Olá **destinos** guia, localize Olá **descobertos destinos**. (Cada volume será um destino de descoberta). status do dispositivo Olá devem aparecer como **inativo**.
   
    ![destinos descobertos](./media/storsimple-virtual-array-deploy3-iscsi-setup/image24.png)
5. Selecione um dispositivo de destino e clique em **Conectar**. Depois Olá dispositivo estiver conectado, o status de saudação deve mudar muito**conectado**. (Para obter mais informações sobre como usar o iniciador iSCSI da Microsoft hello, consulte [instalando e configurando o Microsoft iSCSI Initiator][1].
   
    ![selecionar dispositivo de destino](./media/storsimple-virtual-array-deploy3-iscsi-setup/image25.png)
6. No host do Windows, pressione a tecla de logotipo do Windows hello + X e, em seguida, clique em **executar**.
7. Em Olá **executar** caixa de diálogo, digite **Diskmgmt.msc**. Clique em **Okey**e hello **gerenciamento de disco** caixa de diálogo será exibida. painel direito da saudação mostrará volumes Olá em seu host.
8. Em Olá **gerenciamento de disco** janela, hello volumes montados serão exibidos conforme mostrado na ilustração a seguir de saudação. Com o botão direito volume Olá descoberto (clique em nome do disco Olá) e, em seguida, clique em **Online**.
   
    ![Gerenciamento de Disco](./media/storsimple-virtual-array-deploy3-iscsi-setup/image26.png)
9. Clique com o botão direito do mouse e selecione **Inicializar Disco**.
   
    ![inicializar disco 1](./media/storsimple-virtual-array-deploy3-iscsi-setup/image27.png)
10. Na caixa de diálogo hello, selecione Olá discos tooinitialize e, em seguida, clique em **Okey**.
    
    ![inicializar disco 2](./media/storsimple-virtual-array-deploy3-iscsi-setup/image28.png)
11. Assistente de novo Volume simples Olá é iniciado. Selecione um tamanho de disco e clique em **Avançar**.
    
    ![assistente de novo volume 1](./media/storsimple-virtual-array-deploy3-iscsi-setup/image29.png)
12. Atribuir um volume de toohello de letra de unidade e, em seguida, clique em **próximo**.
    
    ![assistente de novo volume 2](./media/storsimple-virtual-array-deploy3-iscsi-setup/image30.png)
13. Insira o volume de Olá Olá parâmetros tooformat. **No Windows Server, há suporte somente para NTFS.** Definir Olá too64K de tamanho de unidade de alocação. Forneça um rótulo para o volume. É uma prática recomendada para este nome de volume do nome toobe toohello idênticos fornecido no StorSimple Virtual Array. Clique em **Avançar**.
    
    ![assistente de novo volume 3](./media/storsimple-virtual-array-deploy3-iscsi-setup/image31.png)
14. Verifique os valores de saudação para seu volume e, em seguida, clique em **concluir**.
    
    ![assistente de novo volume 4](./media/storsimple-virtual-array-deploy3-iscsi-setup/image32.png)
    
    Olá volumes serão exibidos como **Online** em Olá **gerenciamento de disco** página.
    
    ![volumes online](./media/storsimple-virtual-array-deploy3-iscsi-setup/image33.png)

## <a name="next-steps"></a>Próximas etapas

Saiba como toouse Olá interface da web local muito[administrar sua matriz Virtual StorSimple](storsimple-ova-web-ui-admin.md).

## <a name="appendix-a-get-hello-iqn-of-a-windows-server-host"></a>Apêndice a: saudação de Get IQN de um host do Windows Server

Executar Olá seguindo as etapas tooget Olá iSCSI IQN (nome qualificado) de um host do Windows que está executando o Windows Server 2012.

#### <a name="tooget-hello-iqn-of-a-windows-host"></a>Olá tooget IQN do host do Windows

1. Inicie o iniciador iSCSI da Microsoft hello no seu host do Windows.
2. Em Olá **propriedades do iniciador iSCSI** janela Olá **configuração** , selecione e copie a cadeia de caracteres de saudação do hello **nome do iniciador** campo.
   
    ![Propriedades do Iniciador iSCSI](./media/storsimple-virtual-array-deploy3-iscsi-setup/image34.png)
3. Salve esta cadeia de caracteres.

<!--Reference link-->
[1]: https://technet.microsoft.com/library/ee338480(WS.10).aspx



