---
title: Acerca de toma de notas, hacer una wiki y así
author: lmcj
type: post
date: 2022-03-20T15:51:15+00:00
categories:
  - Update
tags:
  - PKM
  - Software
toc: true
---
 

Hace poco decidí mantener mis notas de todo lo posible usando el plugin para vim/neovim  
vimwiki pero terminé usando Obsidian.

Todo comenzó cuando por el inicio de febrero [EL DAVID][1] me recordó que [Joplin][2] existe, lo que derivó en una conversación sobre toma de notas y _sISteMas dE gEStIón De COnOcIMiEnTo_ (PKM por Personal Knowledge Management) y salió a relucir [Obsidian][3]. Sobre lo cual EL DAVID dijo:

> El pedo es que es de paga y no pienso pagar por un explorador de archivos glorificado.

A lo que yo contesté (después de ir a ver):

> No güey, la versión personal es gratis.

A raíz de esto, me dediqué a investigar más sobre estos sistemas porque ciertamente necesitaba una solución para mi toma de notas que hasta la fecha ha sido un caos, y caí (también El David me comentó) en la cuenta de que mucho de esto está basado en un método de toma de notas llamado [Zettelkasten][4], el cual se basa en ordenar las notas jerárquicamente y típicamente por cronología, utilizando etiquetas y demás meta información para relacionar las notas unas con otras. Mira la verdad es que puedo estar mal, porque no es un método que me interese demasiado, mi mente funciona mejor por categorías (o al menos eso pensaba) y este método aparentemente no las utiliza mucho, si quieres leer más al respecto por aquí están unos cuantos enlaces:

  * [El sitio zettelkasten.de][5] --- donde tienen foros y hablan únicamente sobre este método, incluso promueven un software para MacOS.
  * [La guía para Zettelkasten de Zettlr][6] --- intenté utilizar este software que es _muuuuuuuuy_ bueno pero no es para mí, de hecho si te gusta el método Zettelkasten yo lo recomendaría antes que Obsidian.
  * [Un post de Obsidian][7] --- donde hablan sobre esto y la raza agrega consejos e interpretaciones.

Ahora, cuando digo que a mí no me interesa el método Zettelkasten porque no se adapta a mi forma de pensar, eso no quiere decir que no se adaptará a ti si también prefieres organizar las cosas por categorías como yo. Precisamente en esos links puedes ver que hay muchísimas formas de organizarse con este sistema. En mi caso simplemente no encontré la forma de adaptar mi forma de tomar notas. De hecho otra cosa que te recomendaría sería buscar contenido sobre Obsidian en YouTube, por ejemplo puedes buscar a [Bryan Jenks][8] quien parece que es de lo único que habla. Además de este método hay otros, y en principio todos pueden unirse de una manera que se te acomode.

> Desde que comencé a escribir esta entrada he estado usando mi nuevo sistema regularmente y descubierto algunas cosas, en particular, el método Zettelkasten es muy útil para tomar notas de una manera más rápida, porque entonces no tienes que pensar en la taxonomía de tu sistema antes de comenzar a hacer notas y simplemente dejar que la estructura surja naturalmente haciendo enlaces entre las notas. Estoy pensando seriamente en cambiar mi sistema de nuevo para evitar esta estructura pre-diseñada que tenía, y que ahora veo quizá no es lo mejor, esto lo expandiré en otra entrada.

Sin embargo, fuera del método como tal, mi búsqueda era por el software perfecto para ejecutar mi toma de notas. Mis necesidades son más o menos las siguientes:

  * Evitar usar el mouse.
  * Archivos de texto (control de versiones y _futureproof_)
  * Categorías.
  * Sincronizar ente dispositivos.
  * Agregar notas a mi página.
  * Escribir matemáticas.
  * Citar desde mi base de datos de referencias (Zotero, BibLaTeX).
  * Agregar imágenes y demás archivos.

Y como siempre ningún software puede ser todo para todos, entonces si todas estas cosas no existen por default debería haber la forma de agregar _plugins_ o algo por el estilo.

## Lo que he intentado

Todo esto es sobre todo porque durante el último año he tenido tantos problemas para organizar la información, he intentado de todo, usar papel y lápiz, y termino teniendo un desastre de hojas poco organizado, además el no tener una casa fija me detiene a esto porque realmente no tengo suficiente espacio para tener todo esto organizado y en el momento en que deba mudarme cómo le voy a hacer para mover mis notas, todo se puede perder.

Para evitar el acumular papel he intentado usar Xournal++ o OneNote para mantener notas escritas a mano pero en mi computadora, y uno pensaría que OneNote es suficiente para esto por la forma en que se estructura, pero de entrada la única razón por la que lo uso es porque tengo Windows en la compu de la escuela, y cuando acabe el doctorado esa compu va a regresar a la escuela y yo no voy a usar Windows en una compu personal.

Pero aún así, OneNote es un programa que no me llena en el sentido de que si quiero utilizarlo para escribir algo que pueda utilizar para mi tesis o algún artículo, y dado a que se usa LaTeX para eso, no hay mejor que tener todo en archivos de texto. Además tiene un montón de bugs horribles de los que ni quiero hablar. [Xournal++][9] es el mejor software para notas a mano que he encontrado, quizá en MacOS hay algo mejor y lo que tú quieras, pero no tengo la experiencia por ahí. El problema de Xournal++ es de nuevo que, obvio, no guarda las cosas en archivos de texto el soporte de LaTeX es mejor que en OneNote, pero no como uno quisiera, y en contraste con OneNote, no hay manera de organizar tus notas dentro del programa, claro que puedes tener todo organizado en directorios (lo cual he hecho) pero la verdad es que no es lo mismo, pierdes el flujo de trabajo.

E incluso he intentado usar una wiki, precisamente con Vimwiki, que es un _plugin_ para Vim/Neovim y está súper bien implementado, pero de alguna forma cuando lo intenté usar en el pasado nunca encontré la forma de organizarme con ello, quizá no estaba en el _mindset_ correcto. Sin embargo como comencé a ver tantas cosas respecto al uso de PKM decidí darle otra oportunidad ya que estos métodos típicamente permiten tener archivos de texto, los cuales puedes versionar y tener en un repositorio o cualquier otra forma de almacenamiento que te guste, obvio también con sus problemas, pero ya estaba vendido a la idea.

## Opciones para crear un PKM

Terminé reduciéndome a las siguientes opciones:

  * [Vimwiki][10]

Así es, estaba ahuevado a usar Vimwiki ya que esto permite tener todo el poder de Vim en tus manos e integrarlo con un montón más de cosas que de todos modos ya hago con Vim. Pero de forma más realista hay algunas otras cosas que necesitaba y por eso en realidad mis opciones poco a poco fui descubriendo más software para el mismo propósito y consideré estar abierto a usar los siguientes:

  * [Vimwiki][10] o algún otro plugin por el estilo
  * [Obsidian][3], el cual estaba (y aún estoy) reacio a usar porque no es software libre
  * [Zettlr][11], software libre y muy buena opción

Esto dependiendo de cual probara ser una mejor opción. De tal forma que en lo que sigue voy a explicar mi viaje a través de cada uno y decir en qué casos recomiendo cada uno.

## Vimwiki

Por cierto que mencioné usar ya sea este o algún otro plugin similar, en particular los otros que considero son:

  * [wiki.vim][12] --- inspirado en Vimwiki pero realmente esta hecho _from scratch_, una ventaja ante Vimwiki es el uso de Pandoc para convertir archivos a otros formatos, mientras que Vimwiki puede únicamente convertir a HTML si y sólo si estás usando su sintaxis, entonces puedes usar Markdown (a continuación hablo de eso).
  * [Waikiki][13] --- inspirado en Vimwiki pero sin muchas de las características porque el autor decidió que no necesitaba todo lo que Vimwiki ofrece, honestamente creo que voy a pasarme a usar Waikiki porque en ocasiones puedo querer usar Vim para editar esto.

Pero vamos a Vimwiki, ya agregué el link varias veces pero aquí esta una vez más por si lo quieres calar: [https://vimwiki.github.io/][10]. Qué puedo decir de Vimwiki, es un plugin maravilloso.

### Las características

Es lo que he usado más, a continuación una lista de algunas de las características:

  * Tiene una sintaxis propia, los archivos tienen extensión `.wiki`.
  * _Tab_ para saltar entre los links.
  * _Enter_ para seguir links.
  * Exportar a HTML con toda la estructura de tu wiki (directorios) de tal forma que puedes hacer una página web.
  * Soporte de matemáticas (LaTeX), pero obvio Vim no puede pre-visualizarlas entonces para esto debes mandarlo a HTML y usar MathJax, lo cual no es tan malo (es como cuando escribes algo en LaTeX y lo quieres estar visualizando a cada rato **porque no le sabes**), además con conceal puedes ver más o menos lo que escribes.
  * Etiquetas para filtrado.
  * Los links a archivos son de verdad, nada de usar alguna solución escondida para buscarlos, los estoy viendo Zettlr y Obsidian, tienes la opción de decorarlos obviamente, y con el conceal de vim los escondes.
  * TODO EL PODER DE VIM

### El problema

Sin embargo anteriormente dije que terminé usando Obsidian, ¿porque si me gusta Vimwiki no estoy usándolo? Bueno el problema es que la sintaxis es única y no es muy usada fuera de Vim, y aunque es tan rica como Markdown (o incluso más), el hecho de que no sea tan usada hace que existan pocas soluciones para algo fuera de Vim. Puede utilizar Markdown de hecho, pero en ese caso no podrás exportar a HTML lo que estás haciendo, la exportación a HTML solamente es soportada con la sintaxis de Vimwiki.  
Y como menciono, aunque la solución para ver lo que escribes en mates está _okey_, sigue interrumpiendo tu flujo de trabajo y no hay como tener algo que te muestre lo que escribes en tiempo real como Zettlr y Obsidian.

Otra cosa es que la integración con tu base de datos de referencias obvio no esta hecha desde el plugin, claro que puedes integrarla con Vim y listo, pero yo lo que quisiera es una forma de citar dentro de mi escrito de alguna manera, es decir en cada página de la wiki quiero tener una lista de referencias al final o bien una forma de ir rápidamente a saber qué diablos estoy citando, lo cual estaba haciendo literal copiando y pegando desde Zotero, como si estuviéramos en el pinche siglo XVII.  
Entonces esto no esta tan ideal.

Dado que estas dos cosas son una parte gigante de lo que hago actualmente, no puedo tener soluciones sub-óptimas para ello, de hecho si tengo tantas cosas en mi camino para hacer notas para el doctorado esto me afectaría gravemente en mi desempeño y no queremos eso.  
Por lo tanto Vimwiki no puedo usarlo, al menos para notas del doctorado que se traten de matemáticas.

Otra cosa que en ocasiones necesito es agregar imágenes a mi texto (gráficas y así) y obvio Vim no sirve para esto porque pues es en la terminal, y aunque según sé hay terminales que te permiten ver imágenes, como _kitty_, aún no estoy preparado para configurarme eso.

### Cuándo usar Vimwiki

Aún cuando Vimwiki no será mi principal herramienta de toma de notas, creo que tiene muchas características que hacen tu vida muy sencilla **si eres un usuario de Vim**.

Entonces yo pienso usar Vimwiki (o Waikiki), para notas sobre otras cosas que no envuelvan matemáticas. Al final del día en mi wiki también guardo mis notas de lecturas, programación, y cualquier otra cosa que vaya aprendiendo en mi vida. Por lo que únicamente el doctorado no lo puedo manejar con Vimwiki.

Recuerda que la idea de usar Markdown, es poder leerlo así como está, en particular con las capacidades de conceal de Vim tienes para leer la mayoría de lo que escribes en Markdown sin ningún problema.

## Zettlr

Dejo de nuevo el link por aquí, sobre todo si puede ser de utilidad para ti: [https://www.zettlr.com/][11].

Zettlr es un software muy poderoso para editar archivos de Markdown y tiene casi todas las características que Obsidian tiene y más, y como es software libre obvio era lo que pensaba usar cuando vi que Vimwiki no iba a ser una buena solución.

### Las características

  * Evitar usar el mouse.
  * Archivos de texto (control de versiones y _futureproof_)
  * Categorías.
  * Sincronizar ente dispositivos.
  * Escribir matemáticas.
  * Citar desde mi base de datos de referencias (Zotero, BibLaTeX).
  * Agregar imágenes y demás archivos.

Sí, adivinaste, la lista de arriba es exactamente la misma que puse más arriba sobre mis necesidades para mi sistema excepto por una cosa (la encontraste), pero aún así no estoy usando Zettlr, ¿por qué? Bueno, primero permite que te explique porque es que cumple todo

  * Tiene modo Vim (debes usar el mouse pero solamente para interactuar con le resto de la GUI, y además tiene shortcuts)
  * Es un editor de Markdown.
  * Soporta etiquetas, carpetas y demás.
  * De nuevo, es un editor de Markdown entonces la sincronización la llevo a cabo con _git_.
  * Puedes pre-visualizar matemáticas.
  * Integración directa con Zotero.
  * Puedes ver otros archivos de cualquier tipo e incluirlos.

### El problema

¿Sí viste lo que falta? Falta poder incluirlo en mi página. Zettlr puede exportar tus archivos a cualquier formato que quieras porque utiliza _Pandoc_ y eso está muy bien, sin embargo la forma en que los exporta es la siguiente:

Imagina que esta es la estructura de tu directorio

    directorio
    |
    |__archivo1.md
    |__archivo2.md
    |
    |__subdirectorio1
    |  |__archivo11.md
    |
    |__subdirectorio2
       |__archivo21.md
       |__archivo22.md

Zettlr va a convertir esta estructura en un vector aplanado que te muestre los archivos en ese orden, de forma que tendrás un arreglo

`archivo1.md, archivo2.md, archivo11.md, archivo21.md, archivo22.md]`

Y luego va a concatenar todos esos archivos en un solo archivo del tipo al que quieras exportar tu trabajo.

Esta solución no es mala, de hecho está excelente, si estás escribiendo un libro o un artículo. Pero mis notas no son para eso, mis notas son para mí y para ponerlas en mi sitio web. De forma que yo lo que quiero es una forma de exportar todas mis notas y que se respete la estructura de directorios, y se cree es estructura.

Otro problema es la forma en que maneja los links, esta sí me dio mucho asco. Zettlr tiene una forma excelente de buscar los archivos en tu directorio, de forma que simplemente tecleas `[[` y te ofrece los archivos a usar, igualito que Obsidian. El problema es que no puede usar las rutas verdaderas de los archivos, si las usas se queda bien pendejo y no puede encontrarte nada. Otro problema es que para manejar links internos no puedes utilizar links de Markdown, es decir los `[descripción](link.a.algo)`.

  
Estos son exclusivamente para cosas externas, de forma que si quieres utilizar Zettlr para abrirlos, debes establecer Zettlr como tu programa predeterminado para abrir archivos `.md`, lo cual definitivamente no es una opción, además de que si sí lo haces literal lo que vas a hacer es lanzar Zettlr de nuevo y tomando en cuenta que usa _eLEcTrOn_ puede que no sea la idea más sensible. Los links internos deben ser _wikilinks_, es decir `[[link.interno|descripción]]` lo cual no es estándar en Markdown y si no utilizas Zettlr para exportar (que ya vimos que en mi caso no es una opción) va a ser un pedo.

### Cuando usar Zettlr

Aún cuando acabo de decir que Zettlr es una pendejada (y si ves mis _commits_) concluirías lo mismo, considero que Zettlr es un programa súper cabrón y que si no fuera porque no he jugado tanto con él quizá ya hubiera encontrado la forma de evitar estos problemas que encontré, pero bueno, necesitaba una solución rápida, no puedo dejar de trabajar nomás porque no estoy contento con el software.

Dicho eso, yo recomiendo usar Zettlr en dos casos principales:

  * Estas haciendo un proyecto, escribiendo un libro, un artículo y solamente necesitas al final exportar eso a PDF o cualquier otra cosa. Aquí realmente brilla, porque se integra con Zotero, puedes usar Markdown o LaTeX, al final exportar y todo se queda junto.
  * Quieres hacer un Zettelkasten, de hecho tienen por ahí unas guías para ello:
  * [Guide Zettelkasten][6]
  * [Zettelkasten Method][14]
  * [WTF is a Zettelkasten?][15]

## Obsidian

Obsidian es software de propietario, pero debo reconocer que hasta el momento es la mejor herramienta para mi caso de uso, por aquí te dejo el link: [https://obsidian.md/][3].

Yo suelo usar software libre tanto como puedo, pero también creo que hay que ser tan ecléctico como se pueda, en ocasiones las mejores herramientas son de propietario y no tiene sentido hacerse la vida difícil por querer adherirse a ciertos principios. Me cuesta muchísimo trabajo, pero es una forma más inteligente de trabajar.

### Las características

Esencialmente tiene exactamente las mismas características de Zettlr excepto por la integración con Zotero. También es una pendejada para exportar a HTML.

Tiene cantidad de plugins para hacer cosas, pero no uso mas que tres al momento:

  * [obsidian-consistent-attachment-and-links][16] --- mantiene consistencia con los links, es decir evita que obsidian use sus métodos de búsqueda para los links y te permite tener las rutas completas, y evita el uso de _wikilinks_
  * [quick\_latex\_obsidian][17] --- provee algunos snippets para usar LaTeX, tipo _UltiSnips_
  * [obsidian-citation-plugin][18] --- integra Obsidian con tu base de datos de referencia, lo hace de una manera muy especial que pensé al inicio que no me serviría pero en realidad considero que es muy útil

Aunque los plugins son bien útiles, la verdad es que no estoy seguro si me quedaré con Obsidian, no quiero modificar mi forma de trabajar alrededor de Obsidian. Simplemente no me gusta confiar en que Obsidian siempre estará ahí, porque es de propietario y muchos intereses se mueven alrededor del dinero, por lo que en cualquier momento se puede convertir en _shitware_

Pero en general Obsidian, es un programa muy chingón, tiene shortcuts sensibles, modo Vim, la pre-visualización de mates e imágenes está preciosa (_chef kiss_), el plugin para mates es muy similar a _UltiSnips_ aunque según entiendo no puedes agregar más snippets (puedo estar equivocado), y puedes hacer que se comporte exactamente como quieras con los plugins.

### El problema

Me duele en el _cora_ tener que usar software de propietario, pero es lo mejor hasta el momento.

Además los plugins son bien dañinos si en algún momento quiero cambiarme (y de hecho es el plan) a Zettlr, porque entonces todas las herramientas que utilice ahí no se van a traducir a Zettlr. Es por eso que solamente estoy utilizando unos cuantos que de hecho no cambian mucho mi flujo de trabajo y únicamente ayudan a mantener consistencia en los archivos.

### Cuándo usar Obsidian

Bueno, pues aparentemente en mi caso. Y en general es una opción muy buena para comenzar con esta onda de los PKM, porque la raza que usa Obsidian está obsesionada con esto y hay muchísimo contenido para aprender, muchísimos tipos de flujos de trabajo que puedes adaptar.

## Conclusión

Continuaré usando Obsidian en conjunto con Vimwiki, y calando Zettlr para ver si puedo evitar las cosas que no me gustaron y cambiarme completamente a Zettlr.

En particular creo que continuaré usando Zettlr en caso de que quiera escribir algún artículo o algo por el estilo, la verdad esa funcionalidad me gustó mucho, y la forma en que se integra con Zotero está bellísima.

Aún debo encontrar una manera de exportar mis notas a HTML, y lo que seguramente voy a hacer es un script con Pandoc o bien usar [pyssg][19], y cuando tenga eso y si encuentro una forma de evitar el manejo terrible que tiene Zettlr con los links, seguro me pasaré a usar Zettlr porque la neta estoy mucho más cómodo usando software libre.

 [1]: https://www.luevano.xyz/
 [2]: https://joplinapp.org/
 [3]: https://obsidian.md/
 [4]: https://es.wikipedia.org/wiki/Zettelkasten
 [5]: https://zettelkasten.de/
 [6]: https://docs.zettlr.com/en/guides/guide-zettelkasten/
 [7]: https://forum.obsidian.md/t/obsidian-zettelkasten/1999
 [8]: https://www.youtube.com/results?search_query=bryan+jenks+%26%26+obsidian
 [9]: https://xournalpp.github.io/
 [10]: https://vimwiki.github.io/
 [11]: https://www.zettlr.com/
 [12]: https://github.com/lervag/wiki.vim
 [13]: https://github.com/fcpg/vim-waikiki
 [14]: https://docs.zettlr.com/en/academic/zkn-method/
 [15]: https://www.zettlr.com/post/what-is-a-zettelkasten
 [16]: https://github.com/dy-sh/obsidian-consistent-attachments-and-links
 [17]: https://github.com/joeyuping/quick_latex_obsidian
 [18]: https://github.com/hans/obsidian-citation-plugin
 [19]: https://github.com/luevano/pyssg
