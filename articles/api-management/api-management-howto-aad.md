---
title: contas de desenvolvedor aaaAuthorize usando o Active Directory do Azure - gerenciamento de API do Azure | Microsoft Docs
description: "Saiba como tooauthorize usuários usando o Active Directory do Azure no gerenciamento de API."
services: api-management
documentationcenter: API Management
author: steved0x
manager: erikre
editor: 
ms.assetid: 33a69a83-94f2-4e4e-9cef-f2a5af3c9732
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: ebf5447a509a47df35e4262138bfcf423cb1dd5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthorize-developer-accounts-using-azure-active-directory-in-azure-api-management"></a>Como desenvolvedor de tooauthorize contas usando Active Directory do Azure no gerenciamento de API do Azure
## <a name="overview"></a>Visão geral
Este guia mostra como tooenable acessar o portal do desenvolvedor toohello para os usuários do Active Directory do Azure. Este guia também mostra como toomanage grupos de usuários do Active Directory do Azure, adicionando grupos externos que contêm Olá usuários do Active Directory do Azure.

> Olá toocomplete as etapas neste guia primeiro você deve ter um Azure Active Directory no qual toocreate um aplicativo.
> 
> 

## <a name="how-tooauthorize-developer-accounts-using-azure-active-directory"></a>Como desenvolvedor de tooauthorize contas usando Active Directory do Azure
tooget iniciado, clique em **portal do publicador** no portal do Azure para seu serviço de gerenciamento de API de saudação. Isso leva toohello portal do publicador de gerenciamento de API.

![Portal do editor][api-management-management-console]

> Se você ainda não tiver criado uma instância do serviço de gerenciamento de API, consulte [criar uma instância do serviço de gerenciamento de API] [ Create an API Management service instance] em Olá [Introdução ao gerenciamento de API do Azure] [ Get started with Azure API Management] tutorial.
> 
> 

Clique em **segurança** de saudação **gerenciamento de API** menu Olá esquerda e clique em **identidades externas**.

![Identidades externas][api-management-security-external-identities]

Clique em **Active Directory do Azure**. Anote Olá **URL de redirecionamento** e passar tooyour Active Directory do Azure no hello Portal clássico do Azure.

![Identidades externas][api-management-security-aad-new]

Clique em Olá **adicionar** botão toocreate um novo aplicativo do Active Directory do Azure e escolha **adicionar um aplicativo que minha organização esteja desenvolvendo**.

![Adicionar novo aplicativo do Active Directory do Azure][api-management-new-aad-application-menu]

Insira um nome para o aplicativo hello, selecione **Web aplicativo e/ou API da Web**e clique no botão Avançar hello.

![Novo aplicativo do Active Directory do Azure][api-management-new-aad-application-1]

Para **URL de logon**, digite Olá URL de entrada de seu portal do desenvolvedor. Neste exemplo, Olá **URL de logon** é `https://aad03.portal.current.int-azure-api.net/signin`. 

Para Olá **URL de ID do aplicativo**, insira o saudação padrão domínio ou um domínio personalizado para Olá Active Directory do Azure e acrescentar tooit uma cadeia de caracteres exclusiva. Neste exemplo, Olá domínio padrão de **https://contoso5api.onmicrosoft.com** é usado com o sufixo de saudação do **/api** especificado.

![Propriedades do novo aplicativo do Active Directory do Azure][api-management-new-aad-application-2]

Clique em toosave de botão de seleção hello e criar o aplicativo hello e alternar toohello **configurar** guia aplicativo novo do tooconfigure hello.

![Novo aplicativo do Active Directory do Azure criado][api-management-new-aad-app-created]

Se vários Active Directories do Azure for toobe usado para esse aplicativo, clique em **Sim** para **aplicativo é multilocatário**. saudação padrão é **não**.

![Aplicativo é multilocatário][api-management-aad-app-multi-tenant]

Saudação de cópia **URL de redirecionamento** de saudação **Active Directory do Azure** seção Olá **identidades externas** guia no portal do publicador hello e cole-a saudação **URL de resposta** caixa de texto. 

![URL de resposta][api-management-aad-reply-url]

Rolar para o fim da saudação toohello configurar guia, selecione Olá **permissões de aplicativo** lista suspensa e verifique **ler dados do diretório**.

![Permissões de aplicativo][api-management-aad-app-permissions]

Selecione Olá **delegar permissões** lista suspensa e verifique **habilitar logon e ler perfis dos usuários**.

![Permissões delegadas][api-management-aad-delegated-permissions]

> Para obter mais informações sobre o aplicativo e as permissões delegadas, consulte [acessando Olá Graph API][Accessing hello Graph API].
> 
> 

Saudação de cópia **Id do cliente** toohello área de transferência.

![Id do Cliente][api-management-aad-app-client-id]

Alternar o portal do publicador toohello voltar e cole no hello **Id do cliente** copiado da configuração de aplicativo do Active Directory do Azure hello.

![Id do Cliente][api-management-client-id]

Alternar a configuração do Active Directory do Azure toohello voltar e, em seguida, clique em Olá **selecionar duração** suspensa no hello **chaves** seção e especificar um intervalo. Neste exemplo, **1 ano** é usado.

![Chave][api-management-aad-key-before-save]

Clique em **salvar** toosave Olá configuração e exibição Olá a chave. Copiar Olá chave toohello área de transferência.

> Anote esta chave. Quando você fechar a janela de configuração do Active Directory do Azure hello, chave de saudação não pode ser exibida novamente.
> 
> 

![Chave][api-management-aad-key-after-save]

Switch back toohello publicador portal e colar Olá chave em Olá **segredo do cliente** caixa de texto.

![Segredo do cliente][api-management-client-secret]

**Permitido locatários** Especifica os diretórios que têm acesso toohello APIs da instância de serviço de gerenciamento de API de saudação. Especifique domínios de saudação do hello toowhich de instâncias do Active Directory do Azure você deseja acesso toogrant. Você pode separar múltiplos domínios com novas linhas, espaços ou vírgulas.

![Locatários permitidos][api-management-client-allowed-tenants]


Depois de saudação desejado a configuração for especificada, clique em **salvar**.

![Salvar][api-management-client-allowed-tenants-save]

Depois de saudação alterações são salvas, usuários Olá Olá especificaram do Active Directory do Azure pode entrar no portal do desenvolvedor toohello, seguindo as etapas de saudação em [fazer logon no portal do desenvolvedor toohello usando uma conta do Active Directory do Azure] [Log in toohello Developer portal using an Azure Active Directory account].

Vários domínios podem ser especificados em Olá **permitido locatários** seção. Antes de qualquer usuário pode fazer logon de um domínio diferente Olá original em que o aplicativo hello foi registrado, um administrador global do domínio diferente da saudação deve conceder permissão para Olá aplicativo tooaccess dados do diretório. permissão de toogrant administrador global Olá deve ir muito`https://<URL of your developer portal>/aadadminconsent` (por exemplo, https://contoso.portal.azure-api.net/aadadminconsent), digite nome de domínio de saudação de Olá locatário do Active Directory que desejam toogive acesso tooand clique em enviar. Seguir Olá exemplo, um administrador global do `miaoaad.onmicrosoft.com` está tentando o portal do desenvolvedor específico de toothis de permissão de toogive. 

![Permissões][api-management-aad-consent]

Na próxima tela de Olá, administrador global Olá serão solicitada tooconfirm a concessão de permissão de saudação. 

![Permissões][api-management-permissions-form]

> Se um administrador global não tenta toolog em antes de permissões são concedidas por um administrador global, Olá tentativa de logon falhar e uma tela de erro é exibida.
> 
> 

## <a name="how-tooadd-an-external-azure-active-directory-group"></a>Como tooadd um externas do Azure Active Directory agrupar
Depois de habilitar o acesso de usuários no Active Directory do Azure, você pode adicionar grupos do Active Directory do Azure para gerenciamento de API toomore facilmente gerenciam associação de saudação de desenvolvedores Olá no grupo de saudação com produtos de saudação desejado.

> tooconfigure um grupo externo do Active Directory do Azure, hello Azure Active Directory primeiro deve ser configurado no guia de identidades Olá pelo procedimento na seção anterior Olá Olá. 
> 
> 

Grupos externos do Active Directory do Azure são adicionados do hello **visibilidade** guia do produto Olá para o qual você deseja que o grupo de toohello toogrant acesso. Clique em **produtos**e clique em nome de saudação do produto desejado hello.

![Configurar produto][api-management-configure-product]

Alternar toohello **visibilidade** guia e, em seguida, clique em **adicionar grupos do Active Directory do Azure**.

![Adicionar grupos][api-management-add-groups]

Selecione Olá **locatário do Azure Active Directory** da lista suspensa de saudação e, em seguida, nome de saudação de tipo de grupo desejado Olá Olá **grupos** toobe adicionado a caixa de texto.

![Selecionar grupo][api-management-select-group]

Este nome de grupo pode ser encontrado na Olá **grupos** lista para Active Directory do Azure, conforme mostrado no exemplo a seguir de saudação.

![Lista de grupos do Active Directory do Azure][api-management-aad-groups-list]

Clique em **adicionar** toovalidate Olá nome do grupo e adicione o grupo de saudação. Neste exemplo, Olá **Contoso 5 desenvolvedores** grupo externo é adicionado. 

![Grupo adicionado][api-management-aad-group-added]

Clique em **salvar** toosave Olá nova seleção de grupo.

Depois de um grupo do Active Directory do Azure foi configurado de um produto, é disponível toobe verificada em Olá **visibilidade** guia Olá outros produtos na instância de serviço de gerenciamento de API de saudação.

tooreview e configurar as propriedades de saudação para grupos externos quando eles foram adicionados, clique em nome de saudação do grupo Olá Olá **grupos** guia.

![Gerenciar grupos][api-management-groups]

Aqui você pode editar Olá **nome** e hello **descrição** do grupo de saudação.

![Editar grupo][api-management-edit-group]

Usuários de saudação configurado Active Directory do Azure pode entrar no modo de exibição e o portal do desenvolvedor toohello e assinar tooany grupos para os quais têm visibilidade seguindo instruções Olá Olá seção a seguir.

## <a name="how-toolog-in-toohello-developer-portal-using-an-azure-active-directory-account"></a>Como toolog no portal do desenvolvedor toohello usando uma conta do Active Directory do Azure
toolog no portal do desenvolvedor hello usando uma conta do Active Directory do Azure configurada nas seções anteriores do hello, abra uma nova janela de navegador usando Olá **URL de logon** na configuração de aplicativo do Active Directory hello e clique em **Active Directory do azure**.

![Portal do desenvolvedor][api-management-dev-portal-signin]

Insira as credenciais de saudação de um dos usuários de saudação no Active Directory do Azure e clique em **entrar**.

![Entrar][api-management-aad-signin]

Pode ser solicitado que você preencha um formulário de registro se qualquer informação adicional for necessária. Preencha o formulário de registro hello e clique em **inscrever**.

![Registro][api-management-complete-registration]

O usuário agora está conectado ao portal do desenvolvedor Olá para sua instância de serviço de gerenciamento de API.

![Registro completo][api-management-registration-complete]

[api-management-management-console]: ./media/api-management-howto-aad/api-management-management-console.png
[api-management-security-external-identities]: ./media/api-management-howto-aad/api-management-security-external-identities.png
[api-management-security-aad-new]: ./media/api-management-howto-aad/api-management-security-aad-new.png
[api-management-new-aad-application-menu]: ./media/api-management-howto-aad/api-management-new-aad-application-menu.png
[api-management-new-aad-application-1]: ./media/api-management-howto-aad/api-management-new-aad-application-1.png
[api-management-new-aad-application-2]: ./media/api-management-howto-aad/api-management-new-aad-application-2.png
[api-management-new-aad-app-created]: ./media/api-management-howto-aad/api-management-new-aad-app-created.png
[api-management-aad-app-permissions]: ./media/api-management-howto-aad/api-management-aad-app-permissions.png
[api-management-aad-app-client-id]: ./media/api-management-howto-aad/api-management-aad-app-client-id.png
[api-management-client-id]: ./media/api-management-howto-aad/api-management-client-id.png
[api-management-aad-key-before-save]: ./media/api-management-howto-aad/api-management-aad-key-before-save.png
[api-management-aad-key-after-save]: ./media/api-management-howto-aad/api-management-aad-key-after-save.png
[api-management-client-secret]: ./media/api-management-howto-aad/api-management-client-secret.png
[api-management-client-allowed-tenants]: ./media/api-management-howto-aad/api-management-client-allowed-tenants.png
[api-management-client-allowed-tenants-save]: ./media/api-management-howto-aad/api-management-client-allowed-tenants-save.png
[api-management-aad-delegated-permissions]: ./media/api-management-howto-aad/api-management-aad-delegated-permissions.png
[api-management-dev-portal-signin]: ./media/api-management-howto-aad/api-management-dev-portal-signin.png
[api-management-aad-signin]: ./media/api-management-howto-aad/api-management-aad-signin.png
[api-management-complete-registration]: ./media/api-management-howto-aad/api-management-complete-registration.png
[api-management-registration-complete]: ./media/api-management-howto-aad/api-management-registration-complete.png
[api-management-aad-app-multi-tenant]: ./media/api-management-howto-aad/api-management-aad-app-multi-tenant.png
[api-management-aad-reply-url]: ./media/api-management-howto-aad/api-management-aad-reply-url.png
[api-management-aad-consent]: ./media/api-management-howto-aad/api-management-aad-consent.png
[api-management-permissions-form]: ./media/api-management-howto-aad/api-management-permissions-form.png
[api-management-configure-product]: ./media/api-management-howto-aad/api-management-configure-product.png
[api-management-add-groups]: ./media/api-management-howto-aad/api-management-add-groups.png
[api-management-select-group]: ./media/api-management-howto-aad/api-management-select-group.png
[api-management-aad-groups-list]: ./media/api-management-howto-aad/api-management-aad-groups-list.png
[api-management-aad-group-added]: ./media/api-management-howto-aad/api-management-aad-group-added.png
[api-management-groups]: ./media/api-management-howto-aad/api-management-groups.png
[api-management-edit-group]: ./media/api-management-howto-aad/api-management-edit-group.png

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[Accessing hello Graph API]: http://msdn.microsoft.com/library/azure/dn132599.aspx#BKMK_Graph

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API toouse OAuth 2.0 user authorization]: #step2
[Test hello OAuth 2.0 user authorization in hello Developer Portal]: #step3
[Next steps]: #next-steps

[Log in toohello Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account

