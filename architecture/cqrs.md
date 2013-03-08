CQRS ideas
-----------

### Why has read model

* Pros
  * the standalone read model can be used to load balance
  * the read model can have different presentation with the write mode
  * simipfy and break down the responsiblity

* Cons
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
  _ event store
  - event handler
  - view
  - events


### Sample

* the command sent to bus should be valid
* the validation reads from read model
* the business rule is important

#### Command bus
  - it can send the command asynchroniously or synchroniously

#### Event bus
  - it can resent the failed event

#### Event store
  - the events are stored by aggregate id
  - the events can have snapshot if events are a lot

## Thinking
   - we may have 3 copy of data, the events and snapshot and view


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

