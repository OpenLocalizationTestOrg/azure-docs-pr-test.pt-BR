---
title: "Visão geral do modelo de licença do PlayReady dos Serviços de Mídia"
description: "Este tópico fornece uma visão geral de um modelo de licença do PlayReady usado para configurar as licenças do PlayReady."
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
ms.openlocfilehash: be19f616e36916655390cd05e738e93c08dcdf68
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="media-services-playready-license-template-overview"></a><span data-ttu-id="00b6f-103">Visão geral do modelo de licença do PlayReady dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="00b6f-103">Media Services PlayReady license template overview</span></span>
<span data-ttu-id="00b6f-104">Os Serviços de Mídia do Azure fornecem um serviço de distribuição de licenças do Microsoft PlayReady.</span><span class="sxs-lookup"><span data-stu-id="00b6f-104">Azure Media Services now provides a service for delivering Microsoft PlayReady licenses.</span></span> <span data-ttu-id="00b6f-105">Quando o player de usuário final (por exemplo, Silverlight) tenta reproduzir o conteúdo protegido por PlayReady, uma solicitação é enviada para o serviço de entrega de licença para obtenção de uma.</span><span class="sxs-lookup"><span data-stu-id="00b6f-105">When the end user player (for example, Silverlight) tries to play your PlayReady protected content, a request is sent to the license delivery service to obtain a license.</span></span> <span data-ttu-id="00b6f-106">Se o serviço de licença aprova a solicitação, ele emite a licença que é enviada ao cliente e pode ser usada para descriptografar e reproduzir o conteúdo especificado.</span><span class="sxs-lookup"><span data-stu-id="00b6f-106">If the license service approves the request, it issues the license which is sent to the client and can be used to decrypt and play the specified content.</span></span>

<span data-ttu-id="00b6f-107">Os Serviços de Mídia também fornecem APIs que permitem que você configure suas licenças do PlayReady.</span><span class="sxs-lookup"><span data-stu-id="00b6f-107">Media Services also provides APIs that let you configure your PlayReady licenses.</span></span> <span data-ttu-id="00b6f-108">As licenças contêm os direitos e restrições que você deseja que o tempo de execução do PlayReady DRM imponha quando um usuário está tentando reproduzir conteúdo protegido.</span><span class="sxs-lookup"><span data-stu-id="00b6f-108">Licenses contain the rights and restrictions that you want for the PlayReady DRM runtime to enforce when a user is trying to playback protected content.</span></span>
<span data-ttu-id="00b6f-109">Abaixo estão alguns exemplos de restrições de licença PlayReady que você pode especificar:</span><span class="sxs-lookup"><span data-stu-id="00b6f-109">Below are some examples of PlayReady license restrictions that you can specify:</span></span>

* <span data-ttu-id="00b6f-110">A data e horário em que a licença é válida.</span><span class="sxs-lookup"><span data-stu-id="00b6f-110">The DateTime from which the license is valid.</span></span>
* <span data-ttu-id="00b6f-111">O valor de data e hora em que a licença expira.</span><span class="sxs-lookup"><span data-stu-id="00b6f-111">The DateTime value when the license expires.</span></span> 
* <span data-ttu-id="00b6f-112">Para a licença a ser salva no armazenamento persistente no cliente.</span><span class="sxs-lookup"><span data-stu-id="00b6f-112">For the license to be saved in persistent storage on the client.</span></span> <span data-ttu-id="00b6f-113">Licenças persistentes normalmente são usadas para permitir a reprodução off-line do conteúdo.</span><span class="sxs-lookup"><span data-stu-id="00b6f-113">Persistent licenses are typically used to allow offline playback of the content.</span></span>
* <span data-ttu-id="00b6f-114">O nível mínimo de segurança que um player deve ter para reproduzir o conteúdo.</span><span class="sxs-lookup"><span data-stu-id="00b6f-114">The minimum security level that a player must have to play your content.</span></span> 
* <span data-ttu-id="00b6f-115">O nível de proteção de saída para os controles de saída para conteúdo áudio\video.</span><span class="sxs-lookup"><span data-stu-id="00b6f-115">The output protection level for the output controls for audio\video content.</span></span> 
* <span data-ttu-id="00b6f-116">Para obter mais informações, consulte a seção Controles de Saída (3.5) no documento [Regras de conformidade do PlayReady](https://www.microsoft.com/playready/licensing/compliance/) .</span><span class="sxs-lookup"><span data-stu-id="00b6f-116">For more information, see the Output Controls section (3.5) in the [PlayReady Compliance Rules](https://www.microsoft.com/playready/licensing/compliance/) document.</span></span>

> [!NOTE]
> <span data-ttu-id="00b6f-117">Atualmente, só é possível configurar o PlayRight da licença do PlayReady (esse direito é necessário).</span><span class="sxs-lookup"><span data-stu-id="00b6f-117">Currently, you can only configure the PlayRight of the PlayReady license (this right is required).</span></span> <span data-ttu-id="00b6f-118">O PlayRight permite que o cliente para reproduza o conteúdo.</span><span class="sxs-lookup"><span data-stu-id="00b6f-118">The PlayRight gives the client the ability to playback the content.</span></span> <span data-ttu-id="00b6f-119">O PlayRight também permite configurar restrições específicas para reprodução.</span><span class="sxs-lookup"><span data-stu-id="00b6f-119">The PlayRight also allows configuring restrictions specific to playback.</span></span> <span data-ttu-id="00b6f-120">Para obter mais informações, consulte [PlayReadyPlayRight](media-services-playready-license-template-overview.md#PlayReadyPlayRight).</span><span class="sxs-lookup"><span data-stu-id="00b6f-120">For more information, see [PlayReadyPlayRight](media-services-playready-license-template-overview.md#PlayReadyPlayRight).</span></span>
> 
> 

<span data-ttu-id="00b6f-121">Para configurar as licenças do PlayReady usando os serviços de mídia, você deve configurar o modelo de licença do PlayReady de serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="00b6f-121">To configure PlayReady licenses using Media Services, you must configure the Media Services PlayReady license template.</span></span> <span data-ttu-id="00b6f-122">O modelo é definido em XML.</span><span class="sxs-lookup"><span data-stu-id="00b6f-122">The template is defined in XML.</span></span>

<span data-ttu-id="00b6f-123">O exemplo a seguir mostra o modelo mais simples (e mais comum) que configura uma licença básica de transmissão.</span><span class="sxs-lookup"><span data-stu-id="00b6f-123">The following example shows the simplest (and most common) template that configures a basic streaming license.</span></span> <span data-ttu-id="00b6f-124">Com esta licença, os clientes poderão reproduzir o conteúdo protegido do seu PlayReady.</span><span class="sxs-lookup"><span data-stu-id="00b6f-124">With this license, your clients would be able to playback your PlayReady protected content.</span></span>

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

<span data-ttu-id="00b6f-125">O XML está de acordo com o esquema XML do modelo da licença de PlayReady definido no modelo de licença PlayReady seção do esquema XML.</span><span class="sxs-lookup"><span data-stu-id="00b6f-125">The XML conforms to the PlayReady license template XML schema defined in the PlayReady license template XML schema section.</span></span>

<span data-ttu-id="00b6f-126">Serviços de mídia também define um conjunto de classes .NET que podem ser usado para serializar para o XML e desserializar do XML.</span><span class="sxs-lookup"><span data-stu-id="00b6f-126">Media Services also defines a set of .NET classes that could be used to serialized and deserialized to and from the XML.</span></span> <span data-ttu-id="00b6f-127">Para obter uma descrição das classes principais, confira [Classes do .NET de Serviços de Mídia](media-services-playready-license-template-overview.md#classes).</span><span class="sxs-lookup"><span data-stu-id="00b6f-127">For description of main classes, see [Media Services .NET classes](media-services-playready-license-template-overview.md#classes).</span></span> <span data-ttu-id="00b6f-128">que são usadas para configurar modelos de licença.</span><span class="sxs-lookup"><span data-stu-id="00b6f-128">that are used to configure license templates.</span></span>

<span data-ttu-id="00b6f-129">Para obter um exemplo de ponta a ponta que usa classes do .NET para configurar o modelo de licença do PlayReady, consulte [Usando o serviço de entrega de licença e criptografia dinâmica PlayReady](media-services-protect-with-drm.md).</span><span class="sxs-lookup"><span data-stu-id="00b6f-129">For an end-to-end example that uses .NET classes to configure the PlayReady license template, see [Using PlayReady Dynamic Encryption and License Delivery Service](media-services-protect-with-drm.md).</span></span>

## <span data-ttu-id="00b6f-130"><a id="classes"></a>Classes do .NET de serviços de mídia que são usadas para configurar modelos de licença</span><span class="sxs-lookup"><span data-stu-id="00b6f-130"><a id="classes"></a>Media Services .NET classes that are used to configure license templates</span></span>
<span data-ttu-id="00b6f-131">A seguir estão que as principais classes do .NET são usadas para configurar modelos de licença do PlayReady de serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="00b6f-131">The following are the main .NET classes are used to configure Media Services PlayReady license templates.</span></span> <span data-ttu-id="00b6f-132">Essas classes são mapeadas para os tipos definidos em [Esquema XML de modelo de licença do PlayReady](media-services-playready-license-template-overview.md#schema).</span><span class="sxs-lookup"><span data-stu-id="00b6f-132">These classes map to the types defined in [PlayReady license template XML schema](media-services-playready-license-template-overview.md#schema).</span></span>

<span data-ttu-id="00b6f-133">A classe [MediaServicesLicenseTemplateSerializer](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.mediaserviceslicensetemplateserializer.aspx) é usada para serializar e desserializar de e para o XML do modelo de licença dos serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="00b6f-133">The [MediaServicesLicenseTemplateSerializer](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.mediaserviceslicensetemplateserializer.aspx) class is used to serialize and deserialize to and from the Media Services license template XML.</span></span>

### <a name="playreadylicenseresponsetemplate"></a><span data-ttu-id="00b6f-134">PlayReadyLicenseResponseTemplate</span><span class="sxs-lookup"><span data-stu-id="00b6f-134">PlayReadyLicenseResponseTemplate</span></span>
<span data-ttu-id="00b6f-135">[PlayReadyLicenseResponseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicenseresponsetemplate.aspx) -essa classe representa o modelo para a resposta enviada de volta para o usuário final.</span><span class="sxs-lookup"><span data-stu-id="00b6f-135">[PlayReadyLicenseResponseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicenseresponsetemplate.aspx) - This class represents the template for the response sent back to the end user.</span></span> <span data-ttu-id="00b6f-136">Ela contém um campo para uma cadeia de caracteres de dados personalizados entre o servidor de licença e o aplicativo (pode ser útil para a lógica de aplicativo personalizado), bem como uma lista de um ou mais modelos de licença.</span><span class="sxs-lookup"><span data-stu-id="00b6f-136">It contains a field for a custom data string between the license server and the application (may be useful for custom app logic) as well as a list of one or more license templates.</span></span>

<span data-ttu-id="00b6f-137">Esta é a classe de "nível superior" na hierarquia de modelo.</span><span class="sxs-lookup"><span data-stu-id="00b6f-137">This is the “top level” class in the template hierarchy.</span></span> <span data-ttu-id="00b6f-138">O que significa que o modelo de resposta inclui uma lista de modelos de licença e os modelos de licença incluem (direta ou indiretamente) todas as outras classes que compõem os dados do modelo a seresem serializado.</span><span class="sxs-lookup"><span data-stu-id="00b6f-138">Meaning that the response template includes a list of license templates and the license templates include (directly or indirectly) all of the other classes that make up the template data to be serialized.</span></span>

### <a name="playreadylicensetemplate"></a><span data-ttu-id="00b6f-139">PlayReadyLicenseTemplate</span><span class="sxs-lookup"><span data-stu-id="00b6f-139">PlayReadyLicenseTemplate</span></span>
<span data-ttu-id="00b6f-140">[PlayReadyLicenseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicensetemplate.aspx) -a classe representa um modelo de licença para criar licenças PlayReady a ser retornado para os usuários finais.</span><span class="sxs-lookup"><span data-stu-id="00b6f-140">[PlayReadyLicenseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicensetemplate.aspx) - The class represents a license template for creating PlayReady licenses to be returned to the end users.</span></span> <span data-ttu-id="00b6f-141">Ela contém os dados na chave de conteúdo na licença e todos os direitos ou restrições a serem aplicados no tempo de execução pelo PlayReady DRM ao usar a chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="00b6f-141">It contains the data on the content key in the license and any rights or restrictions to be enforced by the PlayReady DRM runtime when using the content key.</span></span>

### <span data-ttu-id="00b6f-142"><a id="PlayReadyPlayRight"></a>PlayReadyPlayRight</span><span class="sxs-lookup"><span data-stu-id="00b6f-142"><a id="PlayReadyPlayRight"></a>PlayReadyPlayRight</span></span>
<span data-ttu-id="00b6f-143">[PlayReadyPlayRight](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadyplayright.aspx) -essa classe representa o PlayRight de uma licença do PlayReady.</span><span class="sxs-lookup"><span data-stu-id="00b6f-143">[PlayReadyPlayRight](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadyplayright.aspx) - This class represents the PlayRight of a PlayReady license.</span></span> <span data-ttu-id="00b6f-144">Ele concede ao usuário a capacidade de reproduzir o conteúdo de acordo com as restrições de zero ou mais restrições configuradas na licença e no próprio PlayRight (de política específica de reprodução).</span><span class="sxs-lookup"><span data-stu-id="00b6f-144">It grants the user the ability to playback the content subject to the zero or more restrictions configured in the license and on the PlayRight itself (for playback specific policy).</span></span> <span data-ttu-id="00b6f-145">Grande parte da política no PlayRight tem a ver com restrições de saída que controlam os tipos de saída nas quais o conteúdo pode ser reproduzido e todas as restrições que devem ser colocadas em vigor durante o uso de uma determinada saída.</span><span class="sxs-lookup"><span data-stu-id="00b6f-145">Much of the policy on the PlayRight has to do with output restrictions which control the types of outputs that the content can be played over and any restrictions that must be put in place when using a given output.</span></span> <span data-ttu-id="00b6f-146">Por exemplo, se a DigitalVideoOnlyContentRestriction estiver habilitada, o tempo de execução de DRM só permitirá que o vídeo seja exibido em saídas digitais (saídas de vídeo analógicas não poderão passar o conteúdo).</span><span class="sxs-lookup"><span data-stu-id="00b6f-146">For example, if the DigitalVideoOnlyContentRestriction is enabled, then the DRM runtime will only allow the video to be displayed over digital outputs (analog video outputs won’t be allowed to pass the content).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="00b6f-147">Esses tipos de restrições podem ser muito poderosos, mas também podem afetar a experiência do usuário.</span><span class="sxs-lookup"><span data-stu-id="00b6f-147">These types of restrictions can be very powerful but can also affect the consumer experience.</span></span> <span data-ttu-id="00b6f-148">Se as proteções de saída são configuradas de maneira muito restritiva, o conteúdo pode ser impagável no caso de alguns clientes.</span><span class="sxs-lookup"><span data-stu-id="00b6f-148">If the output protections are configured too restrictive, the content might be unplayable on some clients.</span></span> <span data-ttu-id="00b6f-149">Para obter mais informações, consulte o documento [Regras de conformidade do PlayReady](https://www.microsoft.com/playready/licensing/compliance/) .</span><span class="sxs-lookup"><span data-stu-id="00b6f-149">For more information, see the [PlayReady Compliance Rules](https://www.microsoft.com/playready/licensing/compliance/) document.</span></span>
> 
> 

<span data-ttu-id="00b6f-150">Para obter um exemplo de quais níveis de proteção o Silverlight dá suporte, consulte: [Suporte do Silverlight para proteções de saída](http://go.microsoft.com/fwlink/?LinkId=617318).</span><span class="sxs-lookup"><span data-stu-id="00b6f-150">For an example of what protection levels Silverlight supports, see: [Silverlight support for output protections](http://go.microsoft.com/fwlink/?LinkId=617318).</span></span>

## <span data-ttu-id="00b6f-151"><a id="schema"></a>Esquema XML do modelo de licença do PlayReady</span><span class="sxs-lookup"><span data-stu-id="00b6f-151"><a id="schema"></a>PlayReady license template XML schema</span></span>
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



## <a name="media-services-learning-paths"></a><span data-ttu-id="00b6f-152">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="00b6f-152">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="00b6f-153">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="00b6f-153">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

