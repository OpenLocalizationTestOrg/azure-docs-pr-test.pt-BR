## <a name="what-are-service-bus-queues"></a>O que são as filas do Barramento de Serviço?
Filas do Barramento de Serviço dão suporte a um modelo de comunicação de **sistema de mensagens agenciado** . Ao usar filas, os componentes de um aplicativo distribuído não se comunicam diretamente uns com os outros, mas trocam mensagens por meio de uma fila, que atua como um intermediário (agente). Um produtor de mensagens (remetente) transmite uma fila de mensagens toohello e, em seguida, continua o processamento. De forma assíncrona, um consumidor de mensagens (destinatário) recebe a mensagem de saudação da fila de saudação e processa-o. produtor Olá não tem toowait por uma resposta do consumidor de saudação em ordem toocontinue tooprocess e enviar mais mensagens. As filas oferecem **primeiro a entrar, PEPS (primeiro)** tooone de entrega ou mais consumidores concorrentes da mensagem. Ou seja, as mensagens são normalmente recebidas e processadas por receptores Olá no hello ordem em que eles foram adicionados toohello fila, e cada mensagem é recebida e processada por apenas um cliente de mensagem.

![Conceitos de fila](./media/howto-service-bus-queues/sb-queues-08.png)

Filas do Barramento de Serviço são uma tecnologia de uso geral que pode ser usada para uma grande variedade de cenários:

* Comunicação entre as funções Web e de trabalho em um aplicativo multicamada do Azure.
* Comunicação entre aplicativos locais e aplicativos hospedados pelo Azure em uma solução híbrida.
* Comunicação entre os componentes de um aplicativo distribuído executado localmente em diferentes organizações ou departamentos de uma organização.

Usando filas permite que você tooscale seus aplicativos mais fácil e habilitar a arquitetura de tooyour mais resiliência.


