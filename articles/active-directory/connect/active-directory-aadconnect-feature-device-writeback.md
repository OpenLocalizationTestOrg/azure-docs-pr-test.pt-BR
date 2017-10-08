---
title: 'Azure AD Connect: habilitando write-back de dispositivo | Microsoft Docs'
description: Este documento detalhes como tooenable dispositivo write-back usando o Azure AD Connect
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: c0ff679c-7ed5-4d6e-ac6c-b2b6392e7892
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 2566a514137fed85b21929207cf3230e6878ebbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-enabling-device-writeback"></a>Azure AD Connect: habilitando o write-back do dispositivo
> [!NOTE]
> TooAzure uma assinatura Premium do AD é necessária para write-back do dispositivo.
> 
> 

Olá documentação a seguir fornece informações sobre como recurso de write-back de dispositivo de saudação tooenable no Azure AD Connect. Write-back do dispositivo é usado em Olá os seguintes cenários:

* Habilitar o acesso condicional com base em dispositivos tooADFS (2012 R2 ou superior) (terceira parte confiável) de aplicativos protegidos.

Isso fornece segurança adicional e garantia de que acessar tooapplications é concedida somente tootrusted dispositivos. Para saber mais sobre acesso condicional, consulte [Gerenciando risco com acesso condicional](../active-directory-conditional-access.md) e [Configurando o acesso condicional no local usando o registro do dispositivo do Azure Active Directory](../active-directory-conditional-access-automatic-device-registration-setup.md).

> [!IMPORTANT]
> <li>Dispositivos devem estar localizados no hello mesma floresta como usuários hello. Desde que os dispositivos devem ser gravados tooa única floresta, esse recurso não atualmente suporta uma implantação com várias florestas de usuário.</li>
> <li>Objeto de configuração do registro de dispositivo somente uma pode ser adicionado a floresta do toohello no local do Active Directory. Este recurso não é compatível com uma topologia onde Olá local do Active Directory é diretórios toomultiple sincronizado do AD do Azure.</li>> 

## <a name="part-1-install-azure-ad-connect"></a>Parte 1: instalar o Azure AD Connect
1. Instale o Azure AD Connect usando configurações expressas ou personalizadas. A Microsoft recomenda toostart com todos os usuários e grupos sincronizados com êxito antes de ativar o write-back do dispositivo.

## <a name="part-2-prepare-active-directory"></a>Parte 2: preparar o Active Directory
Use Olá tooprepare etapas para usar o write-back de dispositivo a seguir.

1. Da máquina Olá onde o Azure AD Connect está instalado, inicie o PowerShell no modo elevado.
2. Se o módulo do Active Directory PowerShell Olá não estiver instalado, instale-o usando Olá comando a seguir:
   
   `Add-WindowsFeature RSAT-AD-PowerShell`
3. Se o módulo do Azure Active Directory PowerShell Olá não estiver instalado, baixe e instale-o de [Azure módulo Active Directory para Windows PowerShell (versão de 64 bits)](http://go.microsoft.com/fwlink/p/?linkid=236297). Este componente tem uma dependência em Olá Assistente de conexão, que é instalado com o Azure AD Connect.
4. Com credenciais de administrador corporativo, execute Olá comandos a seguir e, em seguida, saia do PowerShell.
   
   `Import-Module 'C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1'`
   
   `Initialize-ADSyncDeviceWriteback {Optional:–DomainName [name] Optional:-AdConnectorAccount [account]}`

Credenciais de administrador corporativo serão necessárias, já que o namespace de configuração toohello alterações são necessárias. Um administrador de domínio não terá permissões suficientes.

![Powershell para habilitar o write-back do dispositivo](./media/active-directory-aadconnect-feature-device-writeback/powershell.png)

Descrição:

* Se ainda não existirem, ele criará e configurará novos contêineres e objetos em CN=Device Registration Configuration,CN=Services,CN=Configuration,[forest-dn].
* Se não existir, cria e configura novos contêineres e objetos em CN=RegisteredDevices,[domain-dn]. Objetos de dispositivo serão criados neste contêiner.
* Define as permissões necessárias no hello conta de conector AD do Azure, dispositivos toomanage no seu Active Directory.
* Só precisa toorun em uma floresta, mesmo se a conexão do AD do Azure está sendo instalado em várias florestas.

Parâmetros:

* DomainName: domínio do Active Directory no qual os objetos do dispositivo serão criados. Observação: todos os dispositivos para determinada floresta do Active Directory serão criados em um único domínio.
* AdConnectorAccount: Conta do Active Directory que será usada pelo Azure AD Connect toomanage objetos no diretório de saudação. Isso é usada pelo Azure AD Connect sincronização tooconnect tooAD de conta de saudação. Se você tiver instalado usando as configurações expressas, é prefixada com MSOL_ de conta de saudação.

## <a name="part-3-enable-device-writeback-in-azure-ad-connect"></a>Parte 3: habilitar o dispositivo write-back na conexão do AD do Azure
Use Olá seguindo o procedimento tooenable dispositivo write-back na conexão do AD do Azure.

1. Execute novamente o Assistente de instalação de saudação. Selecione **personalizar opções de sincronização** Olá as tarefas adicionais de página e clique em **próximo**.
   ![Instalação Personalizada - Personalizar opções de sincronização](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback2.png)
2. Na página de recursos opcionais de hello, Write-back de dispositivo estará não esmaecida. Observe que, se hello etapas de preparação do Azure AD Connect não sejam concluídas write-back de dispositivo estará esmaecido out na página de recursos opcionais de saudação. Marque a caixa Olá para write-back do dispositivo e clique em **próximo**. Se a caixa de seleção Olá ainda estiver desabilitada, consulte Olá [seção de solução de problemas](#the-writeback-checkbox-is-still-disabled).
   ![Instalação Personalizada - Recursos opcionais de write-back de dispositivo](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback3.png)
3. Na página de write-back Olá, você verá o domínio Olá fornecido como floresta de write-back de dispositivo saudação padrão.
   ![Florestas de destino do write-back de dispositivo da Instalação Personalizada](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback4.png)
4. Concluir a instalação de saudação do hello assistente sem alterações de configuração adicionais. Se necessário, consulte muito[instalação personalizada do Azure AD Connect.](active-directory-aadconnect-get-started-custom.md)

## <a name="enable-conditional-access"></a>Habilitar o acesso condicional
Tooenable instruções detalhadas sobre esse cenário estão disponíveis em [definindo o acesso condicional no local, usando o registro do dispositivo do Azure Active Directory](../active-directory-conditional-access-automatic-device-registration-setup.md).

## <a name="verify-devices-are-synchronized-tooactive-directory"></a>Verifique se que os dispositivos são sincronizado tooActive diretório
O write-back do dispositivo agora deve estar funcionando corretamente. Lembre-se de que pode levar horas too3 para dispositivo objetos toobe gravados tooAD.  tooverify seus dispositivos estão sendo sincronizados corretamente, Olá depois de concluir as regras de sincronização de saudação:

1. Inicie o Centro Administrativo do Active Directory.
2. Expanda RegisteredDevices, dentro de saudação domínio sendo federado.
   ![Dispositivos registrados do Centro de Administração do Active Directory](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback5.png)
3. Dispositivos registrados atuais serão listados lá.
   ![Lista de dispositivos registrados do Centro de Administração do Active Directory](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback6.png)

## <a name="troubleshooting"></a>Solucionar problemas
### <a name="hello-writeback-checkbox-is-still-disabled"></a>caixa de seleção de write-back de saudação ainda está desabilitada.
Se a caixa de seleção Olá para write-back de dispositivo não estiver habilitado, mesmo se você tiver seguido as etapas acima, a saudação Olá etapas a seguir irá guiá-lo por meio de instalação que Olá assistente está verificando antes de caixa hello está habilitada.

Primeiro as prioridades:

* Verifique se pelo menos uma floresta tem 2012R2 do Windows Server. tipo de objeto de dispositivo Olá deve estar presente.
* Se o Assistente de instalação de saudação já está em execução, as alterações não serão detectadas. Nesse caso, conclua o Assistente de instalação hello e executá-lo novamente.
* Certifique-se de saudação conta que fornecer no script de inicialização de saudação é realmente Olá correto usuário usado por Olá conector do Active Directory. tooverify isso, siga estas etapas:
  * Saudação do menu de início, abra **serviço de sincronização**.
  * Olá abrir **conectores** guia.
  * Localize Olá conector com o tipo de serviços de domínio do Active Directory e selecioná-lo.
  * Em **Ações**, selecione **Propriedades**.
  * Vá muito**conectar-se a floresta do diretório tooActive**. Verifique se esse nome de usuário e domínio Olá especificado no script de toohello tela correspondência Olá conta fornecida.
    ![Conta do conector no Sync Service Manager](./media/active-directory-aadconnect-feature-device-writeback/connectoraccount.png)

Verifique a configuração no Active Directory:

* Verifique se esse Olá Device Registration Service está localizado no local de saudação abaixo (CN = DeviceRegistrationService, CN = Serviços de registro de dispositivo, CN = Device Registration Configuration, CN = Services, CN = Configuration) no contexto de nomenclatura de configuração.

![Solucionar problemas, DeviceRegistrationService no namespace de configuração](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot1.png)

* Verifique se há apenas um objeto de configuração pesquisando Olá namespace de configuração. Se houver mais de um, exclua a cópia de saudação.

![Solucionar problemas, procure objetos duplicados Olá](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot2.png)

* No objeto de serviço de registro de dispositivo hello, certifique-se de saudação atributo msDS-DeviceLocation está presente e tem um valor. Pesquisa esse local e verifique se ele estiver presente com hello objectType msDS-DeviceContainer.

![Solucionar problemas, msDS-DeviceLocation](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot3.png)

![Solucionar problemas, classe de objeto RegisteredDevices](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot4.png)

* Verificar conta Olá usada pelo Olá que conector do Active Directory tem as permissões necessárias no contêiner de dispositivos registrados Olá encontrado pela etapa anterior hello. Isso é permissões Olá esperado neste contêiner:

![Solucionar problemas, verificar permissões no contêiner](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot5.png)

* Verificar Olá conta do Active Directory tem permissões no hello CN = Device Registration Configuration, CN = Services, CN = objeto de configuração.

![Solucionar problemas, verificar permissões na configuração de registro do dispositivo](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot6.png)

## <a name="additional-information"></a>Informações adicionais
* [Gerenciamento de riscos com acesso condicional](../active-directory-conditional-access.md)
* [Configurando o acesso condicional no local usando o registro do dispositivo do Azure Active Directory](../active-directory-device-registration-on-premises-setup.md)

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre [Como integrar suas identidades locais ao Active Directory do Azure](active-directory-aadconnect.md).

