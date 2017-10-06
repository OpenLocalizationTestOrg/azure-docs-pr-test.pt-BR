---
title: "aaaAdd um laboratório de tooa repositório Git no Azure DevTest Labs | Microsoft Docs"
description: "Adicionar um repositório Git do GitHub ou do Visual Studio Team Services à sua fonte de artefatos personalizados no Azure DevTest Labs"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 01b459f7-eaf2-45a8-b4b5-2c0a821b33c8
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: tarcher
ms.openlocfilehash: e590559ffb2d497e39823e35c3f66974f42f13c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-git-repository-toostore-custom-artifacts-and-azure-resource-manager-templates"></a>Adicionar um artefatos do Git repositório toostore personalizados e modelos do Gerenciador de recursos do Azure

Se você quiser muito[criar artefatos personalizados](devtest-lab-artifact-author.md) para Olá máquinas virtuais no laboratório, ou [usar o Azure Resource Manager modelos toocreate um ambiente de teste personalizada](devtest-lab-create-environment-from-arm.md), você também deve adicionar uma tooinclude de repositório Git particular artefatos de saudação ou modelos do Gerenciador de recursos do Azure que sua equipe cria. repositório de saudação pode ser hospedado em [GitHub](https://github.com) ou na [Visual Studio Team Services (VSTS)](https://visualstudio.com).

Nós fornecemos um [repositório Github dos artefatos](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts) que podem ser implantados ou personalizados para seus laboratórios. Quando você personaliza ou cria um artefato, você não pode armazená-los no repositório público hello – você deve criar seu próprio repositório privado. 

Quando você cria uma máquina virtual, você pode salvar modelo do Azure Resource Manager hello, personalizá-lo se você deseja e, em seguida, usá-lo posteriormente tooeasily criar VMs mais. Você deve criar seu próprio repositório toostore seus modelos personalizados do Azure Resource Manager.  

* toolearn como toocreate um repositório GitHub, consulte [GitHub Bootcamp](https://help.github.com/categories/bootcamp/).
* toolearn como toocreate um projeto do Team Services com um repositório Git, consulte [conectar tooVisual Studio Team Services](https://www.visualstudio.com/get-started/setup/connect-to-visual-studio-online).

Olá, captura de tela a seguir mostra um exemplo da aparência de um repositório que contém os artefatos no GitHub:  
![Repositório de artefatos de exemplo no GitHub](./media/devtest-lab-add-repo/devtestlab-github-artifact-repo-home.png)

## <a name="get-hello-repository-information-and-credentials"></a>Obter credenciais e informações de saudação do repositório
tooadd um laboratório de tooyour repositório, você deve primeiro obter certas informações do seu repositório. Olá seguintes seções o orientam em obter essas informações para repositórios hospedado no GitHub e do Visual Studio Team Services.

### <a name="get-hello-github-repository-clone-url-and-personal-access-token"></a>Obter token de acesso pessoal e URL de clone do repositório de GitHub Olá
URL de clone do repositório do tooget Olá GitHub e o token de acesso pessoal, siga estas etapas:

1. Procure toohello home page do repositório GitHub Olá que contém o artefato de saudação ou definições de modelo do Gerenciador de recursos do Azure.
2. Selecione **Clonar ou baixar**.
3. Saudação do hello selecione botão toocopy **url de clone HTTPS** toohello área de transferência e salve a URL de saudação para uso posterior.
4. Selecione a imagem do perfil Olá no canto superior direito de saudação do GitHub e selecione **configurações**.
5. Em Olá **configurações pessoais** menu saudação à esquerda, selecione **tokens de acesso pessoal**.
6. Selecione **Gerar novo token**.
7. Em Olá **novo token de acesso pessoal** , insira um **Token descrição**, aceite itens padrão Olá Olá **selecione escopos**e, em seguida, escolha **gerar Token**.
8. Salve o token de saudação gerada conforme necessário mais tarde.
9. Você pode fechar o GitHub agora.   
10. Continuar toohello [conectar seu repositório do laboratório toohello](#connect-your-lab-to-the-repository) seção.

### <a name="get-hello-visual-studio-team-services-repository-clone-url-and-personal-access-token"></a>Obter token de acesso pessoal e URL de clone do repositório do hello do Visual Studio Team Services
URL de clone do repositório do tooget saudação do Visual Studio Team Services e o token de acesso pessoal, siga estas etapas:

1. Olá abrir home page de sua coleção de equipe (por exemplo, `https://contoso-web-team.visualstudio.com`) e, em seguida, selecione o seu projeto.
2. Na página de início do projeto hello, selecione **código**.
3. URL de clone Olá tooview, no projeto Olá **código** página, selecione **Clone**.
4. Salve Olá URL precisar posteriormente neste tutorial.
5. Selecione toocreate um Token de acesso pessoal, **meu perfil** Olá usuário suspensa no menu da conta.
6. Na página de informações de perfil hello, selecione **segurança**.
7. Em Olá **segurança** guia, selecione **adicionar**.
8. Em Olá **criar um token de acesso pessoal** página:

   * Insira um **descrição** de token de saudação.
   * Selecione **180 dias** de saudação **expira em** lista.
   * Escolha **todas as contas acessíveis** de saudação **contas** lista.
   * Escolha Olá **todos os escopos** opção.
   * Escolha **Criar Token**.
9. Quando terminar, o novo token de saudação aparece no hello **Tokens de acesso pessoal** lista. Selecione **copiar Token**e, em seguida, salve o valor do token Olá para uso posterior.
10. Continuar toohello [conectar seu repositório do laboratório toohello](#connect-your-lab-to-the-repository) seção.

## <a name="connect-your-lab-toohello-repository"></a>Conecte-se o repositório de toohello de laboratório
1. Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Selecione **mais serviços**e, em seguida, selecione **DevTest Labs** da lista de saudação.
3. Saudação de laboratórios, selecione lista laboratório desejado hello.   
4. No painel esquerdo do hello, selecione **políticas e configurações**.
5. No laboratório de saudação **políticas e configurações** área, selecione **repositórios**.
6. Em Olá **repositórios** área, selecione **+ adicionar**.

    ![Adicionar um botão de repositório](./media/devtest-lab-add-repo/devtestlab-add-repo.png)
7. Em Olá segundo **repositórios** especifique Olá informações a seguir:

   * **Nome** -Insira um nome para o repositório de saudação.
   * **Url de Clone de Git** -insira Olá Git URL de clone HTTPS que você copiou anteriormente do GitHub ou Visual Studio Team Services.
   * **Ramificação** -insira Olá ramificação tooget suas definições.
   * **Token de acesso pessoal** -insira o token de acesso pessoal Olá é obtido anteriormente do GitHub ou Visual Studio Team Services.
   * **Caminhos de pastas** -Insira pelo menos um caminho relativo toohello clone URL da pasta que contém o artefato ou definições de modelo do Gerenciador de recursos do Azure. Ao especificar um subdiretório, verifique se tooinclude Olá barra invertida no caminho da pasta hello.

     ![Área de repositórios](./media/devtest-lab-add-repo/devtestlab-repo-blade.png)
8. Selecione **Salvar**.

## <a name="next-steps"></a>Próximas etapas
Depois que você criou seu repositório Git particular, você pode fazer uma ou ambas das seguintes hello, dependendo de suas necessidades:
* Armazenamento de seu [artefatos personalizados](devtest-lab-artifact-author.md), que você pode usar toocreate posterior novas VMs.
* [Criar ambientes de várias VMs e recursos de PaaS com modelos do Azure Resource Manager](devtest-lab-create-environment-from-arm.md) e, em seguida, armazene os modelos de saudação em seu repositório privado.

Quando você cria uma máquina virtual, você pode verificar artefatos hello ou modelos são adicionados tooyour repositório do Git. Eles estão disponíveis imediatamente na lista de saudação de artefatos ou modelos, com nome de saudação do seu repositório privado mostrado na coluna Olá que especifica a origem de saudação. 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="related-blog-posts"></a>Postagens de blogs relacionadas
* [Como tootroubleshoot falhando artefatos no Azure DevTest Labs](devtest-lab-troubleshoot-artifact-failure.md)
* [Ingressar em um domínio de AD usando um modelo do Gerenciador de recursos no Azure DevTest Labs de tooexisting VM](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)
