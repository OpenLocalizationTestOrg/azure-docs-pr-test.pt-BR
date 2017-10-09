---
title: "dados pessoais aaaProtect em trânsito com criptografia no Azure | Microsoft Docs"
description: Usando a criptografia em dados pessoais tooprotect do Azure
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 218ad3f49326e8dec299a6d92b18116da65eae71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-encryption-technologies-protect-personal-data-in-transit-with-encryption"></a>Tecnologias de criptografia do Azure: proteger dados pessoais em trânsito com criptografia

Este artigo o ajudará a entender e usar dados de toosecure de tecnologias de criptografia do Azure em trânsito. 

Privacidade de saudação proteção dos dados pessoais enquanto trafegam pela rede Olá é uma parte essencial de uma estratégia de segurança em várias camadas de defesa em profundidade. A criptografia em trânsito é projetado tooprevent um invasor intercepta as transmissões de ser capaz de dados de saudação tooview ou usar.

## <a name="scenario"></a>Cenário

Uma empresa cruzeiro grandes, com sede Olá dos Estados Unidos, está expandindo suas roteiros de toooffer operações Mediterrâneo hello, Adriatic e mares báltico, bem como Olá Britânicas. toosupport os esforços adquiriu várias linhas de cruzeiro menores na Itália, Alemanha, Dinamarca e hello UK 

empresa de saudação usa dados corporativos do Microsoft Azure toostore na nuvem hello. Eles incluem informações de identificação pessoal, como nomes, endereços, números de telefone e informações de cartão de crédito de sua base global de clientes. Ele também inclui informações de recursos humanos tradicionais, como endereços, números de telefone, números de identificação de imposto e médicas informações sobre os funcionários da empresa em todos os locais. linha de cruzeiro Olá também mantém um banco de dados grande de membros do programa de recompensa e fidelidade que incluem informações pessoais tootrack relações com os clientes atuais e anteriores.

Dados pessoais de clientes são inseridos no banco de dados de saudação de escritórios remotos da empresa Olá em agentes Olá mundo todo. Documentos que contêm informações de cliente são transferidos entre Olá rede tooAzure de armazenamento.

## <a name="problem-statement"></a>Problema declarado

empresa Olá deve proteger a privacidade de saudação do cliente e dados pessoais de funcionários enquanto ele estão em trânsito tooand dos serviços do Azure.

## <a name="company-goal"></a>Meta da empresa

Olá tooensure de meta da empresa que dados pessoais são criptografados quando desativar o disco. Se pessoas não autorizadas interceptarem dados pessoais do hello fora do disco, ele deve ser em um formulário que será renderizado ilegível. A aplicação da criptografia deve ser fácil ou completamente transparente, para os usuários e administradores.

## <a name="solutions"></a>Soluções

Os serviços do Azure fornecem vários toohelp ferramentas e tecnologias de proteger dados pessoais em trânsito.

### <a name="azure-storage"></a>Armazenamento do Azure

Dados armazenados na nuvem Olá devem passar de cliente hello, que pode estar fisicamente localizado em qualquer lugar no mundo hello, toohello data center do Azure. Quando os dados são recuperados por usuários, novamente, trafegam na Olá oposta direção. Dados que estão em trânsito Olá Internet pública sempre está em risco de interceptação por invasores. É importante tooprotect privacidade de saudação dos dados pessoais usando criptografia de nível de transporte toosecure como ele se move entre locais.

Olá protocolo HTTPS fornece um canal de comunicação seguro e criptografado em relação a saudação da Internet. HTTPS deve ser usado tooaccess objetos no armazenamento do Azure e ao chamar APIs REST. Impor o uso do protocolo HTTPS Olá ao usar [assinaturas de acesso compartilhado](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) objetos de armazenamento (SAS) toodelegate acesso tooAzure. Há dois tipos de SAS: SAS de Serviço e SAS de Conta.

#### <a name="how-do-i-construct-a-service-sas"></a>Como fazer para construir uma SAS de Serviço?

Um serviço SAS delegados acesso tooa recurso em apenas um dos serviços de armazenamento da saudação (serviço blob, fila, tabela ou arquivo). tooconstruct uma SAS do serviço, Olá a seguir:

1. Especifique a saudação o campo de versão assinado

2. Especifique a saudação recurso assinado (Blob e somente serviço de arquivo)

3. Especificar parâmetros de consulta tooOverride cabeçalhos de resposta (serviço Blob e arquivo de serviço somente)

4. Especifique a saudação nome da tabela (serviço de tabela somente)

5. Especifique a política de acesso de saudação

6. Especifique a saudação intervalo de validade da assinatura

8. Especifique as permissões

9. Especifique o endereço IP ou o intervalo de IP

10. Especifique a saudação protocolo HTTP

11. Especifique os intervalos de acesso da tabela

12. Especifique a saudação identificador assinado

13. Especifique a saudação assinatura

Para obter instruções mais detalhadas, consulte [Construindo uma SAS de Serviço](https://docs.microsoft.com/rest/api/storageservices/Constructing-a-Service-SAS?redirectedfrom=MSDN).

#### <a name="how-do-i-construct-an-account-sas"></a>Como fazer para construir uma SAS de Conta?

Uma SAS da conta delega tooresources de acesso em um ou mais dos serviços de armazenamento de saudação. Você também pode delegar acesso tooread, gravação e operações de exclusão em contêineres de blob, tabelas, filas e compartilhamentos de arquivos que não são permitidos com um serviço de SAS. Construção de uma conta de SAS é semelhante toothat de uma SAS do serviço. Para obter instruções detalhadas, consulte [Construindo uma SAS de Conta.](https://docs.microsoft.com/rest/api/storageservices/Constructing-an-Account-SAS?redirectedfrom=MSDN)

#### <a name="how-do-i-enforce-https-when-calling-rest-apis"></a>Como fazer para impor o HTTPS ao chamar APIs REST?

tooenforce o uso de saudação de HTTPS ao chamar objetos tooaccess de APIs REST em contas de armazenamento, você pode habilitar Secure transferir necessário Olá conta de armazenamento. 

1. No portal do Azure de Olá, selecione **criar conta de armazenamento**, ou para uma conta de armazenamento existente, selecione **configurações** e, em seguida, **configuração**.

2. Em **Transferência Segura Obrigatória**, selecione **Habilitada**.

![Criando uma conta de armazenamento](media/protect-personal-data-in-transit-encryption/create-storage-account.png)

Para obter instruções mais detalhadas, incluindo como tooenable proteger transferir obrigatório programaticamente, consulte [precisam proteger transferir](https://docs.microsoft.com/azure/storage/storage-require-secure-transfer).

#### <a name="how-do-i-encrypt-data-in-azure-file-storage"></a>Como fazer para criptografar dados no Armazenamento de Arquivos do Azure?

tooencrypt dados em trânsito com [armazenamento de arquivo do Azure](https://docs.microsoft.com/azure/storage/storage-file-how-to-use-files-portal), você pode usar o SMB 3. x com o Windows 8, 8.1 e 10 e Windows Server 2012 R2 e Windows Server 2016. Quando você estiver usando o serviço de arquivos do Azure Olá, qualquer conexão sem criptografia falhará ao "Seguro transferência necessária" está habilitado. Isso inclui cenários de uso de SMB 2.1, SMB 3.0 sem criptografia e alguns tipos de saudação cliente Linux SMB.

#### <a name="azure-client-side-encryption"></a>Criptografia do Lado do Cliente do Azure

Outra opção para proteger dados pessoais enquanto estão sendo transferidos entre um aplicativo cliente e o Armazenamento do Azure é a [Criptografia do Lado do Cliente](https://docs.microsoft.com/azure/storage/storage-client-side-encryption). Olá dados são criptografados antes de serem transferidos para o armazenamento do Azure e ao recuperar dados de saudação do armazenamento do Azure, os dados de saudação são descriptografados depois de ser recebida no lado do cliente de saudação.

### <a name="azure-site-to-site-vpn"></a>VPN site a site do Azure

Um maneira eficiente tooprotect pessoal os dados em trânsito entre uma rede corporativa ou o usuário e a saudação rede virtual do Azure são toouse uma [site a site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal) ou [ponto a site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) rede Virtual privada (VPN). Uma conexão VPN cria um encapsulamento criptografado seguro em Olá da Internet.

#### <a name="how-do-i-create-a-site-to-site-vpn-connection"></a>Como fazer para criar uma conexão VPN site a site?

Uma VPN site a site se conecta a vários usuários em Olá tooAzure de rede corporativa. toocreate uma conexão site a site no hello portal do Azure, Olá a seguir:

1. Crie uma rede virtual.

2. Especifique um servidor DNS.

3. Crie uma sub-rede de gateway hello.

4. Crie gateway VPN hello. 

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-01.png)

5. Crie gateway de rede local hello.

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-02.png)

6. Configure o dispositivo VPN.

7. Crie conexão de VPN hello.

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-03.png)

8. Verifique se a conexão de VPN hello.

Para obter instruções mais detalhadas sobre como conexão toocreate uma site a site no hello Azure portal, consulte [criar uma Site a Site conexão no hello Portal do Azure]. (https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)

#### <a name="how-do-i-create-a-point-to-site-vpn-connection"></a>Como fazer para criar uma conexão VPN ponto a site?

Uma VPN ponto a Site cria uma conexão segura de uma rede virtual do computador tooa de clientes individuais. Isso é útil quando você deseja tooAzure tooconnect de um local remoto, como de central casa ou em um hotel ou conferência. toocreate uma conexão ponto a site no hello portal do Azure,

1. Crie uma rede virtual.

2. Adicione uma sub-rede de gateway.

3. Especifique um servidor DNS. (opcional)

4. Crie um gateway de rede virtual.

5. Gere certificados.

6. Adicione pool de endereços de cliente de saudação.

7. Carregar dados de certificado pública do certificado de raiz hello.

8. Gerar e instale o pacote de configuração de cliente VPN hello.

9. Instale um certificado do cliente exportado.

10. Conecte-se tooAzure.

11. Verifique a conexão.

Para obter instruções mais detalhadas, consulte [configurar uma conexão de ponto para Site tooa VNet usando a autenticação de certificado: Portal do Azure.](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)

### <a name="ssltls"></a>SSL/TLS

A Microsoft recomenda que você sempre use dados de tooexchange protocolos SSL/TLS em diferentes locais. As organizações que escolha toouse [ExpressRoute](https://docs.microsoft.com/azure/expressroute/) toomove grandes conjuntos de dados em um link WAN de alta velocidade dedicado também pode criptografar dados Olá Olá usando SSL/TLS ou outros protocolos para proteção adicional de nível de aplicativo.

### <a name="encryption-by-default"></a>Criptografia por padrão

A Microsoft usa os dados de tooprotect de criptografia em trânsito entre clientes e serviços de nuvem do Azure. Se você estiver interagindo com o armazenamento do Azure por meio de saudação Portal do Azure, todas as transações ocorrem por meio de HTTPS.

[Segurança de camada de transporte](https://en.wikipedia.org/wiki/Transport_Layer_Security) (TLS) é o protocolo de saudação que data centers da Microsoft tentará toonegotiate com sistemas de cliente que se conectam tooMicrosoft serviços de nuvem. O TLS fornece autenticação forte, privacidade de mensagem e integridade (habilita a detecção de adulteração, interceptação e falsificação de mensagens), interoperabilidade, flexibilidade de algoritmo, facilidade de implantação e uso.

O [PFS](https://en.wikipedia.org/wiki/Forward_secrecy) (Perfect Forward Secrecy) também é utilizado para que cada conexão entre os sistemas cliente dos clientes e os serviços de nuvem da Microsoft usem chaves exclusivas. Serviços de nuvem tooMicrosoft conexões também tirar proveito de criptografia de 2.048 bits RSA com comprimentos de chave. Olá combinação de TLS, comprimentos de chave RSA de 2.048 bits, e PFS torna muito mais difícil para alguém toointercept e acessar dados em trânsito entre clientes e serviços de nuvem da Microsoft.

Os dados em trânsito são Always Encrypted no [Data Lake Store] (https://docs.microsoft.com/azure/data-lake-store/data-lake-store-security-overview). Além disso mídia toopersistent do tooencrypting dados toostoring anterior, Olá dados são sempre protegidos em trânsito usando HTTPS. HTTPS é Olá único protocolo com suporte para Olá que interfaces Data Lake repositório REST.

## <a name="summary"></a>Resumo

empresa Olá pode fazer o seu objetivo de proteção de privacidade de dados e hello pessoal desses dados impondo HTTPS conexões tooAzure armazenamento, usando assinaturas de acesso compartilhado e habilitando seguro transferir necessárias em contas de armazenamento hello. Ela também pode proteger os dados pessoais usando conexões SMB 3.0 e implementando a criptografia do lado do cliente. Olá de conexões de VPN site a site da rede corporativa toohello rede virtual do Azure e conexões de VPN de ponto para site de usuários individuais criará um túnel seguro por meio do qual dados pessoais podem viajar com segurança. Práticas recomendadas de criptografia de padrão da Microsoft serão proteger ainda mais privacidade Olá dos dados pessoais.

## <a name="next-steps"></a>Próximas etapas

- [Melhores práticas de segurança de dados e criptografia do Azure](https://docs.microsoft.com/azure/security/azure-security-data-encryption-best-practices)

- [Planejamento e design do Gateway de VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design)

- [Perguntas frequentes de gateway de VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-vpn-faq)

- [Comprar e configurar um certificado SSL para o Serviço de Aplicativo do Azure](https://docs.microsoft.com/azure/app-service-web/web-sites-purchase-ssl-web-site)
