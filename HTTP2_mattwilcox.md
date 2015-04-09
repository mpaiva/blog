#HTTP2 para desenvolvedores de web.

HTTP2 vai significar uma mudança na forma como devemos construir websites. As boas práticas de HTTP1 são prejudiciais no mundo do HTTP2.

> *HTTP1 é lento e ineficiente para a maioria dos casos de uso de hoje na web.*

HTTP1.x é a versão do HTTP que nós já conhecemos quando entramos o endereço de um web site. É um protocolo antigo que foi concebido antes mesmo de sabermos o que essa imensa rede mundial de computadores se tornaria. Apesar desse protocolo continuar funcionando como esperado, simplesmente não é tão eficiente como no início, porque ultimamente estamos exigindo algo muito mais complexo do que este protocolo foi projetado originalmente.

Para que os sites carreguem em tempo aceitável usando HTTP1, desenvolvemos uma série de técnicas; hacks na verdade; para conseguirmos extrair um bom desempenho deste protocolo antigo. São eles:

* Usando CSS Sprites: Combine várias imagens em uma só imagem e utilizando CSS para mostrar apenas uma parte dessa imagem num devido lugar da página.
* Concatenando o Código: Tornando vários arquivos de CSS ou JS e consolidá-los em um único arquivo maior.
* Servindo arquivos de um domínio sem o uso de cookies.
* Usando Partições de Shard: Criando registros de Alias no DNS de diferentes domínios ou sub-domínios para hospedagem dos arquivos de imagens.

As duas primeiras técnicas visam evitar várias solicitações HTTP. Em HTTP1 um pedido é uma coisa muito cara e leva muito tempo, cada pedido pode ser baixados com os cookies que devem ser enviados como parte do pedido, e nada disso é compactado. É mais rápido agrupar um monte de coisas e fazer tudo de uma só vez no lado do cliente do que continuar enviando pedidos para o servidor cada momento que o código precisa de um arquivo.

A terceira técnica é usada para minimizar o tempo necessário para obter os arquivos; cookies, se estiver definido, deve ser enviado para o domínio solicitado junto com cada pedido - que acrescenta-se a um monte de espaço 'desperdiçado' na linha. Se os seus arquivos estão em um domínio diferente (exemplo: imagens.meusite.com) que não usa cookies, então o pedido desses arquivos não precisará enviar cookies com eles, o que será um pouco mais rápido.

A última técnica, sharding, é porque os navegadores costumavam permitir apenas duas solicitações HTTP simultâneas fossem feitas por domínio. Se você criar um novo domínio para alguns de seus arquivos, então você dobra a quantidade de conexões simultâneas o navegador irá permitir a fim de obter seus arquivos. Assim, você pode baixar o conteúdo do site mais rapidamente. Na realidade, sharding não tem sido muito útil nos últimos anos, pois os fabricantes de navegadores decidiram eliminar essa restrição das duas conexões 'era tonto, e eles ignoraram.

## HTTP2

> *Não use as boas práticas do HTTP1 como base para um site que está sendo hospedado em HTTP2.*

O protocolo HTTP2 está quase aqui, ele é baseado no SPDY®, e isso torna tudo muito mais eficiente. Significa também que todas as técnicas de desempenho HTTP1 são prejudiciais. Eles irão fazer um site HTTP2 mais lento, e não mais rápido. Portanto, não use as boas práticas do HTTP1 como base para um site que está sendo hospedado em HTTP2.

HTTP2 faz com que o custo de múltiplos pedidos diminua por causa de um número de técnicas já incluídas:
* HTTP2 pode deixar a conexão em aberta para reutilização por um longo de tempo, para que não haja a necessidade daquela negociação cara que HTTP1 faz com o servidor em cada solicitação.
* Ao contrário do HTTP1, o novo protocolo usa compactação de arquivos e assim o tamanho da solicitação é significativamente menor - e, como resultado, mais rápida.
* HTTP2 é multiplex, ou seja, pode enviar e receber várias coisas ao mesmo tempo através de uma única conexão.

O que tudo isso significa, é que não só as técnicas que usamos no HTTP1 estão obsoletas, mas como também, farão as coisas ficarem mais lentas. Você poderá estar baixando arquivos desnecessários para a página a ser servida (concatenação de código e CSS sprites são suscetíveis à isso), e a técnica de sharding invoca pesquisas de DNS que irão retardar as coisas, na verdade, no HTTP2 voce não precisar de usar shard de forma alguma.

Resumindo, quando você desenvolver o front-end (html/css/js) para um site que será servido através do HTTP2, tenha a certeza de que você não está usando velhas técnicas de desempenho do HTTP1, o que irão prejudicar o seu HTTP2 site.

## Aprendendo Mais sobre HTTP2
Existe [um excelente artigo (em inglês)](http://daniel.haxx.se/http2/), escrito por Daniel Stenberg, no qual ele detalha muito mais esse assunto que também se encontra disponível em PDF.

## Tradução
A tradução deste artigo para o Português foi devidamente autorizada pelo autor, [Matt Wilcox](https://mattwilcox.net/web-development/http2-for-front-end-web-developers).
