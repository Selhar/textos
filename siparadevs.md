### O que significa invadir um sistema e porquê sistemas são invadidos

Segurança da informação é algo pouco falado e pouco entendido, mesmo entre quem trabalha com programação de ponta ainda há a noção de que hackers usam capuz preto e terminais com letras verdes, além de fazerem ASCII art extremamente detalhada junto de cada payload. Isso torna necessária uma contextualização do que certos termos significam e porquê sistemas são invadidos em primeiro lugar.

Há um grande leque de motivações por trás de cada ataque, porém como o foco desse post é no que uma desenvolvedora pode fazer para proteger seus sistemas, e não no que um profissional da segurança pode fazer (essa distinção de escopo é muito importante, porque os tipos de preocupações são completamente diferentes), as motivações focadas aqui serão duas: Recursos computacionais e recursos monetários

## Recursos computacionais
Um pouquinho de recurso computacional de milhares de pessoas implica em *muito* recurso computacional, seja para minerar bitcoins, seja para DDoS, TODO: mais exemplos e clarificação do que esses exemplos significam

###### 1. Dados
Informação é dinheiro, quanto mais detalhada e fresca, melhor. E digo isso em um sentido extremamente literal, depois de conseguir um banco de dados cheio de informações esse arquivo pode ser vendido de forma relativamente fácil. O valor pelo qual isso é vendido vai depender do tipo de informação, mas mesmo que você consiga os dados dos jogadores de ragnarok online, essas informações são provavelmente replicadas em diversos sites, o mesmo e-mail, a mesma senha, logo a noção de que seu site "não guarda informações relevantes" é praticamente inexistente.
###### 2. Tráfego
O tráfego de um site pode ser redirecionado, seja para usar esse poder de redirecionamento para voltar no Dourado do big brother (isso de fato aconteceu), seja para redirecionar o usuário à uma cópia da mesma página original, porém no servidor de quem está atacando. O que é comum em bancos, não necessariamente o banco estando vulnerável, mas a máquina do cliente estar vulnerável e ter suas informações de DNS alteradas, o que faz com que acessar o site do banco redirecione para http://definitivamenteumsiteseguro.banco.com.br com o mesmo layout e funcionamento, exceto que enviando dados para quem está roubando as informações.
###### 3. Robôs/boxes/algum termo que traduza um computador zumbi
###### 4. hacktivism
###### 5. curiosidade

TODO:
1. mais exemplos
2. mais clareza no que cada coisa significa em um nível não técnico
3. mais ênfase em como danificar sistemas é indesejado
4. deixar mais claro que o foco é em sistemas web comuns dia a dia java primefaces jquery e não necessariamente pra todo caso imaginável que alguém que trabalha com isso com certeza vai pensar que "ah mas tem o caso de 1995 quando o cara se vestiu de mickey e invadiu a disney". O foco não é no tipo de coisa que vão escrever writeup que vai ser repassada no mirc por décadas, e sim no que uma desenvolvedora padrão vai encontrar.
