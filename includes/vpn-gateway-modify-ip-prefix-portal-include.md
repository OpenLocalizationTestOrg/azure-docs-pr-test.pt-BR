### <a name="noconnection"></a>prefixos de endereço IP da gateway de rede local toomodify - nenhuma conexão de gateway

#### <a name="tooadd-additional-address-prefixes"></a>prefixos de endereço adicional tooadd:

1. Em Olá recursos de Gateway de rede Local, em Olá **configurações** seção, clique em **configuração**.
2. Adicionar espaço de endereço IP de saudação em Olá *adicionar intervalo de endereços adicional* caixa.
3. Clique em **salvar** toosave suas configurações.

#### <a name="tooremove-address-prefixes"></a>prefixos de endereço tooremove:

1. Em Olá recursos de Gateway de rede Local, em Olá **configurações** seção, clique em **configuração**.
2. Clique em Olá **'…'** na linha de saudação que contém o prefixo Olá deseja tooremove.
3. Clique em **Remover**.
4. Clique em **salvar** toosave suas configurações.

### <a name="withconnection"></a>toomodify local de rede gateway prefixos de endereço IP - existente de conexão de gateway

Se você tiver uma conexão de gateway e deseja tooadd ou remove os prefixos de endereço IP de saudação contidos no seu gateway de rede local, você precisa Olá toodo etapas, na ordem a seguir. Isso resulta em algum tempo de inatividade para a conexão VPN. Ao modificar prefixos de endereço IP, gateway VPN Olá toodelete não é necessário. Você só precisa de conexão de saudação tooremove.

#### <a name="1-remove-hello-connection"></a>1. Remova conexão hello.

1. Em Olá recursos de Gateway de rede Local, em Olá **configurações** seção, clique em **conexões**.
2. Clique em Olá **...**  na linha de saudação para cada conexão, em seguida, clique em **excluir**.
3. Clique em **salvar** toosave suas configurações.

#### <a name="2-modify-hello-address-prefixes"></a>2. Modifique os prefixos de endereço hello.

prefixos de endereço adicional tooadd:

1. Em Olá recursos de Gateway de rede Local, em Olá **configurações** seção, clique em **configuração**.
2. Adicione espaço de endereço IP hello.
3. Clique em **salvar** toosave suas configurações.

prefixos de endereço tooremove:

1. Em Olá recursos de Gateway de rede Local, em Olá **configurações** seção, clique em **configuração**.
2. Clique em Olá **...**  na linha de saudação que contém o prefixo Olá deseja tooremove.
3. Clique em **Remover**.
4. Clique em **salvar** toosave suas configurações.

#### <a name="3-recreate-hello-connection"></a>3. Recrie a conexão de saudação.

1. Navegue toohello Gateway de rede Virtual para sua rede virtual. (Não hello Gateway de rede Local.)
2. Em Olá Gateway de rede Virtual, no hello **configurações** seção, clique em **conexões**.
3. Clique em Olá **+ adicionar** tooopen Olá **Adicionar conexão** folha.
4. Recrie sua conexão.
5. Clique em **Okey** toocreate conexão de saudação.
