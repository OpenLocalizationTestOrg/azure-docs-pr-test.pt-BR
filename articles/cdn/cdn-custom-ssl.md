---
title: "AAA \"Habilitar HTTPS em um domínio personalizado CDN do Azure | Microsoft Docs\""
description: "Saiba como tooenable HTTPS no ponto de extremidade CDN do Azure com um domínio personalizado."
services: cdn
documentationcenter: 
author: camsoper
manager: erikre
editor: 
ms.assetid: 10337468-7015-4598-9586-0b66591d939b
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: casoper
ms.openlocfilehash: 93746222616c9ed7977ec3b22c38ac1d43b118f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-https-on-an-azure-cdn-custom-domain"></a>Como ativar HTTPS em um domínio personalizado CDN do Azure

[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

Suporte HTTPS para domínios personalizados do Azure CDN permite que você toodeliver o conteúdo seguro via SSL usando sua própria segurança de saudação do domínio nome tooimprove de dados em trânsito. Olá fluxo de trabalho de ponta a ponta tooenable HTTPS para seu domínio personalizado foi simplificada por meio de um botão do mouse, gerenciamento de certificados completo e todos os sem nenhum custo adicional.

É privacidade de saudação tooensure crítico e integridade dos dados de todos os dados confidenciais de aplicativos web em trânsito. Usando Olá protocolo HTTPS garante que seus dados confidenciais são criptografados quando ela é enviada pela Olá da internet. Ele fornece confiabilidade, autenticação e protege seus aplicativos Web contra ataques. Atualmente, o CDN do Azure oferece suporte a HTTPS em um ponto de extremidade CDN. Por exemplo, se você criar um ponto de extremidade CDN do CDN do Azure (por exemplo, https://contoso.azureedge.net), o HTTPS será habilitado por padrão. Com HTTPS de domínio personalizado, você também pode habilitar a entrega segura para um domínio personalizado (por exemplo, https://www.contoso.com). 

Estes são alguns dos atributos de chave de saudação do recurso HTTPS:

- Sem custo adicional: não há custos de aquisição ou renovação do certificado e não há custo adicional para tráfego HTTPS. Você paga apenas GB de saída de hello CDN.

- Habilitação Simple: um clique de provisionamento está disponível no hello [portal do Azure](https://portal.azure.com). Você também pode usar a API REST ou outro recurso de saudação de tooenable de ferramentas de desenvolvedor.

- Gerenciamento de certificado completo: todos os certificados de aquisição e gerenciamento são manipulados para você. Os certificados são automaticamente provisionados e renovados tooexpiration anterior. Isso remove completamente os riscos de saudação de interrupção do serviço como resultado de um certificado expira.

>[!NOTE] 
>Suporte a HTTPS tooenabling anterior, você já deve ter estabelecido um [domínio personalizado CDN do Azure](./cdn-map-content-to-custom-domain.md).

## <a name="step-1-enabling-hello-feature"></a>Etapa 1: Habilitar o recurso de saudação 

1. Em Olá [portal do Azure](https://portal.azure.com), procure o perfil CDN tooyour Verizon padrão ou premium.

2. Na lista de saudação de pontos de extremidade, clique o ponto de extremidade de saudação que contém seu domínio personalizado.

3. Clique em Olá domínio personalizado para o qual você deseja tooenable HTTPS.

    ![Folha de ponto de extremidade](./media/cdn-custom-ssl/cdn-custom-domain.png)

4. Clique em **na** tooenable HTTPS e salvar a alteração de saudação.

    ![Caixa de diálogo personalizada HTTPS](./media/cdn-custom-ssl/cdn-enable-custom-ssl.png)


## <a name="step-2-domain-validation"></a>Etapa 2: validação de domínio

>[!IMPORTANT] 
>Conclua a validação completa de domínio antes de ativar o HTTPS no seu domínio personalizado. Você tem 6 dias tooapprove Olá domínio de negócios. A solicitação será cancelada se não tiver aprovação em 6 dias úteis.  

Depois de habilitar HTTPS em seu domínio personalizado, nosso provedor do certificado HTTPS DigiCert validará a propriedade de seu domínio entrando em contato com o inscrito Olá para seu domínio, com base nas informações de inscrito WHOIS, por email (por padrão) ou telefone. DigiCert também enviará Olá toohello de email de verificação abaixo endereços. Se as informações de inscrito WHOIS forem privadas, verifique se é possível aprovar diretamente por meio de um desses endereços.

>admin@<your-domain-name.com> administrator@<your-domain-name.com>  
>webmaster@<your-domain-name.com>  
>hostmaster@<your-domain-name.com>  
>postmaster@<your-domain-name.com>


Ao receber o email de saudação, você tem duas opções de verificação:

1. Você pode aprovar todas as futuras pedidos feitos por meio de saudação mesma conta para Olá mesmo domínio de raiz, por exemplo, consoto.com. Essa é uma abordagem recomendada, se você estiver planejando tooadd personalizado domínios adicionais Olá futura para Olá mesmo domínio de raiz.
 
2. Assim, você pode aprovar usada nesta solicitação de nome de host específico hello. Uma aprovação adicional será necessária para as solicitações seguintes.

    Email de exemplo:
    
    ![Caixa de diálogo personalizada HTTPS](./media/cdn-custom-ssl/domain-validation-email-example.png)

Após a aprovação, DigiCert adicionará seu certificado de SAN de toohello de nome de domínio personalizado. o certificado Olá será válido por um ano e será automaticamente renovado antes que ele expirou.

## <a name="step-3-wait-for-hello-propagation-then-start-using-your-feature"></a>Etapa 3: Aguarde a propagação de saudação e começar a usar o recurso

Depois que o nome de domínio Olá é validado demorará too6 8 horas para toobe HTTPS de recurso do domínio personalizado Olá active. Após a conclusão do processo de saudação, status de "HTTPS personalizado" hello em Olá portal do Azure será definido muito "Enabled". O HTTPS com seu domínio personalizado está pronto para uso.

## <a name="frequently-asked-questions"></a>Perguntas frequentes

1. *Quem é o provedor de certificado hello e que tipo de certificado é usado?*

    Usamos o certificado de nomes de alternativos da entidade (SAN) fornecido pela DigiCert. Um certificado SAN pode proteger vários nomes de domínio totalmente qualificados com um certificado.

2. *Posso usar o meu certificado dedicado?*
    
    Não no momento, mas seu em Olá roteiro.

3. *Se não receber email de verificação de domínio de saudação do DigiCert?*

    Entre em contato com a Microsoft se você não receber um email dentro de 24 horas.

4. *Usar um certificado SAN é menos seguro do que um certificado dedicado?*
    
    Um certificado SAN segue Olá mesmos padrões de criptografia e segurança, como um certificado dedicado. Todos os certificados SSL emitidos usam SHA-256 para uma maior segurança do servidor.

5. *Eu posso usar HTTPS do domínio personalizado com o CDN do Azure do Akamai?*

    Atualmente, esse recurso só está disponível com o CDN do Azure da Verizon. Estamos trabalhando em dar suporte a esse recurso com o Azure CDN do Akamai nos próximos meses de saudação.


## <a name="next-steps"></a>Próximas etapas

- Saiba como tooset a um [domínio personalizado no ponto de extremidade CDN do Azure](./cdn-map-content-to-custom-domain.md)


