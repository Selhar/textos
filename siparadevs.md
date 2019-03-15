# Porquê sistemas são invadidos?

Segurança da informação é algo pouco falado e pouco entendido, mesmo entre quem trabalha com programação de ponta ainda há a noção de que hackers usam capuz preto e terminais com letras verdes, além de fazerem ASCII art extremamente detalhada junto de cada payload. Isso torna necessária uma contextualização do que certos termos significam e porquê sistemas são invadidos em primeiro lugar.

Raramente a intenção de um hacker é danificar o sistema invadido, o objetivo costuma ser obtenção de recursos, sejam esses recursos monetários ou computacionais. Por recursos computacionais quero dizer acesso ao processamento de máquinas externas ou rede de uma máquina externa, quando operações ilegais são planejadas dificilmente os envolvidos vão querer fazer isso dos próprios computadores, portanto ter acesso a computadores externos permite que você conecte em uma VPS e dessa VPS tenha acesso a um sistema sem ligação com você, assim todos requests saindo do seu computador vão à VPS e os requests da VPS vão à máquina de um desconhecido, a partir daí essa operação pode ser executada com consideravelmente menos risco aos envolvidos. Há outros métodos mas inevitavelmente alguém vai ter que enviar requests de algum terminal e quão menos relacionado ao envolvido esse terminal for, melhor, o que costuma significar "qualquer um que estava vulnerável e disponível".

Agora, por recursos monetários quero dizer a obtenção de algo que pode ser vendido, esse algo geralmente é representado em dados mas também pode ser o acesso à um conjunto de sistemas comprometidos (e acesso à sistemas comprometidos implica em diversos usos, de DDoS até controle de bots). O que quero dizer com tudo isso é que a grande maioria das vulnerabilidades vão ser exploradas em massa, e não de forma direcionada, quanto mais fácil for roubar os dados ou tomar o controle de parte do seu sistema web, mais provável você será vítima de um ataque. Não é tanto questão de tornar o sistema imune, mas fazer com que o seu sistema seja trabalho demais pra ser um alvo desejável.

Com essas duas motivações explicadas (e não são as únicas motivações, porém são os casos mais relevantes para quem mantém sistemas web) fica fácil entender a distinção de responsabilidade entre uma equipe de segurança e uma equipe de desenvolvimento. A desenvolvedora precisa ter o cuidado para que seu sistema não seja um dos sistemas extremamente vulneráveis e fácil de se conseguir acesso, já uma equipe de segurança vai fazer toda uma análise para não só evitar vulnerabilidades genéricas, como vulnerabilidades mais direcionadas. É como a diferença entre ter o cuidado de trancar sua porta ao sair de casa e contratar um serviço de guarda costas 24hrs, correlacionando com sistemas web o problema é que a esmagadora maioria não tranca a porta. Esse post é sobre trancar a porta **TODO: pelo amor de cristo gramática e repetição**

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
