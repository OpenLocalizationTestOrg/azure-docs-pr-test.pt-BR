---
title: "Extensão do painel de acesso do Azure para o IE usando um GPO de aaaDeploy | Microsoft Docs"
description: "Como toouse agrupar complemento do política toodeploy saudação do Internet Explorer para o portal de meus aplicativos hello."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 7c2d49c8-5be0-4e7e-abac-332f9dfda736
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 926f15950bbe81d2fbfe1b0b856470da40880d7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-hello-access-panel-extension-for-internet-explorer-using-group-policy"></a>Como tooDeploy Olá extensão do painel de acesso do Internet Explorer usando a diretiva de grupo
Este tutorial mostra como toouse tooremotely de política de grupo instalar extensão do painel de acesso de saudação do Internet Explorer em computadores de seus usuários. Essa extensão é necessária para usuários do Internet Explorer que precisam de toosign em aplicativos que são configurados usando [com base em senha de logon único](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).

É recomendável que administradores automatizarem a implantação de saudação da extensão. Caso contrário, os usuários têm toodownload e instalarem extensão Olá por conta própria, que é toouser propensas a erros e requer permissões de administrador. Este tutorial apresenta um método de automatização de implantações de software usando a política de grupo. [Saiba mais sobre a política de grupo.](https://technet.microsoft.com/windowsserver/bb310732.aspx)

Olá extensão do painel de acesso também está disponível para [Chrome](https://go.microsoft.com/fwLink/?LinkID=311859) e [Firefox](https://go.microsoft.com/fwLink/?LinkID=626998), nenhum deles exigem tooinstall de permissões de administrador.

## <a name="prerequisites"></a>Pré-requisitos
* Você configurou o [serviços de domínio do Active Directory](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), e você tiver ingressado domínio de tooyour máquinas dos usuários.
* Você deve ter hello "Editar configurações de" permissão tooedit Olá objeto de política de grupo (GPO). Por padrão, membros da saudação grupos de segurança a seguir têm essa permissão: os administradores de domínio, administradores de empresa e proprietários de criadores de diretiva de grupo. [Saiba mais.](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx)

## <a name="step-1-create-hello-distribution-point"></a>Etapa 1: Criar um ponto de distribuição de saudação
Primeiro, você deve colocar o pacote do instalador Olá em um local de rede que pode ser acessado por máquinas de saudação que desejar extensão de saudação do tooremotely instalar em. toodo isso, siga estas etapas:

1. Faça logon no servidor toohello como um administrador
2. Em Olá **Gerenciador do servidor** janela, ir muito**arquivos e serviços de armazenamento**.
   
    ![Abrir Serviços de Arquivo e Armazenamento](./media/active-directory-saas-ie-group-policy/files-services.png)
3. Vá toohello **compartilhamentos** guia. Em seguida, clique em **Tarefas** > **Novo Compartilhamento...**
   
    ![Abrir Serviços de Arquivo e Armazenamento](./media/active-directory-saas-ie-group-policy/shares.png)
4. Olá completa **Assistente de novo compartilhamento** e tooensure do conjunto de permissões que ele possa ser acessado de computadores dos usuários. [Saiba mais sobre compartilhamentos.](https://technet.microsoft.com/library/cc753175.aspx)
5. Baixar Olá pacote do Microsoft Windows Installer (arquivo. msi) a seguir: [Extension.msi do painel de acesso](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access Panel Extension.msi)
6. Copie o local de tooa desejado no compartilhamento de saudação do pacote hello instalador.
   
    ![Copie o compartilhamento de toohello de arquivo hello. msi.](./media/active-directory-saas-ie-group-policy/copy-package.png)
7. Verifique se as máquinas cliente tooaccess capaz de pacote do instalador de saudação do compartilhamento de saudação. 

## <a name="step-2-create-hello-group-policy-object"></a>Etapa 2: Criar hello objeto de diretiva de grupo
1. Faça logon no servidor de toohello que hospeda sua instalação de serviços de domínio Active Directory (AD DS).
2. No Gerenciador do servidor de saudação, vá muito**ferramentas** > **Group Policy Management**.
   
    ![Vá tooTools > Gerenciamento de diretiva de grupo](./media/active-directory-saas-ie-group-policy/tools-gpm.png)
3. No painel esquerdo de saudação do hello **Group Policy Management** janela, exibir sua hierarquia de unidade organizacional (UO) e determinar em qual escopo você gostaria que a política de grupo tooapply hello. Por exemplo, você pode decidir toopick um pequeno toodeploy tooa da UO poucos usuários de teste, ou você pode escolher uma nível superior OU toodeploy tooyour toda a organização.
   
   > [!NOTE]
   > Se você deseja toocreate ou editar suas unidades organizacionais (UOs), alternar toohello back Gerenciador do servidor e vá muito**ferramentas** > **computadores e usuários do Active Directory**.
   > 
   > 
4. Depois de selecionar uma UO, clique com o botão direito do mouse nela e selecione **Criar um GPO neste domínio e vinculá-lo aqui...**
   
    ![Criar um novo GPO](./media/active-directory-saas-ie-group-policy/create-gpo.png)
5. Em Olá **novo GPO** prompt, digite um nome para Olá novo objeto de diretiva de grupo.
   
    ![Nome hello novo GPO](./media/active-directory-saas-ie-group-policy/name-gpo.png)
6. Com o botão direito Olá objeto de política de grupo que você criou e selecione **editar**.
   
    ![Editar saudação novo GPO](./media/active-directory-saas-ie-group-policy/edit-gpo.png)

## <a name="step-3-assign-hello-installation-package"></a>Etapa 3: Atribuir Olá pacote de instalação
1. Determinar se você gostaria que a extensão de saudação toodeploy com base em **configuração do computador** ou **configuração do usuário**. Ao usar [configuração do computador](https://technet.microsoft.com/library/cc736413%28v=ws.10%29.aspx), extensão hello está instalado no computador de hello, independentemente de qual os usuários fazem logon tooit. Com [configuração do usuário](https://technet.microsoft.com/library/cc781953%28v=ws.10%29.aspx), os usuários têm a extensão de saudação instalado para eles, independentemente de quais computadores fazem logon.
2. No painel esquerdo de saudação do hello **Editor de gerenciamento de política de grupo** janela, vá tooeither de saudação caminhos de pastas, dependendo do tipo de configuração que você escolheu a seguir:
   
   * `Computer Configuration/Policies/Software Settings/`
   * `User Configuration/Policies/Software Settings/`
3. Clique com o botão direito do mouse em **Instalação do software** e selecione **Novo** > **Pacote...**
   
    ![Criar um novo pacote de instalação de software](./media/active-directory-saas-ie-group-policy/new-package.png)
4. Vá toohello pasta compartilhada que contém o pacote do instalador de saudação do [etapa 1: criar um ponto de distribuição de saudação](#step-1-create-the-distribution-point), selecione o arquivo. msi de saudação e clique em **abrir**.
   
   > [!IMPORTANT]
   > Se Olá compartilhamento esteja localizado no mesmo servidor, verifique se você está acessando o. msi de saudação por meio do caminho do arquivo de rede hello, em vez de caminho do arquivo local hello.
   > 
   > 
   
    ![Selecione o pacote de instalação de saudação da pasta compartilhada hello.](./media/active-directory-saas-ie-group-policy/select-package.png)
5. Em Olá **implantar Software** prompt, selecione **atribuído** para o método de implantação. Em seguida, clique em **OK**.
   
    ![Selecione Atribuído e clique em OK.](./media/active-directory-saas-ie-group-policy/deployment-method.png)

extensão de saudação agora está implantado toohello UO que você selecionou. [Saiba mais sobre a instalação do Software de Política de Grupo.](https://technet.microsoft.com/library/cc738858%28v=ws.10%29.aspx)

## <a name="step-4-auto-enable-hello-extension-for-internet-explorer"></a>Etapa 4: Saudação de ativação automática extensão para o Internet Explorer
Além disso toorunning Olá installer, todas as extensões para o Internet Explorer deve ser explicitamente ativado antes de ser usada. Siga as etapas de saudação abaixo tooenable Olá extensão do painel de acesso usando a política de grupo:

1. Em Olá **Editor de gerenciamento de política de grupo** janela, vá tooeither de saudação seguintes caminhos, dependendo do tipo de configuração que você escolheu na [etapa 3: atribuir Olá pacote de instalação](#step-3-assign-the-installation-package):
   
   * `Computer Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
2. Clique com o botão direito do mouse em **Lista de Complementos** e selecione **Editar**.
    ![Edite a Lista de Complementos.](./media/active-directory-saas-ie-group-policy/edit-add-on-list.png)
3. Em Olá **lista de complementos** janela, selecione **habilitado**. Em seguida, em Olá **opções** seção, clique em **Mostrar...** .
   
    ![Clique em Habilitar e clique em Mostrar...](./media/active-directory-saas-ie-group-policy/edit-add-on-list-window.png)
4. Em Olá **Mostrar conteúdo** janela, executar Olá etapas a seguir:
   
   1. Para a coluna primeiro hello (Olá **nome do valor** campo), copiar e colar Olá identificação de classe a seguir:`{030E9A3F-7B18-4122-9A60-B87235E4F59E}`
   2. Segunda coluna de hello (Olá **valor** campo), tipo no seguinte valor de saudação:`1`
   3. Clique em **Okey** tooclose Olá **Mostrar conteúdo** janela.
      
      ![Preencha os valores hello especificados acima.](./media/active-directory-saas-ie-group-policy/show-contents.png)
5. Clique em **Okey** tooapply suas alterações e fechar Olá **lista de complementos** janela.

Olá extensão deve agora ser habilitada para máquinas Olá Olá selecionado UO. [Saiba mais sobre como usar tooenable de diretiva de grupo ou desabilite complementos do Internet Explorer.](https://technet.microsoft.com/library/dn454941.aspx)

## <a name="step-5-optional-disable-remember-password-prompt"></a>Etapa 5 (opcional): Desabilitar o prompt "Lembrar senha"
Quando usando Olá extensão do painel de acesso de usuários entrar toowebsites, Internet Explorer pode mostrar a seguir Olá prompt perguntando "deseja toostore sua senha?"

![](./media/active-directory-saas-ie-group-policy/remember-password-prompt.png)

Se você desejar tooprevent que os usuários vejam esse prompt, siga as etapas de saudação abaixo tooprevent preenchimento automático de senhas reconheçam:

1. Em Olá **Editor de gerenciamento de política de grupo** janela, vá toohello caminho listado abaixo. Essa configuração só está disponível em **Configuração do usuário**.
   
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/`
2. Localizar configuração Olá denominada **ativar o recurso de preenchimento automático de saudação para nomes de usuário e senhas em formulários**.
   
   > [!NOTE]
   > Versões anteriores do Active Directory podem listar essa configuração com o nome da saudação **não permitir senha de preenchimento automático toosave**. configuração Olá para essa configuração é diferente da saudação configuração descrito neste tutorial.
   > 
   > 
   
    ![Lembre-se toolook para isso em configurações de usuário.](./media/active-directory-saas-ie-group-policy/disable-auto-complete.png)
3. Olá acima configuração clique com botão direito e selecione **editar**.
4. Na janela de saudação intitulada **ativar o recurso de preenchimento automático de saudação para nomes de usuário e senhas em formulários**, selecione **desabilitado**.
   
    ![Selecione Desabilitar](./media/active-directory-saas-ie-group-policy/disable-passwords.png)
5. Clique em **Okey** tooapply essas alterações e a janela de saudação fechar.

Usuários não serão ser capaz de toostore suas credenciais ou usar credenciais de preenchimento automático tooaccess armazenado anteriormente. No entanto, essa política permitem que os usuários toocontinue toouse preenchimento automático para outros tipos de campos de formulário, como campos de pesquisa.

> [!WARNING]
> Se essa política está habilitada depois que os usuários escolheu toostore algumas credenciais, a política será *não* Limpar credenciais Olá que já foram armazenadas.
> 
> 

## <a name="step-6-testing-hello-deployment"></a>Etapa 6: Teste implantação
Siga as etapas de saudação abaixo tooverify se Olá extensão implantação foi bem-sucedida:

1. Se você implantou usando **configuração do computador**, logon em um computador cliente que pertence a toohello UO que você selecionou na [etapa 2: criar hello GPO](#step-2-create-the-group-policy-object). Se você implantou usando **configuração do usuário**, verifique se toosign em como um usuário que pertence a toothat UO.
2. Pode levar alguns sinal ins Olá de diretiva de grupo altera toofully atualização com esse computador. atualização do tooforce hello, abra um **Prompt de comando** janela e execução hello comando a seguir:`gpupdate /force`
3. Você deve reiniciar a máquina Olá para local de tootake instalação Olá. Inicialização pode levar consideravelmente mais tempo do que o normal ao extensão Olá instala.
4. Depois de reiniciar, abra o **Internet Explorer**. No hello canto direito superior da janela de saudação, clique em **ferramentas** (ícone de engrenagem Olá) e, em seguida, selecione **gerenciar complementos**.
   
    ![Vá tooTools > Gerenciar complementos](./media/active-directory-saas-ie-group-policy/manage-add-ons.png)
5. Em Olá **gerenciar complementos** janela, verifique se esse Olá **extensão do painel de acesso** foi instalado e que seu **Status** foi definido muito**habilitado**.
   
    ![Verifique se esse Olá extensão do painel de acesso está instalado e habilitado.](./media/active-directory-saas-ie-group-policy/verify-install.png)

## <a name="related-articles"></a>Artigos relacionados
* [Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure](active-directory-apps-index.md)
* [Acesso a aplicativos e logon único com o Active Directory do Azure](active-directory-appssoaccess-whatis.md)
* [Solução de problemas Olá extensão do painel de acesso para o Internet Explorer](active-directory-saas-ie-troubleshooting.md)

