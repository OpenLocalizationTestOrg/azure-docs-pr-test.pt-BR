---
title: "aaaCreate ambientes de várias VMs e os recursos de PaaS com modelos do Gerenciador de recursos do Azure | Microsoft Docs"
description: "Saiba como toocreate ambientes de várias VMs e recursos de PaaS no Azure DevTest Labs de um modelo do Gerenciador de recursos do Azure"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/31/2017
ms.author: tarcher
ms.openlocfilehash: ab8628f6cb5a666435258efb93921ec69ad3a13a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-multi-vm-environments-and-paas-resources-with-azure-resource-manager-templates"></a>Criar ambientes de várias VMs e recursos de PaaS com modelos do Azure Resource Manager

Olá [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) permite que você tooeasily [criar e adicionar um laboratório de tooa VM](https://docs.microsoft.com/en-us/azure/devtest-lab/devtest-lab-add-vm). Isso funciona bem para criar uma VM por vez. No entanto, se o ambiente de saudação contiver várias VMs, cada VM tem toobe criada individualmente. Para cenários como um aplicativo da Web de várias camado ou um farm do SharePoint, um mecanismo é tooallow necessário para a criação de saudação de várias VMs em uma única etapa. Usando modelos do Azure Resource Manager, você pode definir agora a infraestrutura de saudação e a configuração de sua solução do Azure e repetidamente implantar várias VMs em um estado consistente. Este recurso fornece Olá benefícios a seguir:

- Os modelos do Azure Resource Manager são carregados diretamente a partir de seu repositório de controle de origem (GitHub ou Git do Team Services).
- Uma vez configurado, os usuários podem criar um ambiente selecionando um modelo do Azure Resource Manager Olá portal do Azure como o que podem fazer com outros tipos de [VM bases](./devtest-lab-comparing-vm-base-image-types.md).
- Recursos de PaaS do Azure podem ser provisionados em um ambiente de um modelo do Azure Resource Manager na adição tooIaaS VMs.
- custo de saudação de ambientes pode ser acompanhado no laboratório Olá adição tooindividual máquinas virtuais criadas por outros tipos de bases de dados.
- Recursos de PaaS são criados e aparecerão no custo de controle; No entanto, o desligamento automático VM não é aplicável a tooPaaS recursos.
- Os usuários têm Olá mesmo controle de política VM para ambientes que eles têm para máquinas virtuais do laboratório único.

Saiba mais sobre Olá muitas [benefícios do uso de modelos do Gerenciador de recursos](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#the-benefits-of-using-resource-manager) toodeploy, atualizar ou excluir todos os seus recursos de laboratório em uma única operação.

> [!NOTE]
> Quando você usa um modelo do Gerenciador de recursos como uma base toocreate laboratório mais máquinas virtuais, há algumas diferenças tookeep em mente se você estiver criando várias VMs ou VMs único. Usar o modelo do Azure Resource Manager de uma máquina virtual explica essas diferenças mais detalhadamente.
>
>

## <a name="configure-azure-resource-manager-template-repositories"></a>Configurar os repositórios de modelo do Azure Resource Manager

Como uma saudação práticas recomendadas com infraestrutura como código e configuração como código, modelos de ambiente devem ser gerenciadas no controle de origem. O Azure DevTest Labs segue essa prática e carrega todos os modelos do Azure Resource Manager diretamente a partir de seus repositórios GitHub ou VSTS Git. Como resultado, os modelos do Gerenciador de recursos podem ser usados em ciclo de toda versão de saudação do hello teste toohello ambiente de produção.

Há algumas regras toofollow tooorganize seus modelos do Azure Resource Manager em um repositório:

- arquivo de modelo mestre Olá deve ser nomeado `azuredeploy.json`. 

    ![Principais arquivos de modelo do Azure Resource Manager](./media/devtest-lab-create-environment-from-arm/master-template.png)

- Se você quiser toouse valores de parâmetros definidos em um arquivo de parâmetro, o arquivo de parâmetro hello deve ser nomeado `azuredeploy.parameters.json`.
- Você pode usar parâmetros de saudação `_artifactsLocation` e `_artifactsLocationSasToken` tooconstruct Olá parametersLink valor do URI, permitindo que o DevTest Labs tooautomatically gerenciar modelos de aninhados. Consulte [Como o Azure DevTest Labs facilita as implantações de modelo do Resource Manager para ambientes de teste](https://blogs.msdn.microsoft.com/devtestlab/2017/05/23/how-azure-devtest-labs-makes-nested-arm-template-deployments-easier-for-testing-environments/) para obter mais informações.
- Metadados podem ser a descrição e o nome de exibição do modelo de saudação toospecify definido. Esses metadados devem estar em um arquivo denominado `metadata.json`. Olá arquivo de metadados de exemplo a seguir ilustra como toospecify Olá exibem o nome e a descrição: 

```json
{
 
"itemDisplayName": "<your template name>",
 
"description": "<description of hello template>"
 
}
```

Olá etapas a seguir orientam você na adição de um laboratório de tooyour repositório usando Olá portal do Azure. 

1. Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Selecione **mais serviços**e, em seguida, selecione **DevTest Labs** da lista de saudação.
1. Saudação de laboratórios, selecione lista laboratório desejado hello.   
1. Na folha do laboratório hello, selecione **políticas e configurações**.

    ![Configuração e políticas](./media/devtest-lab-create-environment-from-arm/configuration-and-policies-menu.png)

1. De saudação **políticas e configurações** lista de configurações, selecione **repositórios**. Olá **repositórios** folha lista repositórios Olá que foram adicionados toohello laboratório. Um repositório chamado `Public Repo` é gerado automaticamente para todos os laboratórios e conecta toohello [repositório GitHub do DevTest Labs](https://github.com/Azure/azure-devtestlab) que contém vários artefatos VM para seu uso.

    ![Repositório público](./media/devtest-lab-create-environment-from-arm/public-repo.png)

1. Selecione **adicionar +** tooadd seu repositório de modelo do Gerenciador de recursos do Azure.
1. Quando Olá segundo **repositórios** abre a folha, insira as informações necessárias Olá da seguinte maneira:
    - **Nome** -insira o nome de repositório de saudação que é usado no laboratório de saudação.
    - **URL de clone de Git** -insira a URL de clone HTTPS de GIT saudação do GitHub ou Visual Studio Team Services.  
    - **Ramificação** -insira Olá ramificação nome tooaccess suas definições de modelo do Gerenciador de recursos do Azure. 
    - **Token de acesso pessoal** -é usado o token de acesso pessoal Olá toosecurely acessar o repositório. Selecione de seu token do Visual Studio Team Services tooget  **&lt;YourName >> meu perfil > Segurança > token de acesso público**. tooget seu token do GitHub, selecione seu avatar seguida selecionando **Configurações > token de acesso público**. 
    - **Caminhos de pastas** - o usando um dos campos de entrada hello dois, digite o caminho da pasta de saudação que começa com uma barra invertida - / - e é relativo tooyour Git clone URI tooeither suas definições de artefato (primeiro campo de entrada) ou o modelo do Gerenciador de recursos do Azure definições.   
    
        ![Repositório público](./media/devtest-lab-create-environment-from-arm/repo-values.png)

1. Depois que todos os campos de saudação necessárias são inseridos e passam na validação de saudação, selecione **salvar**.

Olá próxima seção guiará você por meio da criação de ambientes de um modelo do Gerenciador de recursos do Azure.

## <a name="create-an-environment-from-an-azure-resource-manager-template"></a>Criar um ambiente a partir de um modelo do Azure Resource Manager

Quando um repositório de modelos do Azure Resource Manager tiver sido configurado no laboratório hello, os usuários do laboratório podem criar um ambiente usando o portal do Azure com hello etapas a seguir:

1. Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Selecione **mais serviços**e, em seguida, selecione **DevTest Labs** da lista de saudação.
1. Saudação de laboratórios, selecione lista laboratório desejado hello.   
1. Na folha do laboratório hello, selecione **adicionar +**.
1. Olá **escolher uma base** folha exibe imagens de base Olá podem ser usados com modelos do Azure Resource Manager Olá listados primeiro. Selecione Olá desejada do modelo do Gerenciador de recursos do Azure.

    ![Escolher uma base](./media/devtest-lab-create-environment-from-arm/choose-a-base.png)
  
1. Em Olá **adicionar** folha, digite Olá **nome do ambiente** valor. nome do ambiente de saudação que é usuários tooyour exibido no laboratório de saudação. campos de entrada restantes Olá são definidos no modelo do Azure Resource Manager Olá. Se os valores padrão são definidos no modelo de saudação ou Olá `azuredeploy.parameter.json` arquivo estiver presente, os valores padrão são exibidos nesses campos de entrada. Para parâmetros de tipo *proteger a cadeia de caracteres*, você pode usar os segredos de saudação armazenados no laboratório de saudação [repositório pessoal do segredo](https://azure.microsoft.com/en-us/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store).

    ![Adicionar folha](./media/devtest-lab-create-environment-from-arm/add.png)

    > [!NOTE]
    > Há diversos valores de parâmetro que, mesmo se especificados, são exibidos como valores vazios. Portanto, se os usuários atribuir tooparameters esses valores em um modelo do Azure Resource Manager, DevTest Labs não exiba valores hello; em vez disso, mostrando campos de entrada em branco em que os usuários do laboratório Olá necessário tooenter um valor ao criar o ambiente de saudação.
    > 
    > - GEN-UNIQUE
    > - GEN-UNIQUE-[N]
    > - GEN-SSH-PUB-KEY
    > - GEN-PASSWORD 
 
1. Selecione **adicionar** toocreate ambiente de saudação. ambiente de saudação inicia imediatamente o provisionamento com o status de saudação exibindo em Olá **minhas máquinas virtuais** lista. Um novo grupo de recursos é criado automaticamente pelo Olá laboratório tooprovision todos os recursos de saudação definidos no modelo do Azure Resource Manager hello.
1. Depois de criar o ambiente hello, selecione o ambiente de saudação em hello **minhas máquinas virtuais** liste tooopen folha de grupo de recursos de saudação e procurar todos os recursos de saudação provisionados no ambiente de saudação do.
    
    ![Lista Minhas máquinas virtuais](./media/devtest-lab-create-environment-from-arm/all-environment-resources.png)
   
   Também é possível expandir a lista da saudação apenas tooview Olá ambiente de máquinas virtuais que são provisionados no ambiente de saudação.
    
    ![Lista Minhas máquinas virtuais](./media/devtest-lab-create-environment-from-arm/my-vm-list.png)

1. Clique em qualquer Olá ambientes tooview Olá ações disponíveis - como a aplicação de artefatos, anexar discos de dados, alterando o tempo de desligamento automático e muito mais.

    ![Ações do ambiente](./media/devtest-lab-create-environment-from-arm/environment-actions.png)

## <a name="next-steps"></a>Próximas etapas
* Quando uma máquina virtual tiver sido criada, você pode se conectar toohello VM selecionando **conectar** na folha de saudação da VM.
* Exibir e gerenciar recursos em um ambiente selecionando ambiente Olá no hello **minhas máquinas virtuais** lista no laboratório. 
* Explorar Olá [modelos do Gerenciador de recursos do Azure da Galeria de modelos de início rápido do Azure](https://github.com/Azure/azure-quickstart-templates)
