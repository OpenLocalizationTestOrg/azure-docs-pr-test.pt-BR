---
title: aaaSet matriz Virtual do StorSimple como servidor de arquivos | Microsoft Docs
description: "Este tutorial terceiro na implantação de matriz Virtual StorSimple instrui você tooset um dispositivo virtual como servidor de arquivos."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: f609f6ff-0927-48bb-a68a-6d8985d2fe34
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/17/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 89cade37980f342695c0adee42c4ade0e1d53d2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---set-up-as-file-server-via-azure-portal"></a>Implantar o StorSimple Virtual Array — configurar como um servidor de arquivos por meio do portal do Azure
![](./media/storsimple-virtual-array-deploy3-fs-setup/fileserver4.png)

## <a name="introduction"></a>Introdução
Este artigo descreve como tooperform a configuração inicial, registrar o servidor de arquivos do StorSimple, configuração de dispositivo concluída Olá e criar e se conectar a compartilhamentos tooSMB. Isso é Olá último artigo Olá série de tutoriais de implantação necessários toocompletely implantar sua matriz virtual como um servidor de arquivos ou um servidor iSCSI.

processo de instalação e configuração de saudação pode levar cerca de 10 toocomplete de minutos. informações de Olá neste artigo se aplicam somente a implantação de toohello de saudação matriz Virtual StorSimple. Para implantação de saudação de dispositivos da série StorSimple 8000, vá para: [implantar seu dispositivo da série StorSimple 8000 executando atualização 2](storsimple-deployment-walkthrough-u2.md).

## <a name="setup-prerequisites"></a>Pré-requisitos de configuração
Antes de configurar e de instalar a Matriz Virtual StorSimple, verifique se:

* Você possua uma matriz virtual e tooit conectado como Olá detalhada em [provisionar uma matriz de StorSimple Virtual no Hyper-V](storsimple-virtual-array-deploy2-provision-hyperv.md) ou [provisionar uma matriz Virtual do StorSimple no VMware](storsimple-virtual-array-deploy2-provision-vmware.md).
* Você tem a chave de registro do serviço de saudação do serviço do Gerenciador de dispositivos de StorSimple Olá que você criou toomanage StorSimple Virtual matrizes. Para obter mais informações, consulte [etapa 2: chave de registro de serviço Get hello](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key) para matriz Virtual StorSimple.
* Quando se trata de saudação outra matriz virtual que você está registrando com um serviço existente do Gerenciador de dispositivos de StorSimple, você deve ter o chave de criptografia de dados de serviço de saudação. Essa chave foi gerada quando o primeiro dispositivo de saudação foi registrado com êxito com esse serviço. Se você perdeu essa chave, consulte [chave de criptografia de dados de serviço do Get hello](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key) para sua matriz Virtual StorSimple.

## <a name="step-by-step-setup"></a>Configuração passo a passo
Use Olá acompanhamento tooset instruções passo a passo e configurar sua matriz Virtual StorSimple.

## <a name="step-1-complete-hello-local-web-ui-setup-and-register-your-device"></a>Etapa 1: Concluir instalação de interface do usuário da web local hello e registrar seu dispositivo
#### <a name="toocomplete-hello-setup-and-register-hello-device"></a>toocomplete Olá instalação e registrar dispositivo Olá
1. Abra uma janela do navegador e conecte-se a interface da web local toohello. Tipo:
   
   `https://<ip-address of network interface>`
   
   Use a URL de conexão de Olá anotado na etapa anterior hello. Você vir um erro indicando que há um problema com o certificado de segurança do site hello. Clique em **continuar toothis página da Web**.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image2.png)
2. Entrar toohello web da interface do usuário da sua matriz virtual como **StorSimpleAdmin**. Insira a senha de administrador de dispositivo de saudação alterada na etapa 3: matriz virtual do início Olá em [provisionar uma matriz de StorSimple Virtual no Hyper-V](storsimple-virtual-array-deploy2-provision-hyperv.md) ou [provisionar uma matriz Virtual do StorSimple no VMware](storsimple-virtual-array-deploy2-provision-vmware.md).
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image3.png)
3. Você será direcionado toohello **início** página. Esta página descreve Olá várias configurações necessárias tooconfigure e registrar Olá array virtual com o serviço do Gerenciador de dispositivos de StorSimple hello. Olá **as configurações de rede**, **configurações de proxy da Web**, e **configurações de tempo** são opcionais. Olá, somente as configurações exigidas são **configurações do dispositivo** e **configurações de nuvem**.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image4.png)
4. Em Olá **as configurações de rede** página em **interfaces de rede**, DATA 0 será configurado automaticamente para você. Cada interface de rede é definida automaticamente pelo endereço IP padrão tooget (DHCP). Assim, um endereço IP, uma sub-rede e um gateway serão atribuídos automaticamente (tanto para IPv4 quanto para IPv6).
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image5.png)
   
   Se você adicionou mais de uma interface de rede durante o provisionamento de saudação do dispositivo hello, você pode configurá-los aqui. Observe que você pode configurar a interface de rede apenas como IPv4 ou como IPv4 e IPv6. Não há suporte para configurações somente IPv6.
5. Servidores DNS são necessários porque eles são usados quando o dispositivo tenta toocommunicate com seus provedores de serviço de armazenamento de nuvem ou tooresolve seu dispositivo pelo nome quando configurado como um servidor de arquivos. Em Olá **as configurações de rede** página em Olá **servidores DNS**:
   
   1. Um servidor DNS primário e um secundário são configurados automaticamente. Se você escolher tooconfigure endereços IP estáticos, você pode especificar servidores DNS. Para alta disponibilidade, recomendamos que você configure um servidor DNS primário e um secundário.
   2. Clique em **aplicar** tooapply e validar as configurações de rede hello.
6. Em Olá **configurações do dispositivo** página:
   
   1. Atribuir uma única **nome** tooyour dispositivo. Esse nome pode ter de 1 a 15 caracteres e pode conter letras, números e hifens.
   2. Clique em Olá **servidor de arquivos** ícone ![](./media/storsimple-virtual-array-deploy3-fs-setup/image6.png) para Olá **tipo** de dispositivo que você está criando. Um servidor de arquivos permitirá que você pastas toocreate compartilhado.
   3. Como o dispositivo é um servidor de arquivos, você precisará de domínio de tooa toojoin Olá dispositivo. Insira um **Nome de domínio**.
   4. Clique em **Aplicar**.
7. Uma caixa de diálogo aparecerá. Insira suas credenciais de domínio no formato especificado hello. Clique o ícone de verificação de saudação. as credenciais de domínio de Hello são verificadas. Você verá uma mensagem de erro se Olá credenciais estão incorretas.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image7.png)
8. Clique em **Aplicar**. Isso se aplica e validar as configurações de dispositivo de saudação.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image8.png)
   
   > [!NOTE]
   > Certifique-se de que o virtual array está em sua própria unidade organizacional (UO) do Active Directory e nenhum objeto de diretiva de grupo (GPO) é aplicada tooit ou herdado. Política de grupo pode instalar aplicativos como software antivírus no hello matriz Virtual StorSimple. Instalar software adicional não é suportado e pode causar corrupção toodata. 
   > 
   > 
9. Opcionalmente, configure seu servidor proxy da Web. Embora a configuração do proxy da Web seja opcional, saiba que se você usar um proxy da Web, só poderá configurá-lo aqui.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image9.png)
   
   Em Olá **proxy Web** página:
   
   1. Olá fonte **URL do proxy Web** neste formato: *http://&lt;endereço IP de host ou FQDN&gt;: número da porta*. Observe que não há suporte para URLs HTTPS.
   2. Especifique a **Autenticação** como **Básica** ou **Nenhuma**.
   3. Se usar a autenticação, você também precisará tooprovide um **Username** e **senha**.
   4. Clique em **Aplicar**. Isso validar e aplicar configurações de proxy da web de saudação configurada.
10. (Opcionalmente) definir configurações de tempo de saudação para seu dispositivo, como o fuso horário e Olá servidores NTP primários e secundário. Os servidores NTP são necessários, pois seu dispositivo deve sincronizar a hora para que ele possa se autenticar com seus provedores de serviço de nuvem.
    
    ![](./media/storsimple-virtual-array-deploy3-fs-setup/image10.png)
    
    Em Olá **configurações de tempo** página:
    
    1. Na lista suspensa hello, selecione Olá **fuso horário** com base em localização geográfica hello, no qual Olá dispositivo está sendo implantado. Olá fuso horário padrão para o dispositivo é PST. Seu dispositivo usará esse fuso horário para todas as operações agendadas.
    2. Especifique um **servidor NTP primário** para seu dispositivo ou aceite o valor padrão Olá time.windows.com. Certifique-se de que sua rede permite toopass de tráfego NTP do toohello seu data center da Internet.
    3. Opcionalmente, especifique um **Servidor NTP secundário** para o dispositivo.
    4. Clique em **Aplicar**. Isso irá validar e aplicar as configurações de tempo de saudação configurada.
11. Defina as configurações de nuvem de saudação para seu dispositivo. Nesta etapa, você concluir a configuração de dispositivo local hello e, em seguida, registre o dispositivo de saudação com seu serviço de Gerenciador de dispositivos do StorSimple.
    
    1. Digite hello **chave de registro** que você obteve na [etapa 2: chave de registro de serviço Get hello](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key) para matriz Virtual StorSimple.
    2. Se esse for o primeiro dispositivo Registrando com esse serviço, você verá Olá **chave de criptografia de dados de serviço**. Copie essa chave e salve-a em um local seguro. Essa chave é necessária com hello serviço Registro tooregister chave dispositivos adicionais com hello serviço do Gerenciador de dispositivos do StorSimple. 
       
       Se esse não for o primeiro dispositivo de saudação que você está registrando com esse serviço, você precisará de chave de criptografia de dados de serviço do tooprovide Olá. Para obter mais informações, consulte Olá tooget [chave de criptografia de dados de serviço](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key) no local da web da interface do usuário.
    3. Clique em **Registrar**. Isso reiniciará o dispositivo hello. Talvez seja necessário toowait 2 a 3 minutos antes de dispositivo de saudação for registrado com êxito. Após a reinicialização do dispositivo hello, você será levado toohello logon na página.
       
       ![](./media/storsimple-virtual-array-deploy3-fs-setup/image13.png)
12. Retorne toohello portal do Azure. Vá muito**todos os recursos**, pesquise seu serviço de Gerenciador de dispositivos do StorSimple.
    
    ![](./media/storsimple-virtual-array-deploy3-fs-setup/searchdevicemanagerservice1.png) 
13. Em Olá filtrado lista, selecione o serviço de Gerenciador de dispositivos do StorSimple e navegue muito**gerenciamento > dispositivos**. Em Olá **dispositivos** folha, verifique se o dispositivo Olá foi conectado com êxito o serviço toohello e tem status de saudação **pronto tooset backup**.
    
    ![Configurar um servidor de arquivos](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs2m.png)

## <a name="step-2-configure-hello-device-as-file-server"></a>Etapa 2: Configurar dispositivo hello como servidor de arquivos
Executar Olá etapas Olá [portal do Azure](https://portal.azure.com/) toocomplete Olá necessária a configuração do dispositivo.

#### <a name="tooconfigure-hello-device-as-file-server"></a>dispositivo de saudação tooconfigure como servidor de arquivos
1. Serviço de Gerenciador de dispositivos de StorSimple tooyour go e, em seguida, vá muito **gerenciamento > dispositivos**. Em Olá **dispositivos** folha, dispositivo Olá selecione que você acabou de criar. Este dispositivo aparecerão como **pronto tooset backup**.
   
   ![Configurar um servidor de arquivos](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs2m.png) 
2. Clique em dispositivo hello e você verá uma mensagem de cabeçalho indicando que o dispositivo Olá é toosetup pronto.
   
    ![Configurar um servidor de arquivos](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs3m.png)
3. Clique em **configurar** na barra de comandos de saudação. Isso abre a saudação **configurar** folha. Em Olá **configurar** folha, Olá a seguir:
   
    1. nome do servidor de arquivo Hello é preenchida automaticamente.
    
    2. Certifique-se de criptografia de armazenamento em nuvem hello está definida muito**habilitado**. Isso irá criptografar todos os dados de Olá enviada toohello nuvem. 
    
    3. Uma chave AES de 256 bits é usada com a chave definida pelo usuário Olá para criptografia. Especifique uma chave de 32 caracteres e, em seguida, execute novamente tooconfirm chave Olá-lo. Chave de saudação de registro em um aplicativo de gerenciamento de chaves para referência futura.
    
    4. Clique em **definir as configurações necessárias** credenciais de conta de armazenamento toospecify toobe usado com seu dispositivo. Clique em **adicionar novo** se não houver nenhuma credencial de conta de armazenamento configurada. **Garantir que a conta de armazenamento Olá que usar suporte blobs de bloco. Blobs de página não têm suporte.** Para obter mais informações sobre [blobs de blocos e blobs de página](https://docs.microsoft.com/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs).
   
    ![Configurar um servidor de arquivos](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs6m.png) 
4. Em Olá **adicionar credenciais de conta de armazenamento** folha, Olá a seguir: 

    1. Escolha assinatura atual se a conta de armazenamento Olá for no hello mesma assinatura que o serviço de saudação. Especifique outro armazenamento Olá conta está fora da assinatura do serviço de saudação. 
    
    2. Na lista suspensa hello, escolha uma conta de armazenamento existente. 
    
    3. local Hello será preenchido automaticamente com base em Olá especificado conta de armazenamento. 
    
    4. Habilite SSL tooensure um canal de comunicação de rede segura entre o dispositivo hello e nuvem hello.
    
    5. Clique em **adicionar** tooadd esse armazenamento de credenciais de conta. 
   
        ![Configurar um servidor de arquivos](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs8m.png)

5. Depois que a credencial da conta de armazenamento Olá é criado com êxito, Olá **configurar** folha será atualizada toodisplay Olá especificadas credenciais da conta de armazenamento. Clique em **Configurar**.
   
   ![Configurar um servidor de arquivos](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs11m.png)
   
   Você verá que um servidor de arquivos está sendo criado. Depois que o servidor de arquivos de saudação é criado com êxito, você será notificado.
   
   ![Configurar um servidor de arquivos](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs13m.png)
   
   status do dispositivo Olá também será alterada muito**Online**.
   
   ![Configurar um servidor de arquivos](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs14m.png)
   
   Você pode continuar tooadd um compartilhamento.

## <a name="step-3-add-a-share"></a>Etapa 3: adicionar um compartilhamento
Executar Olá etapas Olá [portal do Azure](https://portal.azure.com/) toocreate um compartilhamento.

#### <a name="toocreate-a-share"></a>toocreate um compartilhamento
1. Selecione o dispositivo de servidor de arquivo hello configurada na saudação anterior da etapa e clique em **...**  (ou com o botão direito). No menu de contexto hello, selecione **Adicionar compartilhamento**. Como alternativa, você pode clicar em **+ Adicionar compartilhamento** na barra de comandos de dispositivo hello.
   
   ![Adicionar um compartilhamento](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs15m.png)
2. Especifique Olá configurações de compartilhamento a seguir:

    1. Um nome exclusivo para seu compartilhamento. nome da saudação deve ser uma cadeia de caracteres com 3 caracteres too127.
    
    2. Um recurso opcional **descrição** para compartilhamento de saudação. Descrição de saudação ajudará a identificar os proprietários do compartilhamento hello.
    
    3. Um **tipo** para compartilhamento de saudação. Olá tipo pode ser **em camadas** ou **localmente afixado**, com sendo hierárquico Olá padrão. Para cargas de trabalho que exigem garantias locais, menos latências e um melhor desempenho, selecione um compartilhamento **Fixado localmente** . Para todos os outros dados, selecione um compartilhamento **Em camadas** .
    Um compartilhamento localmente afixado é muito provisionado e garante que os dados primários de Olá no compartilhamento de saudação permanece dispositivo toohello local e não despejar toohello nuvem. Um compartilhamento em camadas em Olá outro lado escassamente provisionado. Quando você cria um compartilhamento em camadas, 10% do espaço de saudação é provisionado na camada local hello e 90% do espaço de saudação é provisionado na nuvem hello. Por exemplo, se você provisionar um volume de 1 TB, 100 GB reside no espaço local hello e 900 GB é usado na nuvem hello quando Olá camadas de dados. Por sua vez, isso significa que, se você executar o fora de todo o espaço local Olá no dispositivo hello, não é possível provisionar um compartilhamento em camadas.
   
    4. Em Olá **definir padrão permissões completas** campo, atribua Olá permissões toohello do usuário ou grupo Olá que acessa esse compartilhamento. Especificar nome de saudação do Olá Olá de usuário ou grupo no  *john@contoso.com*  formato. É recomendável que você use um tooaccess de privilégios de administrador do usuário grupo (em vez de um único usuário) tooallow esses compartilhamentos. Depois que você atribuiu permissões de saudação aqui, você pode usar Explorador de arquivos toomodify essas permissões.
   
    5. Clique em **adicionar** toocreate compartilhamento de saudação. 
    
        ![Adicionar um compartilhamento](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs18m.png)
   
        Você será notificado de que a criação do compartilhamento hello está em andamento.
   
        ![Adicionar um compartilhamento](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs19m.png)
   
    Depois Olá compartilhamento é criado com hello especificar configurações, hello **compartilhamentos** folha atualizará o novo compartilhamento de saudação tooreflect. Por padrão, o monitoramento e o backup são habilitados para compartilhamento de saudação.
   
    ![Adicionar um compartilhamento](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs22m.png)

## <a name="step-4-connect-toohello-share"></a>Etapa 4: Conectar toohello compartilhamento
Você precisará tooconnect tooone ou mais compartilhamentos que você criou na etapa anterior hello. Execute estas etapas em seu host conectado de Windows Server tooyour matriz Virtual StorSimple.

#### <a name="tooconnect-toohello-share"></a>compartilhamento de toohello tooconnect
1. Pressione ![](./media/storsimple-virtual-array-deploy3-fs-setup/image22.png) + r. Na janela de execução hello, especifique Olá *&#92; &#92;&lt; nome do servidor de arquivos&gt;*  como caminho hello, substituindo *nome do servidor de arquivo* com dispositivo Olá nome é atribuído tooyour servidor de arquivos. Clique em **OK**.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image23.png)
2. Isso abre o Gerenciador de Arquivos. Agora você deve ser capaz de toosee compartilhamentos de Olá que você criou como pastas. Selecione e clique duas vezes em um conteúdo de saudação tooview compartilhamento (pasta).
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image24.png)
3. Agora você pode adicionar arquivos toothese compartilhamentos e fazer um backup.

## <a name="next-steps"></a>Próximas etapas
Saiba como toouse Olá interface da web local muito[administrar sua matriz Virtual StorSimple](storsimple-ova-web-ui-admin.md).

