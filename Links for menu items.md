
Ralf Köster [11:01 AM] 
Is there anywhere some documentation how to use routes? I want to create an entry to a single pages page in a menu. E.g. 
``<li><a href="{{ path('zikulapagesmodule_display_impressum') }}">Impressum</a></li>``
But that is not working :
``An exception has been thrown during the rendering of a template ("Unable to generate a URL for the named route "zikulapagesmodule_display_impressum" as such route does not exist.") in ZikulaOsnabrueckTheme:Include:main_menu.html.twig at line 20.``

What will do the trick?

[11:02] 
I tried several paths but all of them do have the same resul (e.g a "2" instead of impressum)

Ralf Köster [11:09 AM] 
at the moment I will use
``<li><a href="/pages/display/impressum">Impressum</a></li>``
But why did we do it in the above way inside the admin_menu?

kaik [11:14 AM] 
Well route ``'zikulapagesmodule_display_impressum'``  will not exist

Ralf Köster [11:14 AM] 
:simple_smile:

[11:14] 
why not? The page is there

kaik [11:15 AM] 
difference between ``'zikulapagesmodule_display_impressum'``  and ``/pages/display/impressum``

[11:15] 
lets first split second one into bits

[11:15] 
pages - module name

[11:15] 
display - function name

[11:16] 
impressum - is parameter

Ralf Köster [11:16 AM] 
ok understood

kaik [11:16 AM] 
what is hidden is "type" means user

[11:16] 
do old url will look

[11:17] 
``module=pages&type=user&func=display....``

Ralf Köster [11:17 AM] 
yes, that I know

[11:17] 
now route will look like

kaik [11:17 AM] 
``zikulapagesmodule_user_display``

Ralf Köster [11:17 AM] 
and the page itself?

[11:18] 
the parameter

kaik [11:18 AM] 
now the page itself will need to look into pages module just a second

[11:19] 
so display function route annotation look like this ``/display/{urltitle}/{pagenum}``

[11:19] 
so parameters are urltitle and pagenum

[11:20] 
and now all together

Ralf Köster [11:20 AM] 
what is urltitle?

[11:20] 
id?

kaik [11:21 AM] 
impressum

[11:21] 
and all together         ``<li><a href="{{ path('zikulapagesmodule_user_display', {urltitle: page.urltitle}) }}">{{ page.title }}</a></li>``

Ralf Köster [11:21 AM] 
why than pagenum?

kaik [11:22 AM] 
pagenum is well you can have one big page split into small ones and pagenum is small page id

[11:22] 
:simple_smile:

Ralf Köster [11:23 AM] 
``{urltitle: page.urltitle}`` That is unclear for me

kaik [11:23 AM] 
like in word you have .doc document with its name and this name is urltitle  while pages inside document are pagenum

[11:24] 
``{urltitle: page.urltitle}``

[11:24] 
ok so

[11:24] 
``path()`` is twig function

[11:24] 
as you might now inside ``()`` you are passing parameters to path function

[11:25] 
first parameter is actual route you want to use

[11:25] 
and second parameter is paramerters array

[11:25] 
``{'parameter_name': parameter_value}``

Ralf Köster [11:26 AM] 
I am getting more confused :disappointed:
``<li><a href="{{ path('zikulapagesmodule_user_display', 'impressum') }}">Impressum</a></li>``

[11:26] 
would this be right?

[11:26] 
for my menu?

kaik [11:28 AM] 
well you may try it, but I bet more on ``<li><a href="{{ path('zikulapagesmodule_user_display', {urltitle: 'impressum'}) }}">Impressum</a></li>``

Ralf Köster [11:28 AM] 
ah! ok, now I understand what you explained above (hopefully)

[11:29] 
But what is better if I use it this way instead of ``/pages/display/impressum``

kaik [11:32 AM] 
well first one is more flexible I guess you can manipulate parameters in nice manner... I do not use second way that much so I do not know

[11:32] 
its pros and cons

Ralf Köster [11:33 AM] 
ok. Thanks a lot for the short lesson!

[11:33] 
Now I ask myself where we can document this lesson learnt
