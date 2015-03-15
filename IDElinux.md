# Introduction #

Follow this guide:
http://wiki.pinguino.cc/index.php/Linux

- note: you should install python-svn

If you get this error:
```
  File "/home/...../pinguinoX.3rev399/wxgui/editor/dic.py", line 33, in <module>
    if os.name == "posix": date = "/".join([t[3], t[1], t[5]])
IndexError: list index out of range
```
comment lines 33, 34, 35 in /pinguinoX.3rev399/wxgui/editor/dic.py and leave only the last else:
```
#if os.name == "posix": date = "/".join([t[3], t[1], t[5]])
#elif os.name == "nt": date = "/".join([t[2], t[1], t[4]])
#else: date = "dd/mm/aaaa"
date = "dd/mm/aaaa"
```