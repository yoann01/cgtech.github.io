:maya: :python: By Dhruv Govil

When I write a Python class that exposes the functionality of a Maya node , I override ```py__repr__```  so that it returns the node's path so I can just pass the object to any Maya commands and it just works.

:GitHub: By Thomas Masencal

If you append .patch to a Github commit URL, you get the patch file: https://github.com/KelSolaar/colour/commit/e38b3e706e4e3581dd4e9c7806fe84422abadac2.patch

:maya: By Yantor3d

TIL Maya can't load audio if the file basename starts with a number.
https://twitter.com/yantor3d/status/1433464047278575622

:python: By Lee Dunham

Remember that if you really want to use the nasty from foo import * it is worth considering using the __all__ variable in foo to control what is going to be imported.

https://stackoverflow.com/questions/44834/can-someone-explain-all-in-python/64130#64130

:houdini: By Paul Ambrosiussen

Did you know you can comment one or multiple lines of code in #Houdini using CTRL+/ ? (in the VEXpression editor)

https://twitter.com/ambrosiussen_p/status/1463177572766863374?s=20

:Maya: By Stuart

Maya's internal angular units are radians, even if the settings are set to degrees? And that's why the unitConversion gets added when both input and output are meant to be degrees ?

Confirmed: addAttr -ln "rotTest2"  -at doubleAngle  -dv 0 |nurbsCircle1; and then connecting to a rotate attribute doesn't create an unitConversion node.

https://tech-artists.slack.com/archives/C0AN0KPMZ/p1643739680183619

:Maya: By Mark Jackson

You can have a string of any length but if stored in an UI element and the element is selected, the tring become clamped to 16bit = 32,767 characters.

http://markj3d.blogspot.com/2012/11/maya-string-attr-32k-limit.html

:Houdini: By Richard C Thomas

Hou-ple, Pulling Lops into Sops? Want to grab data using these VEX methods... https://sidefx.com/docs/houdini/solaris/vex.html
Don't forget to use op: ! 
I hope you never know the frustration of the last 2 hours.

```py
string stage = "op:/stage/OUT";
matrix mat = usd_primvar(stage, root, "xformOP:transform", 0);
```

https://twitter.com/DoesCG/status/1502363843208622097


:python: By Thomas Mansencal

Remember that you can use a semi-colon as a "line break" in python. It is super useful to pass commands to the interpreter, e.g. 
```pypython -c “import sys;import pprint;pprint(dir(sys))”```


:GitHub: By Oleksii Holub

GitHub now supports special "warning" and "note" blockquotes for callouts in your markdown content.
```sh
> **Warning**
> Some text
```

https://twitter.com/Tyrrrz/status/1554784140326748161