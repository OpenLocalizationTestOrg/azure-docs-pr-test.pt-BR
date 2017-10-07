---
title: aaaSetting o acesso condicional no local, usando o registro de dispositivo do Active Directory do Azure | Microsoft Docs
description: "Um guia passo a passo tooenabling acesso condicional tooon aplicativos locais usando os serviços de Federação do Active Directory (AD FS) no Windows Server 2012 R2."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 6ae9df8b-31fe-4d72-9181-cf50cfebbf05
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 808e3b96873102aebae667153f588dcdb205e884
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-on-premises-conditional-access-by-using-azure-active-directory-device-registration"></a>Configurando o acesso condicional local usando o registro de dispositivo do Azure Active Directory
Quando você precisar de junção tooworkplace usuários toohello seus dispositivos pessoais serviço de registro de dispositivo do Azure Active Directory (AD do Azure), seus dispositivos podem ser marcados como organização tooyour conhecidos. A seguir é um guia passo a passo para habilitar aplicativos de locais de tooon de acesso condicional usando os serviços de Federação do Active Directory (AD FS) no Windows Server 2012 R2.

> [!NOTE]
> Uma licença do Office 365 ou do Azure AD Premium é necessária ao usar dispositivos registrados nas políticas de acesso condicional do serviço de registro de dispositivo do Azure Active Directory. Elas incluem políticas que são impostas pelo AD FS em recursos locais.
> 
> Para obter mais informações sobre cenários de acesso condicional Olá para recursos locais, consulte [ingresse tooworkplace de qualquer dispositivo para SSO e autenticação de dois fatores contínua em aplicativos da empresa](https://technet.microsoft.com/library/dn280945.aspx).

Esses recursos estão disponíveis toocustomers que adquirir uma licença Azure Active Directory Premium.

## <a name="supported-devices"></a>Dispositivos com suporte
* Dispositivos Windows 7 ingressados no domínio
* Dispositivos Windows 8.1 pessoais e ingressados no domínio
* iOS 6 e posterior para o navegador Safari Olá
* Android 4.0 ou posterior, Samsung GS3 ou telefones posteriores, Samsung Galaxy Note 2 ou tablets posteriores

## <a name="scenario-prerequisites"></a>Pré-requisitos do cenário
* Assinatura tooOffice 365 ou Azure Active Directory Premium
* Um locatário do Azure Active Directory
* Windows Server Active Directory (Windows Server 2008 ou posterior)
* Esquema atualizado no Windows Server 2012 R2
* Licença do Azure Active Directory Premium
* Windows Server 2012 R2 serviços de federação, configurado para SSO tooAzure AD
* Proxy de Aplicativo Web do Windows Server 2012 R2 
* Azure AD Connect (Microsoft Azure Active Directory Connect) [(Baixar o Azure AD Connect)](http://www.microsoft.com/en-us/download/details.aspx?id=47594)
* Domínio verificado

## <a name="known-issues-in-this-release"></a>Problemas conhecidos nesta versão
* Políticas de acesso condicional baseado em dispositivo exigem tooActive de write-back de objeto de dispositivo diretório do Active Directory do Azure. Pode demorar até toothree horas para dispositivo objetos toobe gravados tooActive Directory.
* dispositivos iOS 7 sempre solicitar Olá usuário tooselect um certificado durante a autenticação de certificado de cliente.
* Algumas versões do iOS 8 anteriores ao iOS 8.3 não funcionam.

## <a name="scenario-assumptions"></a>Suposições de cenário
Este cenário pressupõe que você tenha um ambiente híbrido que consiste em um locatário do Azure AD e um Active Directory local. Esses locatários devem ser conectados com o Azure AD Connect, com um domínio verificado e com o AD FS para SSO. Use Olá toohelp de lista de verificação que você configurar seu ambiente de acordo com os requisitos de toohello a seguir.

## <a name="checklist-prerequisites-for-conditional-access-scenario"></a>Lista de verificação: pré-requisitos para o cenário de acesso condicional
Conecte seu locatário do Azure AD à instância do Active Directory local.

## <a name="configure-azure-active-directory-device-registration-service"></a>Configurar o serviço de registro de dispositivo do Azure Active Directory
Use esta guia toodeploy e configurar o serviço de registro de dispositivo Olá Active Directory do Azure para sua organização.

Este guia pressupõe que você tenha configurado o Windows Server Active Directory e se inscreveu tooMicrosoft Active Directory do Azure. Consulte os pré-requisitos de saudação descritos anteriormente.

Olá toodeploy serviço de registro de dispositivo do Active Directory do Azure com o Active Directory do Azure locatário tarefas completa Olá Olá lista de verificação na ordem a seguir. Quando um link de referência tópico conceitual tooa, retorne toothis checklist posteriormente, para que você pode continuar com a saudação demais tarefas. Algumas tarefas incluem uma etapa de validação de cenário que pode ajudá-lo a confirmar se a etapa Olá foi concluída com êxito.

## <a name="part-1-enable-azure-active-directory-device-registration"></a>Parte 1: Habilitar o registro de dispositivo do Azure Active Directory
Siga as etapas de Olá Olá tooenable de lista de verificação e configurar o serviço de registro de dispositivo do Active Directory do Azure Olá.

| Tarefa | Referência | 
| --- | --- |
| Habilite o registro de dispositivo no Active Directory do Azure locatário tooallow dispositivos toojoin Olá no local de trabalho. Por padrão, o Azure multi-Factor Authentication não está habilitado para o serviço de saudação. No entanto, recomendamos usar a Autenticação Multifator ao registrar um dispositivo. Antes de habilitar a Autenticação Multifator no serviço de registro do Active Directory, verifique se o AD FS está configurado para um provedor de Autenticação Multifator. |[Habilitar o registro de dispositivo do Azure Active Directory](active-directory-device-registration-get-started.md)| 
|Os dispositivos descobrem o serviço de registro de dispositivo do Azure Active Directory procurando registros DNS conhecidos. Configure o DNS de sua empresa, de modo que os dispositivos possam descobrir seu serviço de registro de dispositivo do Azure Active Directory. |[Configurar a descoberta de registro de dispositivo do Azure Active Directory](active-directory-device-registration-get-started.md)| 


## <a name="part-2-deploy-and-configure-windows-server-2012-r2-active-directory-federation-services-and-set-up-a-federation-relationship-with-azure-ad"></a>Parte 2: implantar e configurar os Serviços de Federação do Active Directory do Windows Server 2012 R2 e configurar uma relação de federação com o AD do Azure

| Tarefa | Referência |
| --- | --- |
| Implante serviços de domínio do Active Directory com extensões de esquema do Windows Server 2012 R2 hello. Não é necessário tooupgrade qualquer um dos seus controladores de domínio tooWindows Server 2012 R2. atualização do esquema Olá é requisito somente hello. |[Atualize o esquema do Active Directory Domain Services](#upgrade-your-active-directory-domain-services-schema) |
| Os dispositivos descobrem o serviço de registro de dispositivo do Azure Active Directory procurando registros DNS conhecidos. Configure o DNS de sua empresa, de modo que os dispositivos possam descobrir seu serviço de registro de dispositivo do Azure Active Directory. |[Preparar seu Active Directory para dar suporte a dispositivos](#prepare-your-active-directory-to-support-devices) |

## <a name="part-3-enable-device-writeback-in-azure-ad"></a>Parte 3: habilitar write-back de dispositivos no AD do Azure
| Tarefa | Referência |
| --- | --- |
| Conclua a parte dois de “Habilitando o write-back de dispositivo no Azure AD Connect”. Depois de concluir o processo, retorne toothis guia. |[Habilitando write-back de dispositivo no Azure AD Connect](#upgrade-your-active-directory-domain-services-schema) |

## <a name="optional-part-4-enable-multi-factor-authentication"></a>[Opcional] Parte 4: Habilitar a Autenticação Multifator
É altamente recomendável que você configure uma saudação várias opções para a autenticação multifator. Se você quiser toorequire multi-Factor Authentication, consulte [escolha a solução de segurança de autenticação multifator Olá para você](../multi-factor-authentication/multi-factor-authentication-get-started.md). Ele inclui uma descrição de cada solução e links toohelp, você pode configurar a solução Olá de sua escolha.

## <a name="part-5-verification"></a>Parte 5: verificação
Olá implantação agora está concluída e você pode experimentar alguns cenários. Use Olá a seguir contém links tooexperiment com o serviço de saudação e familiarizar-se com seus recursos.

| Tarefa | Referência |
| --- | --- |
| Una o local de trabalho de tooyour alguns dispositivos usando o serviço de registro de dispositivo do Active Directory do Azure. Una dispositivos iOS, Windows e Android. |[Unir dispositivos tooyour no local de trabalho usando o serviço de registro de dispositivo do Active Directory do Azure](#join-devices-to-your-workplace-using-azure-active-directory-device-registration) |
| Exibir e habilitar ou desabilitar os dispositivos registrados usando o portal do administrador hello. Nesta tarefa, você pode exibir alguns dispositivos registrados usando o portal do administrador hello. |[Visão geral do serviço de registro de dispositivo do Azure Active Directory](active-directory-device-registration-get-started.md) |
| Verifique se que objetos de dispositivo são gravados do Active Directory do Azure tooWindows servidor Active Directory. |[Verifique se os dispositivos registrados são gravados tooActive diretório](#verify-registered-devices-are-written-back-to-active-directory) |
| Agora que os usuários podem registrar seus dispositivos, você pode criar políticas de acesso de aplicativo no AD FS que permitem apenas dispositivos registrados. Nesta tarefa, você cria uma regra de acesso do aplicativo e uma mensagem personalizada de acesso negado. |[Criar uma política de acesso do aplicativo e uma mensagem personalizada de acesso negado](#create-an-application-access-policy-and-custom-access-denied-message) |

## <a name="integrate-azure-active-directory-with-on-premises-active-directory"></a>Integrar o Azure Active Directory ao Active Directory local
Esta etapa ajuda você a integrar o locatário do Azure AD ao Active Directory local, usando o Azure AD Connect. Embora etapas Olá estão disponíveis no portal clássico do Azure de saudação, anote as instruções especiais que estão listados nesta seção.

1. Entre no toohello portal clássico do Azure usando uma conta que seja um administrador global no AD do Azure.
2. No painel esquerdo do hello, selecione **do Active Directory**.
3. Em Olá **diretório** , selecione seu diretório.
4. Selecione Olá **integração de diretórios** guia.
5. Em Olá **implantar e gerenciar** seção, siga as etapas 1 a 3 toointegrate Active Directory do Azure com seu diretório local.
   
   1. Adicionar domínios.
   2. Instalar e executar o Azure AD Connect usando as instruções de saudação em [instalação personalizada do Azure AD Connect](connect/active-directory-aadconnect-get-started-custom.md).
   3. Verificar e gerenciar a sincronização de diretórios. Instruções de logon único estão disponíveis nessa etapa.
   
   Além disso, configure a federação com o AD FS, conforme descrito em [Instalação personalizada do Azure AD Connect](connect/active-directory-aadconnect-get-started-custom.md).

## <a name="upgrade-your-active-directory-domain-services-schema"></a>Atualizar o esquema de serviços do Domínio do Active Directory
> [!NOTE]
> Depois de atualizar o esquema do Active Directory, o processo de saudação não pode ser revertido. É recomendável que você execute uma atualização Olá primeiro em um ambiente de teste.
> 

1. Entrar no controlador de domínio de tooyour com uma conta que tenha o administrador da empresa e direitos de administrador de esquema.
2. Saudação de cópia **[media] \support\adprep** tooone de diretório e subdiretórios dos controladores de domínio do Active Directory (onde **[media]** é a mídia de instalação do Windows Server 2012 R2 do hello caminho toohello ).
4. Em um prompt de comando, vá toohello **adprep** diretório e execute **adprep.exe /forestprep**. Siga as instruções na tela de saudação toocomplete atualização do esquema de saudação.

## <a name="prepare-your-active-directory-toosupport-devices"></a>Preparar os dispositivos de toosupport do Active Directory
> [!NOTE]
> Isso é uma operação única que você deve executar tooprepare seus dispositivos de toosupport de floresta do Active Directory. toocomplete neste procedimento, você deve estar conectado com permissões de administrador corporativo e sua floresta do Active Directory deve ter o esquema do Windows Server 2012 R2 hello.
> 


### <a name="prepare-your-active-directory-forest"></a>Prepare sua floresta do Active Directory
1. No servidor de federação, abra uma janela de comando do Windows PowerShell e, depois, digite **Initialize-ADDeviceRegistration**. 
2. Quando solicitado para **ServiceAccountName**, digite nome Olá Olá da conta de serviço selecionada como conta de serviço de saudação do AD FS. Se for uma conta gMSA, insira a conta de saudação no hello **domain\accountname$** formato. Para uma conta de domínio, use o formato de saudação **domain\accountname**.

### <a name="enable-device-authentication-in-ad-fs"></a>Habilitar a autenticação de dispositivo no AD FS
1. No servidor de federação, abra o console de gerenciamento de saudação do AD FS e vá muito**do AD FS** > **políticas de autenticação**.
2. Em Olá **ações** painel, selecione **Editar autenticação primária Global**.
3. Marque a opção **Habilitar autenticação de dispositivo** e, depois, selecione **OK**.
4. Por padrão, o AD FS remove periodicamente dispositivos não utilizados do Active Directory. Desabilite essa tarefa ao usar o serviço de registro de dispositivo do Azure Active Directory para que os dispositivos possam ser gerenciados no Azure.

### <a name="disable-unused-device-cleanup"></a>Desabilitar a limpeza de dispositivos não utilizados
No servidor de federação, abra uma janela de comando do Windows PowerShell e, depois, digite **Set-AdfsDeviceRegistration -MaximumInactiveDays 0**.

### <a name="prepare-azure-ad-connect-for-device-writeback"></a>Preparar o Azure AD Connect para write-back do dispositivo
Conclua a parte 1: Preparar o Azure AD Connect.

## <a name="join-devices-tooyour-workplace-by-using-azure-active-directory-device-registration-service"></a>Junção de local de trabalho de tooyour de dispositivos usando o serviço de registro de dispositivo do Active Directory do Azure

### <a name="join-an-ios-device-by-using-azure-active-directory-device-registration"></a>Ingressar um dispositivo iOS usando o registro de dispositivo do Azure Active Directory
Registro de dispositivo do Active Directory do Azure usa o processo de registro de perfil por satélite Olá para dispositivos iOS. Este processo começa quando Olá usuário se conecta a URL do perfil de registro toohello com o Safari. formato de URL Olá é o seguinte:

    https://enterpriseregistration.windows.net/enrollmentserver/otaprofile/"yourdomainname"

Nesse caso, `yourdomainname` é Olá nome de domínio que você configurou com o Active Directory do Azure. Por exemplo, se seu nome de domínio for contoso.com, Olá URL é da seguinte maneira:

    https://enterpriseregistration.windows.net/enrollmentserver/otaprofile/contoso.com

Há muitos toocommunicate de diferentes maneiras tooyour essa URL que os usuários. Por exemplo, um método recomendável é publicar essa URL em uma mensagem personalizada de acesso negado do aplicativo no AD FS. Essa informação é abordada na seção de seguir Olá [criar uma política de acesso do aplicativo e a mensagem de acesso negado personalizada](#create-an-application-access-policy-and-custom-access-denied-message).

### <a name="join-a-windows-81-device-by-using-azure-active-directory-device-registration"></a>Ingressar um dispositivo Windows 8.1 usando o registro de dispositivo do Azure Active Directory
1. No dispositivo Windows 8.1, selecione **Configurações do Computador** > **Rede** > **Local de Trabalho**.
2. Insira seu nome de usuário no formato UPN; por exemplo, **dan@contoso.com**.
3. Selecione **Ingressar**.
4. Quando solicitado, entre com suas credenciais. Olá dispositivo agora está Unido.

### <a name="join-a-windows-7-device-by-using-azure-active-directory-device-registration"></a>Ingressar um dispositivo Windows 7 usando o registro de dispositivo do Azure Active Directory
tooregister Windows 7 dispositivos que ingressaram no domínio, você precisa toodeploy pacote de software de registro de dispositivo de saudação. Olá pacote de software é chamado no local de trabalho para o Windows 7 e do disponível para download em Olá [site Microsoft Connect](https://connect.microsoft.com/site1164). 

As instruções sobre como toouse Olá pacote estão disponíveis em [como tooconfigure o registro automático do Windows ingressado no domínio dispositivos com o Active Directory do Azure](active-directory-conditional-access-automatic-device-registration-setup.md).

## <a name="verify-that-registered-devices-are-written-back-tooactive-directory"></a>Verifique se que os dispositivos registrados são gravados tooActive diretório
Você pode exibir e verificar se os objetos foram gravados tooyour do Active Directory usando LDP.exe ou ADSI Editar. Ambos estão disponíveis com as ferramentas do administrador do Active Directory hello.

Por padrão, os objetos de dispositivo sejam gravados do Active Directory do Azure são colocados em Olá mesmo domínio que o farm do AD FS.

    CN=RegisteredDevices,defaultNamingContext

## <a name="create-an-application-access-policy-and-custom-access-denied-message"></a>Criar uma política de acesso do aplicativo e uma mensagem personalizada de acesso negado
Considere Olá seguinte cenário: criar um aplicativo de terceira parte confiável no AD FS e configurar uma regra de autorização de emissão que permite que apenas os dispositivos registrados. Agora apenas os dispositivos que estão registrados são permitidos aplicativo hello de tooaccess. 

toomake-o fácil para seu aplicativo de toohello usuários toogain acesso, configurar uma mensagem de acesso negado personalizada que inclui instruções sobre como toojoin seu dispositivo. Agora os usuários têm uma maneira perfeita tooregister seus dispositivos para que possam acessar um aplicativo.

Olá etapas a seguir mostram como tooimplement neste cenário.

> [!NOTE]
> Esta seção pressupõe que você já tenha configurado uma relação de confiança de terceira parte confiável para o seu aplicativo no AD FS.
> 

1. Abra Olá ferramenta AD FS MMC e, em seguida, selecione **do AD FS** > **relações de confiança** > **terceira parte confiável**.
2. Localize Olá aplicativo toowhich que essa nova regra de acesso se aplica. Aplicativo hello e, em seguida, selecione **editar regras de declaração**.
3. Selecione Olá **regras de autorização de emissão** guia e, em seguida, selecione **Adicionar regra**.
4. De saudação **regra de declaração** lista do menu suspenso de modelo, selecione **permitir ou negar usuários com base em uma declaração de entrada**. Em seguida, selecione **Avançar**.
5. Em Olá **nome da regra de declaração** , digite **permitem o acesso de dispositivos registrados**.
6. De saudação **tipo de declaração de entrada** lista suspensa, selecione **é um usuário registrado**.
7. Em Olá **valor de declaração de entrada** , digite **true**.
8. Selecione Olá **permitir acesso toousers com esta declaração de entrada** botão de opção.
9. Selecione **Concluir** e, depois, **Aplicar**.
10. Remova todas as regras que são mais permissivas do que a regra de saudação criado. Por exemplo, remover a regra padrão de saudação **tooall de acesso permite que os usuários**.

Seu aplicativo está agora configurado tooallow acessar somente quando o usuário Olá é proveniente de um dispositivo que eles registraram e uniram toohello no local de trabalho. Para obter políticas de acesso mais avançadas, consulte [Gerenciar riscos com a Autenticação Multifator adicional em aplicativos confidenciais](https://technet.microsoft.com/library/dn280949.aspx).

Em seguida, você configura uma mensagem de erro personalizada para seu aplicativo. mensagem de erro de saudação permite que os usuários saber o que deve associar seu espaço de trabalho do dispositivo toohello antes que possam acessar o aplicativo hello. Você pode criar uma mensagem personalizada de acesso negado do aplicativo usando um HTML personalizado e o PowerShell.

No servidor de federação, abra uma janela de comando do PowerShell e, em seguida, digite hello comando a seguir. Substitua partes do comando Olá com itens que são tooyour específicas do sistema:

    Set-AdfsRelyingPartyWebContent -Name "relying party trust name" -ErrorPageAuthorizationErrorMessage
Você deve registrar seu dispositivo antes de poder acessar este aplicativo.

**Se você estiver usando um dispositivo iOS, selecione esse link toojoin seu dispositivo**:

    a href='https://enterpriseregistration.windows.net/enrollmentserver/otaprofile/yourdomain.com

Una essa área de trabalho do tooyour de dispositivo iOS.

Se estiver usando um dispositivo Windows 8.1, poderá ingressá-lo selecionando **Configurações do Computador**> **Rede** > **Local de Trabalho**.

Em Olá anterior comandos, **nome de confiança de terceiros confiável** é o nome de saudação do objeto de confiança da terceira parte do seu aplicativo no AD FS.
E **SeuDomínio** é Olá nome de domínio que você configurou com o Azure Active Directory (por exemplo, contoso.com).
Ser tooremove-se de que qualquer quebras de linha (se houver) do hello HTML conteúda que você passe toohello **Set-AdfsRelyingPartyWebContent** cmdlet.

Agora, quando os usuários acessam seu aplicativo em um dispositivo que não está registrado com hello serviço de registro de dispositivo do Active Directory do Azure, eles veem uma página que parece semelhante toohello captura de tela a seguir.

![Captura de tela de um erro quando os usuários não tiverem registrado seus dispositivos com o Azure AD](./media/active-directory-conditional-access/error-azureDRS-device-not-registered.gif)


