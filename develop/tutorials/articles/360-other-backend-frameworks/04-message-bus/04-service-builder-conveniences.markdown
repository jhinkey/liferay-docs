

## Service Builder Service Conveniences [](id=service-builder-service-conveniences)

Liferay has integrated some convenience facilities in Service Builder that
leverage the Message Bus, specifically `@Async` and `@Clusterable`.

### @Async Service Method Annotation [](id=async-service-method-annotation)

All Service Builder generated local and remote services (`*Service` and
`*LocalService`) are wrapped with special AOP (aspect-oriented programming)
advice. If you annotate a public method in your local or remote service
implementation with `@Async`, calls to the method are converted to asynchronous method calls.

This lets you quickly implement fire and forget capabilities to your services,
which is especially useful for features such as notifications.

### @Clusterable Service Method Annotation [](id=clusterable-service-method-annotation)

Service Builder service class methods annotated with `@Clusterable` are invoked across the cluster. They use Message Bus and Cluster Link. The annotation can be further qualified with these attributes:

-   `onMaster`: whether to only execute the request if the current 
    portal JVM is holding the cluster wide "master" token

-   `acceptor`: specifies a custom `ClusterInvokeAcceptor` to determine 
    whether the given portal JVM should accept and thus execute the request.

TODO summary or closing sentences
