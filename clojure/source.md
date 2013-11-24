# Thought reading clojure source code

## what is done for clojure.main

RT -> has static block -> call doInit -> load("clojure.core"
                                      -> (in-ns 'user)
                                      -> (:refer 'clojure.core)
                                      -> load("user")
(require "clojure.core")
(invoke "clojure.main/main")

## What is Var and Symbol
