# Introdução à segurança da informação para times de desenvolvimento web

A imagem de hackers como pessoas extremamente habilidosas que tomam energético, ouvem The prodigy e vestem capuzes pretos pode criar um mau entendimento sobre o que é segurança de sistemas, essa imagem idealizada faz com que tentativas de ataque sejam vistas como monstros implacáveis que só equipes de segurança com seus próprios monstros implacáveis podem resolver, quando muitas vezes são só pôneis fofos com fome e tudo o que você precisava fazer para evitar a entrada na sua casa era fechar a porta.

Antes de qualquer coisa é importante contextualizar a motivação por trás de ataques, há uma diferença entre um texto feito para profissionais de segurança da informação e um texto para profissionais de desenvolvimento web. Infelizmente segurança e performance são duas áreas negligenciadas na grande maioria das fontes de ensino e acabam sendo deixadas para especialistas. Porém, assim como o esforço para manter uma casa limpa é muito menor caso a frequência de faxina seja alta, se as pessoas que desenvolvem para web entendem o que é seguro e tomam pequenas medidas no dia a dia para evitar práticas inseguras, a necessidade de reestruturação de última hora será bem menor.

## Porquê sistemas são invadidos?

Existem dezenas motivações pelas quais um ataque começa, mas o que é relevante para desenvolvimento web são motivações por dinheiro ou recursos. A distinção entre dinheiro e recursos é tênue nesse meio e para esse texto eu vou definir dinheiro como um recurso intrinsecamente valioso, como informações de usuários (logins, senhas, CPFs, informações de cartão de crédito..), propriedade intelectual (códigos fonte, informações internas, arquivos..) e quaisquer outras coisas que podem ser vendidas mas normalmente não são muito úteis pra quem as adquiriu.
Recursos, por outro lado, apesar de que podem ser vendidos exatamente da mesma forma, eles têm uma utilidade intrinseca e prática, esses recursos são computacionais e vêm de máquinas comprometidas, eles podem ser usados de toda forma imaginável, desde servir para deixar um servidor pirata de Mu online funcionando, até sustentar um ataque DDos que derruba toda a Playstation Network[\[1\]](https://thehackernews.com/2018/11/gaming-server-ddos-attack.html)[\[2\]](https://www.theverge.com/2017/8/18/16170536/mirai-ddos-playstation-network-dyn-internet-angry-gamers)[\[3\]](https://www.scmagazine.com/home/security-news/sony-psn-downed-hacking-group-claims-ddos-attack/)[\[4\]](https://www.esecurityplanet.com/network-security/sony-networks-taken-down-by-ddos-attack.html) e usos mais especializados como segurança e anonimato. O ponto a se entender aqui é que em ambos os casos a intenção nunca é danificar o sistema sendo atacado, o ideal é nunca ser percebido. Portanto a noção de que você nunca sofreu um ataque pode ser equivocada, quando na realidade você só nunca soube que sofreu um ataque.

Além dessa distinção de recursos é importante fazer uma distinção de ataques direcionados e ataques não direcionados. Ataques direcionados costumam envolver hackers de fato que analisam um sistema e determinam como invadir, esse tipo de ataque está fora do escopo do que uma equipe de desenvolvimento web pode impedir porque envolve vetores de ataque além de software e acaba passando por toda camada OSI, desde quais práticas de segurança os envolvidos no projeto usam até quem fisicamente pode entrar na sala dos servidores.

Já ataques não direcionados buscam sistemas vulneráveis, quaisquer sistemas vulneráveis vão ser úteis e desejáveis, principalmente os que possuem uma enorme base de usuários e precisam passar por 45 reuniões antes de atualizar uma dependência. O trabalho de uma equipe de desenvolvimento web aqui é tornar o sistema o menos desejável possível. Nenhum sistema é imune, é computacionalmente impossível tornar um sistema **imune**, mas há um imensurável mar de distância entre imunidade e "vulnerável para qualquer um que pesquisar sql injection string wordpress". Por isso os cuidados da equipe de desenvolvimento são importantíssimos e não podem ser deixados para quando for tarde demais.

## Como evitar que o seu sistema seja comprometido

Vale notar que diferentes tecnologias vão possuir diferentes vulnerabilidades. É importante pesquisar o que sua stack provê de graça, quais convenções existem e o que elas garantem. Muitas vezes, simplesmente seguir as recomendações documentadas evita boa parte dos problemas, então antes de quebrar o padrão oferecido pela tecnologia que você está usando, é essencial se informar exatamente no que essa quebra de padrão implica.
Dito isso, abaixo está uma lista das [vulnerabilidades mais frequentes](https://www.owasp.org/images/7/72/OWASP_Top_10-2017_%28en%29.pdf.pdf) no desenvolvimento web, como elas funcionam e como se proteger.

### 1 - SQL injection
todo: reescrever literalmente tudo, muito técnico e abstrato

SQL-I é um problema de interpretação de dados, quando se recebe uma informação do usuário essa informação precisa ser higienizada antes de ser enviada para processamento, sendo mais específico, quando você tem um form idealmente esse dado não vai chegar no servidor e ser diretamente enviado ao banco de dados, antes desse envio deve haver um intencional momento de verificação da integridade desses dados. Isso pode ser tratado à nível de framework ou de forma manual, mas de uma forma ou de outra é responsabilidade da equipe de desenvolvimento garantir que os dados que chegam ao banco de dados são válidos. Claro, nem sempre isso é previsível mas o fato de haver um esforço consciente em limitar o que é considerado como input válido já vai tornar qualquer sistema anos luz mais seguro do que simplesmente transformar um campo de input em um select.

#### 1.1 - GraphQL
A especificação do graphQL provê uma natural separação entre a execução de uma query e o processamento dessa query. Ter essas duas frentes separadas pode parecer um detalhe mas na realidade tem uma implicação muito poderosa, que o papel do desenvolvimento se torna livre de riscos, a partir do momento que a estrutura de processamento de queries é criada, pode-se assumir que os dedos que chegam ao time de desenvolvimento são saudáveis. Isso tira a responsabilidade do dia a dia e deposita essa responsabilidade em decisões de arquitetura, facilitando o processo de desenvolvimento.

Para exemplificar, a query anterior em GraphQL teria essa estrutura:
**EXEMPLO**

#### 1.2 - Material de estudo extra
Eu pensei em colocar uma lista de recomendações que podem ser legais pra se entender melhor o problema, mas por experiência ninguém vai consumir todo o material recomendado, então achei melhor fazer uma **excelente** recomendação em cada um desses tópicos que, caso você se interesse pode ser uma porta de entrada para se aprofundar na área. Para SQLI e manipulação de *inputs* em geral, recomendo essa apresentação(em inglês) que pode ser um pouco avançada demais, mas nada de outro mundo, o esforço de pesquisar termos desconhecidos é compensado pelo conteúdo da apresentação:
https://www.youtube.com/watch?v=3kEfedtQVOY

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

