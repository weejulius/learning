Zsh learning
------------

## Tips

* replace path, for example, replace /usr/bin/java to /usr/share/java
  - **cd** bin share

* global aliases
  - aliase **-g** gp='|grep -i' eg. ps ax gp java => ps ax|grep -i java

* extended globbing
  - \*\*/=recursive eg. ls -l \*\*/*.log

* env settings editing
  - eg. vared PATH

* rename
  - firstly autoload -U zmv, and then use zmv. eg. zmv '(*).txt' '$1.html'


