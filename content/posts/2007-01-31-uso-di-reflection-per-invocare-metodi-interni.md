---
title: Uso di reflection per invocare metodi interni
author: mtammacco
type: post
date: 2007-01-31T18:48:00+00:00
url: /archive/2007/01/31/uso-di-reflection-per-invocare-metodi-interni.aspx
categories:
  - .NET Framework 1.0 / 1.1 / 2.0

---
In un <a title="" href="/cs/blogs/maurizio/archive/2006/11/02/51.aspx" target="" name="" rel="noopener">post</a> precedente ho parlato dell&#8217;uso dell&#8217;attributo AllowPartiallyTrustedCallers a proposito della sicurezza applicata all&#8217;invocazione di metodi pubblici definiti all&#8217;interno di un assembly strong-named.  Rimanendo sempre sullo stesso tema, un altro attributo utile a &#8220;limitare&#8221; i possibili chiamanti di un determinato metodo è StrongNameIdentityPermissionAttribute, usato in questo modo:

<pre class="brush: csharp; title: ; notranslate" title="">[StrongNameIdentityPermissionAttribute(SecurityAction.LinkDemand, PublicKey = “public key”)]
public string MyMethod(string parameter) {}
</pre>

La presenza di questo attributo permette la chiamata al metodo MyMethod dell&#8217;esempio solo al codice contenuto in un assembly firmato con strong name e che presenta la chiave pubblica specificata nell&#8217;attributo stesso. Qualsiasi altro codice che tentasse di invocare il metodo in questione provoca una eccezione del tipo SecurityException. Questa forma di sicurezza è la più affidabile a disposizione se vogliamo proteggere ad esempio metodi sensibili dall&#8217;invocazione da parte di codice maligno. Se invece il metodo in questione non è invocato dall&#8217;esterno dell&#8217;assembly, in altre parole non è public, potremmo pensare che basterebbe limitare il suo ambito di visibilità (es.: private, internal in C# oppure friend in VB.NET) per renderlo sicuro da chiamate da parte di codice non affidabile. Putroppo questa convinzione è errata, poichè attraverso l&#8217;uso delle tecniche di reflection può essere invocato qualsiasi metodo con qualsiasi ambito di visibilità, quindi anche i metodi marcati come internal o private. Infatti, utilizzando il tool Reflector oppure semplicemente ildasm è possibile leggere la firma di metodi con qualsiasi visibilità (quindi public, private, protected ed internal). Se il metodo MyMethod fosse &#8220;internal&#8221;, conoscendo la sua firma è possibile invocarlo da un altro assembly via reflection in questo modo:

<pre class="brush: csharp; title: ; notranslate" title="">object x = Activator.CreateInstanceFrom(“MyAssembly.dll”, “MyAssembly.MyNamespace”).Unwrap();
string result = x.GetType().InvokeMember(“MyMethod”, System.Reflection.BindingFlags.InvokeMethod | System.Reflection.BindingFlags.Instance  
      | System.Reflection.BindingFlags.NonPublic, null, x, new object[] { “string parameter” }) as string;
</pre>

bypassando quindi la protezione imposta dal livello di visibilità.

Da notare che richiamare un metodo non pubblico attraverso reflection richiede il permesso ReflectionPermission, impostabile attraverso l&#8217;uso dell&#8217;attributo ReflectionPermissionAttribute (in modo dichiarativo), oppure in modo programmatico.

In assenza di questo permesso è possibile invocare via reflection solo i metodi pubblici.