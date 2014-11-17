---
title: "Exceptions vs Tell Don’t Ask"
created_at: 12/10/2014
kind: article
author: Philip Calçado
origin: http://philcalcado.com/2006/03/09/exceptions-vs-tell-dont-ask/
---

Uma thread legal na lista de discussão do RioJUG sobre o princípio de Tell Don’t Ask…

Considerando que o esquema de histórico do Yahoo! é horrível, vou colar aqui.

Bruno Iecker:

>Oi galera,
>tenho uma dúvida em relação a quando lançar uma Exception.
>Vou tentar criar um exemplo, deve sair bem maluco, para exemplificar minha dúvida:

<pre>
<code class="c#">
//forma 1
if(usuario.isMaior())
{
	usuario.addFavorito(sexo);
}

//forma 2
try
{
	usuario.addFavorito(sexo);
}
catch (ConteudoNaoPermitidoException e) {
	e.printStackTrace();
}
</code> 
</pre>


>Bem, da primeira forma, evito a Exception e entendi (provavelmente errado) que seria essa a recomendação do 
>livro Effective Java (tem um resumo aqui). Mas assim, eu não estaria violando o príncipio Tell, don’t ask? 
>Além de expor um método isMaior que poderia ser privado.

>Abs,
>Bruno. 

Phillip Calçado

>Olá,

>>On 3/7/06, Bruno Iecker wrote:
>> Bem, da primeira forma, evito a Exception e entendi (provavelmente errado) que seria essa a recomendação do livro Effective Java (tem um resumo aqui). Mas assim, eu não estaria violando o príncipio Tell, don’t ask? Além de expor um método isMaior que poderia ser privado.

>Sim, estaria. Você pode melhorar a separação de responsabilidades:

>Segundo etnendi, a lógica de adicionar um favorito é a seguinte:

>“Se o favorito for restrito para usuários maiores de idade, rejeite.”

>E no exemplo essa lógica é responsabilidade do usuário. Nenhuma outra classe deve implementá-la, então você não pode fazer


<pre>
<code class="c#">
    if(usuario.isMario())
  </code> 
</pre>  
    O que fazer então?

    Você pode fazer assim:


<pre>
<code class="c#">
if(usuario.podeAdicionar(sexo))
{
	usuario.addFavorito(sexo);
}
  </code> 
</pre>  

    E seu usuario:

<pre>
<code class="c#">

    class usuario{
    …

    public boolean podeAdicionar(Favorito f){
    if(f.isRestrito()) return (this.idade > 18);
    else return true;
    }

    public void addFavorito(Favorito f){

    if(podeAdicionar(f)){
    favoritos.add(f);
    }
    else{
    throw new FavoritoNaoEhValidoException();
    }
    }

    }

  </code> 
</pre>  

    Assim você mantêm as responsabilidades das classes no devido lugar.

    []s

Bruno Iecker

    Oi Phillip,

    fiquei mais confuso… É que acho que expressei mal a minha dúvida.

    O meu exemplo é hipotético, mas vamos lá…

    //Phillip escreveu

    if(usuario.podeAdicionar(sexo))
    {
    usuario.addFavorito (sexo);
    }

    Neste caso, de qualquer forma, eu ainda não estaria perguntando ao usuario?

    Utilizando o seu exemplo… por que não fazer apenas:

    usuario.addFavorito(sexo);

    e deixar o método podeAdicionar privado em Usuario?

    Abs,
    Bruno.

    PS.: Sim, trocar o método isMaior por podeAdicionar melhorou bastante porque agora não exponho aos clientes a lógica de permissão, mas não era essa a minha dúvida. ;-)

Phillip Calçado

    Oi,

    On 3/7/06, Bruno Iecker wrote:
    > Utilizando o seu exemplo… por que não fazer apenas: (…) e deixar o método podeAdicionar privado em Usuario?

    Falando de “tell don’t ask” puramente acho que vai depender do nível
    de encapsulamento que você quer no processo de adicionar. É bem
    relativo ao problema enfrentado.

    Sobre exceções em geral, caso fosse uma operação complicada onde você
    não pode perguntar antes, algo do tipo do gato de Schrödinger (onde o
    ato de observar/perguntar causa incerteza:
    http://en.wikipedia.org/wiki/Schr%C3%B6dinger%27s_cat) você ia ter que
    usar exceções ou se basear no retorno do método.

    Para decidir entre um ou outro (retorno ou exceção) entra o que é
    válido ou não para sua classe. Vamos tentar aplicar Design by Contract
    (uma pequena introduçãozinha aqui:
    http://fragmental.com.br/wiki/index.php?title=Contratos_Nulos).

    Se sua classe assume (pré-condição) que o argumento é sempre válido, a
    classe que chama deve enviar apenas argumentos válidos. Se os
    argumentos não forem válidos essa é uma condição clara onde uma
    exceção deve ser lançada (algo do tipo illegalArgumentException).

    Nesse caso, sua classe cliente é “bem-intencionada” e quer enviar
    apenas argumentos válidos ao usuário, mas ela não pode saber por si só
    o que é válido ou não, tem que perguntar a alguém (no caso, ao
    usuario).

    Se sua classe Usuário não especifica no seu contrato que espera apenas
    argumentos válidos, ela deve ser capaz de lidar com qualquer
    argumento. Como isso vai ser implementado depende do problema mas
    geralmente lançar uma exceção não é algo “justo” pois ninguém quebrou
    nenhum contrato.