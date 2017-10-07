---
title: aaaDeploy um aplicativo web com um modelo - banco de dados do Azure Cosmos | Microsoft Docs
description: "Saiba como toodeploy uma conta de banco de dados do Azure Cosmos, aplicativos de Web do serviço de aplicativo do Azure e um exemplo de aplicativo da web usando um modelo do Gerenciador de recursos do Azure."
services: cosmos-db, app-service\web
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 087d8786-1155-42c7-924b-0eaba5a8b3e0
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: b2bdde9279aad570606d7bf06dfc710f564b4d0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-azure-cosmos-db-and-azure-app-service-web-apps-using-an-azure-resource-manager-template"></a>Implantar o Azure Cosmos DB e Aplicativos Web do Serviço de Aplicativo do Azure usando um modelo do Azure Resource Manager
Este tutorial mostra como toouse uma toodeploy de modelo do Gerenciador de recursos do Azure e integrar [banco de dados do Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/), uma [do serviço de aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) aplicativo web e um aplicativo da web de exemplo.

Usando modelos do Azure Resource Manager, você pode automatizar facilmente implantação hello e a configuração de recursos do Azure.  Este tutorial mostra como toodeploy um aplicativo web e configurar automaticamente as informações de conexão da conta de banco de dados do Azure Cosmos.

Após concluir este tutorial, você será capaz de tooanswer Olá perguntas a seguir:  

* Como usar um toodeploy de modelo do Gerenciador de recursos do Azure e integrar uma conta de banco de dados do Azure Cosmos e um aplicativo web no serviço de aplicativo do Azure?
* Como usar um toodeploy de modelo do Gerenciador de recursos do Azure e integrar um aplicativo Webdeploy, um aplicativo web no aplicativo Web de aplicativos de serviço e uma conta de banco de dados do Azure Cosmos?

<a id="Prerequisites"></a>

## <a name="prerequisites"></a>Pré-requisitos
> [!TIP]
> Enquanto este tutorial presume experiência anterior com o Azure Resource Manager modelos ou JSON, deve ser toomodify Olá referenciado modelos ou opções de implantação, dados de Conhecimento de cada uma dessas áreas será necessário.
> 
> 

Antes de seguir as instruções de saudação neste tutorial, certifique-se de que você tenha a seguinte hello:

* Uma assinatura do Azure. O Azure é uma plataforma baseada em assinatura.  Para obter mais informações sobre como adquirir uma assinatura, confira [Opções de compra](https://azure.microsoft.com/pricing/purchase-options/), [Ofertas para membros](https://azure.microsoft.com/pricing/member-offers/) ou [Avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).

## <a id="CreateDB"></a>Etapa 1: Baixar arquivos de modelo Olá
Vamos começar baixando arquivos de modelo de Olá, que vamos usar neste tutorial.

1. Baixar Olá [criar uma conta de banco de dados do Azure Cosmos, aplicativos Web e implantar um exemplo de aplicativo de demonstração](https://portalcontent.blob.core.windows.net/samples/DocDBWebsiteTodo.json) pasta local do modelo tooa (por exemplo, C:\Azure Cosmos DBTemplates). Esse modelo implantará uma conta do Azure Cosmos DB, um aplicativo Web do Serviço de Aplicativo e um aplicativo Web.  Ele também automaticamente configura a conta de banco de dados do Azure Cosmos Olá web aplicativo tooconnect toohello.
2. Baixar Olá [criar uma conta de banco de dados do Azure Cosmos e um exemplo de aplicativos Web](https://portalcontent.blob.core.windows.net/samples/DocDBWebSite.json) pasta local do modelo tooa (por exemplo, C:\Azure Cosmos DBTemplates). Este modelo implantará uma conta de banco de dados do Azure Cosmos, um aplicativo do serviço de aplicativo web e modificará saudação do aplicativo configurações tooeasily superfície Azure Cosmos DB conexão informações do site, mas não inclui um aplicativo web.  

<a id="Build"></a>

## <a name="step-2-deploy-hello-azure-cosmos-db-account-app-service-web-app-and-demo-application-sample"></a>Etapa 2: Implantar a conta de banco de dados do Azure Cosmos hello, exemplo de aplicativo do serviço de aplicativo web app e demonstração
Agora, vamos implantar nosso primeiro modelo.

> [!TIP]
> modelo de saudação não valida o nome do aplicativo web hello e nome de conta do banco de dados do Azure Cosmos inserida abaixo são um) válido e b) disponível.  É altamente recomendável que você verifique a disponibilidade de saudação do hello nomes planejar a implantação de saudação do toosupply toosubmitting anterior.
> 
> 

1. Logon toohello [Portal do Azure](https://portal.azure.com), clique em novo e procure "Implantação de modelo".
    ![Captura de tela de implantação de modelo de saudação da interface do usuário](./media/create-website/TemplateDeployment1.png)
2. Selecione o item de implantação de modelo hello e clique em **criar** ![captura de tela de implantação de modelo de saudação da interface do usuário](./media/create-website/TemplateDeployment2.png)
3. Clique em **Editar modelo**, cole o conteúdo Olá Olá DocDBWebsiteTodo.json do arquivo de modelo e clique em **salvar**.
   ![Captura de tela de implantação de modelo de saudação da interface do usuário](./media/create-website/TemplateDeployment3.png)
4. Clique em **Editar parâmetros**, forneça valores para cada um dos parâmetros obrigatórios hello e clique em **Okey**.  parâmetros de saudação são da seguinte maneira:
   
   1. SITENAME: Especifica Olá nome do aplicativo do serviço de aplicativo web e é usada tooconstruct Olá URL que você usará tooaccess Olá web app (por exemplo, se você especificar "mydemodocdbwebapp", será Olá URL pela qual você irá acessar Olá web app mydemodocdbwebapp.azurewebsites.NET).
   2. HOSTINGPLANNAME: Especifica o nome de saudação do serviço de aplicativo toocreate do plano de hospedagem.
   3. O local: Especifica Olá local do Azure em recursos do aplicativo que toocreate hello Azure Cosmos DB e web.
   4. DATABASEACCOUNTNAME: Especifica o nome de saudação do hello Azure Cosmos DB conta toocreate.   
      
      ![Captura de tela de implantação de modelo de saudação da interface do usuário](./media/create-website/TemplateDeployment4.png)
5. Escolha um grupo de recursos existente ou forneça um nome toomake um novo grupo de recursos e escolha um local para o grupo de recursos de saudação.

    ![Captura de tela de implantação de modelo de saudação da interface do usuário](./media/create-website/TemplateDeployment5.png)
6. Clique em **revisar os termos legais**, **compra**e, em seguida, clique em **criar** toobegin implantação de saudação.  Selecione **toodashboard Pin** para implantação resultante Olá sejam facilmente visível em sua home page portal do Azure.
   ![Captura de tela de implantação de modelo de saudação da interface do usuário](./media/create-website/TemplateDeployment6.png)
7. Quando termina de implantação hello, folha de grupo de recursos de saudação será aberto.
   ![Captura de tela da folha de grupo de recursos de saudação](./media/create-website/TemplateDeployment7.png)  
8. toouse Olá aplicativo, basta navegar URL do aplicativo web toohello (no exemplo hello acima, Olá URL seria http://mydemodocdbwebapp.azurewebsites.net).  Você verá Olá aplicativo web a seguir:
   
   ![Aplicativo Todo de exemplo](./media/create-website/image2.png)
9. Vá em frente e criar algumas tarefas no aplicativo web de saudação e, em seguida, retornar toohello folha de grupo de recursos no portal do Azure de saudação. Clique em recursos de conta de banco de dados do Azure Cosmos Olá na lista de recursos de saudação e, em seguida, clique em **Explorer consulta**.
    ![Captura de tela de saudação de lente resumo com Olá web aplicativo realçado](./media/create-website/TemplateDeployment8.png)  
10. Execução de consulta padrão hello, "Selecionar * de c" e inspecionar os resultados de saudação.  Observe que essa consulta Olá recuperou representação Olá Olá de itens de tarefas criada na etapa 7 acima.  Sinta-se livre tooexperiment com consultas; Por exemplo, tente executar SELECT * FROM c c.isComplete de onde = true tooreturn todos os itens de tarefas que foram marcados como concluídos.
    
    ![Captura de tela de folhas de Gerenciador de consulta e os resultados de saudação mostrando Olá resultados da consulta](./media/create-website/image5.png)
11. Sinta-se livre tooexplore Olá experiência do portal do Azure Cosmos DB ou modificar o aplicativo de tarefas do exemplo hello.  Quando você estiver pronto, vamos implantar outro modelo.

<a id="Build"></a> 

## <a name="step-3-deploy-hello-document-account-and-web-app-sample"></a>Etapa 3: Implantar hello conta de documento e o aplicativo web de exemplo
Agora, vamos implantar nosso segundo modelo.  Este modelo é útil tooshow como você pode injetar informações de conexão de banco de dados do Azure Cosmos como ponto de extremidade da conta e a chave mestra em um aplicativo web, como configurações de aplicativo ou como uma cadeia de caracteres de conexão personalizada. Por exemplo, talvez você tenha seu próprio aplicativo web que você deseja toodeploy com uma conta de banco de dados do Azure Cosmos e tem informações de conexão Olá preenchidas automaticamente durante a implantação.

> [!TIP]
> modelo de saudação não valida o nome do aplicativo web hello e nome de conta do banco de dados do Azure Cosmos inserida abaixo são um) válido e b) disponível.  É altamente recomendável que você verifique a disponibilidade de saudação do hello nomes planejar a implantação de saudação do toosupply toosubmitting anterior.
> 
> 

1. Em Olá [Portal do Azure](https://portal.azure.com), clique em novo e procure "Implantação de modelo".
    ![Captura de tela de implantação de modelo de saudação da interface do usuário](./media/create-website/TemplateDeployment1.png)
2. Selecione o item de implantação de modelo hello e clique em **criar** ![captura de tela de implantação de modelo de saudação da interface do usuário](./media/create-website/TemplateDeployment2.png)
3. Clique em **Editar modelo**, cole o conteúdo Olá Olá DocDBWebSite.json do arquivo de modelo e clique em **salvar**.
   ![Captura de tela de implantação de modelo de saudação da interface do usuário](./media/create-website/TemplateDeployment3.png)
4. Clique em **Editar parâmetros**, forneça valores para cada um dos parâmetros obrigatórios hello e clique em **Okey**.  parâmetros de saudação são da seguinte maneira:
   
   1. SITENAME: Especifica Olá nome do aplicativo do serviço de aplicativo web e é usada tooconstruct Olá URL que você usará tooaccess Olá web app (por exemplo, se você especificar "mydemodocdbwebapp", será Olá URL pela qual você irá acessar Olá web app mydemodocdbwebapp.azurewebsites.NET).
   2. HOSTINGPLANNAME: Especifica o nome de saudação do serviço de aplicativo toocreate do plano de hospedagem.
   3. O local: Especifica Olá local do Azure em recursos do aplicativo que toocreate hello Azure Cosmos DB e web.
   4. DATABASEACCOUNTNAME: Especifica o nome de saudação do hello Azure Cosmos DB conta toocreate.   
      
      ![Captura de tela de implantação de modelo de saudação da interface do usuário](./media/create-website/TemplateDeployment4.png)
5. Escolha um grupo de recursos existente ou forneça um nome toomake um novo grupo de recursos e escolha um local para o grupo de recursos de saudação.

    ![Captura de tela de implantação de modelo de saudação da interface do usuário](./media/create-website/TemplateDeployment5.png)
6. Clique em **revisar os termos legais**, **compra**e, em seguida, clique em **criar** toobegin implantação de saudação.  Selecione **toodashboard Pin** para implantação resultante Olá sejam facilmente visível em sua home page portal do Azure.
   ![Captura de tela de implantação de modelo de saudação da interface do usuário](./media/create-website/TemplateDeployment6.png)
7. Quando termina de implantação hello, folha de grupo de recursos de saudação será aberto.
   ![Captura de tela da folha de grupo de recursos de saudação](./media/create-website/TemplateDeployment7.png)  
8. Clique em recursos de aplicativo Web hello na lista de recursos de saudação e, em seguida, clique em **configurações do aplicativo** ![captura de tela de saudação do grupo de recursos](./media/create-website/TemplateDeployment9.png)  
9. Observe que como há configurações de aplicativo presentes para o ponto de extremidade de banco de dados do Azure Cosmos hello e cada uma das chaves de mestre de banco de dados do Azure Cosmos hello.

    ![Captura de tela das configurações do aplicativo](./media/create-website/TemplateDeployment10.png)  
10. Sinta-se livre toocontinue explorando Olá Portal do Azure ou execute um dos nossos Azure Cosmos DB [exemplos](http://go.microsoft.com/fwlink/?LinkID=402386) toocreate seu próprio aplicativo de banco de dados do Azure Cosmos.

<a name="NextSteps"></a>

## <a name="next-steps"></a>Próximas etapas
Parabéns! Você implantou o Azure Cosmos DB, um aplicativo Web do Serviço de Aplicativo e um aplicativo Web de exemplo usando modelos do Azure Resource Manager.

* toolearn mais sobre o banco de dados do Azure Cosmos, clique em [aqui](http://azure.com/docdb).
* toolearn mais sobre aplicativos da Web do serviço de aplicativo do Azure, clique em [aqui](http://go.microsoft.com/fwlink/?LinkId=325362).
* toolearn mais sobre modelos do Azure Resource Manager, clique em [aqui](https://msdn.microsoft.com/library/azure/dn790549.aspx).

## <a name="whats-changed"></a>O que mudou
* Para um guia toohello alteração de sites tooApp serviço consulte: [do serviço de aplicativo do Azure e seu impacto sobre os serviços do Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)
* Para um guia toohello alteração de saudação antigo portal toohello novo portal consulte: [referência para navegação Olá Portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkId=529715)

> [!NOTE]
> Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](http://go.microsoft.com/fwlink/?LinkId=523751), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo. Nenhum cartão de crédito é exigido, sem compromissos.
> 
> 

