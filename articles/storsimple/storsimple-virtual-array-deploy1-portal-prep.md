---
title: "preparação aaaPortal para matriz Virtual StorSimple | Microsoft Docs"
description: "Toodeploy primeiro tutorial matriz virtual StorSimple envolve preparar Olá portal do Azure"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 68a4cfd3-94c9-46cb-805c-46217290ce02
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5332b235e7296a9274f2e7dafcdf72f4b9cdadf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---prepare-hello-azure-portal"></a>Implantar StorSimple Virtual Array - preparar Olá portal do Azure

![](./media/storsimple-virtual-array-deploy1-portal-prep/getstarted4.png)
## <a name="overview"></a>Visão geral

Isso é Olá primeiro artigo Olá série de tutoriais de implantação necessários toocompletely implantar sua matriz virtual como um servidor de arquivos ou um servidor iSCSI usando o modelo do Gerenciador de recursos de saudação. Este artigo descreve Olá preparação necessários toocreate e configurar o Gerenciador de dispositivos do StorSimple serviço anterior tooprovisioning uma matriz virtual. Este artigo também vincula out pré-requisitos de configuração e a lista de verificação de configuração de implantação do tooa.

Você precisa de privilégios toocomplete Olá a instalação e configuração do processo de administrador. É recomendável que você examine a lista de verificação de configuração de implantação Olá antes de começar. preparação do portal Olá leva menos de 10 minutos.

informações de saudação publicadas neste artigo se aplicam a implantação de toohello de matrizes Virtual do StorSimple em Olá portal do Azure e a nuvem do Microsoft Azure Government.

### <a name="get-started"></a>Introdução
fluxo de trabalho de implantação de Olá consiste em preparar portal hello, provisionamento de uma matriz virtual em seu ambiente virtualizado e concluir a instalação de saudação. tooget iniciado com a implantação de matriz Virtual StorSimple hello como um servidor de arquivos ou um servidor iSCSI, é necessário toohello toorefer tabulados recursos a seguir.

#### <a name="deployment-articles"></a>Artigos sobre implantação

toodeploy sua matriz Virtual StorSimple, consulte toohello artigos Olá prescrita sequência a seguir.

| **#** | **Nesta etapa** | **Para fazer isso...** | **Use estes documentos.** |
| --- | --- | --- | --- |
| 1. |**Configurar Olá portal do Azure** |Criar e configurar o Gerenciador de dispositivos do StorSimple serviço anterior tooprovisioning uma matriz Virtual StorSimple. |[Preparar o portal de saudação](storsimple-virtual-array-deploy1-portal-prep.md) |
| 2. |**Provisionar Olá Virtual Array** |Para o Hyper-V, provisionar e conecte-se tooa matriz Virtual do StorSimple em um sistema de host executando o Hyper-V no Windows Server 2012 R2, Windows Server 2012 ou Windows Server 2008 R2. <br></br> <br></br> Para VMware, provisionar e conecte-se tooa matriz Virtual do StorSimple em um sistema de host executando o VMware ESXi 5.5 e acima.<br></br> |[Provisionar uma matriz virtual no Hyper-V](storsimple-virtual-array-deploy2-provision-hyperv.md) <br></br> <br></br> [Provisionar uma matriz virtual no VMware](storsimple-virtual-array-deploy2-provision-vmware.md) |
| 3. |**Configurar Olá Virtual Array** |Para o servidor de arquivos, executar a configuração inicial, registrar o servidor de arquivos do StorSimple e concluir a configuração de dispositivo de saudação. Em seguida, é possível provisionar compartilhamentos SMB. <br></br> <br></br> Para o servidor iSCSI, execute a instalação inicial, registrar seu servidor do StorSimple iSCSI e concluir a configuração de dispositivo de saudação. Em seguida, é possível provisionar volumes iSCSI. |[Configurar a matriz virtual como um servidor de arquivos](storsimple-virtual-array-deploy3-fs-setup.md)<br></br> <br></br>[Configurar a matriz virtual como um servidor iSCSI](storsimple-virtual-array-deploy3-iscsi-setup.md) |

Agora você pode começar tooset backup Olá portal do Azure.

## <a name="configuration-checklist"></a>Lista de verificação da configuração

lista de verificação de configuração de saudação descreve informações Olá necessárias toocollect antes de configurar o software Olá no StorSimple Virtual Array. Preparar essas informações à frente de tempo ajudam a simplificar o processo de saudação do dispositivo do StorSimple Olá em seu ambiente de implantação. Dependendo se sua matriz Virtual StorSimple é implantado como um servidor de arquivos ou um servidor iSCSI, você precisa de um dos Olá listas de verificação a seguir.

* Baixar Olá [StorSimple Virtual Array arquivo Server Configuration Checklist](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayFileServerConfigurationChecklist.pdf).
* Baixar Olá [matriz Virtual StorSimple iSCSI lista de verificação de configuração de servidor](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayiSCSIServerConfigurationChecklist.pdf).

## <a name="prerequisites"></a>Pré-requisitos

Aqui você pode encontrar os pré-requisitos de configuração de saudação para seu serviço de Gerenciador de dispositivos do StorSimple, sua matriz Virtual do StorSimple e rede de datacenter hello.

### <a name="for-hello-storsimple-device-manager-service"></a>Para Olá serviço do Gerenciador de dispositivos de StorSimple

Antes de começar, verifique se:

* Você tem sua conta da Microsoft com credenciais de acesso.
* Você tem sua conta de armazenamento do Microsoft Azure com credenciais de acesso.
* Sua assinatura do Microsoft Azure deve estar habilitada para o serviço Gerenciador de Dispositivos StorSimple.

### <a name="for-hello-storsimple-virtual-array"></a>Para Olá matriz Virtual StorSimple

Antes de implantar um dispositivo virtual, verifique se:

* Você tem acesso tooa host sistema executando o Hyper-V no Windows Server 2008 R2 ou posterior ou VMware (ESXi 5.5 ou posterior) que pode ser usado tooa Provisione um dispositivo.
* sistema de host de saudação é capaz de toodedicate Olá seguintes recursos tooprovision sua matriz virtual:
  
  * Um mínimo de quatro núcleos.
  * Pelo menos 8 GB de RAM. Se você planejar a matriz de virtual tooconfigure hello como servidor de arquivos, 8 GB dá suporte a arquivos de 2 milhões. Você precisa de 2-4 milhões de arquivos de 16 GB RAM toosupport.
  * Uma interface de rede.
  * Um disco virtual de 500 GB para dados do sistema.

### <a name="for-hello-datacenter-network"></a>Para a rede de datacenter Olá

Antes de começar, verifique se:

* rede de saudação em seu data center é configurada de acordo com os requisitos de rede de saudação para seu dispositivo StorSimple. Para obter mais informações, consulte Olá [requisitos do sistema StorSimple Virtual Array](storsimple-ova-system-requirements.md).
* Sua Matriz Virtual StorSimple tem uma largura de banda de Internet dedicada de 5 Mbps (ou mais) sempre disponível. Essa largura de banda não deve ser compartilhada com outros aplicativos.

## <a name="step-by-step-preparation"></a>Preparação passo a passo

Use Olá seguindo as instruções passo a passo tooprepare seu portal para Olá serviço do Gerenciador de dispositivos do StorSimple.

## <a name="step-1-create-a-new-service"></a>Etapa 1: Criar um novo serviço

Uma única instância de serviço do Gerenciador de dispositivos de StorSimple Olá pode gerenciar várias matrizes de Virtual do StorSimple. Execute Olá etapas toocreate uma instância de serviço do Gerenciador de dispositivos de StorSimple Olá a seguir. Se você tiver um toomanage de serviço existente do Gerenciador de dispositivos de StorSimple suas matrizes de virtuais, ignore esta etapa e vá muito[etapa 2: chave de registro de serviço Get hello](#step-2-get-the-service-registration-key).

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

> [!IMPORTANT]
> Se você não tiver habilitado a criação automática de saudação de uma conta de armazenamento com seu serviço, você precisará toocreate pelo menos uma conta de armazenamento depois que você criou com êxito um serviço.
> 
> * Se você não criou uma conta de armazenamento automaticamente, vá muito[configurar uma nova conta de armazenamento para o serviço de saudação](#optional-step-configure-a-new-storage-account-for-the-service) para obter instruções detalhadas.
> * Se você tiver habilitado a criação automática de uma conta de armazenamento hello, vá muito[etapa 2: chave de registro de serviço Get hello](#step-2-get-the-service-registration-key).
> 
> 

## <a name="step-2-get-hello-service-registration-key"></a>Etapa 2: Obter a chave de registro de serviço Olá

Depois de saudação de serviço do Gerenciador de dispositivos do StorSimple estiver em execução, você precisará chave de registro tooget Olá. Essa chave é usada tooregister e conectar seu dispositivo StorSimple com o serviço de saudação.

Executar Olá etapas Olá [portal do Azure](https://portal.azure.com/).

[!INCLUDE [storsimple-virtual-array-get-service-registration-key](../../includes/storsimple-virtual-array-get-service-registration-key.md)]

> [!NOTE]
> Olá, chave de registro de serviço é usado tooregister todos Olá dispositivos de StorSimple Gerenciador de dispositivos que necessitam de tooregister com o serviço do Gerenciador de dispositivos do StorSimple.
> 
> 

## <a name="step-3-download-hello-virtual-array-image"></a>Etapa 3: Baixar a imagem de matriz virtual Olá

Depois que você tiver a chave de registro de serviço hello, você precisará toodownload Olá matriz virtual apropriada imagem tooprovision uma matriz virtual no sistema host. imagens de matriz virtual Olá são específicas do sistema operacional e podem ser baixadas na página de início rápido de saudação em Olá portal do Azure.

> [!IMPORTANT]
> software de saudação em execução no hello matriz Virtual StorSimple só pode ser usado com Olá serviço do Gerenciador de dispositivos do StorSimple.
> 
> 

Executar Olá etapas Olá [portal do Azure](https://portal.azure.com/).

#### <a name="tooget-hello-virtual-array-image"></a>imagem de matriz virtual Olá tooget

1. O logon no hello [portal do Azure](https://portal.azure.com/). 
2. No portal do Azure de Olá, clique em **procurar > gerenciadores de dispositivos de StorSimple**.
3. Selecione um serviço Gerenciador de Dispositivos StorSimple existente. Em Olá **Gerenciador de dispositivos de StorSimple** folha, clique em **início rápido**. 
4. Clique em Olá link correspondente toohello imagem que você deseja toodownload de saudação Microsoft Download Center. arquivos de imagem de saudação são aproximadamente 4,8 GB.
   
   * VHDX para Hyper-V no Windows Server 2012 e posterior
   * VHD para Hyper-V no Windows Server 2008 R2 e posterior
   * VMDK para VMWare ESXi 5.5 e posterior
5. Baixe e descompacte Olá arquivo tooa unidade local, fazer uma anotação de onde o arquivo descompactado hello está localizado.

## <a name="optional-step-configure-a-new-storage-account-for-hello-service"></a>Etapa opcional: configurar uma nova conta de armazenamento para o serviço de saudação

Esta etapa é opcional e deve ser executada somente se você não tiver habilitado a criação automática de saudação de uma conta de armazenamento com seu serviço.

Se você precisar de uma conta de armazenamento do Azure em uma região diferente de toocreate, consulte [como uma conta de armazenamento do toocreate](../storage/common/storage-create-storage-account.md#create-a-storage-account) para obter instruções passo a passo.

Executar Olá etapas Olá [portal do Azure](https://ms.portal.azure.com/) em Olá Gerenciador de dispositivos do StorSimple serviço página tooadd uma conta de armazenamento do Microsoft Azure.

#### <a name="tooadd-a-storage-account-credential-that-has-hello-same-azure-subscription-as-hello-device-manager-service"></a>tooadd uma credencial da conta de armazenamento tem Olá a mesma assinatura do Azure como serviço de Gerenciador de dispositivos Olá

1. Navegue tooyour serviço do Gerenciador de dispositivos, selecione e clique duas vezes nele. Isso abre o hello **visão geral** folha.
2. Selecione **credenciais da conta de armazenamento** em Olá **configuração** seção.
3. Clique em **Adicionar**.
4. Em Olá **adicionar uma conta de armazenamento** folha, Olá a seguir:
   
    1. Para **Assinatura**, selecione **Atual**.
   
    2. Forneça o nome de saudação da sua conta de armazenamento do Azure.
   
    3. Selecione **habilitar** toocreate um canal seguro para comunicação de rede entre sua nuvem de dispositivo e hello StorSimple. Selecione **Desabilitar** somente se você estiver operando em uma nuvem privada.
   
    4. Clique em **Adicionar**. Você será notificado depois da conta de armazenamento Olá é criada com êxito.<br></br>
   
     ![Adicionar uma credencial de conta de armazenamento existente](./media/storsimple-virtual-array-manage-storage-accounts/ova-add-storageacct.png)

## <a name="next-step"></a>Próxima etapa

Olá próxima etapa é tooprovision uma máquina virtual para sua matriz Virtual StorSimple. Dependendo do seu sistema operacional de host, consulte Olá detalhadas instruções:

* [Provisionar um StorSimple Virtual Array no Hyper-V](storsimple-virtual-array-deploy2-provision-hyperv.md)
* [Provisionar um StorSimple Virtual Array no VMware](storsimple-virtual-array-deploy2-provision-vmware.md)

