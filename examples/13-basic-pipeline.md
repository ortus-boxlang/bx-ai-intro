# BoxLang AI Pipelines

## Purpose

Pipelines are a fluent way to chain AI operations together in sequence. Instead of calling multiple functions and managing intermediate results, pipelines enable composable, readable chains of operations that flow from input to output.

## When to Use

- **Data transformation flows**: Process AI responses through multiple transformations
- **Multi-step AI operations**: Chain models, tools, and data processing together
- **Reusable workflows**: Build once, use anywhere with the fluent API
- **Complex logic**: Combine different AI components (models, tools, memory, transformers) into a single expression

Each step can modify data, validate it, transform it, or trigger side effects before passing control to the next step.  You can make it simple or complex as needed, and the fluent API keeps it readable.

## Execution Sequence

```
┌─────────────────────────────────────────────────────────────────┐
  │ Pipeline Execution Flow                                          │
└─────────────────────────────────────────────────────────────────┘

1. Create Message
   └─→ aiMessage( "Your prompt" )
        └─→ add system/user messages with .system(), .user()

2. Convert to Model
   └─→ .toDefaultModel()  OR  .to( aiModel( "openai" ) )
        └─→ Creates AiModel runnable with AI provider

3. Add Options (optional)
   └─→ .addTools( [ tool1, tool2 ] )
   └─→ .configure( params )

4. Chain Transformers (optional)
   └─→ .to( aiTransform( "json" ) )
   └─→ .to( customTransformer )
   └─→ .to( lambda => transform(lambda) )

5. Execute Pipeline
   └─→ .run()                              [sync, return result]
       .stream( chunk => {...} )           [async, stream chunks]
       .run( returnFormat: new Class() )   [structured output]

6. Output
   └─→ Raw string, parsed JSON, typed object, or stream
```

## Runnable Sequence

A pipeline is a sequence of runnable objects that are executed in order. Each runnable takes the output of the previous one as its input, allowing you to build complex workflows with clear data flow.  This is represented by the `AiRunnableSequence` class, which manages the execution of the chain.

Once you create the first sequence object by calling a `to(), pipe(), toModel(), toDefaultModel()` it will create the first sequence. You can then chain additional runnables to that sequence. When you call `run()` on the sequence, it will execute all the runnables in order, passing the output of each as the input to the next.

## Runnable Objects

Objects that implement `IAiRunnable` can be chained in pipelines. They have these core methods:

- **`run( input, params )`** – Execute synchronously and return result
- **`stream( callback, input, params )`** – Stream results chunk-by-chunk
- **`to( next ), pipe( next )`** – Chain to the next runnable in the pipeline

They also have all the methods of their specific type (e.g. `AiModel`, `AiTransformRunnable`, etc.) for configuration and chaining, plus all the `AiBaseRunnable` methods.

### Built-in Runnables

- **`AiMessage`**
- **`AiModel`**
- **`AiTransformRunnable`**
- **`Tool`**
- **`AiAgent`**
- **`AiRunnableSequence`**

## Common Methods

### Creating Runnables

```java
aiMessage()        // Start with a message
aiModel()             // Start with a model
aiAgent() 			  // Start with an agent
```

### Pipeline Methods

```java
.to( ANY RUNNABLE ) 			   // Chain to another runnable
.pipe( ANY RUNNABLE ) 			   // Alias for .to()
.toModel( aiModel() ) 				// Chain to a model of your choice
.toDefaultModel() 				// Chain to the default model
.transform( closure/lambda, class name, instance ) // Chain to a custom transformation function or class
```

### Metadata, Params, and Options

```java
withName( name ) 				   // Name the runnable for debugging
getName() 					   // Get the name of the runnable
withParams( params ) 				   // Add custom parameters to the runnable
getMergedParams( params ) 				   // Get merged parameters from the runnable and pipeline
clearParams() 					   // Clear custom parameters
withOptions( options ) 				   // Add custom options to the runnable
getMergedOptions( options ) 				   // Get merged options from the runnable and pipeline
clearOptions() 					   // Clear custom options
```

### Return Formats

```java
singleMessage() 				   // Return a single message object
allMessages() 					   // Return all messages in the sequence
asJson() 					   // Return output as JSON string
asXml() 					   // Return output as XML string
rawResponse() 				   // Return raw response from the model
structuredOutput( schema ) 				   // Parse output into an instance of the specified schema
schema( schema ) 				   // Alias for structuredOutput()
```

### Execution

```java
.run( input, params, options )                           // Execute and return result
.stream( chunk => { ... }, input, params, options )      // Stream with callback
```
