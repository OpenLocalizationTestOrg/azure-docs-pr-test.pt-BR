---
title: Perguntas frequentes sobre o RemoteApp do aaaAzure | Microsoft Docs
description: Saiba toohello respostas mais perguntas frequentes sobre o Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: swadhwa
editor: 
ms.assetid: bad66603-91f9-437f-8a70-236405d2a27f
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: da981fea9e38b4e74694aeaba5f97c8ed897ccd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-remoteapp-faq"></a>Perguntas frequentes sobre o RemoteApp do Azure
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

Fomos informados Olá seguintes perguntas sobre o Azure RemoteApp. Você tem outras? Visite Olá [RemoteApp fóruns](https://social.msdn.microsoft.com/Forums/azure/home?forum=AzureRemoteApp) e queremos saber o que você precisa tooknow ou suspensa um comentário abaixo.

## <a name="cant-find-what-youre-looking-for-have-a-question-we-didnt-answer"></a>Não encontrou o que você está procurando? Tem alguma pergunta que não respondemos?
Se você não pode encontrar informações de saudação é necessário, ou você tiver uma pergunta adicional que não estamos abordando aqui, acesse toohello [Fórum do Azure RemoteApp](http://aka.ms/araforum) e faça sua pergunta lá. Sempre poderemos adicionar mais respostas aqui.

## <a name="what-is-azure-remoteapp"></a>O que é o RemoteApp do Azure?
* **O que é o RemoteApp do Azure?** RemoteApp é um serviço do Azure ajuda a fornecer acesso remoto seguro tooapplications de muitos dispositivos de usuário diferente. Saiba mais sobre o [RemoteApp do Azure](remoteapp-whatis.md).
* **Quais são as opções de implantação de Olá?** Há dois tipos de coleções do RemoteApp: nuvem e híbrida. A que você precisa dependerá de alguns fatores, como se você precisa ingressar em um domínio. Falamos sobre todas essas decisões [aqui](remoteapp-collections.md).

## <a name="quick-tips-on-using-azure-remoteapp"></a>Dicas rápidas sobre como usar o Azure RemoteApp
* **Quanto tempo até eu ser desconectado? Quanto tempo pode ter ocioso antes de fornecer me inicialização Olá?** 4 horas. Se você ou um de seus usuários ficar ocioso por 4 horas, você será conectado automaticamente do Azure RemoteApp. Check-out Olá outras configurações padrão [assinatura do Azure e limites de serviço, cotas e restrições](../azure-subscription-service-limits.md).
* **Posso testar esse serviço gratuitamente?** Sim. Há uma avaliação gratuita disponível por 30 dias. Após o término hello avaliação, você poderá fazer a transição tooa pagas conta (que você pode usar em produção) ou parar de usar o serviço de saudação. Iniciar sua avaliação gratuita indo muito[portal.azure.com](http://portal.azure.com) -criar uma nova instância do RemoteApp. Com a versão de avaliação gratuita hello, você pode criar 2 instâncias do RemoteApp com 10 usuários por instância. Lembre-se de que esta avaliação dura 30 dias.
  
  ## <a name="azure-remoteapp-subscription-details"></a>Detalhes da assinatura do RemoteApp do Azure
* **Quais são os limites de serviço Olá?** Você pode saber mais sobre as configurações padrão de saudação e serviço limites do Azure RemoteApp em [assinatura do Azure e limites de serviço, cotas e restrições](../azure-subscription-service-limits.md). Avise-nos se você tiver mais dúvidas.
* **Quantos usuários são necessário toohave?** Há um mínimo de 20 usuários. Deixe-me repetir que toobe super clear - Olá mínimo é 20. Você será cobrado por 20. 
* **Qual é o custo do RemoteApp?** Verifique os [Detalhes de preços do Azure RemoteApp ](https://azure.microsoft.com/pricing/details/remoteapp/).
* **Um tipo de coleção custa mais do que o outro?** Sim, pode custar, dependendo dos requisitos de coleção. Uma coleção híbrida requer uma conexão de rede do Azure RemoteApp tooyour local. Se você usar uma VNET/Rota Expressa existente, não há nenhum custo adicional. Mas se você usar uma nova rede virtual do Azure e um gateway ou rota expressa, você será cobrado por Olá [gateway VPN](https://azure.microsoft.com/pricing/details/vpn-gateway) ou [rota expressa](https://azure.microsoft.com/pricing/details/expressroute/). Esse custo (detalhado em links de saudação) é sobre o Azure RemoteApp mensal de custo.

## <a name="collections---whats-supported-which-should-you-use-and-others"></a>Coleções - para o que há suporte, o que você deve usar e outros
* **Há suporte para aplicativos personalizados da linha de negócios (LOB)?** Sim. toouse um aplicativo personalizado no Azure RemoteApp, crie um [imagem de modelo personalizado](remoteapp-create-custom-image.md)e, em seguida, carregá-lo toohello coleção do RemoteApp.
* **Meu aplicativo LOB personalizado funcionará no Azure RemoteApp?**  Olá melhor toofigure de forma que a saída é tootest-lo. Check-out Olá [Centro de compatibilidade de área de trabalho remota](http://www.rdcompatibility.com/compatibility/default.aspx).
* **Qual método de implantação (nuvem ou híbrido) é o melhor para a minha organização?** Coleções de híbrida fornecem experiência mais completa de saudação se desejar que a integração total com logon único (SSO) e conectividade de rede em local seguro. Coleções de nuvem fornecem uma maneira ágil e fácil tooisolate sua implantação usando vários métodos de autenticação. Leia mais sobre Olá [opções de implantação](remoteapp-whatis.md).
* **Temos SQL ou outro banco de dados local ou no Azure. Qual o tipo de implantação que nós usamos?** Isso depende de onde está o seu banco de dados SQL ou back-end. Se o banco de dados de saudação estiver em uma rede privada, use coleção híbrida de saudação. Se o banco de dados de saudação toohello exposto à Internet e permite que o cliente conexões tooconnect tooit, você pode usar a coleção de nuvem hello.
* **E o mapeamento de unidade, USB e porta serial, o compartilhamento de área de transferência e o redirecionamento de impressora?** Todos esses recursos têm suporte no RemoteApp do Azure. O redirecionamento de impressora e o compartilhamento de área de transferência estão habilitados por padrão. Você pode aprender mais sobre redirecionamento [aqui](remoteapp-redirection.md). 

## <a name="template-images"></a>Imagens de modelo
* **Posso usar uma nuvem ou máquina virtual existente como modelo Olá para Minha coleção do RemoteApp?** Sim! Você pode criar uma imagem com base em uma VM do Azure, use uma das imagens de saudação incluídas com sua assinatura ou criar uma imagem personalizada. Check-out Olá [opções de imagem do RemoteApp](remoteapp-imageoptions.md).

## <a name="network-options"></a>Opções de rede
* **coleção de híbrida Olá requer uma rede virtual. Podemos usar nossa VNET existente?** Você pode se hello, rede virtual existente é uma rede virtual do Azure. Consulte "etapa 1: configurar a rede virtual" no hello [instruções de coleção híbrida](remoteapp-create-hybrid-deployment.md) para obter mais informações.
* **Posso usar uma VNET com uma coleção de nuvem?** Sim, é possível. Confira [Criar uma coleção de nuvem](remoteapp-create-cloud-deployment.md), em especial a Etapa 1, para obter mais informações.

## <a name="authentication-options"></a>Opções de autenticação
* **E quanto à autenticação? Há suporte para quais métodos?**  contas da Microsoft e contas do Active Directory do Azure, o que são contas do Office 365 também dá suporte a coleção de nuvem hello. a coleção de híbrida Olá suporta apenas as contas do Active Directory do Azure que foram sincronizadas (usando uma ferramenta como [sincronização do Active Directory do Azure](http://blogs.technet.com/b/ad/archive/2014/09/16/azure-active-directory-sync-is-now-ga.aspx)) de uma implantação do Windows Server Active Directory; especificamente, seja sincronizado com hello Opção de sincronização de senha ou sincronizados com a federação de serviços de Federação do Active Directory (AD FS) configurada. Você também pode configurar a [Autenticação multifator (MFA)](https://azure.microsoft.com/services/multi-factor-authentication/).

> [!NOTE]
> os usuários do Active Directory do Azure Olá devem ser do locatário Olá associado à sua assinatura. (Você pode exibir e modificar sua assinatura do hello **configurações** no portal de saudação. Consulte [locatário de Active Directory do Azure Olá alteração usado pelo RemoteApp](remoteapp-changetenant.md) para obter mais informações.)
> 
> 

* **Por que eu não pode dar o acesso à conta do Active Directory do Azure?**  usuários do Active Directory do Azure Olá devem ser do diretório de Olá associado à sua assinatura. Você pode exibir ou modificar esse diretório na guia Configurações de saudação no portal de saudação. Consulte [locatário de Active Directory do Azure Olá alteração usado pelo RemoteApp](remoteapp-changetenant.md) para obter mais informações.

## <a name="clients---what-device-can-i-use-tooaccess-azure-remoteapp"></a>Os clientes - o dispositivo pode usar o tooaccess Azure RemoteApp?
Você pode encontrar informações de cliente válido, incluindo as etapas de instalação diferentes clientes Olá no [acessar seus aplicativos no Azure RemoteApp](remoteapp-clients.md).

* **Quais dispositivos e sistemas operacionais dão suporte os aplicativos cliente Olá?**
  Primeiro, os computadores hello e tablets: 
  
  * Windows 10 (visualização de cliente)
  * Windows 8.1 e Windows 8
  * Windows 7 Service Pack 1
  * Mac OS X
  * Windows RT
  * Tablets Android
  * iPads

    Olá telefones e:
  * iPhone
  * Telefone Android
  * Windows Phone
    
    [Baixe](https://www.remoteapp.windowsazure.com/ClientDownload/AllClients.aspx) um cliente RemoteApp agora.
* **O RemoteApp do Azure dá suporte a clientes finos?** Sim, hello clientes Windows Embedded dinâmico a seguir têm suporte:
  
  * Windows Embedded Standard 7
  * Windows Embedded 8 Standard
  * Windows Embedded 8.1 Industry Pro
  * Windows 10 IoT Enterprise
* **Qual versão do Windows Server é suportada para Olá Host de sessão de área de trabalho remota (RDSH)?** Windows Server 2012 R2.

## <a name="support-and-feedback"></a>Suporte e comentários
* **O que é o plano de suporte de saudação do RemoteApp?** O suporte para o gerenciamento de assinaturas e cobrança é fornecido sem custo. O suporte técnico está disponível por meio de saudação [planos de serviço do Azure](https://azure.microsoft.com/support/plans/). Você também pode obter suporte gratuito para a comunidade por meio do nosso [Fórum de discussão do Azure](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=AzureRemoteApp). 
* **Como posso enviar comentários?** Visite Olá [Fórum de comentários](https://feedback.azure.com/forums/247748-azure-remoteapp/).
* **Quem posso falar toolearn mais sobre o Azure RemoteApp?** Em adição tooour [Fórum de discussão](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=AzureRemoteApp), que é ótimo lugar toopost perguntas, você pode unir Olá semanalmente [pedir Olá especialistas webinar](https://azureinfo.microsoft.com/US-Azure-WBNR-FY15-11Nov-AzureRemoteAppAskTheExperts-Registration-Page.html), onde falamos sobre todas as coisas RemoteApp.
* **E a documentação do RemoteApp?** Estamos felizes com a pergunta. Além disso toohello conteúdo na gaveta de Ajuda do portal de saudação da Ajuda (clique Olá **?** em qualquer página no portal de saudação), Olá artigos a seguir está disponível tooteach você sobre o RemoteApp:
  
  * **Introdução:**
    * [O que é o RemoteApp?](remoteapp-whatis.md)
    * [O que há imagens de modelo do RemoteApp Olá?](remoteapp-images.md)
    * [Como funciona o licenciamento?](remoteapp-licensing.md)
    * [Como o RemoteApp e o Office funcionam juntos?](remoteapp-o365.md)
    * [Como o redirecionamento funciona no RemoteApp](remoteapp-redirection.md)?
  * **Implantar:**
    * [Criar uma imagem personalizada de modelo](remoteapp-create-custom-image.md)
    * [Criar uma coleção híbrida](remoteapp-create-hybrid-deployment.md)
    * [Criar uma coleção na nuvem](remoteapp-create-cloud-deployment.md)
    * [Configurar o Active Directory do Azure para o RemoteApp](remoteapp-ad.md)
    * [Publicar um aplicativo no RemoteApp](remoteapp-publish.md)
  * **Gerenciar:**
    
    * [Adicionar usuários](remoteapp-user.md)
    * [Práticas recomendadas para configurar e usar o RemoteApp](remoteapp-bestpractices.md)    
    
    Vídeos! Também temos inúmeros vídeos sobre o RemoteApp. Alguns fornecem Introdução ([tooAzure Introdução RemoteApp](https://azure.microsoft.com/documentation/videos/cloud-cover-ep-150-azure-remote-app-with-thomas-willingham-and-nihar-namjoshi/)) enquanto outros orientá-lo por meio de implantação ([implantação de nuvem](https://www.youtube.com/watch?v=3NAv2iwZtGc&feature=youtu.be) e [implantação híbrida](https://www.youtube.com/watch?v=GCIMxPUvg0c&feature=youtu.be)). Experimente-os!

### <a name="help-us-help-you"></a>Ajude-nos a ajudar você
Você sabia que na adição toorating neste artigo e fazer comentários para baixo abaixo, você pode fazer alterações toohello artigo? Falta alguma coisa? Há algo errado? Escrevi algo que não ficou muito claro? Role para cima e clique em **Editar no GitHub** toomake alterações - aqueles virão toous para revisão e, em seguida, uma vez que saia neles, você verá suas alterações e aprimoramentos aqui.

