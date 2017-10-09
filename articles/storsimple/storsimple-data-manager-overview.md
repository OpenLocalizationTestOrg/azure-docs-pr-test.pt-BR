---
title: "Visão geral do Gerenciador de dados do Azure StorSimple aaaMicrosoft | Microsoft Docs"
description: "Fornece uma visão geral da saudação serviço StorSimple Manager de dados (visualização particular)"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/22/2016
ms.author: vidarmsft
ms.openlocfilehash: 5d29f7d26be9f2b36857526bdea770d991cece6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-data-manager-overview-private-preview"></a>Visão geral do Gerenciador de Dados do StorSimple (Visualização particular)

## <a name="overview"></a>Visão geral

Microsoft Azure StorSimple é uma solução de armazenamento de nuvem híbrida endereços Olá complexidades de comumente associadas a compartilhamentos de arquivos de dados não estruturados. StorSimple usa armazenamento em nuvem como uma extensão da saudação solução local e automaticamente dados de camadas de armazenamento de local de saudação e armazenamento em nuvem. Integra a proteção de dados local e instantâneos em nuvem, que elimina a necessidade de saudação de uma infraestrutura de armazenamento amplas. Arquivamento e recuperação de desastres também é consistente com a nuvem Olá atuando como um local externo.

Olá data transformation Services que estamos introduzindo neste documento, permite que você tooseamlessly acesso Olá StorSimple dados na nuvem hello. Esse serviço fornece dados de tooextract APIs do StorSimple e apresentá-lo tooother Azure serviços em formatos que podem ser consumidos imediatamente. formatos de saudação com suporte nesta visualização são blobs do Azure e ativos de serviços de mídia do Azure. Essa transformação permite que você tooeasily durante a transmissão os serviços, como serviços de mídia do Azure, HDInsight do Azure, aprendizado de máquina do Azure e pesquisa do Azure dados toooperate no dispositivo de local de série StorSimple 8000.

Veja abaixo um diagrama de bloco de alto nível que ilustra isso.

![Diagrama de alto nível](./media//storsimple-data-manager-overview/high-level-diagram.png)

Este documento explica como você pode se inscrever para uma visualização particular desse serviço. Ele também explica como você pode usar estes aplicativos de toowrite de serviço que usam dados do StorSimple e outros serviços do Azure na nuvem hello.

## <a name="sign-up-for-data-manager-preview"></a>Inscrever-se para a visualização do Gerenciador de Dados
Antes de se inscrever para o serviço de Gerenciador de dados hello, examine Olá pré-requisitos a seguir.

### <a name="prerequisites"></a>Pré-requisitos

Este exercício supõe que você tem
* uma assinatura ativa do Azure.
* acesso tooa registrado o dispositivo da série 8000 StorSimple
* todos os Olá chaves associadas ao dispositivo da série StorSimple 8000 do hello.

### <a name="sign-up"></a>Inscrição

Olá StorSimple Data Manager está no modo de visualização particular. Execute Olá toosign etapas para uma visualização privada do serviço a seguir:

1.  Faça logon no hello portal do Azure com extensão de Gerenciador de dados StorSimple Olá em: [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager). Use o toolog as credenciais do Azure no.

2.  Clique em Olá  **+**  ícone toocreate um serviço. Clique em **armazenamento** e, em seguida, clique em **consulte todos os** na folha de saudação que é aberta.

    ![Ícone Pesquisar no Gerenciador de Dados do StorSimple](./media/storsimple-data-manager-overview/search-data-manager-icon.png)

3. Você verá o ícone do Gerenciador de dados StorSimple Olá.

    ![Ícone Selecionar Gerenciador de Dados do StorSimple](./media/storsimple-data-manager-overview/select-data-manager-icon.png)

4. Clique no ícone Gerenciador de Dados do StorSimple e clique em **Criar**. Escolha a assinatura de saudação que você deseja tooenable para visualização privada hello e, em seguida, clique em **me inscrever!**

    ![Inscrever-me](./media/storsimple-data-manager-overview/sign-me-up.png)

5. Isso envia uma solicitação tooonboard você. Realizaremos sua integração assim que possível. Após a habilitação de sua assinatura, você poderá criar um serviço de Gerenciador de Dados do StorSimple.

6. tooeasily acessar o serviço de Gerenciador de dados StorSimple hello, clique em Olá ícone de estrela toopin-tooyour Favoritos.

    ![Acessar o Gerenciador de Dados do StorSimple](./media/storsimple-data-manager-overview/access-data-managers.png)


## <a name="next-steps"></a>Próximas etapas

[Usar os dados de interface de usuário de Gerenciador de dados StorSimple tootransform](storsimple-data-manager-ui.md).
