---
title: "aaaConfigure um nome de domínio personalizado em serviços de nuvem | Microsoft Docs"
description: "Saiba como tooexpose seu aplicativo do Azure ou os dados em um domínio personalizado, definindo configurações de DNS."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 6a62c2b7-ea47-4cce-9d6a-0cca38357f42
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 71e553a73b40a8d0512b4d40173500561841772c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-custom-domain-name-for-an-azure-cloud-service"></a>Configurando um nome de domínio personalizado para um serviço de nuvem do Azure
> [!div class="op_single_selector"]
> * [Portal do Azure](cloud-services-custom-domain-name-portal.md)
> * [Portal clássico do Azure](cloud-services-custom-domain-name.md)
> 
> 

Quando você cria um serviço de nuvem, o Azure atribui a ele tooa subdomínio de cloudapp.net. Por exemplo, se seu serviço de nuvem é denominado "contoso", os usuários serão ser capaz de tooaccess seu aplicativo em uma URL como http://contoso.cloudapp.net. O Azure também fornece um endereço IP virtual.

No entanto, você também pode expor sua aplicação em seu próprio nome de domínio, como contoso.com. Este artigo explica como tooreserve ou configurar um nome de domínio personalizado para funções de web do serviço de nuvem.

Você já entendeu o que são os registros CNAME e A? [Salto após Olá explicação](#add-a-cname-record-for-your-custom-domain).

> [!NOTE]
> Agilize o trabalho! Saudação de uso do Azure [orientada passo a passo](http://support.microsoft.com/kb/2990804). Ele torna rápido a associação de um nome de domínio personalizado E a proteção da comunicação (SSL) com os Serviços de Nuvem do Azure.
> 
> 

<p/>

> [!NOTE]
> procedimentos de saudação nesta tarefa aplicam tooAzure serviços de nuvem. Para os Serviços de Aplicativos, veja [isto](../app-service-web/web-sites-custom-domain-name.md). Para as contas de armazenamento, veja [isto](../storage/blobs/storage-custom-domain-name.md).
> 
> 

## <a name="understand-cname-and-a-records"></a>Entenda os registros CNAME e A
CNAME (ou registros de alias) e registros de ambos permitem que você tooassociate um nome de domínio com um servidor específico (ou serviço nesse caso,) porém eles funcionam de forma diferente. Também há algumas considerações específicas ao usar registros com os serviços de nuvem do Azure que você deve considerar antes de decidir quais toouse.

### <a name="cname-or-alias-record"></a>Registro CNAME ou de alias
Um registro CNAME mapeia um *específico* domínio, como **contoso.com** ou **www.contoso.com**, nome de domínio canônico tooa. Nesse caso, o nome de domínio canônico Olá é hello **.cloudapp [myapp] .net** nome de domínio do seu Azure hospedado aplicativo. Depois de criado, Olá CNAME cria um alias para Olá **.cloudapp [myapp] .net**. Olá entrada CNAME resolverá toohello endereço IP do seu **.cloudapp [myapp] .net** serviço automaticamente, para que se mudar de endereço IP Olá Olá do serviço de nuvem, você não tem tootake qualquer ação.

> [!NOTE]
> Alguns registradores de domínio permitem subdomínios toomap ao usar um registro CNAME, como www.contoso.com e não nomes de raiz, como contoso.com. Para obter mais informações sobre os registros CNAME, consulte a documentação de saudação fornecida por seu registrador [Olá entrada da Wikipedia no registro CNAME](http://en.wikipedia.org/wiki/CNAME_record), ou hello [nomes de domínio IETF - implementação e especificação](http://tools.ietf.org/html/rfc1035) documento.
> 
> 

### <a name="a-record"></a>Registro A
Um registro mapeia um domínio, como **contoso.com** ou **www.contoso.com**, *ou um domínio curinga* como  **\*. contoso.com**, endereço IP tooan. No caso de saudação de um serviço de nuvem do Azure, Olá IP virtual do serviço de saudação. Portanto Olá principal benefício de um registro em um registro CNAME é que você pode ter uma entrada que usa um caractere curinga, como \* **. contoso.com**, que poderia tratar as solicitações de vários subdomínios como  **mail.contoso.com**, **login.contoso.com**, ou **www.contso.com**.

> [!NOTE]
> Como um registro é mapeado tooa endereço IP, ele automaticamente não puder resolver o endereço IP de toohello alterações do seu serviço de nuvem. Olá alocar endereço IP usado pelo serviço de nuvem é Olá primeira vez que você implantar tooan o slot vazio (produção ou preparo.) Se você excluir a implantação de saudação slot hello, endereço IP de saudação é liberado pelo Azure e qualquer intervalo de toohello implantações futuras pode receber um novo endereço IP.
> 
> Convenientemente, endereço IP de saudação de um slot de implantação especificada (produção ou preparo) é mantido durante a troca entre o preparo e implantações de produção ou executar uma atualização in-loco de uma implantação existente. Para obter mais informações sobre como executar essas ações, consulte [como serviços em nuvem toomanage](cloud-services-how-to-manage.md).
> 
> 

## <a name="add-a-cname-record-for-your-custom-domain"></a>Adicionar um registro CNAME para seu domínio personalizado
toocreate um registro CNAME, você deve adicionar uma nova entrada na tabela DNS Olá para seu domínio personalizado usando ferramentas de Olá fornecidas por seu registrador. Cada registro tem um método semelhante, mas um pouco diferentes de especificar um registro CNAME, mas Olá conceitos são Olá mesmo.

1. Use uma saudação de toofind esses métodos **. cloudapp.net** nome de domínio atribuído tooyour serviço de nuvem.
   
   * Logon toohello [portal clássico do Azure], selecione seu serviço de nuvem, selecione **painel**e, em seguida, localize Olá **URL do Site** entrada hello **visão rápida**  seção.
     
       ![seção visão rápida mostra a URL do site Olá][csurl]
     
       **OR**  
   * Instalar e configurar [Azure Powershell](/powershell/azure/overview), e, em seguida, use Olá comando a seguir:
     
       ```powershell
       Get-AzureDeployment -ServiceName yourservicename | Select Url
       ```
     
     Salve o nome de domínio Olá usado na URL de saudação retornado por qualquer método, pois você precisará dele durante a criação de um registro CNAME.
2. Faça logon no site do registrador DNS tooyour e vá para a página toohello para gerenciar DNS. Procure links ou áreas do site de saudação rotulados como **nome de domínio**, **DNS**, ou **nome do servidor de gerenciamento**.
3. Agora, encontre onde você pode selecionar ou inserir registros CNAME. Você pode ter o registro de saudação tooselect digite uma lista suspensa ou vá tooan página de configurações avançadas. Você deve procurar palavras Olá **CNAME**, **Alias**, ou **subdomínios**.
4. Você também deve fornecer Olá domínio ou subdomínio alias para Olá CNAME, tais como **www** se você quiser que um alias para toocreate **www.customdomain.com**. Se você quiser toocreate um alias para o domínio raiz da saudação, ele pode estar listado como Olá '**@**' símbolo em Ferramentas DNS do registrador.
5. Em seguida, você deve fornecer um nome do host canônico, que, neste caso, é o domínio **cloudapp.net** do seu aplicativo.

Por exemplo, a saudação após o registro CNAME encaminha todo o tráfego de **www.contoso.com** muito**contoso.cloudapp.net**, nome de domínio personalizado de saudação do seu aplicativo implantado:

| Alias/Nome do host/Subdomínio | Domínio canônico |
| --- | --- |
| www |contoso.cloudapp.net |

Um visitante de **www.contoso.com** nunca verá host true da saudação (contoso.cloudapp.net), Olá processo de encaminhamento é o usuário final de toothe invisível.

> [!NOTE]
> Olá exemplo acima se aplica apenas tootraffic em Olá **www** subdomínio. Uma vez que não é possível usar caracteres curinga com registros CNAME, você deve criar um CNAME para cada domínio/subdomínio. Se você quiser toodirect tráfego de subdomínios, tais como \*. contoso.com, tooyour cloudapp.net endereço, você pode configurar um **redirecionamento de URL** ou **URL Forward** entrada em suas configurações de DNS, ou Crie um registro.
> 
> 

## <a name="add-an-a-record-for-your-custom-domain"></a>Adicionar um registro A ao seu domínio personalizado
toocreate um um registro, você deve primeiro localizar endereço IP virtual de saudação do seu serviço de nuvem. Em seguida, adicione uma nova entrada na tabela DNS Olá para seu domínio personalizado usando ferramentas de Olá fornecidas por seu registrador. Cada registro tem um método semelhante, mas um pouco diferentes de especificar um registro, mas Olá conceitos são Olá mesmo.

1. Use um dos seguinte métodos tooget Olá endereço IP de seu serviço de nuvem de saudação.
   
   * logon toohello [portal clássico do Azure], selecione seu serviço de nuvem, selecione **painel**e, em seguida, localize Olá **endereço IP Virtual público (VIP)** entrada hello **visão rápida** seção.
     
       ![seção visão rápida mostrando Olá VIP][vip]
     
       **OR**  
   * Instalar e configurar [Azure Powershell](/powershell/azure/overview), e, em seguida, use Olá comando a seguir:
     
       ```powershell
       get-azurevm -servicename yourservicename | get-azureendpoint -VM {$_.VM} | select Vip
       ```
     
     Se você tiver vários pontos de extremidade associados ao seu serviço de nuvem, você receberá várias linhas que contém o endereço IP de saudação, mas todos devem exibir hello mesmo endereço.
     
     Salve endereço IP hello, pois você precisará dele durante a criação de um registro.
2. Faça logon no site do registrador DNS tooyour e vá para a página toohello para gerenciar DNS. Procure links ou áreas do site de saudação rotulados como **nome de domínio**, **DNS**, ou **nome do servidor de gerenciamento**.
3. Agora, encontre onde você pode selecionar ou inserir registros A. Você pode ter o registro de saudação tooselect digite uma lista suspensa ou vá tooan página de configurações avançadas.
4. Selecione ou digite o domínio de saudação ou subdomínio que usará esse registro. Por exemplo, selecione **www** se você quiser que um alias para toocreate **www.customdomain.com**. Se você quiser toocreate uma entrada de curinga para todos os subdomínios, insira '__*__'. Isso cobrirá todos os subdomínios, como **mail.customdomain.com**, **login.customdomain.com** e **www.customdomain.com**.
   
    Se você quiser toocreate um um registro para o domínio raiz da saudação, ele pode estar listado como Olá '**@**' símbolo em Ferramentas DNS do registrador.
5. Digite o endereço IP de saudação do seu serviço de nuvem no Olá fornecido campo. Isso associa a entrada de domínio Olá usada no registro Olá com o endereço IP de saudação da sua implantação do serviço de nuvem.

Por exemplo, a saudação um registro a seguir encaminha todo o tráfego de **contoso.com** muito**137.135.70.239**, Olá o endereço IP do seu aplicativo implantado:

| Nome do host/Subdomínio | Endereço IP |
| --- | --- |
| @ |137.135.70.239 |

Este exemplo demonstra como criar um registro a para o domínio raiz da saudação. Se você quiser toocreate toocover de entrada um curinga todos os subdomínios, insira '__*__' como o subdomínio hello.

> [!WARNING]
> Endereços IP no Azure são dinâmicos por padrão. Você provavelmente desejará toouse um [do endereço IP reservado](../virtual-network/virtual-networks-reserved-public-ip.md) tooensure que seu endereço IP não é alterado.
> 
> 

## <a name="next-steps"></a>Próximas etapas
* [Como os serviços de nuvem tooManage](cloud-services-how-to-manage.md)
* [Como tooMap conteúdo CDN tooa domínio personalizado](../cdn/cdn-map-content-to-custom-domain.md)
* [Configuração geral do serviço de nuvem](cloud-services-how-to-configure.md).
* Saiba como muito[implantar um serviço de nuvem](cloud-services-how-to-create-deploy.md).
* Configurar [certificados SSL](cloud-services-configure-ssl-certificate.md).

[Expose Your Application on a Custom Domain]: #access-app
[Add a CNAME Record for Your Custom Domain]: #add-cname
[Expose Your Data on a Custom Domain]: #access-data
[VIP swaps]: http://msdn.microsoft.com/library/ee517253.aspx
[Create a CNAME record that associates hello subdomain with hello storage account]: #create-cname
[portal clássico do Azure]: https://manage.windowsazure.com
[Validate Custom Domain dialog box]: http://i.msdn.microsoft.com/dynimg/IC544437.jpg
[vip]: ./media/cloud-services-custom-domain-name/csvip.png
[csurl]: ./media/cloud-services-custom-domain-name/csurl.png
