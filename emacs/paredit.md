#Paredit mode

##auto pair

| key     | function                        | usage                                                                                                            | example                                        |
| (       | paredit-open-round              | make close parenthese                                                                                            | (a\b)=> (a () b)                               |
| )       | paredit-close-round-and-newline | go to new line from a parenthese pair                                                                            | (a\b)=> (a\b)\n                                |
| M-      | paredit-close-round             | go out from pair                                                                                                 | (a\b)=> (ab)\                                  |
| [       | paredit-open-spuare             | make spuare pair                                                                                                 |                                                |
| ]       | paredit-close-spaure            |                                                                                                                  |                                                |
| "       | paredit-doublequote             |                                                                                                                  |                                                |
| M-"     | paredit-meta-doublequote        | 1. make double quote for words(no double quote)2.(have double quote)move the words after close quote to new line | 1.\(abc)=> "\(abc)" 2. "a\bc" efg=> "abc"\nefg |
| M-;     | paredit-comment-dwim            |                                                                                                                  |                                                |
| C-j     | paredit-newline                 |                                                                                                                  |                                                |
| C-d     | paredit-forward-delete          |                                                                                                                  |                                                |


s(a)
