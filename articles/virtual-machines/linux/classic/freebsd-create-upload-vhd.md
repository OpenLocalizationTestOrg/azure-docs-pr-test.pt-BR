---
title: imagem de aaaCreate e carregar uma VM FreeBSD | Microsoft Docs
description: "Saiba toocreate e carregar um disco rígido virtual (VHD) que contém a saudação FreeBSD sistema operacional toocreate uma máquina virtual do Azure"
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1ef30f32-61c1-4ba8-9542-801d7b18e9bf
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/08/2017
ms.author: kyliel
ms.openlocfilehash: f3bd155e496f1a2713d36bb66ea9824ed4c210ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-a-freebsd-vhd-tooazure"></a>Criar e carregar um VHD FreeBSD tooAzure
Este artigo mostra como toocreate e carregar um disco rígido virtual (VHD) que contém Olá sistema de operacional FreeBSD. Depois que você carregá-lo, você pode usá-lo como toocreate sua própria imagem uma máquina virtual (VM) no Azure.

> [!IMPORTANT] 
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação. Para obter informações sobre como carregar um VHD usando o modelo do Gerenciador de recursos de hello, consulte [aqui](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="prerequisites"></a>Pré-requisitos
Este artigo pressupõe que você tenha Olá itens a seguir:

* **Uma assinatura do Azure**– Se não tiver uma conta, você poderá criar uma em apenas alguns minutos. Se você tiver uma assinatura do MSDN, confira [Crédito Azure mensal para assinantes do Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/). Caso contrário, saiba como muito[criar uma conta de avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).  
* **Ferramentas do Azure PowerShell**– módulo do PowerShell do Azure Olá deve ser instalado e configurado toouse sua assinatura do Azure. módulo de saudação toodownload, consulte [downloads do Azure](https://azure.microsoft.com/downloads/). Um tutorial que descreve como tooinstall e configurar o módulo Olá está disponível aqui. Saudação de uso [Downloads do Azure](https://azure.microsoft.com/downloads/) saudação do cmdlet tooupload VHD.
* **Sistema de operacional FreeBSD instalado em um arquivo. vhd**– um sistema de operacional FreeBSD deve ser instalado tooa do disco rígido virtual. Várias ferramentas existem toocreate arquivos. vhd. Por exemplo, você pode usar uma solução de virtualização, como o arquivo. vhd do Hyper-V toocreate hello e instalar o sistema operacional de saudação. Para obter instruções sobre como tooinstall e use o Hyper-V, consulte [instalar o Hyper-V e criar uma máquina virtual](http://technet.microsoft.com/library/hh846766.aspx).

> [!NOTE]
> Não há suporte para o formato VHDX mais recente de saudação no Azure. Você pode converter o formato de tooVHD de disco de saudação usando o Gerenciador do Hyper-V ou Olá cmdlet [convert-vhd](https://technet.microsoft.com/library/hh848454.aspx). Além disso, há um [tutorial no MSDN sobre como toouse FreeBSD com Hyper-V](http://blogs.msdn.com/b/kylie/archive/2014/12/25/running-freebsd-on-hyper-v.aspx).
>
>

Esta tarefa inclui Olá cinco etapas a seguir:

## <a name="step-1-prepare-hello-image-for-upload"></a>Etapa 1: Preparar a imagem de saudação para carregamento
Na máquina virtual do hello onde você instalou o sistema de operacional FreeBSD hello, conclua Olá procedimentos a seguir:

1. Habilitar DHCP.

        # echo 'ifconfig_hn0="SYNCDHCP"' >> /etc/rc.conf
        # service netif restart
2. Habilitar SSH.

    Certifique-se de servidor SSH hello está instalado e configurado toostart no momento da inicialização. Ele é habilitado por padrão após a instalação do disco FreeBSD. 
3. Instalar um console serial.

        # echo 'console="comconsole vidconsole"' >> /boot/loader.conf
        # echo 'comconsole_speed="115200"' >> /boot/loader.conf
4. Instalar o sudo.

    conta de raiz Hello está desabilitada no Azure. Isso significa que você precise sudo tooutilize de comandos de toorun um usuário sem privilégios com privilégios elevados.

        # pkg install sudo
   
5. Pré-requisitos para agente do Azure.

        # pkg install python27  
        # pkg install Py27-setuptools  
        # ln -s /usr/local/bin/python2.7 /usr/bin/python   
        # pkg install git
6. Instalar o agente do Azure.

    Olá versão mais recente do hello agente do Azure pode sempre ser encontrada no [github](https://github.com/Azure/WALinuxAgent/releases). Olá versão 2.0.10 + com suporte oficial à 10 FreeBSD & 10.1 e versão Olá 2.1.4 + (incluindo 2.2) com suporte oficial à FreeBSD 10.2 e versões posteriores.

        # git clone https://github.com/Azure/WALinuxAgent.git  
        # cd WALinuxAgent  
        # git tag  
        …
        WALinuxAgent-2.0.16
        …
        v2.1.4
        v2.1.4.rc0
        v2.1.4.rc1

    Para o 2.0, vamos usar 2.0.16 como exemplo:

        # git checkout WALinuxAgent-2.0.16
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  

    Para o 2.1, vamos usar 2.1.4 como exemplo:

        # git checkout v2.1.4
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  
        # ln -sf /usr/local/sbin/waagent2.0 /usr/sbin/waagent2.0

   > [!IMPORTANT]
   > Depois de instalar o agente do Azure, é tooverify uma boa ideia que ele está em execução:
   >
   >

        # waagent -version
        WALinuxAgent-2.1.4 running on freebsd 10.3
        Python: 2.7.11
        # ps auxw | grep waagent
        root   639   0.0  0.5 104620 17520 u0- I    05:17    0:00.20 python /usr/local/sbin/waagent -daemon (python2.7)
        # cat /var/log/waagent.log
7. Desprovisione o sistema hello.

    Desprovisionamento Olá sistema tooclean-lo e disponibilizá-lo adequado para reprovisionamento. Olá comando a seguir também exclui última conta de usuário provisionado hello e dados associado de saudação:

        # echo "y" |  /usr/local/sbin/waagent -deprovision+user  
        # echo  'waagent_enable="YES"' >> /etc/rc.conf

    Agora você pode desligar sua VM.

## <a name="step-2-create-a-storage-account-in-azure"></a>Etapa 2: Criar uma conta de armazenamento no Azure
Você precisa de uma conta de armazenamento no Azure tooupload um arquivo. vhd que ela possa ser usada toocreate uma máquina virtual. Você pode usar o hello toocreate portal clássico do Azure uma conta de armazenamento.

1. Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com).
2. Na barra de comandos hello, selecione **novo**.
3. Selecione **Serviços de Dados** > **Armazenamento** > **Criação Rápida**.

    ![Criação rápida de uma conta de armazenamento](./media/freebsd-create-upload-vhd/Storage-quick-create.png)
4. Preencha os campos de saudação da seguinte maneira:

   * Em Olá **URL** , digite um toouse de nome de subdomínio no hello URL da conta de armazenamento. Olá entrada pode conter de 3 a 24 números e letras minúsculas. Esse nome se torna o nome de host de saudação em URL Olá tooaddress usado armazenamento de BLOBs do Azure, armazenamento de fila do Azure, ou recursos de armazenamento de tabela do Azure para a assinatura de saudação.
   * Em Olá **local/grupo de afinidade** menu suspenso, escolha Olá **local ou grupo de afinidade** Olá conta de armazenamento. Um grupo de afinidade permite colocar seus serviços de nuvem e o armazenamento em Olá mesmo data center.
   * Em Olá **replicação** campo, decida se toouse **com redundância geográfica** replicação Olá conta de armazenamento. A replicação geográfica é ativada por padrão. Essa opção replica seu dados tooa local secundário, em nenhum custo tooyou, para que o armazenamento local toothat se uma falha grave o failover ocorre no local primário hello. local secundário Olá é atribuído automaticamente e não pode ser alterado. Se você precisar de mais controle sobre o local de saudação do armazenamento baseado em nuvem devido a requisitos de toolegal ou política organizacional, você pode desativar a replicação geográfica. No entanto, lembre-se de que se ativar replicação geográfica mais tarde, você será cobrado um único tooreplicate de taxa de transferência de dados secundário local de toohello seus dados existente. Serviços de armazenamento sem replicação geográfica são oferecidos com desconto. Encontre mais detalhes sobre como gerenciar a replicação geográfica de contas de armazenamento aqui: [Replicação do Armazenamento do Azure](../../../storage/common/storage-redundancy.md).

     ![Insira os detalhes da conta de armazenamento](./media/freebsd-create-upload-vhd/Storage-create-account.png)
5. Escolha **Criar Conta de Armazenamento**. Olá conta agora aparece em **armazenamento**.

    ![Conta de armazenamento criada com êxito](./media/freebsd-create-upload-vhd/Storagenewaccount.png)
6. Em seguida, crie um contêiner para os seus .vhd carregados. Selecione o nome de conta de armazenamento hello e, em seguida, selecione **contêineres**.

    ![Detalhes da conta de armazenamento](./media/freebsd-create-upload-vhd/storageaccount_detail.png)
7. Escolha **Criar um Contêiner**.

    ![Detalhes da conta de armazenamento](./media/freebsd-create-upload-vhd/storageaccount_container.png)
8. Em Olá **nome** , digite um nome para seu contêiner. Em seguida, no hello **acesso** menu suspenso, selecione o tipo de política de acesso desejado.

    ![Nome do contêiner](./media/freebsd-create-upload-vhd/storageaccount_containervalues.png)

   > [!NOTE]
   > Por padrão, o contêiner de saudação é privado e só pode ser acessado pelo proprietário da conta hello. tooallow acesso de leitura público toohello blobs no contêiner de hello, mas não as propriedades de contêiner toohello e metadados, usam Olá **Blob público** opção. acesso de leitura público completo tooallow para hello contêiner e blobs, use Olá **contêiner público** opção.
   >
   >

## <a name="step-3-prepare-hello-connection-tooazure"></a>Etapa 3: Preparar Olá conexão tooAzure
Antes de carregar um arquivo. vhd, é necessário tooestablish uma conexão segura entre o computador e sua assinatura do Azure. Você pode usar o método do hello Azure Active Directory (AD do Azure) ou Olá certificado método toodo-lo.

### <a name="use-hello-azure-ad-method-tooupload-a-vhd-file"></a>Usar tooupload de método de saudação do AD do Azure um arquivo. vhd
1. Console do Azure PowerShell Olá aberto.
2. Digite hello comando a seguir:  
    `Add-AzureAccount`

    Esse comando abre uma janela de entrada para que você possa entrar com sua conta corporativa ou de estudante.

    ![Janela do PowerShell](./media/freebsd-create-upload-vhd/add_azureaccount.png)
3. O Azure autentica e salva informações de credencial de saudação. Fecha a janela de saudação.

### <a name="use-hello-certificate-method-tooupload-a-vhd-file"></a>Usar tooupload de método de certificado Olá um arquivo. vhd
1. Console do Azure PowerShell Olá aberto.
2. Digite: `Get-AzurePublishSettingsFile`.
3. Uma janela do navegador é aberta e solicita que você toodownload Olá arquivo. publishsettings. Esse arquivo contém informações e um certificado para sua assinatura do Azure.

    ![Procurar página de download](./media/freebsd-create-upload-vhd/Browser_download_GetPublishSettingsFile.png)
4. Salve o arquivo. publishsettings de saudação.
5. Tipo: `Import-AzurePublishSettingsFile <PathToFile>`, onde `<PathToFile>` é o arquivo. publishsettings do hello caminho completo toohello.

   Para obter mais informações, consulte [Introdução aos cmdlets do Azure](http://msdn.microsoft.com/library/windowsazure/jj554332.aspx).

   Para obter mais informações sobre como instalar e configurar o PowerShell, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).

## <a name="step-4-upload-hello-vhd-file"></a>Etapa 4: Carregar o arquivo. vhd de saudação
Quando você carregar o arquivo. vhd de saudação, você pode colocá-lo em qualquer lugar dentro de seu armazenamento de Blob. Estes são alguns termos que você usará ao carregar o arquivo hello:

* **BlobStorageURL** é URL Olá Olá conta de armazenamento que você criou na etapa 2.
* **YourImagesFolder** é o contêiner Olá no armazenamento de Blob onde você deseja toostore suas imagens.
* **VHDName** é Olá rótulo que aparece no hello tooidentify de portal clássico do Azure saudação do disco rígido virtual.
* **PathToVHDFile** é o caminho completo de saudação e o nome do arquivo. vhd de saudação.

Na janela do PowerShell do Azure de Olá usado na etapa anterior hello, digite:

        Add-AzureVhd -Destination "<BlobStorageURL>/<YourImagesFolder>/<VHDName>.vhd" -LocalFilePath <PathToVHDFile>

## <a name="step-5-create-a-vm-with-hello-uploaded-vhd-file"></a>Etapa 5: Criar uma VM com o arquivo. vhd carregado de saudação
Depois de carregar o arquivo. vhd de hello, você pode adicioná-lo como uma lista de toohello de imagem de imagens personalizadas que são associados a sua assinatura e criar uma máquina virtual com esta imagem personalizada.

1. Na janela do PowerShell do Azure de Olá usado na etapa anterior hello, digite:

        Add-AzureVMImage -ImageName <Your Image's Name> -MediaLocation <location of hello VHD> -OS <Type of hello OS on hello VHD>

   > [!NOTE]
   > Use o Linux como tipo de SO hello. versão do Hello atual do PowerShell do Azure aceita apenas "Linux" ou "Windows" como um parâmetro.
   >
   >
2. Depois de concluir as etapas anteriores hello, nova imagem de saudação está listada quando você escolhe Olá **imagens** guia Olá portal clássico do Azure.  

    ![Escolher uma imagem](./media/freebsd-create-upload-vhd/addfreebsdimage.png)
3. Crie uma máquina virtual da Galeria de saudação. Essa nova imagem agora está disponível em **Minhas imagens**.
4. Selecione a nova imagem de saudação. Em seguida, percorra Olá solicita tooset um nome de host, senha, chave SSH e assim por diante.

    ![Imagem personalizada](./media/freebsd-create-upload-vhd/createfreebsdimageinazure.png)
5. Depois de concluir o provisionamento de saudação, você verá seu FreeBSD VM em execução no Azure.

    ![Imagem do FreeBSD no azure](./media/freebsd-create-upload-vhd/freebsdimageinazure.png)
