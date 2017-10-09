---
title: "Conecte-se vários domínios aaaAzure AD"
description: "Este documento descreve a instalação e a configuração de vários domínios de nível superior com o O365 e o Azure AD."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 5595fb2f-2131-4304-8a31-c52559128ea4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 91d87875ceacee4e34f132938e4bb0294fb954e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="multiple-domain-support-for-federating-with-azure-ad"></a>Suporte a Vários Domínios para Federação com o Azure AD
Olá documentação a seguir fornece orientação sobre como toouse vários domínios de nível superior e subdomínios quando federar com domínios do Office 365 ou Azure AD.

## <a name="multiple-top-level-domain-support"></a>Suporte para vários domínios de nível superior
A federação de vários domínios de nível superior com o Azure AD requer configuração adicional que não é necessária na federação de um único domínio de nível superior.

Quando um domínio é federado com o Azure AD, várias propriedades são definidas no domínio Olá no Azure.  Uma delas é IssuerUri.  Esse é um URI que é usado pelo AD do Azure tooidentify domínio Olá Olá token está associado.  Olá URI não precisa tooresolve tooanything, mas ele deve ser um URI válido.  Por padrão, o AD do Azure define esse toohello valor do identificador do serviço de Federação Olá em seu local do AD FS configuration.

> [!NOTE]
> Identificador do serviço de Federação Olá é um URI que identifica exclusivamente um serviço de Federação.  serviço de Federação Olá é uma instância do AD FS que funciona como um serviço de token de segurança de saudação. 
> 
> 

Você pode IssuerUri de exibição usando o comando do PowerShell Olá `Get-MsolDomainFederationSettings -DomainName <your domain>`.

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

Um problema surge quando queremos tooadd mais de um domínio de nível superior.  Por exemplo, digamos que você tenha configurado a federação entre o Azure AD e seu ambiente local.  Para este documento, estou usando bmcontoso.com.  Agora adicionei um segundo domínio de nível superior, bmfabrikam.com.

![Domínios](./media/active-directory-multiple-domains/domains.png)

Quando tentar tooconvert nosso toobe de domínio bmfabrikam.com federado, recebemos um erro.  Olá motivo isso é que o AD do Azure tem uma restrição que não permite Olá Olá de toohave propriedade IssuerUri mesmo valor para mais de um domínio.  

![Erro de federação](./media/active-directory-multiple-domains/error.png)

### <a name="supportmultipledomain-parameter"></a>Parâmetro SupportMultipleDomain
tooworkaround isso, precisamos tooadd um IssuerUri diferente, que pode ser feito usando Olá `-SupportMultipleDomain` parâmetro.  Esse parâmetro é usado com hello cmdlets a seguir:

* `New-MsolFederatedDomain`
* `Convert-MsolDomaintoFederated`
* `Update-MsolFederatedDomain`

Esse parâmetro faz o AD do Azure configurar Olá IssuerUri para que ele se baseia no nome de saudação do domínio de saudação.  Ele será exclusivo nos diretórios no Azure AD.  Usar o parâmetro hello permite toocomplete de comando do PowerShell Olá com êxito.

![Erro de federação](./media/active-directory-multiple-domains/convert.png)

Examinar as configurações de saudação do nosso novo domínio bmfabrikam.com você pode ver o seguinte hello:

![Erro de federação](./media/active-directory-multiple-domains/settings.png)

Observe que `-SupportMultipleDomain` não altera Olá outros pontos de extremidade que são ainda configurado o serviço de Federação tooour toopoint em adfs.bmcontoso.com.

Outra coisa que `-SupportMultipleDomain` does é que ele verifica se o sistema do hello AD FS inclui valor de emissor correto Olá em tokens emitidos para o AD do Azure. Isso é feito por fazer parte do domínio de saudação do usuários Olá UPN e configurá-lo como domínio Olá Olá IssuerUri, ou seja, o sufixo https://{upn} / adfs/services/trust. 

Assim, durante a autenticação tooAzure AD ou o Office 365, Olá IssuerUri elemento token saudação do usuário é domínio de saudação toolocate usado no AD do Azure.  Se uma correspondência não for encontrada Olá autenticação falhará. 

Por exemplo, se um usuário do UPN é bsimon@bmcontoso.com, elemento IssuerUri Olá problemas no AD FS token Olá definirá toohttp://bmcontoso.com/adfs/services/trust. Isso corresponderá a configuração do AD do Azure hello e autenticação será bem-sucedida.

seguinte Olá é a regra de declaração personalizada de saudação que implementa essa lógica:

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)", "http://${domain}/adfs/services/trust/"));


> [!IMPORTANT]
> Em ordem toouse Olá - SupportMultipleDomain alternar durante a tentativa de tooadd nova ou converter já adicionado domínios, você precisa toohave configurar sua confiança federada toosupport-los originalmente.  
> 
> 

## <a name="how-tooupdate-hello-trust-between-ad-fs-and-azure-ad"></a>Como tooupdate Olá confiança entre AD FS e Azure AD
Se você sem configurar Olá federada de confiança entre AD FS e a instância do AD do Azure, talvez seja necessário toore-criar essa relação de confiança.  Isso ocorre porque, quando ele é originalmente instalação sem Olá `-SupportMultipleDomain` parâmetro, Olá IssuerUri é definido com o valor padrão de saudação.  Olá captura de tela abaixo, você verá Olá IssuerUri é definido toohttps://adfs.bmcontoso.com/adfs/services/trust.

Agora, se adicionou com êxito um novo domínio no portal de saudação do AD do Azure e, em seguida, tente tooconvert usando `Convert-MsolDomaintoFederated -DomainName <your domain>`, obtemos Olá erro a seguir.

![Erro de federação](./media/active-directory-multiple-domains/trust1.png)

Se você tentar tooadd Olá `-SupportMultipleDomain` switch receberemos Olá erro a seguir:

![Erro de federação](./media/active-directory-multiple-domains/trust2.png)

Simplesmente tentar toorun `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` em Olá domínio original também resultará em erro.

![Erro de federação](./media/active-directory-multiple-domains/trust3.png)

Use as etapas de saudação abaixo tooadd um domínio de nível superior adicional.  Se você já tiver adicionado um domínio e não tiver usado a saudação `-SupportMultipleDomain` início do parâmetro com etapas Olá para remover e atualizar o domínio original.  Se você não adicionou um domínio de nível superior ainda você pode iniciar com etapas de saudação para adicionar um domínio usando o PowerShell do Azure AD Connect.

Use Olá seguindo as etapas tooremove Olá Online da Microsoft confiança e atualizar o domínio original.

1. No servidor de Federação do AD FS, abra **Gerenciamento do AD FS.** 
2. Olá esquerda, expanda **relações de confiança** e **terceira parte confiável**
3. Em Olá à direita, exclua Olá **plataforma de identidade do Microsoft Office 365** entrada.
   ![Remover o Microsoft Online](./media/active-directory-multiple-domains/trust4.png)
4. Em um computador que tenha [Azure módulo Active Directory para Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) instalado execute seguinte Olá: `$cred=Get-Credential`.  
5. Insira a saudação de nome de usuário e senha de um administrador global para o domínio do AD do Azure Olá com que você está associando
6. No PowerShell, digite `Connect-MsolService -Credential $cred`
7. No PowerShell, digite `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`.  Isso é para o domínio original hello.  Portanto, usar Olá acima domínios seria:`Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`

Use Olá seguindo as etapas tooadd Olá novo domínio de nível superior usando o PowerShell

1. Em um computador que tenha [Azure módulo Active Directory para Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) instalado execute seguinte Olá: `$cred=Get-Credential`.  
2. Insira a saudação de nome de usuário e senha de um administrador global para o domínio do AD do Azure Olá com que você está associando
3. No PowerShell, digite `Connect-MsolService -Credential $cred`
4. No PowerShell, digite `New-MsolFederatedDomain –SupportMultipleDomain –DomainName`

Use Olá seguindo as etapas tooadd Olá novo domínio de nível superior usando o Azure AD Connect.

1. Inicie o Azure AD Connect da área de trabalho de saudação ou menu Iniciar
2. Escolha "Adicionar um domínio do Azure AD" ![Adicionar um domínio do Azure AD](./media/active-directory-multiple-domains/add1.png)
3. Insira as credenciais do Azure AD e do Active Directory
4. Selecione o domínio de segundo Olá desejar tooconfigure para federação.
   ![Adicionar um domínio do Azure AD](./media/active-directory-multiple-domains/add2.png)
5. Clique em Instalar

### <a name="verify-hello-new-top-level-domain"></a>Verifique se o novo domínio de nível superior Olá
Usando o comando do PowerShell Olá `Get-MsolDomainFederationSettings -DomainName <your domain>`você pode exibir hello atualizado IssuerUri.  saudação de captura de tela abaixo mostra as configurações de Federação Olá foram atualizadas no nosso http://bmcontoso.com/adfs/services/trust domínio original

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

E Olá IssuerUri em nosso novo domínio tiver sido definido toohttps://bmfabrikam.com/adfs/services/trust

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/settings2.png)

## <a name="support-for-sub-domains"></a>Suporte para Subdomínios
Quando você adiciona um subdomínio, devido a saudação do AD do Azure forma manipuladas domínios, ele herdará as configurações de saudação do pai de saudação.  Isso significa que Olá IssuerUri precisa toomatch pais de saudação.

Digamos, por exemplo, que tenho bmcontoso.com e adiciono corp.bmcontoso.com.  Isso significa que Olá IssuerUri para um usuário de corp.bmcontoso.com, será preciso toobe **http://bmcontoso.com/adfs/services/trust.**  No entanto, regra padrão Olá implementado acima do AD do Azure, irá gerar um token com um emissor como **http://corp.bmcontoso.com/adfs/services/trust.** que não irão corresponder o valor necessário do domínio hello e a autenticação falhará.

### <a name="how-tooenable-support-for-sub-domains"></a>Como o suporte a tooenable de subdomínios
Em ordem toowork em todo este Olá terceira parte confiável para o Microsoft Online do AD FS precisa toobe atualizado.  toodo isso, você deve configurar uma regra de declaração personalizada para que ele ignora quaisquer subdomínios de sufixo UPN do usuário Olá ao construir o valor de emissor personalizado hello. 

Olá declaração a seguir faz isso:

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

[!NOTE]
último número de saudação em expressão regular Olá definir Olá quantos domínios pai no seu domínio raiz. Aqui temos bmcontoso.com, então são necessários dois domínios pai. Se três pai domínios foram toobe mantido (ou seja: corp.bmcontoso.com), em seguida, o número de saudação teria sido três. Eventualy um intervalo pode ser indicado, correspondência de saudação sempre será feita no máximo toomatch Olá domínios. "{2,3}" corresponderá a dois domínios toothree (ou seja: bmfabrikam.com e corp.bmcontoso.com).

As etapas a seguir do uso Olá tooadd um subdomínios de toosupport declaração personalizada.

1. Abra o gerenciamento do AD FS
2. Clique com botão direito Olá RP Online da Microsoft de confiança e escolha as regras de declaração editar
3. Selecione a terceira regra de declaração hello e substitua ![declaração de edição](./media/active-directory-multiple-domains/sub1.png)
4. Substitua a declaração atual hello:
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)","http://${domain}/adfs/services/trust/"));
   
       with
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

    ![Substituir declaração](./media/active-directory-multiple-domains/sub2.png)

5. Clique em OK.  Clique em Aplicar.  Clique em OK.  Feche o gerenciamento do AD FS.

