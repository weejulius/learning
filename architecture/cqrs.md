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
  - it garantee the order of recieving events for each aggregate root in case the events are received disorderly 

#### Event store
  - the events are fetched for one aggregate root only by aggregate id
  - one aggregate root can have snapshot if its events are a lot

## Thinking
   - we may have 3 copy of data, the events and snapshot and view


<Code>

    {:command :task/add-task
    :task/description "task one"
    :sync false ;; is the command waiting for the result
    }

    (defn dispatch-command [command]
      (let [event handle-add-task command]
        (append-to-eventstore event)
        (publish event))

    (defn handle-add-task[command]
    (create-task {}))

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

