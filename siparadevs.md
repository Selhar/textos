# Porquê sistemas são invadidos?

todo: repetição de palavras

Segurança da informação é algo pouco falado e menos entendido, mesmo entre quem trabalha com programação de ponta ainda há a noção de que hackers usam capuz preto e terminais com letras verdes, além de fazerem ASCII art extremamente detalhada junto de cada payload. Isso torna necessária uma contextualização do que certos termos significam e porquê sistemas são invadidos em primeiro lugar.

Raramente a intenção de um ataque é danificar o sistema, muito pelo contrário, cada sistema comprometido é um recurso que pode ser usado no futuro, seja vendendo as informações encontradas (logins, senhas, CPFs, cartões de crédito, etc..), seja utilizando o poder computacional latente em uma rede de máquinas comprometidas. Existem inúmeras formas que uma vulnerabilidade pode ser aproveitada, mas na maioria dos casos quem está atacando não quer ser percebido, portanto diretamente danificar o sistema é indesejado.  
Com esse objetivo de obtenção de recursos em mente fica mais fácil entender o *mindset* de um hacker, a intenção não é a danificação de sistemas e sim a obtenção de uma longa e potencialmente lucrativa lista de sistemas vulneráveis e acessíveis à qualquer momento, a prioridade **sempre** vai ser o sistema mais vulnerável, mais fácil de entrar e sair sem qualquer tipo de registro. É importante se ter em mente que raramente um ataque vai ser direcionado à um alvo específico, a busca é por "qualquer um que esteja extremamente vulnerável", logo, o papel de uma equipe de desenvolvimento é seguir boas práticas que tornam o sistema indesejável para esse tipo de ataque comum, esses são os ataques mais frequentes e triviais de se evitar. Já uma equipe de segurança é responsável por tornar esse sistema não só indesejável para ataques genéricos como trabalhoso para ataques direcionados, com análises dos tipos de requests que são feitos ao sistema, práticas de como se detectar e reagir à um ataque entre diversos outros protocolos que vão aumentar o nível de habilidade necessário para que esse sistema seja atacado, quase toda multinacional possui algum programa de bug bounty e o objetivo é justamente esse, encontrar e se proteger contra ataques excepcionais. Vale notar também no meio de segurança é comum escrever sobre um ataque bem sucedido, então esse tipo de informação é extramemente acessível, uma pesquisa rápida por qualquer multinacional + writeup provavelmente vai resultar em alguma leitura fantástica sobre vulnerabilidades inimaginavelmente complexas. Como esses casos excepcionais exemplificam, nunca um sistema será imune, sempre vai ser fisicamente possível invadir de algum jeito, a questão é quão complexo será esse ataque. Em resumo, a grande maioria das empresas não precisará de uma equipe especializada em segurança caso tenha uma equipe de desenvolvimento que adota segurança como parte natural do seu processo de desenvolvimento.

# Como evitar que o seu sistema seja invadido

Há diversas formas pelas quais seu sistema pode ser manipulado de uma forma não intencional, mas vale lembrar que a maioria dos frameworks populares por padrão já lida com muitos desses problemas *caso o padrão oferecido pelo framework seja seguido*. 
**TODO: exemplos tipo html_safe**

Dito isso, aqui vai uma lista das [vulnerabilidades mais frequentes](https://www.owasp.org/images/7/72/OWASP_Top_10-2017_%28en%29.pdf.pdf) no desenvolvimento web, como se proteger delas e indicação de quais ferramentas os frameworks já utilizam por padrão para essa defesa:

##### 1 - SQL injection
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
