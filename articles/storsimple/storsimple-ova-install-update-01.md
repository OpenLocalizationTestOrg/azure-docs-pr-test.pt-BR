---
title: "aaaInstall atualizações em uma matriz Virtual StorSimple | Microsoft Docs"
description: "Descreve como toouse Olá matriz Virtual StorSimple web da interface do usuário tooapply atualizações usando o método de portal e o hotfix hello"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 7f1b1e7d-04d0-4ca2-9dbb-77077ff19bb9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 09/07/2016
ms.author: alkohli
ms.openlocfilehash: 10af0f52abb75a5b41562704194157f0d35710bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-updates-on-your-storsimple-virtual-array"></a>Instalar Atualizações em seu StorSimple Virtual Array
## <a name="overview"></a>Visão geral
Este artigo descreve Olá etapas tooinstall necessárias atualizações em sua matriz Virtual StorSimple através da interface do usuário da web local hello e Olá portal clássico do Azure. Você precisa de tookeep de hotfixes ou atualizações de software tooapply sua matriz Virtual StorSimple atualizado. 

Tenha em mente que instalar uma atualização ou um hotfix reinicia seu dispositivo. Considerando que Olá matriz Virtual StorSimple é um dispositivo de nó único, qualquer e/s em andamento será interrompido e o dispositivo apresenta o tempo de inatividade. 

Antes de aplicar uma atualização, é recomendável colocar Olá volumes ou compartilhamentos offline Olá hospedam primeiro e hello, em seguida, o dispositivo. Isso minimiza a possibilidade de dados corrompidos.

> [!IMPORTANT]
> Se você estiver executando a atualização 0,1 ou versões de software GA, você deverá usar o método de hotfix do hello via Olá web local da interface do usuário tooinstall atualização 0.3. Se você estiver executando a atualização 0,2, recomendamos que você instale atualizações Olá via Olá portal clássico do Azure.
> 
> 

## <a name="use-hello-local-web-ui"></a>Use a interface da web local Olá
Há duas etapas ao usar a interface da web local hello:

* Baixar atualização hello ou hotfix Olá
* Instalação da atualização de saudação ou hotfix Olá

### <a name="download-hello-update-or-hello-hotfix"></a>Baixar atualização hello ou hotfix Olá
Execute Olá após atualização de software etapas toodownload Olá Olá catálogo do Microsoft Update.

#### <a name="toodownload-hello-update-or-hello-hotfix"></a>hotfix de atualização ou Olá Olá toodownload
1. Inicie o Internet Explorer e navegue muito[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).
2. Se for a primeira vez usando Olá catálogo do Microsoft Update neste computador, clique em **instalar** quando tooinstall solicitada Olá complemento do catálogo do Microsoft Update.
3. Na caixa de pesquisa de saudação do hello catálogo do Microsoft Update, insira o número de Base de dados de Conhecimento (KB) de Olá Olá hotfix que você deseja toodownload. Digite **3182061** para a Atualização 0.3 e clique em **Pesquisar**.
   
    Olá hotfix listagem aparece, por exemplo, **StorSimple Virtual Array atualização 0.3**.
   
    ![Pesquisar o catálogo](./media/storsimple-ova-install-update-01/download1.png)
4. Clique em **Adicionar**. atualização de saudação é adicionada toohello carrinho.
5. Clique em **Exibir carrinho**.
6. Clique em **Download**. Especifique ou **procurar** tooa local local onde você deseja Olá downloads tooappear. Olá as atualizações são baixadas toohello local especificado e colocada em uma subpasta com mesmo nome como atualização de saudação do hello. pasta Olá também pode ser copiados tooa compartilhamento de rede que seja acessível a partir do dispositivo de saudação.
7. Abra Olá copiou a pasta, você deve ver um arquivo de pacote do Microsoft Update autônomo `WindowsTH-KB3011067-x64`. Esse arquivo é usado tooinstall Olá atualização ou hotfix.

### <a name="install-hello-update-or-hello-hotfix"></a>Instalação da atualização de saudação ou hotfix Olá
Instalação de atualização ou hotfix toohello anterior, verifique se você tem Olá atualização ou hotfix Olá baixado localmente no seu host ou acessível por meio de um compartilhamento de rede. 

Usar atualizações de tooinstall este método em um dispositivo que executa o GA ou 0,1 versões de software de atualização. Esse procedimento leva menos de 2 minutos toocomplete. Executar o seguinte Olá etapas tooinstall Olá atualização ou hotfix.

#### <a name="tooinstall-hello-update-or-hello-hotfix"></a>tooinstall Olá atualização ou hotfix de Olá
1. Olá interface da web local, vá muito**manutenção** > **atualização de Software**.
   
    ![atualizar dispositivo](./media/storsimple-ova-install-update-01/update1m.png)
2. Em **caminho do arquivo de atualização**, insira o nome do arquivo hello para atualização de saudação ou Olá hotfix. Você também pode procurar o arquivo de instalação de atualização ou hotfix toohello se colocado em um compartilhamento de rede. Clique em **Aplicar**.
   
    ![atualizar dispositivo](./media/storsimple-ova-install-update-01/update2m.png)
3. Será exibido um aviso. Fornecido isso é um dispositivo de nó único, depois Olá atualização seja aplicada, Olá dispositivo for reiniciado, e não há tempo de inatividade. Clique o ícone de verificação de saudação.
   
   ![atualizar dispositivo](./media/storsimple-ova-install-update-01/update3m.png)
4. Inicia a atualização de saudação. Depois que o dispositivo Olá foi atualizado com êxito, ele será reiniciado. Olá interface de usuário local não está acessível durante esse período.
   
    ![atualizar dispositivo](./media/storsimple-ova-install-update-01/update5m.png)
5. Após a conclusão da reinicialização hello, você será direcionado toohello **entrar** página. tooverify Olá dispositivo atualizado, na interface do usuário da web local Olá ir muito**manutenção** > **atualização de Software**. Olá exibido software versão deve ser **10.0.0.0.0.10288.0** para atualização 0.3.
   
   > [!NOTE]
   > Estamos versões de software de saudação de relatório de forma ligeiramente diferente na interface da web local hello e Olá portal clássico do Azure. Por exemplo, Olá relatórios de interface do usuário da web local **10.0.0.0.0.10288** e Olá relatórios de portal clássicos do Azure **10.0.10288.0** para Olá mesma versão. 
   > 
   > 
   
    ![atualizar dispositivo](./media/storsimple-ova-install-update-01/update6m.png)

## <a name="use-hello-azure-classic-portal"></a>Use Olá portal clássico do Azure
Se executar o Update 0,2, recomendamos que você instale atualizações por meio de saudação portal clássico do Azure. requer o procedimento portal Olá Olá usuário tooscan, baixar e instalar atualizações de saudação. Esse procedimento utiliza toocomplete cerca de 7 minutos. Executar o seguinte Olá etapas tooinstall Olá atualização ou hotfix.

[!INCLUDE [storsimple-ova-install-update-via-portal](../../includes/storsimple-ova-install-update-via-portal.md)]

Olá após a instalação for concluída (conforme indicado pelo status do trabalho em 100%), vá muito**dispositivos > manutenção > atualizações de Software**. versão do software Olá exibido deve ser 10.0.10288.0.

![atualizar dispositivo](./media/storsimple-ova-install-update-01/azupdate12m.png)

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre a [administração de sua StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).

