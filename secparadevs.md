# Introdução à segurança da informação para times de desenvolvimento web

A imagem de hackers como pessoas extremamente habilidosas que tomam energético, ouvem The prodigy e vestem capuzes pretos pode criar um mau entendimento sobre o que é segurança de sistemas, essa imagem idealizada faz com que tentativas de ataque sejam vistas como monstros implacáveis que só equipes de segurança com seus próprios monstros implacáveis podem resolver, quando muitas vezes são só gatinhos e tudo o que você precisava fazer para evitar a entrada na sua casa era fechar a porta.

Antes de qualquer coisa é importante contextualizar a motivação por trás de ataques, há uma diferença entre um texto feito para profissionais de segurança e um texto para profissionais de desenvolvimento. Infelizmente segurança, assim como performance, são áreas pouco tocadas pela maioria das fontes de ensino e acabam sendo negligenciadas até ser tarde demais. Porém, assim como o esforço para manter uma casa limpa é muito menor caso a frequência de faxina seja alta, se as pessoas que desenvolvem para web entendem o que é seguro e tomam pequenas medidas no dia a dia para evitar práticas inseguras, a necessidade de reestruturação de última hora será bem menor.

## Porquê sistemas são invadidos?

Existem dezenas motivações pelas quais um ataque começa, mas o que é relevante para desenvolvimento web são motivações por dinheiro ou recursos. A distinção entre dinheiro e recursos é tênue nesse meio e para esse texto eu vou definir dinheiro como um recurso intrinsecamente valioso, como informações de usuários (logins, senhas, CPFs, informações de cartão de crédito..), propriedade intelectual (códigos fonte, informações internas, arquivos..) e quaisquer outras coisas que podem ser vendidas mas normalmente não são muito úteis pra quem as adquiriu.
Recursos, por outro lado, apesar de que podem ser vendidos exatamente da mesma forma, eles têm uma utilidade intrinseca e prática, esses recursos são computacionais e vêm de máquinas comprometidas, eles podem ser usados de toda forma imaginável, desde servir para deixar um servidor pirata de Mu online funcionando, até sustentar um ataque DDos que derruba toda a Playstation Network[\[1\]](https://thehackernews.com/2018/11/gaming-server-ddos-attack.html)[\[2\]](https://www.theverge.com/2017/8/18/16170536/mirai-ddos-playstation-network-dyn-internet-angry-gamers)[\[3\]](https://www.scmagazine.com/home/security-news/sony-psn-downed-hacking-group-claims-ddos-attack/)[\[4\]](https://www.esecurityplanet.com/network-security/sony-networks-taken-down-by-ddos-attack.html) e usos mais especializados como segurança e anonimato. O ponto a se entender aqui é que em ambos os casos a intenção nunca é danificar o sistema sendo atacado, o ideal é nunca ser percebido. Portanto a noção de que você nunca sofreu um ataque pode ser equivocada, quando na realidade você só nunca soube que sofreu um ataque.

Além dessa distinção de recursos é importante fazer uma distinção de ataques direcionados e ataques não direcionados. Ataques direcionados costumam envolver hackers de fato que analisam um sistema e determinam como invadir, esse tipo de ataque está fora do escopo do que uma equipe de desenvolvimento web pode impedir porque envolve vetores de ataque além de software e acaba passando por toda camada OSI, desde quais práticas de segurança os envolvidos no projeto usam até quem fisicamente pode entrar na sala dos servidores.

Já ataques não direcionados buscam sistemas vulneráveis, quaisquer sistemas vulneráveis vão ser úteis e desejáveis, principalmente os que possuem uma enorme base de usuários e precisam passar por 45 reuniões antes de atualizar uma dependência. O trabalho de uma equipe de desenvolvimento web aqui é tornar o sistema o menos desejável possível. Nenhum sistema é imune, é computacionalmente impossível tornar um sistema **imune**, mas há um imensurável mar de distância entre imunidade e "vulnerável para qualquer um que pesquisar sql injection string wordpress". Por isso os cuidados da equipe de desenvolvimento são importantíssimos e não podem ser deixados para quando for tarde demais.

## Como evitar que o seu sistema seja comprometido

Vale notar que diferentes tecnologias vão possuir diferentes vulnerabilidades. É importante pesquisar o que sua stack provê de graça, quais convenções existem e o que elas garantem. Muitas vezes, simplesmente seguir as recomendações documentadas evita boa parte dos problemas, então antes de quebrar o padrão oferecido pela tecnologia que você está usando, é essencial se informar exatamente no que essa quebra de padrão implica.
Dito isso, abaixo está uma lista das [vulnerabilidades mais frequentes](https://www.owasp.org/images/7/72/OWASP_Top_10-2017_%28en%29.pdf.pdf) no desenvolvimento web, como elas funcionam e como se proteger.

### 1 - Injection
Injection é uma classe de problemas extremamente complexa que envolve tanto linguística como ciência da computação e implica na manipulação do comportamento de um sistema através do seu *input*. Esse *input* pode ser qualquer tipo de informação que vem de uma fonte externa e potencialmente maliciosa, como por exemplo cookies, parâmetros de URL, forms, webservices, variáveis de ambiente e todo tipo de dado dinâmico que vai então ser enviado à um interpretador.

Funções que executam código arbitrário são historicamente inseguras por isso, utilizar dados não higieniados para executar um comando como `exec()` por exemplo, é como oferecer um café, um beijo na testa e uma mesa prontinha com o servidor do seu sistema interno, alguém mal intencionado vai poder fazer **qualquer coisa**. Se tem uma coisa que eu espero que você absorva desse post é que dados externos devem sempre ser tratados, SQL injection é a vulnerabilidade mais comum em desenvolvimento web mas não é o único tipo de injection, a noção geral de que "*input* externo não é confiável e deve ser sempre tratado" é o que deve ser lembrado no momento de desenvnolvimento. A ideia aqui é dar contexto para que você saiba o que pode ser uma falha de segurança em potencial e mesmo que não saiba como resolver imediatamente, saiba o que pesquisar e porquê.

#### 1.1 - SQL Injection
Vamos supor que em um site hipotético exista a seguinte URL: `.com/profile.php?id=9`, essa URL recebe um ID que é então usado para executar uma query dinâmica como: `SELECT * FROM users WHERE ID=?` onde ? é o input do usuário. A query retorna os dados e o sistema exibe os dados do usuário de ID=9. Caso o sistema use esses dados sem nenhum tipo de filtro, validação ou higienização e passe esses dados externos diretamente ao interpretador SQL, um usuário mal intencional pode manipular o sistema de diversas formas, como por exemplo executar a seguinte URL: `.com/profile.php?id=id='or '1'='1`, isso permite que os dados de todos usuários cadastrados em "users" seja visualizado, até mesmo administradores. Basicamente, nesse momento alguém com más intenções tem uma porta de acesso ao seu servidor SQL e pode fazer o que quiser, incluindo deletar ou manipular todos os dados como este quadrinho do [XKCD](https://www.xkcd.com/327/) exemplifica:  
![XKCD comic about a mother who registered her son's name as an SQL injection](https://imgs.xkcd.com/comics/exploits_of_a_mom.png)

Vale notar que a maioria das *stacks* modernas de desenvolvimento têm algum tratamento de dados e **caso você não fuja do padrão** oferecido pelas ferramentas que usa, boa parte dessas preocupações já vão ser tratadas de fábrica. Essa fulga de padrão por soluções rápidas é a fonte da grande maioria de vetores de ataque modernos, como [esses dados](https://laurent22.github.io/so-injections/) demonstram. Essas queries potencialmente vulneráveis (a vulnerabilidade vai depender de como os dados são tratados internamente) é completamente evitável, em PHP por exemplo existem ferramentas feitas exatamente para essa higienização de dados como [PDO](https://secure.php.net/manual/en/pdo.prepared-statements.php), [MySQLi](https://secure.php.net/manual/en/mysqli.quickstart.prepared-statements.php) entre outros. Então sempre que uma solução fácil e direta que parece burlar certos comportamentos recomendados de uma ferramenta aparecer, tente entender o que essa solução rápida implica e quais as consequências de ignorar esse comportamento padrão.

#### 1.2 - GraphQL
Por razões mais abrangentes do que esse post pode abordar GraphQL é uma excelente ferramenta no tratamento de *inputs*, sejam eles direcionados à um banco de dados ou não. A parte importante do que GraphQL faz é separar o recebimento de dados do processo de consumo desses dados, há um padrão explícito e centralizado por onde toda informação externa vai passar e idealmente ser higienizada de acordo com o tipo de input recebido. GraphQL como tecnologia não ajuda no tratamento dessas informações, mas força o time de desenvolvimento a cuidar dessa etapa que muitas vezes pode ser inteiramente ignorada, principalmente em sistemas que não lidam com usuários diretamente.

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

