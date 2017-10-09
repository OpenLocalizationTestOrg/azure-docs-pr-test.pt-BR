---
title: 'Azure AD Connect: atualizar do DirSync | Microsoft Docs'
description: "Saiba como tooupgrade do DirSync tooAzure AD Connect. Este artigo descreve as etapas de saudação de atualização do DirSync tooAzure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: baf52da7-76a8-44c9-8e72-33245790001c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 05572af410698deaa1392c8837bfcb749efc69e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-upgrade-from-dirsync"></a>Azure AD Connect: atualizar do DirSync
Conexão do AD do Azure é Olá sucessor tooDirSync. Você encontrar formas de saudação, que você pode atualizar do DirSync neste tópico. Essas etapas não funcionam para atualizar de outra versão do Azure AD Connect ou do Azure AD Sync.

Antes de iniciar a instalação do Azure AD Connect, certifique-se muito[download do Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771) e etapas de pré-requisito concluída Olá no [do Azure AD Connect: pré-requisitos de Hardware e](active-directory-aadconnect-prerequisites.md). Em particular, você deseja tooread sobre hello, como essas áreas são diferentes do DirSync:

* versão necessária de saudação do .net e do PowerShell. Versões mais recentes são toobe necessária no servidor de saudação do qual DirSync necessário.
* configuração do servidor proxy Hello. Se você usar um tooreach de servidor proxy Olá da internet, essa configuração deve ser definida antes de atualizar. DirSync usado sempre o servidor de proxy de saudação configurado para o usuário Olá instalá-lo, mas as configurações da máquina do Azure AD Connect usa em vez disso.
* Olá URLs necessária toobe abrir no servidor de proxy de saudação. Para cenários básicos, os cenários DirSync, também têm suportados os requisitos de saudação são Olá mesmo. Se você quiser toouse Olá novos recursos incluídos com o Azure AD Connect, algumas novas URLs devem ser abertas.

> [!NOTE]
> Depois que você habilitou a sua nova conexão do AD do Azure server toostart sincronizando alterações tooAzure AD, não reverta toousing DirSync ou o Azure AD Sync. Downgrade de clientes do Azure AD Connect toolegacy incluindo DirSync e sincronização do AD do Azure não tem suporte e pode levar tooissues como perda de dados no AD do Azure.

Se você não estiver atualizando do DirSync, confira a [documentação relacionada](#related-documentation) para outros cenários.

## <a name="upgrade-from-dirsync"></a>Atualização do DirSync
Dependendo da sua implantação atual do DirSync, há diferentes opções de atualização de saudação. Se Olá esperado tempo de atualização é menos de três horas, recomendação Olá é toodo uma atualização in-loco. Se Olá esperado tempo de atualização é mais de três horas, recomendação Olá é toodo uma implantação paralela em outro servidor. Estima-se que se você tiver mais de 50.000 objetos leva mais de três horas toodo Olá atualização.

| Cenário |
| --- | --- |
| [Atualização in-loco](#in-place-upgrade) |
| [Implantação paralela](#parallel-deployment) |

> [!NOTE]
> Ao planejar tooupgrade do DirSync tooAzure AD Connect, não desinstale o DirSync por conta própria antes da atualização de saudação. Azure AD Connect lerá e migrar a configuração de saudação do DirSync e desinstalar depois de inspecionar o servidor de saudação.

**Atualização in-loco**  
Olá esperado de atualização de saudação do tempo toocomplete é exibida pelo Assistente de saudação. Essa estimativa se baseia na suposição de saudação que leva três horas toocomplete uma atualização para um banco de dados com 50.000 objetos (usuários, contatos e grupos). Se o número de saudação de objetos no banco de dados é menor que 50.000, o Azure AD Connect recomenda uma atualização in-loco. Se você decidir toocontinue, suas configurações atuais são aplicadas automaticamente durante a atualização e o servidor retoma automaticamente a sincronização do active.

Se você quiser toodo uma migração da configuração e fazer uma implantação paralela, em seguida, você pode substituir a recomendação de atualização Olá no local. Por exemplo, você poderia usar Olá oportunidade toorefresh Olá hardware e sistema operacional. Para obter mais informações, consulte Olá [paralelo implantação](#parallel-deployment) seção.

**Implantação paralela**  
Se você tiver mais de 50.000 objetos, é recomendável uma implantação paralela. Isso evita que atrasos operacionais sejam percebidos pelos usuários. Olá instalação do Azure AD Connect tentativas de tempo de inatividade tooestimate Olá para atualização hello, mas se você tiver atualizado o DirSync em Olá anterior, sua própria experiência é guia recomendadas do toobe provavelmente hello.

### <a name="supported-dirsync-configurations-toobe-upgraded"></a>Toobe de configurações com suporte DirSync atualizado
Olá alterações de configuração a seguir têm suporte com o DirSync atualizado:

* Domínio e filtragem de unidade organizacional
* ID alternativa (UPN)
* Sincronização de senha e configurações híbridas do Exchange
* Suas configurações de domínio/floresta e do AD do Azure
* Filtragem com base em atributos de usuário

Olá alteração a seguir não pode ser atualizado. Se você tem essa configuração, a atualização Olá será bloqueada:

* Alterações de DirSync sem suporte, por exemplo, atributos removidos e uso de uma DLL de extensão personalizada

![Atualização bloqueada](./media/active-directory-aadconnect-dirsync-upgrade-get-started/analysisblocked.png)

Nesses casos, Olá recomenda tooinstall um novo servidor do Azure AD Connect em [modo de preparo](active-directory-aadconnectsync-operations.md#staging-mode) e verifique se Olá DirSync antiga e nova configuração de conexão do AD do Azure. Aplique qualquer alteração novamente usando uma configuração personalizada, como descrito em [Configuração personalizada de sincronização do Azure AD Connect](active-directory-aadconnectsync-whatis.md).

as senhas de saudação usadas pelo DirSync Olá para contas de serviço não podem ser recuperadas e não são migradas. Essas senhas são redefinidas durante a atualização de saudação.

### <a name="high-level-steps-for-upgrading-from-dirsync-tooazure-ad-connect"></a>Etapas de alto nível para atualizar do DirSync tooAzure AD Connect
1. Bem-vindo tooAzure AD Connect
2. Análise da configuração do DirSync atual
3. Coletar senha de administrador global do AD do Azure
4. Coletar credenciais para uma conta de administrador de empresa (somente usado durante a instalação de saudação do Azure AD Connect)
5. Instalação do Azure AD Connect
   * Desinstalar o DirSync (ou desabilitá-lo temporariamente)
   * Instalar o Azure AD Connect
   * Opcionalmente, inicie a sincronização

Etapas adicionais são necessárias quando:

* Você está usando no momento o SQL Server completo - local ou remoto
* Você tem mais de 50.000 objetos no escopo para sincronização

## <a name="in-place-upgrade"></a>Atualização in-loco
1. Inicie Olá AD do Azure Connect instalador (MSI).
2. Examine e concorde toolicense termos e aviso de privacidade.  
   ![Bem-vindo tooAzure AD](./media/active-directory-aadconnect-dirsync-upgrade-get-started/Welcome.png)
3. Clique em Avançar análise toobegin da instalação existente do DirSync.  
   ![Analisando instalação de sincronização de diretório existente](./media/active-directory-aadconnect-dirsync-upgrade-get-started/Analyze.png)
4. Quando Olá análise for concluída, você verá as recomendações de saudação sobre como tooproceed.  
   * Se você usa o SQL Server Express e ter menos de 50.000 objetos, Olá tela a seguir é mostrada:  
     ![Análise concluída tooupgrade pronto do DirSync](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisReady.png)
   * Se você usar um SQL Server completo para DirSync, verá esta página:  
     ![Análise concluída tooupgrade pronto do DirSync](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisReadyFullSQL.png)  
     Olá informações sobre Olá existente do SQL Server servidor banco de dados que está sendo usado pelo DirSync são exibidas. Faça os ajustes apropriados se necessário. Clique em **próximo** toocontinue instalação de saudação.
   * Se você tiver mais de 50.000 objetos, verá esta tela:  
     ![Análise concluída tooupgrade pronto do DirSync](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisRecommendParallel.png)  
     tooproceed com uma atualização in-loco, clique em caixa de seleção próxima toothis mensagem hello: **continuar atualizando o DirSync neste computador.**
     toodo um [paralelo implantação](#parallel-deployment) em vez disso, você pode exportar definições de configuração do DirSync hello e mover Olá configuração toohello novo servidor.
5. Forneça a senha de saudação para conta Olá que utilizam tooconnect tooAzure AD. Isso deve ser conta Olá usada atualmente pelo DirSync.  
   ![Insira suas credenciais de AD do Azure](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ConnectToAzureAD.png)  
   Se você encontrar um erro e tiver problemas de conectividade, confira [Solucionar problemas de conectividade](active-directory-aadconnect-troubleshoot-connectivity.md).
6. Forneça uma conta de administrador corporativo para o Active Directory.  
   ![Inserir suas credenciais do ADDS](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ConnectToADDS.png)
7. Agora você está pronto tooconfigure. Quando você clica em **Atualizar**, DirSync é desinstalado e o Azure AD Connect é configurado e começa a sincronização.  
   ![Tooconfigure pronto](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ReadyToConfigure.png)
8. Após a instalação de saudação, sair e entrar novamente tooWindows antes de usar o Gerenciador de serviço de sincronização, o Editor de regra de sincronização, ou tente toomake outras alterações de configuração.

## <a name="parallel-deployment"></a>Implantação paralela
### <a name="export-hello-dirsync-configuration"></a>Exportar configuração do DirSync Olá
**Implantação paralela com mais de 50.000 objetos**

Se você tiver mais de 50.000 objetos, Olá do Azure AD Connect instalação recomenda uma implantação em paralela.

É exibida uma tela semelhante toohello a seguir:  
![Análise concluída](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisRecommendParallel.png)

Se você quiser tooproceed com implantação paralela, é necessário tooperform Olá etapas a seguir:

* Clique em Olá **exportar configurações** botão. Quando você instala o Azure AD Connect em um servidor separado, essas configurações são migradas da sua instalação atual do DirSync tooyour nova conexão do AD do Azure.

Depois que suas configurações foram exportadas com êxito, você pode sair Assistente de conexão do AD do Azure Olá no servidor do DirSync hello. Continue com a próxima etapa de saudação muito[instalar o Azure AD Connect em um servidor separado](#installation-of-azure-ad-connect-on-separate-server)

**Implantação paralela com menos de 50.000 objetos**

Se você tiver menos de 50.000 objetos, mas ainda desejar toodo implantação uma paralela, em seguida, Olá a seguir:

1. Execute hello Azure AD Connect installer (MSI).
2. Quando você vir Olá **tooAzure bem-vindo ao AD Connect** tela sair do assistente instalação Olá clicando hello "X" no canto superior direito de saudação da janela de saudação.
3. Abra um prompt de comando.
4. De saudação instalação local do Azure AD Connect (padrão: C:\Program Files\Microsoft Azure Active Directory Connect) execute Olá comando a seguir: `AzureADConnect.exe /ForceExport`.
5. Clique em Olá **exportar configurações** botão. Quando você instala o Azure AD Connect em um servidor separado, essas configurações são migradas da sua instalação atual do DirSync tooyour nova conexão do AD do Azure.

![Análise concluída](./media/active-directory-aadconnect-dirsync-upgrade-get-started/forceexport.png)

Depois que suas configurações foram exportadas com êxito, você pode sair Assistente de conexão do AD do Azure Olá no servidor do DirSync hello. Continue com a próxima etapa de saudação muito[instalar o Azure AD Connect em um servidor separado](#installation-of-azure-ad-connect-on-separate-server).

### <a name="install-azure-ad-connect-on-separate-server"></a>Instalar o Azure AD Connect em um servidor separado
Quando você instala o Azure AD Connect em um novo servidor, Olá pressupõe-se que você deseja tooperform uma instalação limpa do Azure AD Connect. Como você deseja que a configuração do toouse Olá DirSync, há algumas etapas adicionais tootake:

1. Execute hello Azure AD Connect installer (MSI).
2. Quando você vir Olá **tooAzure bem-vindo ao AD Connect** tela sair do assistente instalação Olá clicando hello "X" no canto superior direito de saudação da janela de saudação.
3. Abra um prompt de comando.
4. De saudação instalação local do Azure AD Connect (padrão: C:\Program Files\Microsoft Azure Active Directory Connect) execute Olá comando a seguir: `AzureADConnect.exe /migrate`.
   Assistente de instalação do Hello AD do Azure Connect é iniciada e apresenta Olá tela a seguir:  
   ![Insira suas credenciais de AD do Azure](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ImportSettings.png)
5. Selecione arquivo de configurações de hello exportada de sua instalação do DirSync.
6. Configure as opções avançadas incluindo:
   * Um local de instalação personalizada para o Azure AD Connect.
   * Uma instância existente do SQL Server (padrão: o Azure AD Connect instala o SQL Server 2012 Express). Não use Olá mesma instância de banco de dados que o servidor DirSync.
   * Uma conta de serviço usada tooconnect tooSQL Server (se o banco de dados do SQL Server for remoto, essa conta deverá ser uma conta de serviço de domínio).
     Essas opções podem ser vistas nesta tela:   
     ![Insira suas credenciais de AD do Azure](./media/active-directory-aadconnect-dirsync-upgrade-get-started/advancedsettings.png)
7. Clique em **Avançar**.
8. Em Olá **tooconfigure pronto** , deixe Olá **iniciar o processo de sincronização de Olá Olá configuração ser concluída assim que** marcada. Olá server está no [modo de preparo](active-directory-aadconnectsync-operations.md#staging-mode) alterações não são exportado tooAzure AD.
9. Clique em **Instalar**.
10. Após a instalação de saudação, sair e entrar novamente tooWindows antes de usar o Gerenciador de serviço de sincronização, o Editor de regra de sincronização, ou tente toomake outras alterações de configuração.

> [!NOTE]
> Começa a sincronização entre o Active Directory do Windows Server e Active Directory do Azure, mas nenhuma alteração é exportado tooAzure AD. Apenas uma ferramenta de sincronização pode exportar ativamente alterações de cada vez. Esse estado é chamado de [modo de preparo](active-directory-aadconnectsync-operations.md#staging-mode).

### <a name="verify-that-azure-ad-connect-is-ready-toobegin-synchronization"></a>Verifique se o Azure AD Connect é toobegin pronto sincronização
tooverify que o Azure AD Connect está pronto tootake através do DirSync, você precisa tooopen **Synchronization Service Manager** no grupo Olá **do Azure AD Connect** saudação do menu de início.

No aplicativo hello, acesse toohello **operações** guia. Nessa guia, confirme concluiu que Olá seguintes operações:

* Importar em Olá conector AD
* Importar em Olá conector AD do Azure
* Sincronização completa Olá conector AD
* Sincronização completa Olá conector AD do Azure

![Importação e sincronização concluídas](./media/active-directory-aadconnect-dirsync-upgrade-get-started/importsynccompleted.png)

Examine o resultado de saudação dessas operações e certifique-se de que não existem erros.

Se você quiser toosee e inspecionar alterações Olá sobre tooAzure toobe exportado AD, leia como tooverify Olá configuração em [modo de preparo](active-directory-aadconnectsync-operations.md#staging-mode). Faça alterações de configuração necessárias até que você não veja nada inesperado.

Você está pronto tooswitch do DirSync tooAzure AD quando você concluir essas etapas e estiver satisfeito com o resultado da saudação.

### <a name="uninstall-dirsync-old-server"></a>Desinstalar o DirSync (servidor antigo)
* Em **Programas e recursos**, localize a **ferramenta de sincronização do Windows Azure Active Directory**
* Desinstale a **Ferramenta de sincronização do Microsoft Azure Active Directory**
* desinstalação Olá pode levar até too15 toocomplete de minutos.

Se você preferir toouninstall DirSync mais tarde, você pode também temporariamente desligar o servidor de saudação ou desabilitar o serviço de saudação. Se algo der errado, esse método permite que você habilite toore-lo. No entanto, não é esperado que passo Olá falhará para que isso não será necessária.

Com DirSync desinstalado ou desativado, não há nenhum servidor ativo exportando tooAzure AD. Olá tooenable próximo da etapa do Azure AD Connect deve ser concluída antes que as alterações no Active Directory local continuará tooAzure toobe sincronizado AD.

### <a name="enable-azure-ad-connect-new-server"></a>Habilitar o Azure AD Connect (novo servidor)
Após a instalação, reabrir o AD do Azure conectar será permitem toomake alterações de configuração adicionais. Iniciar **do Azure AD Connect** saudação do menu de início ou de atalho do hello na área de trabalho de saudação. Verifique se que você não tente toorun Olá instalação MSI novamente.

Você verá a seguinte hello:  
![Tarefas adicionais](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AdditionalTasks.png)

* Selecione **Configurar modo de preparo**.
* Desativar preparo Olá desmarcando **modo de preparo habilitado** caixa de seleção.

![Insira suas credenciais de AD do Azure](./media/active-directory-aadconnect-dirsync-upgrade-get-started/configurestaging.png)

* Clique em Olá **próximo** botão
* Na página de confirmação de saudação, clique em Olá **instalar** botão.

Azure AD Connect é agora o servidor ativo e não alterne toousing voltar do servidor DirSync existente.

## <a name="next-steps"></a>Próximas etapas
Agora que você tem o Azure AD Connect instalado, você pode [verificar a instalação do hello e atribuir licenças](active-directory-aadconnect-whats-next.md).

Saiba mais sobre esses novos recursos que foram habilitados com instalação Olá: [atualização automática](active-directory-aadconnect-feature-automatic-upgrade.md), [impedir exclusões acidentais](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md), e [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-sync.md).

Saiba mais sobre esses tópicos comuns: [Agendador e como a sincronização tootrigger](active-directory-aadconnectsync-feature-scheduler.md).

Saiba mais sobre [Como integrar suas identidades locais ao Active Directory do Azure](active-directory-aadconnect.md).
