---
title: "domínios de aaaCustom no Proxy de aplicativo do Azure AD | Microsoft Docs"
description: "Gerencie domínios personalizados no Proxy de aplicativo do Azure AD para essa URL Olá para o aplicativo hello é Olá mesmo, independentemente de onde os usuários acessá-lo."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 2fe9f895-f641-4362-8b27-7a5d08f8600f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 7a433c411976077210a2435c3c087991c7430755
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-custom-domains-in-azure-ad-application-proxy"></a>Trabalhando com domínios personalizados no Proxy de Aplicativo do AD do Azure

Quando você publica um aplicativo por meio do Proxy de aplicativo do Azure Active Directory, você cria uma URL externa para seu toowhen de toogo de usuários que estão trabalhando remotamente. Essa URL é o domínio padrão de saudação *yourtenant.msappproxy.net*. Por exemplo, se você publicou um aplicativo chamado despesas e seu locatário nomeado Contoso, URL externa Olá seria https://expenses-contoso.msappproxy.net. Se você quiser toouse seu próprio nome de domínio, configure um domínio personalizado para seu aplicativo. 

É recomendável que você configure domínios personalizados para seus aplicativos sempre que possível. Alguns dos benefícios de saudação de domínios personalizados incluem:

- Os usuários podem obter aplicativos toohello com hello a mesma URL, se estiverem trabalhando dentro ou fora da sua rede.
- Se todos os aplicativos têm hello mesmo URLs internas e externas, links em um aplicativo que levam tooanother continuam toowork mesmo fora da rede corporativa hello. 
- Você controla sua identidade visual e cria URLs de saudação desejado. 


## <a name="configure-a-custom-domain"></a>Configurar um domínio personalizado

### <a name="prerequisites"></a>Pré-requisitos

Antes de configurar um domínio personalizado, certifique-se de que você tenha Olá preparados de requisitos a seguir: 
- Um [domínio verificado adicionado tooAzure do Active Directory](active-directory-domains-add-azure-portal.md).
- Um certificado personalizado para o domínio hello, na forma de saudação de um arquivo PFX. 
- Um aplicativo local [publicado por meio do Proxy de Aplicativo](application-proxy-publish-azure-portal.md).

### <a name="configure-your-custom-domain"></a>Configurar seu domínio personalizado

Quando você tiver um desses três requisitos prontos, siga essas tooset etapas o seu domínio personalizado:

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Navegue muito**Active Directory do Azure** > **aplicativos empresariais** > **todos os aplicativos** e escolha o aplicativo hello toomanage desejado.
3. Selecione **Proxy de Aplicativo**. 
4. No campo de URL externa hello, use Olá suspensa lista tooselect seu domínio personalizado. Se você não vir o seu domínio na lista de hello, em seguida, ele ainda não foi verificado ainda. 
5. Selecione **Salvar**
5. Olá **certificado** campo foi desabilitado se torne habilitado. Selecione esse campo. 

   ![Clique em tooupload um certificado](./media/active-directory-application-proxy-custom-domains/certificate.png)

   Se você já carregou um certificado para este domínio, o campo de certificado Olá exibe informações de certificado de saudação. 

6. Carregar certificado PFX hello e digite a senha de saudação certificado hello. 
7. Selecione **salvar** toosave suas alterações. 
8. Adicionar um [registro DNS](../dns/dns-operations-recordsets-portal.md) redirecionamentos Olá novo domínio de msappproxy.net de toohello URL externo. 

>[!TIP] 
>Você só precisa de um certificado tooupload por domínio personalizado. Quando você carregar um certificado, você pode escolher domínio personalizado hello quando você publica um novo aplicativo e não tem toodo a configuração adicional, exceto o registro DNS hello. 

## <a name="manage-certificates"></a>Gerenciar certificados

### <a name="certificate-format"></a>Formato do certificado
Não há nenhuma restrição sobre métodos de assinatura de certificado hello. A Criptografia de Curva Elíptica (ECC), o Nome Alternativo da Entidade (SAN) e outros tipos de certificado são compatíveis. 

Você pode usar um certificado curinga como curinga Olá coincide com a URL externa de saudação desejada. 

Você também pode usar certificados autoassinados. Se você estiver usando uma autoridade de certificação privada, Olá CDP (ponto de distribuição do ponto de revogação de certificado) para o certificado de saudação deve ser pública.

### <a name="changing-hello-domain"></a>Alterar domínio Olá
Todos os domínios verificados aparecem na lista de suspensa Olá URL externa para seu aplicativo. domínio de saudação toochange, apenas atualizar campo para o aplicativo hello. Se o domínio Olá desejado não estiver na lista de hello, [adicioná-lo como um domínio verificado](active-directory-domains-add-azure-portal.md). Se você selecionar um domínio que ainda não tiver um certificado associado, siga o certificado de saudação do tooadd as etapas 5 a 7. Em seguida, certifique-se de que atualizar tooredirect de registro de DNS Olá da saudação nova URL externa. 

### <a name="certificate-management"></a>Gerenciamento de certificados
Você pode usar o mesmo certificado para vários aplicativos, a menos que os aplicativos de saudação compartilham um host externo de saudação. 

Você receber um aviso quando um certificado expira, informando tooupload outro certificado por meio do portal hello. Se o certificado de saudação for revogado, os usuários podem ver um aviso de segurança ao acessar o aplicativo hello. Nós não realizamos verificações de revogação de certificados.  certificado de saudação tooupdate para um determinado aplicativo, navegue toohello aplicativo e siga as etapas 5 a 7 para configurar domínios personalizados em um novo certificado de tooupload de aplicativos publicados. Se o certificado antigo Olá não está sendo usado por outros aplicativos, ele será excluído automaticamente. 

Atualmente todo o gerenciamento de certificado é por meio de páginas de aplicativos individuais para que você precisa de certificados toomanage no contexto de saudação do aplicativos relevantes hello. 

## <a name="next-steps"></a>Próximas etapas
* [Habilitar logon único](active-directory-application-proxy-sso-using-kcd.md) tooyour publicado aplicativos com a autenticação do AD do Azure.
* [Habilitar o acesso condicional](active-directory-application-proxy-conditional-access.md) aplicativos publicados do tooyour.
* [Adicionar seu nome de domínio personalizado tooAzure AD](active-directory-domains-add-azure-portal.md)


