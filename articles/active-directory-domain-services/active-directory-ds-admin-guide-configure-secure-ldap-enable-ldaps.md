---
title: "aaaConfigure seguro LDAP (LDAPS) nos serviços de domínio do AD do Azure | Microsoft Docs"
description: "Configurar o LDAP Seguro (LDAPS) para um domínio gerenciado dos Serviços de Domínio do Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c6da94b6-4328-4230-801a-4b646055d4d7
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: 8781285cd02d690788056b985b017efd7e4d6b3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a>Configurar o LDAPS (LDAP Seguro) para um domínio gerenciado do Azure AD Domain Services

## <a name="before-you-begin"></a>Antes de começar
Certifique-se de que você acabou de [tarefa 2 - Olá exportação tooa de certificado segura LDAP. Arquivo PFX](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).

Escolha se toouse Olá visualização experiência do portal do Azure ou Olá toocomplete de portal clássico do Azure essa tarefa.
> [!div class="op_single_selector"]
> * **Portal do Azure (visualização)**: [habilitar secure LDAP usando Olá portal do Azure](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
> * **Portal clássico do Azure**: [habilitar seguro usando o portal do Azure clássico de saudação do LDAP](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)
>
>


## <a name="task-3---enable-secure-ldap-for-hello-managed-domain-using-hello-azure-portal-preview"></a>Tarefa 3 - habilitar LDAP seguro para Olá domínio gerenciado usando Olá portal do Azure (visualização)
tooenable LDAP seguro, execute Olá etapas de configuração a seguir:

1. Navegue toohello  **[portal do Azure](https://portal.azure.com)**.

2. Procure "serviços de domínio' hello **pesquisar recursos** caixa de pesquisa. Selecione **serviços de domínio do AD do Azure** Olá resultados de pesquisa. Olá **serviços de domínio do AD do Azure** folha lista o domínio gerenciado.

    ![Localize o domínio gerenciado que está sendo provisionado](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. Clique o nome de saudação do hello gerenciado toosee de domínio (por exemplo, ' contoso100.com') mais detalhes sobre o domínio de saudação.

    ![Domain Services – estado de provisionamento](./media/getting-started/domain-services-provisioning-state.png)

3. Clique em **LDAP seguro** no painel de navegação de saudação.

    ![Domain Services – folha LDAP Seguro](./media/active-directory-domain-services-admin-guide/secure-ldap-blade.png)

4. Por padrão, o domínio seguro do LDAP acesso tooyour gerenciado está desabilitado. Ativar/desativar **LDAP seguro** muito**habilitar**.

    ![Habilitar o LDAP seguro](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configure.png)
5. Por padrão, o tooyour de acesso LDAP seguro gerenciados domínio pela Olá que Internet está desabilitado. Ativar/desativar **Olá de permissões de acesso LDAP seguro através da internet** muito**habilitar**, se desejado. 

6. Clique em seguinte de ícone de pasta Olá **. O arquivo PFX com certificado LDAP seguro**. Especifica arquivo PFX do hello caminho toohello com certificado Olá para seguro LDAP acesso toohello domínio gerenciado.

7. Especifique a saudação **toodecrypt de senha. Arquivo PFX**. Fornecer Olá mesma senha usada ao exportar o arquivo PFX do hello certificado toohello.

8. Quando terminar, clique em Olá **salvar** botão.

9. Você verá uma notificação informando que LDAP seguro está sendo configurado para o domínio gerenciado hello. Até que essa operação for concluída, você não pode modificar outras configurações para o domínio de saudação.

    ![Configurar o LDAP seguro para o domínio gerenciado Olá](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configuring.png)

> [!NOTE]
> Leva aproximadamente 10 minutos too15 tooenable LDAP seguro para seu domínio gerenciado. Se Olá fornecida seguro de certificados LDAP não coincide com hello necessário critérios, LDAP seguro não está habilitado para seu diretório e você verá uma falha. Por exemplo, nome de domínio hello está incorreta, certificado Olá já expirou ou expirará em breve. Nesse caso, tente novamente com um certificado válido.
>
>

<br>

## <a name="task-4---configure-dns-tooaccess-hello-managed-domain-from-hello-internet"></a>Tarefa 4 - configurar DNS tooaccess Olá domínio gerenciado de saudação à internet
> [!NOTE]
> **Tarefas opcionais** - se você não planeja tooaccess Olá domínio usando LDAPS Olá da internet, para ignorar esta tarefa de configuração.
>
>

Antes de começar essa tarefa, certifique-se de concluir Olá etapas descritas em [tarefa 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).

Depois que você tiver habilitado o acesso LDAP seguro através da internet de Olá para seu domínio gerenciado, você precisa tooupdate DNS para que os computadores cliente possam encontrar este domínio gerenciado. Final de saudação de tarefa 3, um endereço IP externo é exibido na Olá **propriedades** folha em **endereço de IP externo para acesso de LDAPS**.

Configure seu provedor DNS externo para que o nome DNS Olá de saudação gerenciado endereço IP externo de pontos toothis domínio (por exemplo, ' ldaps.contoso100.com'). Em nosso exemplo, precisamos Olá toocreate entrada DNS a seguir:

    ldaps.contoso100.com  -> 52.165.38.113

É isso – agora você está pronto tooconnect toohello gerenciado Olá de domínio usando o LDAP seguro através da internet.

> [!WARNING]
> Lembre-se de que os computadores cliente devem confiar emissor Olá Olá LDAPS certificado toobe capaz de tooconnect com êxito toohello gerenciados usando LDAPS do domínio. Se você estiver usando uma autoridade de certificação publicamente confiável, você não é necessário toodo qualquer coisa desde que essas emissores de certificado de confiança de computadores cliente. Se você estiver usando um certificado autoassinado, instale a parte pública de saudação do certificado autoassinado Olá no hello repositório de certificados confiáveis no computador do cliente de saudação.
>
>


## <a name="task-5---lock-down-ldaps-access-tooyour-managed-domain-over-hello-internet"></a>Tarefa 5 - bloqueio LDAPS acesso tooyour gerenciado Olá de domínio através da internet
> [!NOTE]
> **Tarefas opcionais** - se você não tiver habilitado o LDAPS domínio gerenciado do acesso toohello Olá da internet, para ignorar esta tarefa de configuração.
>
>

Antes de começar essa tarefa, certifique-se de concluir Olá etapas descritas em [tarefa 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).

Expondo o domínio gerenciado para acesso LDAPS sobre Olá internet representa uma ameaça à segurança. Olá domínio gerenciado é acessível a partir do hello internet na porta Olá usada para LDAP seguro (ou seja, porta 636). Portanto, você pode escolher toorestrict acesso toohello gerenciado domínio toospecific conhecido endereços IP. Para maior segurança, crie um grupo de segurança de rede (NSG) e associá-lo a sub-rede Olá onde você habilitou os serviços de domínio do AD do Azure.

Olá, tabela a seguir ilustra um exemplo NSG que você pode configurar, toolock para acesso LDAP seguro através de saudação à internet. Olá NSG contém um conjunto de regras que permitam o acesso LDAPS entrada pela porta TCP 636 somente de um conjunto especificado de endereços IP. Olá padrão 'DenyAll' regra se aplica tooall outro tráfego de entrada de saudação à internet. Olá NSG regra tooallow LDAPS o acesso por Olá internet de endereços IP especificados tem uma prioridade mais alta que Olá regra DenyAll NSG.

![Acesso ao exemplo NSG toosecure LDAPS por Olá da internet](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

**Mais informações** - [Grupos de segurança de rede](../virtual-network/virtual-networks-nsg.md).

<br>

## <a name="related-content"></a>Conteúdo relacionado
* [Serviços de Domínio do Azure AD - guia de Introdução](active-directory-ds-getting-started.md)
* [Administrar um domínio gerenciado dos Serviços de Domínio do Azure AD](active-directory-ds-admin-guide-administer-domain.md)
* [Administrar a política de grupo em um domínio gerenciado do Azure AD Domain Services](active-directory-ds-admin-guide-administer-group-policy.md)
* [Grupos de segurança de rede](../virtual-network/virtual-networks-nsg.md)
* [Criar um Grupo de Segurança de Rede](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
