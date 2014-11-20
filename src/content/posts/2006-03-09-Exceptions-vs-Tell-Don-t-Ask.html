---
title: "Exceptions vs Tell Don’t Ask"
created_at: 09/03/2006
kind: article
author: Philip Calçado
origin: http://philcalcado.com/2006/03/09/exceptions-vs-tell-dont-ask/
---

<p>Uma <a href="http://groups.yahoo.com/group/riojug/message/15513">thread legal</a> na l<a href="http://groups.yahoo.com/group/riojug">ista de discussão do RioJUG</a> sobre o princípio de <a href="http://www.pragmaticprogrammer.com/ppllc/papers/1998_05.html">Tell Don&#8217;t Ask</a>&#8230;</p>
<p>Considerando que o esquema de histórico do Yahoo! é horrível, vou colar aqui.</p>
<p>Bruno Iecker:</p>
<blockquote><p>Oi galera,</p>
<p>tenho uma dúvida em relação a quando lançar uma Exception.</p>
<p>Vou tentar criar um exemplo, deve sair bem maluco, para exemplificar minha dúvida:</p>
<p>//forma 1<br />
if(usuario.isMaior())<br />
{<br />
   usuario.addFavorito(sexo);<br />
}</p>
<p>//forma 2<br />
try<br />
{<br />
   usuario.addFavorito(sexo);<br />
}<br />
catch (ConteudoNaoPermitidoException e) {<br />
   e.printStackTrace();<br />
}</p>
<p>Bem, da primeira forma, evito a Exception e entendi (provavelmente errado) que seria essa a recomendação do livro Effective Java (tem um resumo aqui). Mas assim, eu não estaria violando o príncipio Tell, don&#8217;t ask? Além de expor um método isMaior que poderia ser privado.</p>
<p>Abs,<br />
Bruno.
</p></blockquote>
<p>Phillip Calçado </p>
<blockquote><p>Olá,</p>
<p>On 3/7/06, Bruno Iecker wrote:<br />
> Bem, da primeira forma, evito a Exception e entendi (provavelmente errado) que seria essa a recomendação do livro Effective Java (tem um  resumo aqui). Mas assim, eu não estaria violando o príncipio Tell, don&#8217;t ask? Além de expor um método isMaior que poderia ser privado.</p>
<p>Sim, estaria. Você pode melhorar a separação de responsabilidades:</p>
<p>Segundo etnendi, a lógica de adicionar um favorito é a seguinte:</p>
<p>&#8220;Se o favorito for restrito para usuários maiores de idade, rejeite.&#8221;</p>
<p>E no exemplo essa lógica é responsabilidade do usuário. Nenhuma outra<br />
classe deve implementá-la, então você não pode fazer</p>
<p>if(usuario.isMario())</p>
<p>O que fazer então?</p>
<p>Você pode fazer assim:</p>
<p>if(usuario.podeAdicionar(sexo))<br />
{<br />
  usuario.addFavorito(sexo);<br />
}</p>
<p>E seu usuario:</p>
<p>class usuario{<br />
&#8230;</p>
<p> public boolean podeAdicionar(Favorito f){<br />
 if(f.isRestrito()) return (this.idade > 18);<br />
 else return true;<br />
 }</p>
<p> public void addFavorito(Favorito f){</p>
<p>  if(podeAdicionar(f)){<br />
    favoritos.add(f);<br />
  }<br />
  else{<br />
   throw new FavoritoNaoEhValidoException();<br />
  }<br />
 }</p>
<p>}</p>
<p>Assim você mantêm as responsabilidades das classes no devido lugar.</p>
<p>[]s</p>
</blockquote>
<p>Bruno Iecker</p>
<blockquote><p>
Oi Phillip,</p>
<p>fiquei mais confuso&#8230; É que acho que expressei mal a minha dúvida.</p>
<p>O meu exemplo é hipotético, mas vamos lá&#8230;</p>
<p>//Phillip escreveu</p>
<p>if(usuario.podeAdicionar(sexo))<br />
{<br />
   usuario.addFavorito (sexo);<br />
}</p>
<p>Neste caso, de qualquer forma, eu ainda não estaria perguntando ao usuario?</p>
<p>Utilizando o seu exemplo&#8230; por que não fazer apenas:</p>
<p>usuario.addFavorito(sexo);</p>
<p>e deixar o método podeAdicionar privado em Usuario?</p>
<p>Abs,<br />
Bruno.</p>
<p>PS.: Sim, trocar o método isMaior por podeAdicionar melhorou bastante porque agora não exponho aos clientes a lógica de permissão, mas não era essa a minha dúvida. ;-)</p></blockquote>
<p>Phillip Calçado</p>
<blockquote><p>Oi,</p>
<p>On 3/7/06, Bruno Iecker <bruno.iecker@gmail.com> wrote:<br />
> Utilizando o seu exemplo&#8230; por que não fazer apenas: (&#8230;) e deixar o método podeAdicionar privado em Usuario?</p>
<p>Falando de &#8220;tell don&#8217;t ask&#8221; puramente acho que vai depender do nível<br />
de encapsulamento que você quer no processo de adicionar. É bem<br />
relativo ao problema enfrentado.</p>
<p>Sobre exceções em geral, caso fosse uma operação complicada onde você<br />
não pode perguntar antes, algo do tipo do gato de Schrödinger (onde o<br />
ato de observar/perguntar causa incerteza:<br />
http://en.wikipedia.org/wiki/Schr%C3%B6dinger%27s_cat) você ia ter que<br />
usar exceções ou se basear no retorno do método.</p>
<p>Para decidir entre um ou outro (retorno ou exceção) entra o que é<br />
válido ou não para sua classe. Vamos tentar aplicar Design by Contract<br />
(uma pequena introduçãozinha aqui:<br />
http://fragmental.com.br/wiki/index.php?title=Contratos_Nulos).</p>
<p>Se sua classe assume (pré-condição) que o argumento é sempre válido, a<br />
classe que chama deve enviar apenas argumentos válidos. Se os<br />
argumentos não forem válidos essa é uma condição clara onde uma<br />
exceção deve ser lançada (algo do tipo illegalArgumentException).</p>
<p>Nesse caso, sua classe cliente é &#8220;bem-intencionada&#8221; e quer enviar<br />
apenas argumentos válidos ao usuário, mas ela não pode saber por si só<br />
o que é válido ou não, tem que perguntar a alguém (no caso, ao<br />
usuario).</p>
<p>Se sua classe Usuário não especifica no seu contrato que espera apenas<br />
argumentos válidos, ela deve ser capaz de lidar com qualquer<br />
argumento. Como isso vai ser implementado depende do problema mas<br />
geralmente lançar uma exceção não é algo &#8220;justo&#8221; pois ninguém quebrou<br />
nenhum contrato.</p></blockquote>