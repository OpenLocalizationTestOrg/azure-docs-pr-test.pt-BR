---
title: aplicativos de HDInsight aaaPublish - Azure | Microsoft Docs
description: Saiba como toocreate e publicar aplicativos de HDInsight.
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 14aef891-7a37-4cf1-8f7d-ca923565c783
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 7da0aa53828563e50ef372df901e1ba541fb40be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-hdinsight-applications-into-hello-azure-marketplace"></a>Publicar aplicativos HDInsight em hello Azure Marketplace
Um aplicativo do HDInsight é um aplicativo que os usuários podem instalar em um cluster HDInsight baseado em Linux. Esses aplicativos podem ser desenvolvidos pela Microsoft, por ISVs (fornecedores independentes de software) ou por conta própria. Neste artigo, você aprenderá como toopublish um aplicativo de HDInsight em hello Azure Marketplace.  Para obter informações gerais sobre a publicação em hello Azure Marketplace, consulte [publicar uma oferta toohello Azure Marketplace](../marketplace-publishing/marketplace-publishing-getting-started.md).

Aplicativos de HDInsight usar Olá *Traga sua própria licença (BYOL)* modelo, onde o provedor do aplicativo é responsável por licenciamento tooend-usuários do aplicativo hello e os usuários finais só é cobrado pelo Azure para recursos de saudação eles Crie, como cluster de HDInsight hello e suas VMs/nós. No momento, a cobrança por aplicativo hello em si não é feita por meio do Azure.

Outro artigo relacionado ao aplicativo do HDInsight:

* [Instalar aplicativos de HDInsight](hdinsight-apps-install-applications.md): Saiba como clusters de tooinstall um tooyour de aplicativo do HDInsight.
* [Instalar aplicativos personalizados do HDInsight](hdinsight-apps-install-custom-applications.md): Saiba como tooinstall e testar aplicativos HDInsight personalizados.

## <a name="prerequisites"></a>Pré-requisitos
toosubmit marketplace de toohello seu aplicativo personalizado, você deve ter criado e testado seu aplicativo personalizado. Consulte Olá artigos a seguir:

* [Instalar aplicativos personalizados do HDInsight](hdinsight-apps-install-custom-applications.md): Saiba como tooinstall e testar aplicativos HDInsight personalizados.

Você também deve ter registrado sua conta de desenvolvedor. Consulte [publicar uma oferta toohello Azure Marketplace](../marketplace-publishing/marketplace-publishing-getting-started.md) e [criar uma conta do Microsoft Developer](../marketplace-publishing/marketplace-publishing-accounts-creation-registration.md).

## <a name="define-application"></a>Definir o aplicativo
Há duas etapas envolvidas para publicar aplicativos toohello Azure Marketplace.  Primeiro você define uma **createUiDef.json** tooindicate de arquivo que seu aplicativo de clusters é compatível com; e, em seguida, você publicar o modelo de saudação do hello portal do Azure. Olá seção a seguir é um arquivo de exemplo createUiDef.json.

    {
        "handler": "Microsoft.HDInsight",
        "version": "0.0.1-preview",
        "clusterFilters": {
            "types": ["Hadoop", "HBase", "Storm", "Spark"],
            "tiers": ["Standard", "Premium"],
            "versions": ["3.4"]
        }
    }


| Campo | Descrição | Valores possíveis |
| --- | --- | --- |
| tipos |tipos de cluster de saudação aplicativo hello é compatível com. |Hadoop, HBase, Storm, Spark (ou qualquer combinação destes) |
| camadas |Olá camadas de cluster que o aplicativo hello é compatível com. |Standard, Premium (ou ambos) |
| versões |tipos de cluster do HDInsight Olá Olá aplicativo é compatível com. |3.4 |

## <a name="application-install-script"></a>Script de instalação do aplicativo
Sempre que um aplicativo é instalado em um cluster (um já existente ou um novo), um nó de borda é criado e script de instalação do aplicativo hello é executada nele.
  > [!IMPORTANT]
  > nome de saudação de nomes de script de instalação de aplicativo hello deve ser exclusivo para um determinado cluster com hello formato a seguir.
  > 
  > name": "[concat('hue-install-v0','-' ,uniquestring(‘applicationName’)]"
  > 
  > Observe que existem em nome de script de toohello de três partes:
  > 
  > 1. Um prefixo de nome de script, que deve incluir o nome do aplicativo hello ou um aplicativo de toohello relevantes do nome.
  > 2. Um "-" para facilitar a leitura.
  > 3. Uma função de cadeia de caracteres exclusiva com o nome do aplicativo hello como Olá parâmetro.
  > 
  > Um exemplo é Olá acima acaba ficando: Matiz-install-v0-4wkahss55hlas em Olá persistente a lista de ações de script. Para uma carga JSON de exemplo, consulte [https://raw.githubusercontent.com/hdinsight/Iaas-Applications/master/Hue/azuredeploy.json](https://raw.githubusercontent.com/hdinsight/Iaas-Applications/master/Hue/azuredeploy.json).
  > 
o script de instalação Olá deve ter Olá características a seguir:
1. Certifique-se de que o script hello é idempotente. Várias chamadas toohello script deve produzir Olá mesmo resultado.
2. Olá script deve ser corretamente com controle de versão. Use um local diferente para o script hello quando você estiver atualizando ou testar as alterações para que os clientes que estão tentando aplicativo hello de tooinstall não são afetados. 
3. Adicione scripts de toohello de log adequado em cada ponto. Olá geralmente logs de script é Olá somente modo toodebug problemas de instalação do aplicativo.
4. Certifique-se de chamadas tooexternal serviços ou recursos têm repetições adequadas para que a instalação de saudação não é afetada por problemas de rede transitório.
5. Se o script está iniciando os serviços em nós hello, verifique se serviços Olá são monitorados e configurado toostart automaticamente em caso de reinicializações de nó.

## <a name="package-application"></a>Aplicativo de pacote
Crie um arquivo zip que contém todos os arquivos necessários para instalar os aplicativos do HDInsight. Você precisa Olá arquivo zip em [publicar aplicativo](#publish-application).

* [createUiDefinition.json](#define-application).
* mainTemplate.json. Confira um exemplo em [Instalar aplicativos personalizados do HDInsight](hdinsight-apps-install-custom-applications.md).
* Todos os scripts obrigatórios.

> [!NOTE]
> Olá arquivos de aplicativo (incluindo arquivos de aplicativo web se houver algum) pode estar localizado em qualquer ponto de extremidade publicamente acessível.
> 

## <a name="publish-application"></a>aplicativo Publicar
Execute Olá etapas toopublish um aplicativo de HDInsight a seguir:

1. Logon toohello [portal do Azure publicação](https://publish.windowsazure.com/).
2. Clique em **modelos de solução** de saudação esquerdo toocreate um novo modelo de solução.
3. Digite um título e clique em **Criar um novo modelo de solução**.
4. Clique em **criar Centro de desenvolvimento e junção Olá programa Azure** tooregister sua empresa se você ainda não tiver feito isso.  Confira [Criar uma conta do Microsoft Developer](../marketplace-publishing/marketplace-publishing-accounts-creation-registration.md).
5. Clique em **definir tooget algumas topologias iniciado**. Um modelo de solução é um "pai" tooall suas topologias. Você pode definir várias topologias em uma oferta/modelo de solução. Quando uma oferta é impulsionada toostaging, ela é enviada por push com todas as suas topologias. 
6. Insira um nome de topologia e, em seguida, clique em hello mais o sinal.
7. Insira uma nova versão e clique em Olá sinal de adição.
8. Carregar arquivo zip do hello preparado na [empacotar aplicativo](#package-application).  
9. Clique em **Solicitar Certificação**. equipe de certificação da Microsoft Hello analisará arquivos hello e certificar topologia hello.

## <a name="next-steps"></a>Próximas etapas
* [Instalar aplicativos de HDInsight](hdinsight-apps-install-applications.md): Saiba como clusters de tooinstall um tooyour de aplicativo do HDInsight.
* [Instalar aplicativos personalizados do HDInsight](hdinsight-apps-install-custom-applications.md): Saiba como toodeploy uma tooHDInsight de aplicativo do HDInsight não publicado.
* [Personalizar clusters HDInsight baseados em Linux usando a ação de Script](hdinsight-hadoop-customize-cluster-linux.md): Saiba como aplicativos adicionais do tooinstall toouse ação de Script.
* [Criar clusters baseados em Linux Hadoop no HDInsight usando modelos do Azure Resource Manager](hdinsight-hadoop-create-linux-clusters-arm-templates.md): Saiba como clusters de toocall Gerenciador de recursos modelos toocreate HDInsight.
* [Use nós de borda vazia no HDInsight](hdinsight-apps-use-edge-node.md): Saiba como toouse vazio de borda nó para acessar o cluster HDInsight, teste de aplicativos de HDInsight e hospedagem de aplicativos de HDInsight.

