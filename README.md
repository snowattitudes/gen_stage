# GenStage

GenStage is a specification for exchanging events between producers and consumers. It also provides a mechanism to specify the computational flow between stages.

This project currently provides the following functionality:

  * `Experimental.GenStage` ([docs](https://hexdocs.pm/gen_stage/Experimental.GenStage.html)) - a behaviour for implementing producer and consumer stages

  * `Experimental.Flow` ([docs](https://hexdocs.pm/gen_stage/Experimental.Flow.html)) - `Flow` allows developers to express computations on collections, similar to the `Enum` and `Stream` modules, although computations will be executed in parallel using multiple `GenStage`s

  * `Experimental.DynamicSupervisor` ([docs](https://hexdocs.pm/gen_stage/Experimental.DynamicSupervisor.html)) - a supervisor designed for starting children dynamically. Besides being a replacement for the `:simple_one_for_one` strategy in the regular `Supervisor`, a `DynamicSupervisor` can also be used as a stage consumer, making it straight-forward to spawn a new process for every event in a stage pipeline

The module names are marked as `Experimental` to avoid conflicts as they are meant to be included in future Elixir releases. In your code, you may add `alias Experimental.{DynamicSupervisor, GenStage}` to the top of your files and use the relative names from then on.

You can find examples on how to use the modules above in the [examples](examples) directory:

  * [ProducerConsumer](examples/producer_consumer.exs) - a simple example of setting up a pipeline of `A -> B -> C` stages and having events flowing through

  * [DynamicSupervisor](examples/dynamic_supervisor.exs) - an example of how to use one or more `DynamicSupervisor` as a consumer to a producer that works as a counter

  * [GenEvent](examples/gen_event.exs) - an example of how to use `GenStage` to implement a `GenEvent` replacement that leverages concurrency and provides more flexibility regarding buffer size and back-pressure

## Installation

GenStage requires Elixir v1.3.

  1. Add `:gen_stage` to your list of dependencies in mix.exs:

        def deps do
          [{:gen_stage, "~> 0.4"}]
        end

  2. Ensure `:gen_stage` is started before your application:

        def application do
          [applications: [:gen_stage]]
        end

## Future research

Here is a list of potential topics to be explored by this project (in no particular order or guarantee):

  * Consider using DynamicSupervisor to implement Task.Supervisor (as a consumer)

  * TCP and UDP acceptors as producers

  * Explore different windowing strategies - the ideas behind the Apache Beam project are interesting, specially the mechanism that divides operations between what/where/when/how (1, 2) as well as windowing from the perspective of aggregation (3)

Other research topics include the Titan (4), Naiad's Differential Dataflow engine (5) and Lasp (6).

### Links

  1. https://cloud.google.com/blog/big-data/2016/05/why-apache-beam-a-google-perspective
  2. http://www.vldb.org/pvldb/vol8/p1792-Akidau.pdf
  3. http://www.vldb.org/pvldb/vol8/p702-tangwongsan.pdf
  4. http://asc.di.fct.unl.pt/~nmp/pubs/clouddp-2013.pdf
  5. http://research-srv.microsoft.com/pubs/176693/differentialdataflow.pdf
  6. https://lasp-lang.org/

## License

Same as Elixir.
