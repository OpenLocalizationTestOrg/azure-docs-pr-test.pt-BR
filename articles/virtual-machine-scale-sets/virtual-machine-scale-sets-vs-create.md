---
title: "aaaDeploy conjunto de escala de máquinas virtuais usando o Visual Studio | Microsoft Docs"
description: "Implantar um conjunto de escala de máquina virtual usando o Visual Studio e um modelo do Resource Manager"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ed0786b8-34b2-49a8-85b5-2a628128ead6
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: guybo
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c89a9f2478ccc3d22989aea604a4273bcc46df82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-virtual-machine-scale-set-with-visual-studio"></a>Como toocreate uma escala de máquina Virtual definido com o Visual Studio
Este artigo mostra como toodeploy uma escala de máquina Virtual do Azure definido usando uma implantação de grupo do Visual Studio recursos.

[Conjuntos de escala de máquinas virtuais do Azure](https://azure.microsoft.com/blog/azure-vm-scale-sets-public-preview/) é um toodeploy de recursos de computação do Azure e gerenciar uma coleção de máquinas virtuais semelhantes com o dimensionamento automático e o balanceamento de carga. É possível provisionar e implantar os Conjuntos de Dimensionamento de Máquinas Virtuais usando os [Modelos do Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates). Os Modelos do Azure Resource Manager podem ser implantados usando a CLI do Azure, o PowerShell, a REST e também diretamente por meio do Visual Studio. O Visual Studio fornece um conjunto de modelos de exemplo, que podem ser implantados como parte de um projeto de Implantação de Grupo de Recursos do Azure.

Implantações de grupo de recursos do Azure são uma maneira toogroup e publicam um conjunto de recursos do Azure relacionados em uma única operação de implantação. Saiba mais sobre eles aqui: [Criando e implantando grupos de recursos do Azure por meio do Visual Studio](../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).

## <a name="pre-requisites"></a>Pré-requisitos
tooget iniciar a implantação de conjuntos de escala de máquina Virtual no Visual Studio, você precisa seguir hello:

* Visual Studio 2013 ou posterior.
* SDK do Azure 2.7, 2.8 ou 2.9

>[!NOTE]
>Essas instruções pressupõem que você esteja usando o Visual Studio com o [SDK do Azure 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).

## <a name="creating-a-project"></a>Criando um projeto
1. Crie um novo projeto no Visual Studio escolhendo **Arquivo | Novo | Projeto**.
   
    ![Arquivo novo][file_new]

2. Em **Visual c# | Nuvem**, escolha **do Azure Resource Manager** toocreate um projeto para implantar um modelo do Gerenciador de recursos do Azure.
   
    ![Criar projeto][create_project]

3. Saudação de modelos, selecione lista Olá Linux ou definir modelo de escala de máquina Virtual Windows.
   
   ![Selecionar modelo][select_Template]

4. Depois de criar seu projeto Consulte scripts de implantação do PowerShell, um modelo do Gerenciador de recursos do Azure e um arquivo de parâmetro hello conjunto de escala de máquina Virtual.
   
    ![Gerenciador de Soluções][solution_explorer]

## <a name="customize-your-project"></a>Personalizar seu projeto
Agora você pode editar Olá modelo toocustomize-lo para as necessidades do seu aplicativo, como adicionar propriedades de extensão VM ou edição carregar regras de balanceamento. Por padrão ao definir modelos de escala de máquina Virtual Olá são toodeploy configurado Olá AzureDiagnostics extensão que torna fácil tooadd regras de dimensionamento automático. Ela também implanta um balanceador de carga com um endereço IP público, configurado com regras NAT de entrada. 

o balanceador de carga Olá permite que você se conectar a instâncias de VM toohello com SSH (Linux) ou RDP (Windows). intervalo de portas de front-end de saudação inicia em 50000. Para linux, isso significa que, se você SSH tooport 50000, é roteada tooport 22 de Olá primeira VM no hello conjunto de escala. Conectar-se tooport 50001 é roteado tooport 22 de saudação segundo VM e assim por diante.

 Uma boa maneira tooedit seus modelos com o Visual Studio é parâmetros de saudação toouse Olá JSON tópicos tooorganize, variáveis e recursos. Uma compreensão de saudação esquema Visual Studio pode apontar erros em seu modelo antes de implantá-lo.

![Gerenciador JSON][json_explorer]

## <a name="deploy-hello-project"></a>Implantar projeto Olá
1. Implante o recurso de conjunto de escala de máquina Virtual Olá toocreate modelo do Gerenciador de recursos do Azure hello. Clique com botão direito no nó do projeto hello e escolha **implantar | Nova implantação**.
   
    ![Implantar o modelo][5deploy_Template]
    
2. Selecione sua assinatura na caixa de diálogo hello "Implantar tooResource grupo".
   
    ![Implantar o modelo][6deploy_Template]

3. A partir daqui, você pode criar seu modelo para toodeploy um grupo de recursos do Azure.
   
    ![Novo grupo de recursos][new_resource]

4. Em seguida, clique em **Editar parâmetros** tooenter parâmetros que são passados tooyour modelo. Forneça Olá username e password para Olá sistema operacional, é necessário toocreate Olá implantação. Se você não tiver as ferramentas do PowerShell para Visual Studio instaladas, é recomendável toocheck **salvar senhas** tooavoid um oculto de linha de comando do PowerShell prompt ou use [keyvault suporte](https://azure.microsoft.com/blog/keyvault-support-for-arm-templates/).
   
    ![Editar Parâmetros][edit_parameters]

5. Agora clique em **Implantar**. Olá **saída** janela mostra o progresso da implantação hello. Observe que a ação de saudação está executando Olá **implantar AzureResourceGroup.ps1** script.
   
   ![Janela de saída][output_window]

## <a name="exploring-your-virtual-machine-scale-set"></a>Explorando o Conjunto de Dimensionamento de Máquinas Virtuais
Após a conclusão da implantação Olá, é possível exibir hello nova máquina Virtual conjunto de escala no Visual Studio de saudação **Cloud Explorer** (atualização Olá lista). O Gerenciador de Nuvem permite que você gerencie recursos do Azure no Visual Studio ao mesmo tempo que desenvolve aplicativos. Você também pode exibir o conjunto de escala de máquinas virtuais em Olá [portal do Azure](https://portal.azure.com) e [Gerenciador de recursos do Azure](https://resources.azure.com/).

![Gerenciador de Nuvem][cloud_explorer]

 Olá portal fornece a melhor maneira de saudação toovisually gerenciar sua infraestrutura do Azure com um navegador da web, enquanto o Gerenciador de recursos do Azure fornece uma maneira fácil de tooexplore e depurar recursos do Azure, fornecendo uma janela em hello "instância exibir" e também mostrando PowerShell comandos para recursos de saudação que você está observando.

## <a name="next-steps"></a>Próximas etapas
Depois que você implantou com êxito os conjuntos de escala de máquina Virtual por meio do Visual Studio, você pode personalizar seu projeto toosuit seus requisitos de aplicativo. Por exemplo, configurar o dimensionamento automático, adicionando um **Insights** recursos, adicionando infraestrutura tooyour modelo (como as máquinas virtuais autônomas) ou implantação de aplicativos usando a extensão do script personalizado hello. Modelos de bom exemplo podem ser encontrados na Olá [modelos de início rápido do Azure](https://github.com/Azure/azure-quickstart-templates) repositório GitHub (procure "vmss").

[file_new]: ./media/virtual-machine-scale-sets-vs-create/1-FileNew.png
[create_project]: ./media/virtual-machine-scale-sets-vs-create/2-CreateProject.png
[select_Template]: ./media/virtual-machine-scale-sets-vs-create/3b-SelectTemplateLin.png
[solution_explorer]: ./media/virtual-machine-scale-sets-vs-create/4-SolutionExplorer.png
[json_explorer]: ./media/virtual-machine-scale-sets-vs-create/10-JsonExplorer.png
[5deploy_Template]: ./media/virtual-machine-scale-sets-vs-create/5-DeployTemplate.png
[6deploy_Template]: ./media/virtual-machine-scale-sets-vs-create/6-DeployTemplate.png
[new_resource]: ./media/virtual-machine-scale-sets-vs-create/7-NewResourceGroup.png
[edit_parameters]: ./media/virtual-machine-scale-sets-vs-create/8-EditParameter.png
[output_window]: ./media/virtual-machine-scale-sets-vs-create/9-Output.png
[cloud_explorer]: ./media/virtual-machine-scale-sets-vs-create/12-CloudExplorer.png
