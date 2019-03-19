# Introdução à segurança da informação para times de desenvolvimento web

A imagem de hackers como pessoas extremamente habilidosas que tomam energético, ouvem The prodigy e estão sempre de capuz preto pode criar um mau entendimento sobre o que é segurança de sistemas, essa imagem idealizada faz com que tentativas de ataque sejam vistas como monstros implacáveis que só equipes de segurança com seus próprios monstros implacáveis podem resolver, quando muitas vezes são só gatinhos e tudo o que você precisava fazer era fechar a porta.

## Porquê sistemas são invadidos?

Existem dezenas motivações pelas quais um ataque começa, mas o que é relevante para desenvolvimento web são motivações por dinheiro ou recursos. Essa distinção pode ser tênue, mas para esse texto eu vou definir dinheiro como um recurso intrinsecamente valioso como informações de usuários (logins e senhas, CPFs, emails, informações de cartão de crédito..), propriedade intelectual (códigos fonte, informações internas, arquivos..) e quaisquer outras coisas que podem ser vendidas mas normalmente não são muito úteis para quem as adquiriu.  
Apesar de poderem ser vendidos da mesma forma, recursos representam poder computacional de máquinas comprometidas e portanto têm infinitas utilidades práticas, desde servir para deixar um servidor pirata de Mu online rodando 24 horas até sustentar um ataque DDos que derruba toda a Playstation Network[\[1\]](https://thehackernews.com/2018/11/gaming-server-ddos-attack.html)[\[2\]](https://www.theverge.com/2017/8/18/16170536/mirai-ddos-playstation-network-dyn-internet-angry-gamers)[\[3\]](https://www.scmagazine.com/home/security-news/sony-psn-downed-hacking-group-claims-ddos-attack/)[\[4\]](https://www.esecurityplanet.com/network-security/sony-networks-taken-down-by-ddos-attack.html), além de usos mais especializados como anonimato, mineração de bitcoins, criação de bots... Basicamente qualquer coisa que um computador pode oferecer. O ponto a se entender aqui é que em ambos os casos a intenção não é danificar o sistema sendo atacado, o objetivo é obter algo e se possível não ser percebido. Portanto o tipo de vulnerabilidade que uma pessoa que desenvolve para web deve priorizar são as que tornam seus dados internos vulneráveis à acesso externo.

Além dessa distinção de recursos é importante fazer uma distinção de ataques direcionados e ataques não direcionados. Ataques direcionados costumam envolver hackers de fato que analisam um sistema e encontram vetores de ataque, dada a natureza de sistemas complexos, não há nenhum sistema que seja imune à um ataque direcionado, vai sempre depender da habilidade e tempo disponível da equipe que está atacando, esse tipo de ataque é responsabilidade de uma equipe de segurança e foge do escopo de desenvolvimento.

Já ataques não direcionados buscam sistemas vulneráveis, quaisquer que sejam, desde empresas antigas com uma ampla base de usuários mas onde quem desenvolve não têm tanta liberdade assim para realizar refatoramentos e atualizações até startups com más práticas de desenvolvimento. Ataques não direcionados é uma rede, o que cair é lucro. Ataques direcionados é a busca por Moby Dick. O objetivo desse post é clarificar quais medidas podem ser tomadas por uma equipe de desenvolvimento para reduzir a possibilidade de que seu sistema seja vítima de ataques genéricos.

## Como evitar que o seu sistema seja comprometido

Vale notar que diferentes tecnologias vão possuir diferentes vulnerabilidades. É importante pesquisar o que sua stack provê (você pode, por exemplo, pesquisar "XSS nodejs/rubyonrails/java"), quais convenções existem e o que elas garantem. Muitas vezes, simplesmente seguir as recomendações documentadas evita boa parte dos problemas, então antes de quebrar o padrão oferecido pela tecnologia que você está usando é essencial se informar sobre exatamente o que essa quebra de padrão implica.
Dito isso, abaixo está uma lista das [vulnerabilidades mais frequentes](https://www.owasp.org/images/7/72/OWASP_Top_10-2017_%28en%29.pdf.pdf) no desenvolvimento web, como elas funcionam e como se proteger.

### 1 - Injection
Injection é uma classe de problemas que envolve tanto linguística como ciência da computação e implica na manipulação do comportamento de um sistema através do seu *input*. Esse *input* pode ser qualquer tipo de informação que vêm de uma fonte externa e potencialmente maliciosa, como por exemplo cookies, parâmetros de URL, forms, webservices, variáveis de ambiente e todo tipo de dado dinâmico que vai então ser enviado à um interpretador.

Funções que executam código arbitrário são historicamente inseguras por essa capacidade de manipulação, utilizar dados não higieniados para executar um comando como `exec()` por exemplo, é como oferecer um café, um beijo na testa e uma mesa prontinha com o servidor do seu sistema interno, alguém mal intencionado vai poder fazer **qualquer coisa**. O que eu mais quero expressar com esse post é que dados externos não devem ser tratados com confiança e "dados externos" têm um significado extremamente amplo e muitas vezes pouco intuitivo. A ideia de que só forms e parâmetros de URL representam dados manipuláveis é equivocada, qualquer request pode ser forjado e enviado ao servidor com extrema facilidade, assim como o consumo de APIs externas não deve ser tratado como seguro; basicamente nada que está vindo de fora do seu sistema pode ser tratado com confiança, especialmente quando estes dados são usados para alimentar interpretadores.

#### 1.1 - SQL Injection
SQL injection é o caso mais frequente de manipulação de interpretadores, uma query dinâmica precisa ser feita e informação dinâmica precisa ser recebida em um form ou URL; basicamente nitroglicerina com um aviso de "mexa antes de beber".

Vamos supor que em um site hipotético exista a seguinte URL: `.com/profile.php?id=9`, essa URL recebe um ID que é então usado para executar uma query dinâmica como: `SELECT * FROM users WHERE ID=?` onde ? é o input do usuário. A query retorna os dados e o sistema exibe o perfil de ID=9. Caso o sistema use esses dados sem nenhum tipo de filtro, validação ou higienização e passe esses dados externos diretamente ao interpretador SQL, um usuário mal intencional pode manipular o sistema de diversas formas, como por exemplo executar a seguinte URL: `.com/profile.php?id=id='or '1'='1`, isso permite que os dados de todos usuários cadastrados em "users" seja visualizado. Basicamente, nesse momento alguém com más intenções tem uma porta de acesso ao seu servidor SQL e pode fazer o que quiser, incluindo deletar ou manipular todos os dados como este quadrinho do [XKCD](https://www.xkcd.com/327/) exemplifica:  
![XKCD comic about a mother who registered her son's name as an SQL injection](https://imgs.xkcd.com/comics/exploits_of_a_mom.png)

Vale notar que a maioria das *stacks* modernas de desenvolvimento têm algum tratamento de dados e **caso você não fuja do padrão** oferecido pelas ferramentas que usa, boa parte dessas preocupações já vão ser tratadas de fábrica. Essa fulga de padrão por soluções rápidas é a fonte da grande maioria dos vetores de ataque modernos, como [estes dados](https://laurent22.github.io/so-injections/) demonstram. Essas queries potencialmente vulneráveis são completamente evitáveis, em Rails por exemplo você já tem essa barreira entre o pedido por informações e o interpretador, um exemplo de sinal vermelho é escrever manualmente uma query em Rails. Em PHP também existem ferramentas que são responsáveis pela higienização de input [PDO](https://secure.php.net/manual/en/pdo.prepared-statements.php), [MySQLi](https://secure.php.net/manual/en/mysqli.quickstart.prepared-statements.php) entre outros. O ponto aqui é que o desenvolvimento moderno de sistemas já se preocupa com SQL injections, assim como todos os carros hoje já vêm com cinto de segurança, ele só precisa ser usado.


#### 1.2 - GraphQL
Por razões mais abrangentes do que esse post pode abordar GraphQL é uma excelente ferramenta no tratamento de *inputs*, sejam eles direcionados à um banco de dados ou não. A parte importante do que GraphQL faz e é relevante independente da tecnologia usada é a separação entre o tratamento de inputs e a execução desses inputs. Idealmente você nunca vai fazer uma chamada direta à um interpretador, especialmente de forma dinâmica. O ideal é que você converse com uma interface, e que essa interface tenha métodos de tratamentos de dados e possa, após higienização, essa interface faça a chamada ao interpretador. GraphQL como tecnologia não garante essa higienização mas faz com que haja um consciente processo de tratamento de dados.

#### 1.3 - Material de estudo extra
(Inglês) - [The science of insecurity](https://www.youtube.com/watch?v=3kEfedtQVOY), uma explicação didática sobre o uso de linguística e ciência da computação no estudo de injections.
(Inglês) - [GraphQL and security](https://mikewilliamson.wordpress.com/2016/09/15/graphql-and-security/), um detalhamento de como GraphQL incentiva boas práticas no processo de absorção de dados.

##### 2 - Autenticação
##### 3 - Exibição de informação restrita em endpoints públicos
##### 4 - Preprocessamento de XML
##### 5 - Controle de acesso à permissões do usuário
##### 6 - Má configuração de sistema
##### 7 - XSS
##### 8 - Serialização
##### 9 - Bibliotecas externas desatualizadas ou sem credibilidade
##### 10 - Falta de logs



link pool:

https://ssd.eff.org/pt-br#index  
https://www.hacker101.com/  

