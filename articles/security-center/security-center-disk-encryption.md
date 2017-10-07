---
title: "aaaEncrypt uma máquina Virtual do Azure | Microsoft Docs"
description: "Este documento ajuda tooencrypt uma máquina Virtual Azure depois de receber um alerta da Central de segurança do Azure."
services: security, security-center
documentationcenter: na
author: TomShinder
manager: swadhwa
editor: 
ms.assetid: f6c28bc4-1f79-4352-89d0-03659b2fa2f5
ms.service: security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/15/2017
ms.author: tomsh
ms.openlocfilehash: 7c7c6eed39d16bde8a0dfaffe3a3331c58101634
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-an-azure-virtual-machine"></a>Criptografar uma Máquina Virtual do Azure
A Central de Segurança do Azure alertará você se houver máquinas virtuais que não estejam criptografadas. Esses alertas mostrará como recomendação de alta gravidade e hello é tooencrypt essas máquinas virtuais.

![Recomendação de criptografia de disco](./media/security-center-disk-encryption/security-center-disk-encryption-fig1.png)

> [!NOTE]
> Olá informações deste documento se aplicam a máquinas virtuais de tooencrypting sem usar uma chave de criptografia de chave (que é necessário para fazer backup de máquinas virtuais usando o Backup do Azure). Consulte o artigo de saudação [disco criptografia para o Microsoft Azure e máquinas virtuais do Linux Azure](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) para obter informações sobre como toouse toosupport uma chave de criptografia de chave do Azure Backup para criptografados máquinas virtuais do Azure.
>
>

tooencrypt máquinas virtuais do Azure que foram identificados pela Central de segurança do Azure que precisam de criptografia, é recomendável Olá etapas a seguir:

* Instalar e configurar o PowerShell do Azure. Isso permitirá que você toorun Olá PowerShell comandos necessário tooset a saudação de pré-requisitos necessários tooencrypt máquinas virtuais do Azure.
* Obter e executar o script do PowerShell do Azure disco criptografia pré-requisitos do Azure Olá
* Criptografar suas máquinas virtuais

meta de saudação deste documento é tooenable você tooencrypt as máquinas virtuais, mesmo se você tem pouca ou nenhuma experiência no Azure PowerShell.
Este documento assume que você está usando o Windows 10 como computador de cliente de saudação do qual você irá configurar a criptografia de disco do Azure.

Há várias abordagens que podem ser usados toosetup Olá pré-requisitos e criptografia tooconfigure para máquinas virtuais do Azure. Se você já estiver bem familiarizado com Azure PowerShell ou CLI do Azure, talvez você prefira abordagens alternativas toouse.

> [!NOTE]
> toolearn mais informações sobre criptografia de tooconfiguring métodos alternativos para máquinas virtuais do Azure, consulte [disco criptografia para o Microsoft Azure e máquinas virtuais do Linux Azure](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).
>
>

## <a name="install-and-configure-azure-powershell"></a>Instalar e configurar o PowerShell do Azure
Você precisa do Azure PowerShell versão 1.2.1, ou superior, instalado no computador. artigo Olá [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) contém todas as etapas de saudação precisar tooprovision toowork seu computador com o Azure PowerShell. Olá mais simples é mencionada no artigo abordagem de instalação toouse Olá Web PI. Mesmo se você já tiver o Azure PowerShell instalado, instale novamente usando a abordagem de Web PI Olá para que você tenha a versão mais recente de saudação do PowerShell do Azure.

## <a name="obtain-and-run-hello-azure-disk-encryption-prerequisites-configuration-script"></a>Obter e executar script de configuração de pré-requisitos de criptografia de disco do Azure Olá
Olá Script de configuração de pré-requisitos de criptografia do Azure disco irá configurar todos os pré-requisitos de saudação necessários para criptografar as máquinas virtuais do Azure.

1. Página do GitHub toohello vá com hello [Script de instalação pré-requisitos do Azure disco criptografia](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).
2. Na página de GibHub hello, clique em Olá **Raw** botão.
3. Use **CTRL-A** tooselect todos os Olá texto na página hello e, em seguida, usar **CTRL-C** toocopy todos Olá texto na área de transferência do hello página toohello.
4. Abra **o bloco de notas** e cole o texto de saudação copiada no bloco de notas.
5. Crie uma nova pasta na unidade C: denominada **AzureADEScript**.
6. Salve o arquivo do bloco de notas hello – clique **arquivo**, em seguida, clique em **Salvar como**. No texto de nome de arquivo hello, digite **"ADEPrereqScript.ps1"** e clique em **salvar**. (Verifique se você colocar Olá Olá nome aspas, caso contrário, ele salvará o arquivo hello com uma extensão de arquivo. txt).

Agora que o conteúdo do script hello for salvo, abra script Olá Olá ISE do PowerShell:

1. No Menu Iniciar do hello, clique em **Cortana**. Peça **Cortana** "PowerShell" digitando **PowerShell** na caixa de texto de pesquisa Olá Cortana.
2. Clique com o botão direito do mouse em **ISE do Windows PowerShell** e clique em **Executar como administrador**.
3. Em Olá **administrador: ISE do Windows PowerShell** janela, clique em **exibição** e, em seguida, clique em **Mostrar painel de Script**.
4. Se você vir Olá **comandos** painel Olá direita da janela de saudação, clique em Olá **"x"** no canto superior direito de saudação do hello painel tooclose-lo. Se o texto de saudação é muito pequeno para você toosee, use **CTRL + adicionar** ("Adição" Olá "+" assinar). Se o texto de saudação é muito grande, use **CTRL + Subtract** (subtrair é hello "-" logon).
5. Clique em **Arquivo** e clique em **Abrir**. Navegue toohello **C:\AzureADEScript** pasta e hello clique duas vezes em Olá **ADEPrereqScript**.
6. Olá **ADEPrereqScript** conteúdo agora deve aparecer em Olá PowerShell ISE e é codificada por cor toohelp você ver vários componentes, como comandos, parâmetros e variáveis com mais facilidade.

Agora você verá algo parecido com hello figura abaixo.

![Janela do ISE do PowerShell](./media/security-center-disk-encryption/security-center-disk-encryption-fig2.png)

painel superior Olá é chamado tooas hello "painel de script" e painel inferior de saudação é chamado tooas hello "console". Usaremos esses termos neste artigo.

## <a name="run-hello-azure-disk-encryption-prerequisites-powershell-command"></a>Execute o comando de PowerShell do hello disco Azure criptografia pré-requisitos
Olá script pré-requisitos de criptografia de disco do Azure pedirá Olá informações a seguir depois de iniciar o script hello:

* **Nome do grupo de recursos** - nome de grupo de recursos que você deseja tooput do hello Olá Cofre de chaves em.  Um novo grupo de recurso com nome de saudação será criado se já houver um com esse nome criado. Se você já tiver um grupo de recursos que você deseja toouse nesta assinatura, em seguida, digite o nome de saudação desse grupo de recursos.
* **Nome do Cofre de chave** -nome do Cofre de chaves de saudação em que a criptografia chaves são toobe colocado. Um novo Cofre da Chave com esse nome será criado caso você ainda não tenha um com esse nome. Se você já tiver um cofre de chaves que você deseja toouse, digite o nome de saudação do hello existente Cofre de chaves.
* **Local** -local do hello Cofre de chaves. Verifique se toobe Cofre de chaves e VMs Olá criptografado no hello mesmo local. Se você não souber o local do hello, há etapas neste artigo que lhe mostrará como toofind-out.
* **Nome do Azure de aplicativo do Active Directory** -nome de aplicativo do Active Directory do Azure que será usado toowrite segredos toohello Cofre de chaves do hello. Será criado um novo aplicativo com esse nome caso ele não exista. Se você já tiver um aplicativo do Active Directory do Azure que você deseja toouse, insira o nome de saudação do aplicativo do Azure Active Directory.

> [!NOTE]
> Se você estiver curioso como toowhy precisar toocreate um aplicativo do Active Directory do Azure, consulte *registrar um aplicativo com o Azure Active Directory* seção Olá artigo [guia de Introdução ao Azure Key Vault](../key-vault/key-vault-get-started.md).
>
>

Execute Olá seguindo as etapas tooencrypt uma máquina Virtual do Azure:

1. Se você fechou Olá ISE do PowerShell, abra uma instância com privilégios elevados do hello PowerShell ISE. Siga as instruções de saudação neste artigo se Olá que PowerShell ISE não ainda estiver aberto. Se você fechou o script hello, abra Olá **ADEPrereqScript.ps1** clicando em **arquivo**, em seguida, **abrir** e selecionando o script hello da saudação **c:\ AzureADEScript** pasta. Se você seguiu neste artigo do início do hello, apenas vá toohello próxima etapa.
2. No console de saudação do hello PowerShell ISE (painel do hello inferior da saudação PowerShell ISE), alterar Olá foco toohello local do script hello digitando **cd c:\AzureADEScript** e pressione **ENTER**.
3. Definir política de execução de saudação em seu computador para que você possa executar o script hello. Tipo **Set-ExecutionPolicy Unrestricted** em Olá console e pressione ENTER. Se você vir uma caixa de diálogo informando sobre os efeitos de saudação da política de tooexecution de alteração de saudação, clique em **Sim tooall** ou **Sim** (se você vir **Sim tooall**, selecione a opção – se Você não vir **Sim tooall**, em seguida, clique em **Sim**).
4. Faça logon na sua conta do Azure. No console do hello, digite **Login AzureRmAccount** e pressione **ENTER**. Será exibida uma caixa de diálogo em que você insira suas credenciais (Verifique se você tem máquinas virtuais do direitos toochange hello – se você não tiver direitos, não será capaz de tooencrypt-los. Se você não tiver certeza, pergunte ao proprietário da assinatura ou ao administrador). Você deverá ver informações sobre seu **Ambiente**, **Conta**, **TenantId**, **SubscriptionId** e **CurrentStorageAccount**. Saudação de cópia **SubscriptionId** tooNotepad. Você precisará toouse isso na etapa &#6;.
5. Localizar sua máquina virtual de qual assinatura pertence tooand seu local. Vá muito[https://portal.azure.com](ttps://portal.azure.com) e faça logon.  No hello lado esquerdo da página de saudação, clique em **máquinas virtuais**. Você verá uma lista de suas máquinas virtuais e assinaturas de saudação pertencerem a.

   ![Máquinas Virtuais](./media/security-center-disk-encryption/security-center-disk-encryption-fig3.png)
6. Retorne toohello PowerShell ISE. Definir Olá assinatura contexto no qual o script hello será executado. No console do hello, digite **AzureRmSubscription selecione – SubscriptionId < your_subscription_Id >** (substitua **< your_subscription_Id >** com sua ID de assinatura real) e pressione  **Digite**. Você verá informações sobre Olá ambiente, **conta**, **TenantId**, **SubscriptionId** e **CurrentStorageAccount**.
7. Agora você está pronto toorun script de saudação. Clique em Olá **Executar Script** botão ou pressione **F5** teclado hello.

   ![Execução de script do PowerShell](./media/security-center-disk-encryption/security-center-disk-encryption-fig4.png)
8. script Hello solicita **resourceGroupName:** -Insira nome de saudação do *grupo de recursos* você deseja toouse, em seguida, pressione **ENTER**. Se você não tiver um, insira um nome que você deseja toouse para um novo. Se você já tiver um *grupo de recursos* que você deseja toouse (como Olá um que sua máquina virtual está em), digite nome Olá Olá grupo de recursos existente.
9. script Hello solicita **keyVaultName:** -Insira nome de saudação do hello *Cofre de chaves* desejado toouse e pressione ENTER. Se você não tiver um, insira um nome que você deseja toouse para um novo. Se você já tiver um cofre de chaves que você deseja toouse, digite o nome de saudação do hello existente *Cofre de chaves*.
10. script Hello solicita **local:** - Insira nome de saudação do local de saudação em qual Olá VM que você deseja tooencrypt está localizado, e pressione **ENTER**. Se você não lembrar local hello, volte toostep #5.
11. script Hello solicita **aadAppName:** -Insira nome de saudação do hello *Active Directory do Azure* aplicativo deseja toouse, em seguida, pressione **ENTER**. Se você não tiver um, insira um nome que você deseja toouse para um novo. Se você já tiver um *aplicativo do Azure Active Directory* que você deseja toouse, digite nome de saudação do hello existente *aplicativo do Azure Active Directory*.
12. Será exibida uma caixa de diálogo de logon. Forneça suas credenciais (Sim, você fez uma vez, mas agora, é necessário toodo-lo novamente).
13. executa o script Hello e ao concluir solicitará que você toocopy valores Olá Olá **aadClientID**, **aadClientSecret**, **diskEncryptionKeyVaultUrl**e **keyVaultResourceId**. Copiar cada área de transferência de toohello esses valores e colá-los no bloco de notas.
14. Retornar toohello PowerShell ISE e coloque o cursor Olá final Olá Olá última linha e pressione **ENTER**.

saída de saudação do script hello deve ser semelhante a tela hello abaixo:

![Saída do PowerShell](./media/security-center-disk-encryption/security-center-disk-encryption-fig5.png)

## <a name="encrypt-hello-azure-virtual-machine"></a>Criptografar Olá máquina virtual do Azure
Você está agora pronto tooencrypt sua máquina virtual. Se sua máquina virtual está localizada em Olá mesmo grupo de recursos, como seu Cofre de chave, você pode mover na seção de etapas de criptografia toohello. No entanto, se sua máquina virtual não está em hello mesmo recurso de grupo como seu Cofre de chaves, você precisará tooenter seguinte Olá console Olá Olá ISE do PowerShell:

**$resourceGroupName = <’GR_da_Máquina_Virtual’>**

Substituir **< Virtual_Machine_RG >** com nome Olá Olá do grupo de recursos contidas na qual as máquinas virtuais, delimitados por aspas simples. Em seguida, pressione **ENTER**.
tooconfirm Olá correto foi digitado o nome de grupo de recursos, digite a seguir Olá Olá console de ISE do PowerShell:

**$resourceGroupName**

Pressione **ENTER**. Você deve ver o nome de saudação do grupo de recursos localizados em suas máquinas virtuais. Por exemplo:

![Saída do PowerShell](./media/security-center-disk-encryption/security-center-disk-encryption-fig6.png)

### <a name="encryption-steps"></a>Etapas de criptografia
Primeiro, é necessário o nome de saudação do PowerShell tootell da máquina virtual de saudação desejado tooencrypt. No console do hello, digite:

**$vmName = <’nome_da_sua_vm’>**

Substituir **<'your_vm_name ' >** com o nome de saudação da VM (Verifique se o nome hello está circundada por uma aspa simples) e, em seguida, pressione **ENTER**.

tooconfirm que Olá correto VM nome foi inserido, digite:

**$vmName**

Pressione **ENTER**. Você deve ver Olá nome da máquina virtual de saudação desejado tooencrypt. Por exemplo:

![Saída do PowerShell](./media/security-center-disk-encryption/security-center-disk-encryption-fig7.png)

Há dois métodos toorun Olá criptografia comando tooencrypt todas as unidades na máquina virtual de saudação. Olá primeiro método é Olá tootype comando no hello console de ISE do PowerShell a seguir:

~~~
Set-AzureRmVMDiskEncryptionExtension -ResourceGroupName $resourceGroupName -VMName $vmName -AadClientID $aadClientID -AadClientSecret $aadClientSecret -DiskEncryptionKeyVaultUrl $diskEncryptionKeyVaultUrl -DiskEncryptionKeyVaultId $keyVaultResourceId -VolumeType All
~~~

Depois de digitar esse comando, pressione **ENTER**.

Olá segundo método é tooclick no painel de script hello (painel superior Olá de saudação PowerShell ISE) e role para baixo toohello inferior do script hello. Realce comando Olá listado acima e, em seguida, clique com botão direito-lo e, em seguida, clique em **executar seleção** ou pressione **F8** teclado hello.

![ISE do PowerShell](./media/security-center-disk-encryption/security-center-disk-encryption-fig8.png)

Independentemente do método hello você usar uma caixa de diálogo será exibida informando que levará 10 a 15 minutos para Olá operação toocomplete. Clique em **Sim**.

Durante o processo de criptografia Olá, você pode retornar toohello Portal do Azure e ver o status de saudação da máquina virtual de saudação. No hello lado esquerdo da página de saudação, clique em **máquinas virtuais**, em seguida no hello **máquinas virtuais** folha, clique Olá nome da máquina virtual de saudação estiver criptografando. Na folha de saudação que aparece, você observará que Olá **Status** diz que é **atualização**. Isso demonstra que a criptografia está em andamento.

![Para obter mais detalhes sobre Olá VM](./media/security-center-disk-encryption/security-center-disk-encryption-fig9.png)

Retorne toohello PowerShell ISE. Quando o script hello for concluído, você verá o que é exibido na figura abaixo a saudação.

![Saída do PowerShell](./media/security-center-disk-encryption/security-center-disk-encryption-fig10.png)

toodemonstrate que Olá máquina virtual agora é criptografada, retornar toohello Portal do Azure e clique em **máquinas virtuais** em Olá lado esquerdo da página de saudação. Clique Olá nome da máquina virtual de saudação que você criptografou. Em Olá **configurações** folha, clique em **discos**.

![Opções de configurações](./media/security-center-disk-encryption/security-center-disk-encryption-fig11.png)

Em Olá **discos** folha, você verá que **criptografia** é **habilitado**.

![Propriedades de discos](./media/security-center-disk-encryption/security-center-disk-encryption-fig12.png)

## <a name="next-steps"></a>Próximas etapas
Neste documento, você aprendeu como tooencrypt uma máquina Virtual do Azure. toolearn mais sobre o Centro de segurança do Azure, consulte o seguinte hello:

* [Monitoramento de integridade de segurança na Central de segurança do Azure](security-center-monitoring.md) – Saiba como toomonitor Olá a integridade de seus recursos do Azure
* [Gerenciando e respondendo toosecurity alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md) -Saiba como alertas de toosecurity toomanage e responder
* [Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md) – localizar perguntas frequentes sobre como usar o serviço de saudação
* [Blog de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) – encontre postagens no blog sobre conformidade e segurança do Azure
