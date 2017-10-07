---
title: "aaaInstall atualização 0,5 na matriz Virtual StorSimple | Microsoft Docs"
description: "Descreve como tooapply toouse Olá matriz Virtual StorSimple web UI atualizações usando Olá método hotfix e o portal do Azure"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/10/2017
ms.author: alkohli
ms.openlocfilehash: c38daa85daa0086e67cf0206d76cb19d9c8b21b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-05-on-your-storsimple-virtual-array"></a>Instalar a Atualização 0.5 em sua StorSimple Virtual Array

## <a name="overview"></a>Visão geral

Este artigo descreve Olá de etapas necessárias tooinstall atualização 0,5 em sua matriz Virtual StorSimple através da interface do usuário da web local hello e Olá portal do Azure. Você precisa de tookeep de hotfixes ou atualizações de software tooapply sua matriz Virtual StorSimple atualizado.

Antes de aplicar uma atualização, é recomendável colocar Olá volumes ou compartilhamentos offline Olá hospedam primeiro e hello, em seguida, o dispositivo. Isso minimiza a possibilidade de dados corrompidos. Depois Olá volumes ou compartilhamentos estiverem offline, você deve fazer backup do dispositivo Olá manual.

> [!IMPORTANT]
> - Atualização de 0,5 corresponde muito**10.0.10290.0** versão do software em seu dispositivo. Para obter informações sobre o que há de novo nesta atualização, acesse muito[notas de versão de atualização 0,5](storsimple-virtual-array-update-05-release-notes.md).
>
> - Se você estiver executando a atualização 0,2 ou posterior, recomendamos que você instalar atualizações de saudação via Olá portal do Azure. Se você estiver executando a atualização 0,1 ou versões de software GA, você deverá usar o método de hotfix do hello via tooinstall da interface do usuário da web local Olá atualização 0,5.
>
> - Tenha em mente que instalar uma atualização ou um hotfix reinicia seu dispositivo. Considerando que Olá matriz Virtual StorSimple é um dispositivo de nó único, qualquer e/s em andamento será interrompido e o dispositivo apresenta o tempo de inatividade.

## <a name="use-hello-azure-portal"></a>Use Olá portal do Azure

Se executar o Update 0.2 e posterior, recomendamos que você instale atualizações por meio de saudação portal do Azure. requer o procedimento portal Olá Olá usuário tooscan, baixar e instalar atualizações de saudação. Esse procedimento utiliza toocomplete cerca de 7 minutos. Executar o seguinte Olá etapas tooinstall Olá atualização ou hotfix.

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal-04.md)]

Depois Olá a instalação estiver concluída, vá tooyour serviço do Gerenciador de dispositivos do StorSimple. Selecione **dispositivos** e selecione e clique em dispositivo Olá acabou de ser atualizado. Vá muito**Configurações > Gerenciar > atualizações de dispositivo**. Olá exibido software versão deve ser **10.0.10290.0**.

## <a name="use-hello-local-web-ui"></a>Use a interface da web local Olá

Há duas etapas ao usar a interface da web local hello:

* Baixar atualização hello ou hotfix Olá
* Instalação da atualização de saudação ou hotfix Olá

### <a name="download-hello-update-or-hello-hotfix"></a>Baixar atualização hello ou hotfix Olá

Execute Olá após atualização de software etapas toodownload Olá Olá catálogo do Microsoft Update.

#### <a name="toodownload-hello-update-or-hello-hotfix"></a>hotfix de atualização ou Olá Olá toodownload

1. Inicie o Internet Explorer e navegue muito[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).

2. Se for a primeira vez usando Olá catálogo do Microsoft Update neste computador, clique em **instalar** quando tooinstall solicitada Olá complemento do catálogo do Microsoft Update.

3. Na caixa de pesquisa de saudação do hello catálogo do Microsoft Update, insira o número de Base de dados de Conhecimento (KB) de Olá Olá hotfix que você deseja toodownload. Digite **4021576** para a Atualização 0.5 e clique em **Pesquisar**.
   
    Olá hotfix listagem aparece, por exemplo, **StorSimple Virtual Array atualização 0,5**.
   
    ![Pesquisar o catálogo](./media/storsimple-virtual-array-install-update-05/download1.png)

4. Clique em **Download**. 

5. Você deverá ver dois toodownload de arquivos, um *. msu* e um *. cab* arquivo. Baixe cada um desses tooa da pasta de arquivos. pasta Olá também pode ser copiados tooa compartilhamento de rede que seja acessível a partir do dispositivo de saudação.

6. Abra a pasta de saudação onde Olá arquivos estão localizados.
    ![Arquivos de pacote de saudação](./media/storsimple-virtual-array-install-update-05/update05folder.png)

    Você verá:
    -  Um arquivo do Pacote Autônomo do Microsoft Update `WindowsTH-KB3011067-x64`. Esse arquivo é um software de dispositivo de saudação tooupdate usado.
    - Um arquivo do Pacote do Agente de Monitoramento Geneva `GenevaMonitoringAgentPackageInstaller`. Esse arquivo é o agente de serviço (MDS) tooupdate usado Olá monitoramento e diagnóstico. Clique duas vezes no arquivo cab de saudação. Um .msi é exibido. Arquivo hello Select, com o botão direito e, em seguida, **extrair** arquivo hello. Você usará Olá _. msi_ agente de saudação do arquivo tooupdate.

        ![Extraia o arquivo de Atualização do Agente de MDS](./media/storsimple-virtual-array-install-update-05/extract-geneva-monitoring-agent-installer.png)
        
    

### <a name="install-hello-update-or-hello-hotfix"></a>Instalação da atualização de saudação ou hotfix Olá

Instalação de atualização ou hotfix toohello anterior, verifique se você tem Olá atualização ou hotfix Olá baixado localmente no seu host ou acessível por meio de um compartilhamento de rede.

Usar atualizações de tooinstall este método em um dispositivo que executa o GA ou 0,1 versões de software de atualização. Esse procedimento leva menos de 2 minutos toocomplete. Executar o seguinte Olá etapas tooinstall Olá atualização ou hotfix.

#### <a name="tooinstall-hello-update-or-hello-hotfix"></a>tooinstall Olá atualização ou hotfix de Olá

1. Olá interface da web local, vá muito**manutenção** > **atualização de Software**.
   
    ![atualizar dispositivo](./media/storsimple-virtual-array-install-update-05/update1m.png)

2. Em **caminho do arquivo de atualização**, insira o nome do arquivo hello para atualização de saudação ou Olá hotfix. Você também pode procurar o arquivo de instalação de atualização ou hotfix toohello se colocado em um compartilhamento de rede. Clique em **Aplicar**.
   
    ![atualizar dispositivo](./media/storsimple-virtual-array-install-update-05/update2m.png)

3. Será exibido um aviso. Fornecido isso é um dispositivo de nó único, depois Olá atualização seja aplicada, Olá dispositivo for reiniciado, e não há tempo de inatividade. Clique o ícone de verificação de saudação.
   
   ![atualizar dispositivo](./media/storsimple-virtual-array-install-update-05/update3m.png)

4. Inicia a atualização de saudação. Depois que o dispositivo Olá foi atualizado com êxito, ele será reiniciado. Olá interface de usuário local não está acessível durante esse período.
   
    ![atualizar dispositivo](./media/storsimple-virtual-array-install-update-05/update5m.png)

5. Após a conclusão da reinicialização hello, você será direcionado toohello **entrar** página. tooverify Olá dispositivo atualizado, na interface do usuário da web local Olá ir muito**manutenção** > **atualização de Software**. Olá exibido software versão deve ser **10.0.0.0.0.10290.0** para atualização de 0,5.
   
   > [!NOTE]
   > Estamos versões de software de saudação de relatório de forma ligeiramente diferente na interface da web local hello e Olá portal do Azure. Por exemplo, Olá relatórios de interface do usuário da web local **10.0.0.0.0.10290** e Olá relatórios portais do Azure **10.0.10290.0** para Olá mesma versão.
   
    ![atualizar dispositivo](./media/storsimple-virtual-array-install-update-05/update6m.png)

6. Olá próxima etapa é o agente do tooupdate Olá MDS. Em Olá **atualização de Software** página, ir toohello **caminho do arquivo de atualização** e procurar toohello `GenevaMonitoringAgentPackageInstaller.msi` arquivo. Repita as etapas de 2 a 4. Depois de matriz virtual Olá for reiniciado, entre na interface do usuário da web local hello.

Olá atualização agora está concluída.

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre a [administração de sua StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).

