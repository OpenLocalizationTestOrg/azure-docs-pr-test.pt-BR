---
title: "Visão geral do modelo de licença PlayReady dos serviços aaaMedia"
description: "Este tópico fornece uma visão geral de um modelo de licença do PlayReady usado tooconfigure licenças do PlayReady."
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: fddce5d0-1278-478f-ae05-9b985c748731
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 5a5ba930c56f70038db204681486ebc4308199fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="media-services-playready-license-template-overview"></a><span data-ttu-id="bec6a-103">Visão geral do modelo de licença do PlayReady dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="bec6a-103">Media Services PlayReady license template overview</span></span>
<span data-ttu-id="bec6a-104">Os Serviços de Mídia do Azure fornecem um serviço de distribuição de licenças do Microsoft PlayReady.</span><span class="sxs-lookup"><span data-stu-id="bec6a-104">Azure Media Services now provides a service for delivering Microsoft PlayReady licenses.</span></span> <span data-ttu-id="bec6a-105">Quando o player do usuário final hello (por exemplo, o Silverlight) tenta tooplay o PlayReady o conteúdo protegido, uma solicitação é enviada toohello licença entrega serviço tooobtain uma licença.</span><span class="sxs-lookup"><span data-stu-id="bec6a-105">When hello end user player (for example, Silverlight) tries tooplay your PlayReady protected content, a request is sent toohello license delivery service tooobtain a license.</span></span> <span data-ttu-id="bec6a-106">Se o serviço de licença Olá Aprovar solicitação de Olá, ele emite licença saudação que é enviada toohello cliente e pode ser usado toodecrypt e play Olá conteúdo especificado.</span><span class="sxs-lookup"><span data-stu-id="bec6a-106">If hello license service approves hello request, it issues hello license which is sent toohello client and can be used toodecrypt and play hello specified content.</span></span>

<span data-ttu-id="bec6a-107">Os Serviços de Mídia também fornecem APIs que permitem que você configure suas licenças do PlayReady.</span><span class="sxs-lookup"><span data-stu-id="bec6a-107">Media Services also provides APIs that let you configure your PlayReady licenses.</span></span> <span data-ttu-id="bec6a-108">As licenças contêm os direitos de saudação e restrições que você deseja para Olá tooenforce de tempo de execução do PlayReady DRM quando um usuário está tentando tooplayback o conteúdo protegeram.</span><span class="sxs-lookup"><span data-stu-id="bec6a-108">Licenses contain hello rights and restrictions that you want for hello PlayReady DRM runtime tooenforce when a user is trying tooplayback protected content.</span></span>
<span data-ttu-id="bec6a-109">Abaixo estão alguns exemplos de restrições de licença PlayReady que você pode especificar:</span><span class="sxs-lookup"><span data-stu-id="bec6a-109">Below are some examples of PlayReady license restrictions that you can specify:</span></span>

* <span data-ttu-id="bec6a-110">DateTime de saudação do qual Olá a licença é válida.</span><span class="sxs-lookup"><span data-stu-id="bec6a-110">hello DateTime from which hello license is valid.</span></span>
* <span data-ttu-id="bec6a-111">saudação do valor de data/hora quando Olá licença expira.</span><span class="sxs-lookup"><span data-stu-id="bec6a-111">hello DateTime value when hello license expires.</span></span> 
* <span data-ttu-id="bec6a-112">Para toobe de licença Olá salvo no armazenamento persistente no cliente de saudação.</span><span class="sxs-lookup"><span data-stu-id="bec6a-112">For hello license toobe saved in persistent storage on hello client.</span></span> <span data-ttu-id="bec6a-113">Licenças persistentes são geralmente usados tooallow reprodução offline conteúdo de hello.</span><span class="sxs-lookup"><span data-stu-id="bec6a-113">Persistent licenses are typically used tooallow offline playback of hello content.</span></span>
* <span data-ttu-id="bec6a-114">Olá nível mínimo que um player deve ter tooplay seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="bec6a-114">hello minimum security level that a player must have tooplay your content.</span></span> 
* <span data-ttu-id="bec6a-115">saudação de nível de proteção para os controles de saída Olá para o conteúdo de áudio/vídeo de saída.</span><span class="sxs-lookup"><span data-stu-id="bec6a-115">hello output protection level for hello output controls for audio\video content.</span></span> 
* <span data-ttu-id="bec6a-116">Para obter mais informações, consulte controles de saída Olá seção (3.5) hello em [as regras de conformidade do PlayReady](https://www.microsoft.com/playready/licensing/compliance/) documento.</span><span class="sxs-lookup"><span data-stu-id="bec6a-116">For more information, see hello Output Controls section (3.5) in hello [PlayReady Compliance Rules](https://www.microsoft.com/playready/licensing/compliance/) document.</span></span>

> [!NOTE]
> <span data-ttu-id="bec6a-117">No momento, você pode configurar apenas Olá PlayRight da licença do PlayReady hello (esse direito é necessário).</span><span class="sxs-lookup"><span data-stu-id="bec6a-117">Currently, you can only configure hello PlayRight of hello PlayReady license (this right is required).</span></span> <span data-ttu-id="bec6a-118">Olá PlayRight oferece cliente Olá conteúdo de Olá Olá capacidade tooplayback.</span><span class="sxs-lookup"><span data-stu-id="bec6a-118">hello PlayRight gives hello client hello ability tooplayback hello content.</span></span> <span data-ttu-id="bec6a-119">Olá PlayRight também permite a configuração tooplayback específicos de restrições.</span><span class="sxs-lookup"><span data-stu-id="bec6a-119">hello PlayRight also allows configuring restrictions specific tooplayback.</span></span> <span data-ttu-id="bec6a-120">Para obter mais informações, consulte [PlayReadyPlayRight](media-services-playready-license-template-overview.md#PlayReadyPlayRight).</span><span class="sxs-lookup"><span data-stu-id="bec6a-120">For more information, see [PlayReadyPlayRight](media-services-playready-license-template-overview.md#PlayReadyPlayRight).</span></span>
> 
> 

<span data-ttu-id="bec6a-121">tooconfigure licenças do PlayReady usando serviços de mídia, você deve configurar o modelo de licença do PlayReady dos serviços de mídia hello.</span><span class="sxs-lookup"><span data-stu-id="bec6a-121">tooconfigure PlayReady licenses using Media Services, you must configure hello Media Services PlayReady license template.</span></span> <span data-ttu-id="bec6a-122">Olá modelo está definido no XML.</span><span class="sxs-lookup"><span data-stu-id="bec6a-122">hello template is defined in XML.</span></span>

<span data-ttu-id="bec6a-123">Olá, exemplo a seguir mostra Olá modelo mais simples (e mais comum) que configura uma licença básica de streaming.</span><span class="sxs-lookup"><span data-stu-id="bec6a-123">hello following example shows hello simplest (and most common) template that configures a basic streaming license.</span></span> <span data-ttu-id="bec6a-124">Com essa licença, seus clientes seriam capaz tooplayback o PlayReady o conteúdo protegido.</span><span class="sxs-lookup"><span data-stu-id="bec6a-124">With this license, your clients would be able tooplayback your PlayReady protected content.</span></span>

    <?xml version="1.0" encoding="utf-8"?>
    <PlayReadyLicenseResponseTemplate xmlns:i="http://www.w3.org/2001/XMLSchema-instance" 
                                      xmlns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1">
      <LicenseTemplates>
        <PlayReadyLicenseTemplate>
          <ContentKey i:type="ContentEncryptionKeyFromHeader" />
          <PlayRight />
        </PlayReadyLicenseTemplate>
      </LicenseTemplates>
    </PlayReadyLicenseResponseTemplate>

<span data-ttu-id="bec6a-125">Olá XML segue toohello PlayReady licença esquema XML do modelo definida no modelo de licença do PlayReady Olá seção do esquema XML.</span><span class="sxs-lookup"><span data-stu-id="bec6a-125">hello XML conforms toohello PlayReady license template XML schema defined in hello PlayReady license template XML schema section.</span></span>

<span data-ttu-id="bec6a-126">Serviços de mídia também definem um conjunto de classes .NET que pode ser usado tooserialized e tooand desserializado de saudação XML.</span><span class="sxs-lookup"><span data-stu-id="bec6a-126">Media Services also defines a set of .NET classes that could be used tooserialized and deserialized tooand from hello XML.</span></span> <span data-ttu-id="bec6a-127">Para obter uma descrição das classes principais, confira [Classes do .NET de Serviços de Mídia](media-services-playready-license-template-overview.md#classes).</span><span class="sxs-lookup"><span data-stu-id="bec6a-127">For description of main classes, see [Media Services .NET classes](media-services-playready-license-template-overview.md#classes).</span></span> <span data-ttu-id="bec6a-128">que são usadas tooconfigure modelos de licença.</span><span class="sxs-lookup"><span data-stu-id="bec6a-128">that are used tooconfigure license templates.</span></span>

<span data-ttu-id="bec6a-129">Para um exemplo de ponta a ponta que use o .NET classes de modelo de licença do PlayReady tooconfigure hello, consulte [usando criptografia dinâmica PlayReady e o serviço de entrega de licenças](media-services-protect-with-drm.md).</span><span class="sxs-lookup"><span data-stu-id="bec6a-129">For an end-to-end example that uses .NET classes tooconfigure hello PlayReady license template, see [Using PlayReady Dynamic Encryption and License Delivery Service](media-services-protect-with-drm.md).</span></span>

## <span data-ttu-id="bec6a-130"><a id="classes"></a>Modelos de licença de classes .NET de serviços de mídia usado tooconfigure</span><span class="sxs-lookup"><span data-stu-id="bec6a-130"><a id="classes"></a>Media Services .NET classes that are used tooconfigure license templates</span></span>
<span data-ttu-id="bec6a-131">Olá seguem as principais classes .NET Olá são modelos de licença do PlayReady dos serviços de mídia tooconfigure usado.</span><span class="sxs-lookup"><span data-stu-id="bec6a-131">hello following are hello main .NET classes are used tooconfigure Media Services PlayReady license templates.</span></span> <span data-ttu-id="bec6a-132">Essas classes mapeiam toohello tipos definidos em [esquema XML do modelo de licença do PlayReady](media-services-playready-license-template-overview.md#schema).</span><span class="sxs-lookup"><span data-stu-id="bec6a-132">These classes map toohello types defined in [PlayReady license template XML schema](media-services-playready-license-template-overview.md#schema).</span></span>

<span data-ttu-id="bec6a-133">Olá [MediaServicesLicenseTemplateSerializer](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.mediaserviceslicensetemplateserializer.aspx) classe é usada tooserialize e desserializar tooand do modelo de licença de serviços de mídia Olá XML.</span><span class="sxs-lookup"><span data-stu-id="bec6a-133">hello [MediaServicesLicenseTemplateSerializer](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.mediaserviceslicensetemplateserializer.aspx) class is used tooserialize and deserialize tooand from hello Media Services license template XML.</span></span>

### <a name="playreadylicenseresponsetemplate"></a><span data-ttu-id="bec6a-134">PlayReadyLicenseResponseTemplate</span><span class="sxs-lookup"><span data-stu-id="bec6a-134">PlayReadyLicenseResponseTemplate</span></span>
<span data-ttu-id="bec6a-135">[PlayReadyLicenseResponseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicenseresponsetemplate.aspx) -essa classe representa o modelo de saudação para resposta de saudação enviada toohello back end usuário.</span><span class="sxs-lookup"><span data-stu-id="bec6a-135">[PlayReadyLicenseResponseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicenseresponsetemplate.aspx) - This class represents hello template for hello response sent back toohello end user.</span></span> <span data-ttu-id="bec6a-136">Ele contém um campo para uma cadeia de caracteres de dados personalizados entre o servidor de licença hello e aplicativo hello (pode ser útil para lógica de aplicativo personalizada), bem como uma lista de um ou mais modelos de licença.</span><span class="sxs-lookup"><span data-stu-id="bec6a-136">It contains a field for a custom data string between hello license server and hello application (may be useful for custom app logic) as well as a list of one or more license templates.</span></span>

<span data-ttu-id="bec6a-137">Esta é a classe de "nível superior" de saudação na hierarquia de saudação do modelo.</span><span class="sxs-lookup"><span data-stu-id="bec6a-137">This is hello “top level” class in hello template hierarchy.</span></span> <span data-ttu-id="bec6a-138">Que significa que o modelo de resposta de saudação inclui uma lista de modelos de licença e modelos de licença Olá incluem (direta ou indiretamente) todas Olá outras classes que compõem a saudação modelo dados toobe serializado.</span><span class="sxs-lookup"><span data-stu-id="bec6a-138">Meaning that hello response template includes a list of license templates and hello license templates include (directly or indirectly) all of hello other classes that make up hello template data toobe serialized.</span></span>

### <a name="playreadylicensetemplate"></a><span data-ttu-id="bec6a-139">PlayReadyLicenseTemplate</span><span class="sxs-lookup"><span data-stu-id="bec6a-139">PlayReadyLicenseTemplate</span></span>
<span data-ttu-id="bec6a-140">[PlayReadyLicenseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicensetemplate.aspx) -classe Olá representa um modelo de licença para a criação de toobe de licenças do PlayReady retornada aos usuários finais de toohello.</span><span class="sxs-lookup"><span data-stu-id="bec6a-140">[PlayReadyLicenseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicensetemplate.aspx) - hello class represents a license template for creating PlayReady licenses toobe returned toohello end users.</span></span> <span data-ttu-id="bec6a-141">Ela contém dados Olá na chave de conteúdo Olá na licença de saudação e qualquer toobe direitos ou restrições impostas por hello em tempo de execução do DRM do PlayReady ao usar a chave de conteúdo de saudação.</span><span class="sxs-lookup"><span data-stu-id="bec6a-141">It contains hello data on hello content key in hello license and any rights or restrictions toobe enforced by hello PlayReady DRM runtime when using hello content key.</span></span>

### <span data-ttu-id="bec6a-142"><a id="PlayReadyPlayRight"></a>PlayReadyPlayRight</span><span class="sxs-lookup"><span data-stu-id="bec6a-142"><a id="PlayReadyPlayRight"></a>PlayReadyPlayRight</span></span>
<span data-ttu-id="bec6a-143">[PlayReadyPlayRight](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadyplayright.aspx) -essa classe representa Olá PlayRight de uma licença do PlayReady.</span><span class="sxs-lookup"><span data-stu-id="bec6a-143">[PlayReadyPlayRight](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadyplayright.aspx) - This class represents hello PlayRight of a PlayReady license.</span></span> <span data-ttu-id="bec6a-144">Ele concede Olá usuário Olá capacidade tooplayback Olá assunto conteúdo toohello zero ou mais restrições configuradas na licença de saudação e em Olá próprio PlayRight (para política específica de reprodução).</span><span class="sxs-lookup"><span data-stu-id="bec6a-144">It grants hello user hello ability tooplayback hello content subject toohello zero or more restrictions configured in hello license and on hello PlayRight itself (for playback specific policy).</span></span> <span data-ttu-id="bec6a-145">Grande parte da diretiva de Olá Olá PlayRight tem toodo com restrições de saída que controlam os tipos de saudação de saídas Olá conteúdo pode ser executado em e quaisquer restrições que devem ser colocadas em vigor durante o uso de uma determinada saída.</span><span class="sxs-lookup"><span data-stu-id="bec6a-145">Much of hello policy on hello PlayRight has toodo with output restrictions which control hello types of outputs that hello content can be played over and any restrictions that must be put in place when using a given output.</span></span> <span data-ttu-id="bec6a-146">Por exemplo, se, em seguida, Olá Olá DigitalVideoOnlyContentRestriction for habilitada, o tempo de execução do DRM só permitirá Olá toobe vídeo exibido em saídas digitais (saídas de vídeo analógico não serão permitidas conteúdo de saudação toopass).</span><span class="sxs-lookup"><span data-stu-id="bec6a-146">For example, if hello DigitalVideoOnlyContentRestriction is enabled, then hello DRM runtime will only allow hello video toobe displayed over digital outputs (analog video outputs won’t be allowed toopass hello content).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bec6a-147">Esses tipos de restrições podem ser muito poderosos mas também podem afetar a experiência do consumidor hello.</span><span class="sxs-lookup"><span data-stu-id="bec6a-147">These types of restrictions can be very powerful but can also affect hello consumer experience.</span></span> <span data-ttu-id="bec6a-148">Se Olá proteções de saída forem configuradas muito restritiva, conteúdo Olá pode ser reproduzido em alguns clientes.</span><span class="sxs-lookup"><span data-stu-id="bec6a-148">If hello output protections are configured too restrictive, hello content might be unplayable on some clients.</span></span> <span data-ttu-id="bec6a-149">Para obter mais informações, consulte Olá [as regras de conformidade do PlayReady](https://www.microsoft.com/playready/licensing/compliance/) documento.</span><span class="sxs-lookup"><span data-stu-id="bec6a-149">For more information, see hello [PlayReady Compliance Rules](https://www.microsoft.com/playready/licensing/compliance/) document.</span></span>
> 
> 

<span data-ttu-id="bec6a-150">Para obter um exemplo de quais níveis de proteção o Silverlight dá suporte, consulte: [Suporte do Silverlight para proteções de saída](http://go.microsoft.com/fwlink/?LinkId=617318).</span><span class="sxs-lookup"><span data-stu-id="bec6a-150">For an example of what protection levels Silverlight supports, see: [Silverlight support for output protections](http://go.microsoft.com/fwlink/?LinkId=617318).</span></span>

## <span data-ttu-id="bec6a-151"><a id="schema"></a>Esquema XML do modelo de licença do PlayReady</span><span class="sxs-lookup"><span data-stu-id="bec6a-151"><a id="schema"></a>PlayReady license template XML schema</span></span>
    <?xml version="1.0" encoding="utf-8"?>
    <xs:schema xmlns:tns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1" xmlns:ser="http://schemas.microsoft.com/2003/10/Serialization/" elementFormDefault="qualified" targetNamespace="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1" xmlns:xs="http://www.w3.org/2001/XMLSchema">
      <xs:import namespace="http://schemas.microsoft.com/2003/10/Serialization/" />
      <xs:complexType name="AgcAndColorStripeRestriction">
        <xs:sequence>
          <xs:element minOccurs="0" name="ConfigurationData" type="xs:unsignedByte" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="AgcAndColorStripeRestriction" nillable="true" type="tns:AgcAndColorStripeRestriction" />
      <xs:simpleType name="ContentType">
        <xs:restriction base="xs:string">
          <xs:enumeration value="Unspecified" />
          <xs:enumeration value="UltravioletDownload" />
          <xs:enumeration value="UltravioletStreaming" />
        </xs:restriction>
      </xs:simpleType>
      <xs:element name="ContentType" nillable="true" type="tns:ContentType" />
      <xs:complexType name="ExplicitAnalogTelevisionRestriction">
        <xs:sequence>
          <xs:element minOccurs="0" name="BestEffort" type="xs:boolean" />
          <xs:element minOccurs="0" name="ConfigurationData" type="xs:unsignedByte" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ExplicitAnalogTelevisionRestriction" nillable="true" type="tns:ExplicitAnalogTelevisionRestriction" />
      <xs:complexType name="PlayReadyContentKey">
        <xs:sequence />
      </xs:complexType>
      <xs:element name="PlayReadyContentKey" nillable="true" type="tns:PlayReadyContentKey" />
      <xs:complexType name="ContentEncryptionKeyFromHeader">
        <xs:complexContent mixed="false">
          <xs:extension base="tns:PlayReadyContentKey">
            <xs:sequence />
          </xs:extension>
        </xs:complexContent>
      </xs:complexType>
      <xs:element name="ContentEncryptionKeyFromHeader" nillable="true" type="tns:ContentEncryptionKeyFromHeader" />
      <xs:complexType name="ContentEncryptionKeyFromKeyIdentifier">
        <xs:complexContent mixed="false">
          <xs:extension base="tns:PlayReadyContentKey">
            <xs:sequence>
              <xs:element minOccurs="0" name="KeyIdentifier" type="ser:guid" />
            </xs:sequence>
          </xs:extension>
        </xs:complexContent>
      </xs:complexType>
      <xs:element name="ContentEncryptionKeyFromKeyIdentifier" nillable="true" type="tns:ContentEncryptionKeyFromKeyIdentifier" />
      <xs:complexType name="PlayReadyLicenseResponseTemplate">
        <xs:sequence>
          <xs:element name="LicenseTemplates" nillable="true" type="tns:ArrayOfPlayReadyLicenseTemplate" />
          <xs:element minOccurs="0" name="ResponseCustomData" nillable="true" type="xs:string">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
        </xs:sequence>
      </xs:complexType>
      <xs:element name="PlayReadyLicenseResponseTemplate" nillable="true" type="tns:PlayReadyLicenseResponseTemplate" />
      <xs:complexType name="ArrayOfPlayReadyLicenseTemplate">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="unbounded" name="PlayReadyLicenseTemplate" nillable="true" type="tns:PlayReadyLicenseTemplate" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ArrayOfPlayReadyLicenseTemplate" nillable="true" type="tns:ArrayOfPlayReadyLicenseTemplate" />
      <xs:complexType name="PlayReadyLicenseTemplate">
        <xs:sequence>
          <xs:element minOccurs="0" name="AllowTestDevices" type="xs:boolean" />
          <xs:element minOccurs="0" name="BeginDate" nillable="true" type="xs:dateTime">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element name="ContentKey" nillable="true" type="tns:PlayReadyContentKey" />
          <xs:element minOccurs="0" name="ContentType" type="tns:ContentType">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ExpirationDate" nillable="true" type="xs:dateTime">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="GracePeriod" nillable="true" type="ser:duration">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="LicenseType" type="tns:PlayReadyLicenseType" />
          <xs:element minOccurs="0" name="PlayRight" nillable="true" type="tns:PlayReadyPlayRight" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="PlayReadyLicenseTemplate" nillable="true" type="tns:PlayReadyLicenseTemplate" />
      <xs:simpleType name="PlayReadyLicenseType">
        <xs:restriction base="xs:string">
          <xs:enumeration value="Nonpersistent" />
          <xs:enumeration value="Persistent" />
        </xs:restriction>
      </xs:simpleType>
      <xs:element name="PlayReadyLicenseType" nillable="true" type="tns:PlayReadyLicenseType" />
      <xs:complexType name="PlayReadyPlayRight">
        <xs:sequence>
          <xs:element minOccurs="0" name="AgcAndColorStripeRestriction" nillable="true" type="tns:AgcAndColorStripeRestriction">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="AllowPassingVideoContentToUnknownOutput" type="tns:UnknownOutputPassingOption">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="AnalogVideoOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="CompressedDigitalAudioOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="CompressedDigitalVideoOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="DigitalVideoOnlyContentRestriction" type="xs:boolean">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ExplicitAnalogTelevisionOutputRestriction" nillable="true" type="tns:ExplicitAnalogTelevisionRestriction">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="FirstPlayExpiration" nillable="true" type="ser:duration">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ImageConstraintForAnalogComponentVideoRestriction" type="xs:boolean">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ImageConstraintForAnalogComputerMonitorRestriction" type="xs:boolean">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ScmsRestriction" nillable="true" type="tns:ScmsRestriction">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="UncompressedDigitalAudioOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="UncompressedDigitalVideoOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
        </xs:sequence>
      </xs:complexType>
      <xs:element name="PlayReadyPlayRight" nillable="true" type="tns:PlayReadyPlayRight" />
      <xs:simpleType name="UnknownOutputPassingOption">
        <xs:restriction base="xs:string">
          <xs:enumeration value="NotAllowed" />
          <xs:enumeration value="Allowed" />
          <xs:enumeration value="AllowedWithVideoConstriction" />
        </xs:restriction>
      </xs:simpleType>
      <xs:element name="UnknownOutputPassingOption" nillable="true" type="tns:UnknownOutputPassingOption" />
      <xs:complexType name="ScmsRestriction">
        <xs:sequence>
          <xs:element minOccurs="0" name="ConfigurationData" type="xs:unsignedByte" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ScmsRestriction" nillable="true" type="tns:ScmsRestriction" />
    </xs:schema>



## <a name="media-services-learning-paths"></a><span data-ttu-id="bec6a-152">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="bec6a-152">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="bec6a-153">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="bec6a-153">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

