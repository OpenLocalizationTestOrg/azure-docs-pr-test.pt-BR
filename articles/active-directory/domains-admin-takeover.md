---
title: "Controle do administrador sobre um diretório não gerenciado ou locatário de sombra no Azure Active Directory | Microsoft Docs"
description: "Como controlar um nome de domínio DNS em um diretório não gerenciado (locatário de sombra) no Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: mtillman
editor: 
ms.assetid: b9f01876-29d1-4ab8-8b74-04d43d532f4b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 11/14/2017
ms.author: curtand
ms.reviewer: elkuzmen
ms.custom: it-pro
ms.openlocfilehash: f18e5883fca9291eb1447c1eebfe0883936fe84f
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2017
---
# <a name="take-over-an-unmanaged-directory-as-administrator-in-azure-active-directory"></a>Controlar um diretório não gerenciado como administrador no Azure Active Directory
Este artigo descreve duas maneiras de controlar um nome de domínio DNS em um diretório não gerenciado no Azure AD (Azure Active Directory). Quando um usuário de autoatendimento se inscreve em um serviço de nuvem que usa o Azure AD, eles são adicionados a um diretório do Azure AD não gerenciado com base em seu domínio de email. Para obter mais informações sobre o autoatendimento ou inscrição “viral” em um serviço, consulte [O que é a inscrição de autoatendimento do Azure Active Directory?]()

## <a name="decide-how-you-want-to-take-over-an-unmanaged-directory"></a>Decida como você deseja controlar um diretório não gerenciado
Durante o processo de controle do administrador, você pode comprovar a propriedade conforme descrito em [Adicionar um nome de domínio personalizado para o Azure AD](add-custom-domain.md). As próximas seções explicam a experiência de administração mais detalhadamente, mas aqui está um resumo:

* Ao realizar um [controle do administrador “interno”](#internal-admin-takeover) de um diretório não gerenciado do Azure, você é adicionado como o administrador global do diretório não gerenciado. Usuários, domínios ou planos de serviço não são migrados para outros diretórios que você administra.

* Ao realizar um [controle do administrador “externo”](#external-admin-takeover) de um diretório não gerenciado do Azure, você adiciona o nome de domínio DNS do diretório não gerenciado ao seu diretório do Azure gerenciado. Ao adicionar o nome de domínio, um mapeamento dos usuários para os recursos é criado no diretório gerenciado do Azure, assim os usuários podem continuar a acessar os serviços sem interrupção. 

## <a name="internal-admin-takeover"></a>Controle de administrador interno

Alguns produtos que incluem o SharePoint e OneDrive, como o Office 365, não dão suporte a controle externo. Se esse for o seu cenário ou se você for um administrador e deseja controlar um locatário de “sombra” não gerenciado criado pelos usuários que usaram inscrição de autoatendimento, faça isso por meio do controle de administrador interno.

1. Crie um contexto de usuário no locatário não gerenciado por meio da inscrição com Power BI, por exemplo. Para fins de conveniência do exemplo, essas etapas pressupõem esse caminho.

2. Abra o [site do Power BI](https://powerbi.com) e selecione **Iniciar gratuitamente**. Insira uma conta de usuário que usa o nome de domínio para a organização como, por exemplo, `admin@fourthcoffee.xyz`. Depois que você inserir o código de verificação, confira seu email para ver o código de confirmação.

3. No email de confirmação do Power BI, selecione **Sim, sou eu**.

4. Entre no [Centro de administração do Office 365](https://portal.office.com/adminportal/Home) com a conta de usuário do Power BI. Você receberá uma mensagem instruindo-lhe a **Tornar-se o administrador** do nome de domínio que já foi verificado no locatário não gerenciado. selecione **Sim, quero ser o administrador**.
  
  ![primeira captura de tela para Tornar-se o administrador](./media/domains-admin-takeover/become-admin-first.png)
  
5. Adicione o registro TXT para provar que você possui o nome de domínio **fourthcoffee.xyz** no seu registrador de nomes de domínio. Neste exemplo, é GoDaddy.com.
  
  ![Adicionar um registro txt para o nome de domínio](./media/domains-admin-takeover/become-admin-txt-record.png)

Quando os registros TXT do DNS forem verificados no seu registrador de nomes de domínio, você poderá gerenciar o locatário do Azure AD.

Após concluir as etapas anteriores, você será o administrador global do locatário Fourth Coffee no Office 365. Para integrar o nome de domínio aos outros serviços do Azure, você pode removê-lo do Office 365 e adicioná-lo a um locatário gerenciado diferente no Azure.

### <a name="adding-the-domain-name-to-a-managed-tenant-in-azure-ad"></a>Como adicionar o nome de domínio a um locatário gerenciado no Azure AD 

1. Abra o [Centro de administração do Office 365](https://portal.office.com/adminportal/Home).
2. Selecione a guia **Usuários** e crie uma nova conta de usuário com um nome como *user@fourthcoffeexyz.onmicrosoft.com* que não usa o nome de domínio personalizado. 
3. Verifique se a nova conta de usuário tem privilégios de administrador global para o locatário do Azure AD.
4. Abra a guia **Domínios** no Centro de administração do Office 365, selecione o nome de domínio e escolha **Remover**. 
  
  ![remover o nome de domínio do Office 365](./media/domains-admin-takeover/remove-domain-from-o365.png)
  
5. Se você tiver usuários ou grupos no Office 365 que fazem referência ao nome de domínio removido, eles deverão ser renomeados para o domínio .onmicrosoft.com. Se você forçar a exclusão do nome de domínio, todos os usuários serão automaticamente renomeados, neste exemplo para *user@fourthcoffeexyz.onmicrosoft.com*.
  
6. Entre no [Centro de administração do Azure AD](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) com uma conta que seja um administrador global para o locatário para o Azure AD.
  
7. Selecione **Personalizar nomes de domínio** e adicione o nome de domínio. Você precisará inserir os registros TXT do DNS para verificar a propriedade do nome de domínio. 
  
  ![domínio adicionado ao Azure AD](./media/domains-admin-takeover/add-domain-to-azure-ad.png)
  
> [!NOTE]
> Os usuários do PowerBI ou do serviço Azure Rights Management que têm licenças atribuídas ao locatário do Office 365 devem salvar seus painéis, se o nome de domínio for removido. Eles devem entrar com um nome de usuário como *user@fourthcoffeexyz.onmicrosoft.com* em vez de *user@fourthcoffee.xyz*.

## <a name="external-admin-takeover"></a>Controle do administrador externo

Se você já gerencia um locatário com os serviços do Azure ou o Office 365, não será possível adicionar um nome de domínio personalizado se ele já estiver verificado em outro locatário do Azure AD. No entanto, do seu locatário gerenciado no Azure AD, você poderá controlar locatário não gerenciado como um controle de administrador externo. O procedimento geral segue o artigo [Adicionar um domínio personalizado ao Azure AD](add-custom-domain.md).

Quando você verificar a propriedade do nome de domínio, o Azure AD remove o nome de domínio do locatário não gerenciado e o migra para o locatário existente. O controle de administrador externo de um diretório não gerenciado requer o mesmo processo de validação de TXT do DNS que o controle de administrador interno. A diferença é que os itens a seguir também são movidos com o nome de domínio:

- Usuários
- Assinaturas
- Atribuições de licença
 
Há suporte para a opção [**ForceTakeover**](#azure-ad-powershell-cmdlets-for-the-forcetakeover-option) para controle de administrador externo do nome de domínio apenas em dois serviços, o Power BI e o Azure RMS.

### <a name="support-for-external-admin-takeover"></a>Suporte para controle de administrador externo
O controle de administrador externo tem suporte nos seguintes serviços online:

- Power BI
- Azure RMS (Rights Management Service)
- Exchange Online

Os planos de serviço com suporte incluem:

- Power BI Gratuito
- Power BI Pro
- PowerApps Gratuito
- PowerFlow Gratuito
- Azure RMS (Rights Management Service) Básico
- Azure RMS (Rights Management Service) Enterprise
- Microsoft Stream
- Avaliação gratuita do Dynamics 365

Não há suporte para controle de administrador externo para qualquer serviço que tenha planos de serviço que incluem o SharePoint, o OneDrive ou o Skype For Business como, por exemplo, por meio de uma assinatura gratuita do Office ou do SKU Básico do Office.

### <a name="azure-ad-powershell-cmdlets-for-the-forcetakeover-option"></a>Cmdlets do Azure AD PowerShell para a opção ForceTakeover
Você pode ver esses cmdlets usados no [exemplo do PowerShell](#powershell-example).


cmdlet | Uso 
------- | -------
`connect-msolservice` | Quando solicitado, entre no seu locatário gerenciado.
`get-msoldomain` | Mostra os nomes de domínio associados ao locatário atual.
`new-msoldomain –name <domainname>` | Adiciona o nome de domínio ao locatário como Não verificado (nenhuma verificação de DNS foi executada ainda).
`get-msoldomain` | O nome de domínio agora está incluído na lista de nomes de domínio associados com seu locatário gerenciado, mas está listado como **Não verificado**.
`get-msoldomainverificationdns –Domainname <domainname> –Mode DnsTxtRecord` | Fornece informações que serão colocadas no novo registro TXT do DNS para o domínio (MS=xxxxx). A verificação pode não acontecer imediatamente porque demora algum tempo para o registro TXT se propagar, portanto, aguarde alguns minutos antes de considerar a opção **-ForceTakeover**. 
`confirm-msoldomain –Domainname <domainname> –ForceTakeover Force` | <li>Se seu nome de domínio ainda não foi verificado, você pode prosseguir com a opção **-ForceTakeover**. Ele verifica se o registro TXT foi criado e inicia o processo de tomada de controle.<li>A opção **-ForceTakeover** deve ser adicionada ao cmdlet apenas ao forçar um controle de administrador externo, como quando o locatário não gerenciado tem serviços do Office 365 que bloqueiam o controle.
`get-msoldomain` | A lista de domínio agora mostra o nome de domínio como **Verificado**.

### <a name="powershell-example"></a>Exemplo de PowerShell

1. Conecte o Azure AD usando as credenciais utilizadas para responder à oferta de autoatendimento:
  ````
    import-module MSOnline
    $msolcred = get-credential
    
    connect-msolservice -credential $msolcred
  ````
2. Obter uma lista de domínios:
  
  ````
    Get-MsolDomain
  ````
3. Execute o cmdlet Get-MsolDomainVerificationDns para criar um desafio:
  ````
    Get-MsolDomainVerificationDns –DomainName *your_domain_name* –Mode DnsTxtRecord
  
    For example:
  
    Get-MsolDomainVerificationDns –DomainName contoso.com –Mode DnsTxtRecord
  ````

4. Copie o valor (o desafio) que é retornado deste comando. Por exemplo:
  ````
    MS=32DD01B82C05D27151EA9AE93C5890787F0E65D9
  ````
5. No seu namespace DNS público, crie um registro DNS txt que contenha o valor que você copiou na etapa anterior. O nome deste registro é o nome do domínio pai, então se você criar este registro de recurso usando a função DNS do Windows Server, deixe o nome do Registro em branco e cole apenas o valor na caixa de texto.
6. Execute o cmdlet Confirm-MsolDomain para verificar o desafio:
  
  ````
    Confirm-MsolEmailVerifiedDomain -DomainName *your_domain_name*
  ````
  
  Por exemplo:
  
  ````
    Confirm-MsolEmailVerifiedDomain -DomainName contoso.com
  ````

Um desafio bem-sucedido fará com que você retorne ao prompt sem erros.

## <a name="next-steps"></a>Próximas etapas
* [Adicionar um nome de domínio personalizado ao Azure AD](add-custom-domain.md)
* [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview)
* [PowerShell do Azure](/powershell/azure/overview)
* [Referência de Cmdlets do Azure](/powershell/azure/get-started-azureps)
* [Set-MsolCompanySettings](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0)

<!--Image references-->
[1]: ./media/active-directory-self-service-signup/SelfServiceSignUpControls.png
