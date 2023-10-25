---
title: Zero Impact Projects
author: mtammacco
type: post
date: 2006-07-19T11:16:00+00:00
url: /archive/2006/07/19/zero-impact-projects.aspx
categories:
  - Visual Studio 2005

---
Ai tempi in cui utilizzavo Visual Studio 6.0 (tanto tempo fa, ma anche adesso, ogni tanto&#8230;:)),  una delle funzionalità dell&#8217;IDE che più mi tornava utile era la possibilità di compilare ed eseguire porzioni di codice senza doverli necessariamente salvare sul disco in progetti e soluzioni (allora si parlava di progetto e gruppi di progetto). In Visual Studio 2002/2003 questa funzionalità è assente, con la conseguenza di veder proliferare sul proprio hard disk progetti e soluzioni che non hanno alcuna utilità ma sono solo il risultato di prove di qualche &#8220;snippet code&#8221;. A dir la verità ho anche utilizzato un tool freeware chiamato [Snippet Compiler][1], molto valido, che, come dice il suo stesso nome, è in grado di compilare ed eseguire al volo snippet code ed opzionalmente salvarli su disco, con tanto di presenza dell&#8217;intellisense, anche se a mio avviso non impeccabile. In Visual Studio 2005 questa funzionalità è riapparsa sotto il nome di &#8220;Zero Impact Projects&#8221; (ZIPs). Infatti, posizionandosi in Tools\Options\Project and Solutions\General, è accessibile il check &#8220;Save new projects when created&#8221; il cui valore di default è &#8220;checked&#8221;. Disattivandolo, ogni nuovo progetto creato non sarà più salvato su disco se non su esplicita richiesta, permettendo il test &#8220;al volo&#8221; di un blocco di codice. Tuttavia, creando uno Zero Impacts Projects viene creata comunque una directory con lo stesso nome del progetto sotto il path &#8220;Visual Studio 2005&#8221; presente nella directory del profilo utente correntemente loggato. Questa directory, anche se vuota, resta presente su disco anche se si opta per non salvare i files del progetto, creando, di fatto, cartelle indesiderate anche se con un impatto molto minore rispetto a Visual Studio 2002/2003.

 [1]: http://www.sliver.com/dotnet/SnippetCompiler/