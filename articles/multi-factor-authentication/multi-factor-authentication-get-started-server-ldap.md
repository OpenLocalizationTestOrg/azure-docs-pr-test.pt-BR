---
title: "aaaLDAP autenticação e o servidor Azure MFA | Microsoft Docs"
description: "Isso é a página de autenticação do Azure multi-factor Olá ajudará na implantação de autenticação LDAP e o servidor Azure multi-Factor Authentication."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: e1a68568-53d1-4365-9e41-50925ad00869
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: kgremban
ms.openlocfilehash: 17a26b57dbf6afa2fcfdb3d19c5b5ba2987a9f79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="ldap-authentication-and-azure-multi-factor-authentication-server"></a>Autenticação LDAP e Servidor de Autenticação Multifator do Azure
Por padrão, Olá servidor Azure multi-Factor Authentication é configurado tooimport ou sincronizar usuários do Active Directory. No entanto, pode ser configurado toobind toodifferent LDAP diretórios, como um diretório ADAM ou controlador de domínio do Active Directory específico. Quando conectado tooa diretório via LDAP, Olá servidor Azure multi-Factor Authentication pode agir como um autenticações de tooperform de proxy LDAP. Ele também permite Olá uso de ligação LDAP como um destino RADIUS, para pré-autenticação de usuários com a autenticação do IIS ou autenticação principal no portal do usuário hello Azure MFA.

toouse Azure multi-Factor Authentication como um proxy LDAP, insira Olá servidor Azure multi-Factor Authentication entre o cliente LDAP de saudação (por exemplo, o dispositivo de VPN, o aplicativo) e o servidor de diretório LDAP hello. Olá servidor Azure multi-Factor Authentication deve ser configurado toocommunicate com servidores de saudação do cliente e o diretório LDAP de saudação. Nessa configuração, hello servidor Azure multi-Factor Authentication aceita solicitações LDAP dos aplicativos e servidores do cliente e encaminha-toohello destino LDAP directory toovalidate Olá primárias credenciais do servidor. Se o diretório LDAP de saudação valida credenciais primárias hello, Azure multi-Factor Authentication realiza uma verificação de identidade segundo e envia uma resposta ao cliente toohello back LDAP. autenticação completa Olá só terá sucesso se autenticação do servidor LDAP hello e verificação de segundo etapa Olá bem-sucedida.

## <a name="configure-ldap-authentication"></a>Configurar a autenticação LDAP
autenticação de LDAP tooconfigure, Olá instalar servidor Azure multi-Factor Authentication em um servidor Windows. Use Olá procedimento a seguir:

### <a name="add-an-ldap-client"></a>Adicionar um cliente LDAP

1. No hello servidor Azure multi-Factor Authentication, selecione o ícone de autenticação LDAP de saudação no menu esquerdo hello.
2. Verificar Olá **habilitar autenticação LDAP** caixa de seleção.

   ![Autenticação LDAP](./media/multi-factor-authentication-get-started-server-ldap/ldap2.png)

3. Olá clientes guia, altere a porta TCP hello e a porta SSL se Olá serviço LDAP do Azure multi-Factor Authentication deve associar toolisten portas toonon padrão para solicitações LDAP.
4. Se você planejar toouse LDAPS do cliente de saudação toohello servidor Azure multi-Factor Authentication, um certificado SSL deve ser instalado em Olá mesmo servidor como servidor MFA. Clique em **procurar** toohello próximo SSL certificado caixa e selecione toouse um certificado de conexão segura hello.
5. Clique em **Adicionar**.
6. Na caixa de diálogo Adicionar cliente LDAP hello, insira o endereço IP de saudação do dispositivo hello, servidor ou aplicativo que autentica toohello servidor e um nome de aplicativo (opcional). nome do aplicativo Hello aparece em relatórios do Azure multi-Factor Authentication e pode ser exibido em mensagens de autenticação SMS ou do aplicativo móvel.
7. Verificar Olá **correspondência de usuários exigir Azure multi-Factor Authentication** caixa se todos os usuários foram ou serão importados para hello servidor e verificação de etapa tootwo de assunto. Se um número significativo de usuários ainda não foi importado no servidor de saudação e/ou está isento da verificação em duas etapas, deixe a caixa de saudação desmarcada. Consulte o arquivo de Ajuda do servidor MFA Olá para obter informações adicionais sobre esse recurso.

Repita essas etapas tooadd mais clientes LDAP.

### <a name="configure-hello-ldap-directory-connection"></a>Configurar a conexão de diretório LDAP Olá

Quando as autenticações de LDAP configurado tooreceive hello Azure multi-Factor Authentication, ele deverá proxy esses diretório LDAP toohello autenticações. Portanto, o guia de destino de Olá exibe somente um único esmaecidas opção toouse um destino LDAP.

1. Olá tooconfigure conexão de diretório LDAP, clique em Olá **integração de diretórios** ícone.
2. Na guia Configurações de saudação, selecione Olá **usar configuração LDAP específica** botão de opção.
3. Selecione **Editar...**
4. Na caixa de diálogo Editar configuração de LDAP hello, preencha os campos de saudação com hello informações necessárias tooconnect toohello LDAP directory. Descrições dos campos de saudação são incluídas no arquivo de Ajuda do servidor Azure multi-Factor Authentication hello.

    ![Integração de diretórios](./media/multi-factor-authentication-get-started-server-ldap/ldap.png)

5. Testar conexão de LDAP Olá clicando Olá **teste** botão.
6. Se o teste de conexão LDAP Olá foi bem-sucedido, clique em Olá **Okey** botão.
7. Clique em Olá **filtros** Olá na guia servidor está pré-configurado tooload contêineres, grupos de segurança e usuários do Active Directory. Se o diretório LDAP diferente de tooa de associação, você provavelmente precisará filtros de saudação tooedit exibidos. Clique em Olá **ajuda** link para obter mais informações sobre os filtros.
8. Clique em Olá **atributos** Olá na guia servidor está pré-configurado toomap atributos do Active Directory.
9. Se você estiver associando tooa outro diretório ou toochange Olá pré-configurado mapeamentos de atributos LDAP, clique em **editar...**
10. Na caixa de diálogo Editar atributos hello, modificar mapeamentos de atributos LDAP Olá para seu diretório. Nomes de atributo podem ser digitados ou selecionados clicando Olá **...** campo de tooeach próximo botão. Clique em Olá **ajuda** link para obter mais informações sobre atributos.
11. Clique em Olá **Okey** botão.
12. Clique em Olá **configurações da empresa** ícone e selecione Olá **resolução de nome de usuário** guia.
13. Se você estiver se conectando tooActive diretório de um servidor ingressado no domínio, deixe Olá **identificadores de segurança (SIDs) usar o Windows para correspondência de nomes de usuário** botão de opção selecionado. Caso contrário, selecione Olá **atributo de identificador exclusivo de usar LDAP para correspondência de nomes de usuário** botão de opção. 

Olá quando **atributo de identificador exclusivo de usar LDAP para correspondência de nomes de usuário** botão de opção é selecionada, Olá servidor Azure multi-Factor Authentication tenta tooresolve cada nome de usuário tooa o identificador exclusivo no diretório LDAP de saudação. Uma pesquisa LDAP é executada em Olá Username atributos definidos em Olá integração de diretórios -> guia atributos. Quando um usuário é autenticado, o nome de usuário de saudação é resolvido toohello o identificador exclusivo no diretório LDAP de saudação. Identificador exclusivo da saudação é usado para o usuário Olá correspondente no arquivo de dados do Azure multi-Factor Authentication hello. Isso permite comparações que não diferenciam maiúsculas de minúsculas, bem como formatos de nome de usuário curtos e longos.

Depois de concluir essas etapas, Olá servidor MFA escuta em portas de saudação configurada para solicitações de acesso LDAP de saudação configurado clientes e age como um proxy para as solicitações toohello diretório LDAP para autenticação.

## <a name="configure-ldap-client"></a>Configurar cliente LDAP
Olá tooconfigure cliente LDAP, use as diretrizes de saudação:

* Configure seu dispositivo, o servidor ou o aplicativo tooauthenticate via LDAP toohello servidor Azure multi-Factor Authentication como se fosse seu diretório LDAP. Use Olá mesmo configurações que normalmente usaria tooconnect diretamente tooyour diretório LDAP, exceto pelo nome do servidor de saudação ou endereço IP, que será da saudação servidor Azure multi-Factor Authentication.
* Configurar Olá LDAP tempo limite too30-60 de segundos para que haja tempo toovalidate Olá as credenciais de usuário com o diretório LDAP de hello, executar uma verificação de segundo etapa hello, receber a resposta e responder a solicitação de acesso LDAP toohello.
* Se estiver usando LDAPS, hello dispositivo ou o servidor faz consultas LDAP de saudação deve confiar Olá certificado SSL instalado no servidor Azure multi-Factor Authentication da saudação.

