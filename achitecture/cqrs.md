CQRS ideas
-----------

### Why has read model

* Cons
  * the standalone read model can be used to load balance
  * the read model can have different presentation with the write mode
  * simiply and responsiblity reperation

* Pros
  * need additional model


### What is the flow

                                  ________________________________
                                  |                                ^
    -command- > -command handler- > -aggregate-  > -event > -repository- > -persistence
                                                          > -event bus-  >|
                                                                          |
                       ||control-  < -query - < -view- < -event handler- <|

* what are added
  - event bus
  - command bus
  - event handler
  - view
  - events


### sample

* it does not introduce event sourcing
* the write model and read model is combined, but has their name convention
* the command sent to bus should be valid
* the business rule is important

<Code>

    {:command :add-task
    :task/description "task one"
    }

    ;; the dispatcher garantees the order of event and command
    (defn dispatch-command [command]
    (dispatch-event handle-add-task command))

    (defn handle-add-task[command]
    (save-task (create-task {})))

    (defn create-task [properties]
    (create-event {:event task-added}))

    (defn save-task [event]
    (d/transact event))

    (defn on-task-added [aggregate event]
    (do aggregate event))


    ;;;;;;;;read model line;;;;;;;;;;;;;;

    ;;view update
    (defn on-task-added [aggregate event]
    (create-task-view))

    (defn query [task-view args]
    (do task-view args))

