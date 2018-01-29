## <a name="how-apim-proxy-server-responds-with-ssl-certificates-in-the-tls-handshake"></a>Como o Servidor Proxy APIM responde com certificados SSL no handshake de TLS

### <a name="clients-calling-with-sni-header"></a>Clientes chamando com o cabeçalho de SNI
Se o cliente tiver um ou vários domínios personalizados configurados para Proxy, o APIM pode responder a solicitações HTTPS dos domínios personalizados (por exemplo, contoso.com), bem como o domínio padrão (por exemplo, apim-service-name.azure-api.net). Com base nas informações do cabeçalho de Indicação de Nome de Servidor (SNI), o APIM responde com um certificado do servidor apropriado.

### <a name="clients-calling-without-sni-header"></a>Clientes chamando sem cabeçalho de SNI
Se o cliente está usando um cliente, que não envia o cabeçalho de [SNI](https://tools.ietf.org/html/rfc6066#section-3), o APIM cria respostas com base na seguinte lógica:

* Se o serviço tem apenas um domínio personalizado configurado para o Proxy, o Certificado Padrão é o certificado que foi emitido para o domínio personalizado do Proxy.
* Se o serviço tiver configurado vários domínios personalizados para o Proxy (com suporte apenas na camada **Premium**), o cliente pode designar qual certificado deve ser o certificado padrão. Para definir o certificado padrão, a propriedade [defaultSslBinding](https://docs.microsoft.com/rest/api/apimanagement/apimanagementservice/createorupdate#hostnameconfiguration) deve ser definida como true (“defaultSslBinding”: “true”). Se o cliente não definir a propriedade, o certificado padrão é o certificado emitido para o domínio de Proxy padrão hospedado em *.azure-api.net.

## <a name="support-for-putpost-request-with-large-payload"></a>Suporte para a solicitação PUT/POST com grande payload

O servidor Proxy do APIM dá suporte à solicitação com grande payload ao usar certificados de cliente em HTTPS (por exemplo, a carga > 40 KB). Para impedir que a solicitação do servidor congele, os clientes podem definir a propriedade ["negotiateClientCertificate": "true"](https://docs.microsoft.com/rest/api/apimanagement/ApiManagementService/CreateOrUpdate#hostnameconfiguration) no nome do host do Proxy. Se a propriedade for definida como true, o certificado do cliente é solicitado ao tempo de conexão SSL/TLS, antes de qualquer troca de solicitação HTTP. Uma vez que a configuração se aplica ao nível do **Nome do host do Proxy**, todas as solicitações de conexão solicitam o certificado do cliente. Os clientes podem configurar até 20 domínios personalizados para o Proxy (com suporte apenas na camada **Premium**) e trabalhar com essa limitação.

