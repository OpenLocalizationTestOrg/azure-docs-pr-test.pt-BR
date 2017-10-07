---
title: Perguntas frequentes sobre o Azure Active Directory | Microsoft Docs
description: "Esta página tem perguntas frequentes sobre o Azure AD Connect."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
ms.assetid: 4e47a087-ebcd-4b63-9574-0c31907a39a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 39c0b127d3dcf6f45607ad8b4647a9ad79dfc732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-azure-active-directory-connect"></a>Perguntas frequentes sobre o Azure Active Directory Connect

## <a name="general-installation"></a>Instalação geral
**P: instalação funcionará se Olá Administrador Global do Azure AD tem 2FA habilitado?**  
Com hello compilações de fevereiro de 2016, isso é suportado.

**P: há um tooinstall de forma autônoma o Azure AD Connect?**  
É apenas tooinstall com suporte do Azure AD Connect usando o Assistente de instalação de saudação. Não há suporte para uma instalação silenciosa e autônoma.

**P: Eu tenho uma floresta em que um domínio não pode ser contatado. Como instalo o Azure AD Connect?**  
Com hello compilações de fevereiro de 2016, isso é suportado.

**P: Olá trabalho de agente de integridade do AD DS no server core?**  
Sim. Depois de instalar o agente de hello, você poderá concluir o processo de registro de hello usando Olá cmdlet do PowerShell a seguir: 

`Register-AzureADConnectHealthADDSAgent -Credentials $cred`

## <a name="network"></a>Rede
**P: tenho um firewall, o dispositivo de rede, ou algo que limita as conexões de tempo máximo de saudação pode permanecer aberto na rede. Qual deve ser o limiar de tempo limite no lado do cliente ao usar o Azure Connect AD?**  
Todos os softwares de rede, dispositivos físicos ou qualquer outra coisa que o tempo máximo de saudação conexões podem permanecer abertos deve usar um limite de pelo menos 5 minutos (300 segundos) para conectividade entre os limites Olá servidor onde hello Azure AD Connect cliente está instalado e o Active Directory do Azure. Isso também se aplica a ferramentas de sincronização do Microsoft Identity tooall lançada anteriormente.

**P: Os SLDs (domínios de rótulo único) têm suporte?**  
Não, o Azure AD Connect não oferece suporte a florestas/domínios locais usando SLDs.

**P: Há suporte a nomes NetBios com pontos?**  
Não, o AD do Azure Connect não oferece suporte a florestas/domínios do local onde o nome de NetBios Olá contém um ponto "." no nome de saudação.

## <a name="federation"></a>Federação
**P: o que fazer se receber um email que me pedindo toorenew meu certificado do Office 365**  
Usar as orientações de saudação descrita no hello [renovar certificados](active-directory-aadconnect-o365-certs.md) tópico sobre como toorenew Olá certificado.

**P: Defini a opção “Atualizar automaticamente terceira parte confiável” para a terceira parte confiável do O365. É necessário tootake qualquer ação quando meu automaticamente o certificado de assinatura de token faz?**  
Usar as orientações de saudação descrita no artigo Olá [renovar certificados](active-directory-aadconnect-o365-certs.md).

## <a name="environment"></a>Ambiente
**P: há suporte para toorename Olá servidor após a instalação do Azure AD Connect?**  
Não. Alterando o nome do servidor de saudação causa toonot de mecanismo de sincronização de saudação será capaz de tooconnect toohello SQL banco de dados e serviço de saudação não será capaz de toostart.

## <a name="identity-data"></a>Dados de identidade
**P: Olá o atributo UPN (userPrincipalName) no AD do Azure não corresponder Olá UPN local - por que?**  
Consulte estes artigos:

* [Olá de nomes de usuário no Office 365, Azure ou Intune não correspondem ao UPN local ou ID de logon alternativo](https://support.microsoft.com/en-us/kb/2523192)
* [As alterações não são sincronizadas pela ferramenta de sincronização do Active Directory do Azure de Olá depois de alterar Olá UPN de uma conta de usuário toouse um domínio federado diferente](https://support.microsoft.com/en-us/kb/2669550)

Você também pode configurar o AD do Azure tooallow Olá sincronização mecanismo tooupdate Olá userPrincipalName conforme descrito em [recursos de serviço de sincronização do Azure AD Connect](active-directory-aadconnectsyncservice-features.md).

**P: há suporte para toosoft correspondência local objetos AD/contato de um grupo com objetos de contato/grupo do AD do Azure existente?**  
Não, não há suporte para esse recurso no momento.

**P: há suporte para toomanually define atributo de ImmutableId no Azure AD grupo/contato existente objetos toohard correspondência local tooon objetos de grupo do AD/contato?**  
Não, não há suporte para esse recurso no momento.



## <a name="custom-configuration"></a>Configuração personalizada
**P: onde estão Olá cmdlets do PowerShell para Azure AD Connect documentado?**  
Com exceção de Olá Olá cmdlets documentados neste site, não há suporte para outros cmdlets do PowerShell encontrados na conexão do AD do Azure para uso do cliente.

**P: posso usar "Servidor de exportação/importação do servidor" encontrada em *Synchronization Service Manager* toomove configuração entre servidores?**  
Não. Essa opção não irá recuperar todos os parâmetros de configuração e não deve ser usada. Em vez disso, você deve usar a configuração básica do Olá Olá Assistente toocreate no segundo servidor de saudação e usar regra de sincronização Olá editor toogenerate PowerShell scripts toomove qualquer regra personalizada entre servidores. Confira [Migração Swing](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).

**P: senhas armazenadas de página Olá entrada do Azure e pode isso impedida, pois ele contém um elemento de entrada de senha com preenchimento automático de hello = "false" atributo?**</br>
No momento não oferecemos suporte modificados atributos HTML Olá Olá senha do campo de entrada, incluindo a marca de preenchimento automático de saudação. Atualmente estamos trabalhando em um recurso que permite o uso de Javascript personalizado que permitirá que você tooadd qualquer campo de senha do atributo toohello. Isso deve ser disponibilizado no último semestre de 2017.

**P: no hello Azure na página de entrada, nomes de usuário para usuários que se conectaram anteriormente com êxito são mostradas.  Esse comportamento pode ser desativado?**</br>
No momento não oferecemos suporte modificados atributos HTML de saudação da página de entrada hello. Atualmente estamos trabalhando em um recurso que permite o uso de Javascript personalizado que permitirá que você tooadd qualquer campo de senha do atributo toohello. Isso deve ser disponibilizado no último semestre de 2017.

**P: há uma maneira tooprevent sessões simultâneas?**</br>
Não.



## <a name="troubleshooting"></a>Solucionar problemas
**P: Como posso obter ajuda com o Azure AD Connect?**

[Saudação de pesquisa da Base de dados de Conhecimento Microsoft (KB)](https://www.microsoft.com/en-us/Search/result.aspx?q=azure%20active%20directory%20connect&form=mssupport)

* Saudação de pesquisa da Base de dados de Conhecimento Microsoft (KB) para problemas de conserto toocommon soluções técnicas sobre o suporte para conexão do AD do Azure.

[Fóruns do Active Directory do Microsoft Azure](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=WindowsAzureAD)

* Você pode pesquisar e navegar para técnico de perguntas e respostas de comunidade hello ou faça sua pergunta, clicando em [aqui](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).

[Atendimento ao cliente do Azure AD Connect](https://manage.windowsazure.com/?getsupport=true)

* Use esse suporte de tooget link por meio de saudação portal do Azure.

