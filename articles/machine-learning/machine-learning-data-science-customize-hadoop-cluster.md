---
title: "clusters de aaaCustomize Hadoop para Olá processo de ciência de dados do Team | Microsoft Docs"
description: "Módulos de Python populares disponibilizados em clusters do Hadoop do Azure HDInsight personalizados."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 0c115dca-2565-4e7a-9536-6002af5c786a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: e192542dd39f71bccbb5163382b4050d0f12ad95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-azure-hdinsight-hadoop-clusters-for-hello-team-data-science-process"></a>Personalizar os clusters de Hadoop de HDInsight do Azure para Olá processo de ciência de dados de equipe
Este artigo descreve como toocustomize uma HDInsight Hadoop cluster instalando Anaconda de 64 bits (Python 2.7) em cada nó ao cluster Olá é provisionado como um serviço HDInsight. Ele também mostra como tooaccess Olá cluster do nó principal toosubmit trabalhos personalizados toohello. Essa personalização faz muitos módulos Python populares, que são incluídos no Anaconda, projetado definidas UDFs (funções) que estão convenientemente disponíveis para uso em usuário tooprocess registros de Hive no cluster hello. Para obter instruções sobre procedimentos Olá usadas neste cenário, consulte [como consultas de Hive toosubmit](machine-learning-data-science-move-hive-tables.md#submit).

menu a seguir Hello links tootopics que descrevem como tooset backup Olá vários ambientes de ciência de dados usado pelo Olá [processo de ciência de dados da equipe (TDSP)](data-science-process-overview.md).

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

## <a name="customize"></a>Personalizar o cluster do Hadoop do Azure HDInsight
Iniciar toocreate um cluster HDInsight Hadoop personalizado, efetuando logon muito[**portal clássico do Azure**](https://manage.windowsazure.com/), clique em **novo** no hello esquerda inferior do canto e, em seguida, selecione os serviços de dados -> HDINSIGHT -> **criação personalizada** toobring backup Olá **detalhes do Cluster** janela. 

![Criar espaço de trabalho](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

Nome de saudação do hello cluster toobe criado na página de configuração 1 e aceitar valores padrão para Olá outros campos. Clique em Olá seta toogo toohello próxima página de configuração. 

![Criar espaço de trabalho](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

Na página de configuração 2, insira o número de saudação do **nós de dados**, selecione Olá **região/rede VIRTUAL**e selecione tamanhos Olá Olá **nó de cabeçalho** e hello **o nó de dados**. Clique em Olá seta toogo toohello próxima página de configuração.

> [!NOTE]
> Olá **região/rede VIRTUAL** tem toobe Olá mesmo como região Olá Olá da conta de armazenamento que será usado para o cluster HDInsight Hadoop de saudação do toobe. Caso contrário, na página de configuração quarta Olá, conta de armazenamento de saudação não serão exibidos na lista suspensa de saudação do **nome da conta**.
> 
> 

![Criar espaço de trabalho](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img3.png)

Na página de configuração 3, forneça um nome de usuário e senha para Olá cluster HDInsight Hadoop. **Não** Olá selecione *Enter Olá Hive/Oozie Metastore*. Em seguida, clique em Olá seta toogo toohello próxima página de configuração. 

![Criar espaço de trabalho](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img4.png)

Na página de configuração 4, especifique o nome de conta de armazenamento hello, contêiner de padrão de saudação do hello cluster HDInsight Hadoop. Se você selecionar *criar contêiner padrão* em Olá **CONTÊINER padrão** lista suspensa, um contêiner com hello mesmo nome como Olá cluster será criado. Clique em Olá seta toogo toohello última página de configuração.

![Criar espaço de trabalho](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img5.png)

No final da saudação **ações de Script** página de configuração, clique em **Adicionar ação de script** botão e, em seguida, preencha os campos de texto de saudação com hello valores a seguir.

* **NOME** -qualquer cadeia de caracteres como nome hello dessa ação de script
* **TIPO DE NÓ** – selecione **Todos os nós**
* **URI do SCRIPT** - *http://getgoing.blob.core.windows.net/publicscripts/Azure_HDI_Setup_Windows.ps1* 
  * *publicscripts* é um contêiner público na conta de armazenamento Olá 
  * *getgoing* usamos tooshare PowerShell script arquivos toofacilitate trabalho dos usuários no Azure
* **PARÂMETROS** - (deixe em branco)

Por fim, clique em Olá marca de seleção toostart Olá a criação do cluster de Hadoop de HDInsight Olá personalizado. 

![Criar espaço de trabalho](./media/machine-learning-data-science-customize-hadoop-cluster/script-actions.png)

## <a name="headnode"></a>Olá acesso cabeçotes de nó de Hadoop Cluster
Você deve habilitar o cluster de Hadoop toohello acesso remoto no Azure antes de poder acessar o nó principal de saudação do cluster de Hadoop de saudação via RDP. 

1. Faça logon no toohello [ **portal clássico do Azure**](https://manage.windowsazure.com/), selecione **HDInsight** Olá esquerda, selecione o cluster Hadoop Olá lista de clusters, clique em Olá  **CONFIGURAÇÃO** guia e, em seguida, clique em Olá **habilitar remoto** ícone final Olá Olá página.
   
    ![Criar espaço de trabalho](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-1.png)
2. Em Olá **configurar área de trabalho remota** janela, insira hello nome de usuário e os campos de senha e selecione a data de validade Olá para acesso remoto. Clique em Olá marca de seleção tooenable Olá acesso remoto toohello nó principal do cluster de Hadoop hello.
   
    ![Criar espaço de trabalho](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-2.png)

> [!NOTE]
> nome de usuário de saudação e a senha para acesso remoto Olá não são Olá nome usuário e senha que você usa ao criar o cluster de Hadoop hello. Eles são um conjunto separado de credenciais. Além disso, a data de expiração de saudação do acesso remoto Olá tem toobe dentro de 7 dias de saudação data atual.
> 
> 

Após a habilitação do acesso remoto, clique em **conectar** final Olá Olá página tooremote no nó principal hello. Logon toohello o nó principal do cluster de Hadoop Olá inserindo credenciais de saudação do usuário de acesso remoto de saudação que você especificou anteriormente.

![Criar espaço de trabalho](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-3.png)

Olá próximas etapas no hello avançado do processo de análise são mapeadas em Olá [processo de ciência de dados da equipe (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) e podem incluir etapas para movem dados para HDInsight, em seguida, processam e exemplo-lo na preparação para aprender com dados saudação com o aprendizado de máquina do Azure.

Consulte [como consultas de Hive toosubmit](machine-learning-data-science-move-hive-tables.md#submit) para obter instruções sobre como tooaccess Olá módulos Python que estão incluídos no Anaconda do nó principal de saudação do cluster de saudação em funções definidas pelo usuário (UDFs) que são usados tooprocess Hive registros armazenados no cluster de saudação.

