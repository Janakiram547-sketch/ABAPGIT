# Where do we close brackets?

The question whether we close opening brackets at the end of the same line or after a break in the next line has been open for a long time and never discussed in depth.
This list demonstrates how the two styles layout different statements 

## Simple calls

No difference for simple calls with no or exactly one parameter:

```ABAP
method( ).
method( 42 ).
method( input = 42 ).
method( CHANGING result = 42 ).
```

## Returning, object, and interface

Also no difference when assigning the returning value and adding object and interface:

```ABAP
result = method( input = 42 ).
result = object->method( input = 42 ).
result = object->interface~method( input = 42 ).
``` 

## Multiple parameters

Same-line layouts multiple parameters in a block style while new-line adopts the formatting known from JSON:

```ABAP
method( input         = 42
        another_input = 23 ).

method(
  input         = 42
  another_input = 23
).
```

## Direction

Adding directions (IMPORTING, EXPORTING, CHANGING) leads to nearly identical statements:

```ABAP
method(
  EXPORTING
    input  = 42
  IMPORTING
    result = DATA(result) ).

method(
  EXPORTING
    input  = 42
  IMPORTING
    result = DATA(result)
).
```

## Simple chains

For simple method chains, both styles produce the same format:

```ABAP
object->first_method( )->second_method( 42 ).
```

## Verbose chains

For verbose method chains, same-line resorts to the new-line format:  

```ABAP
object->first_method(
  EXPORTING
    input  = 42
  IMPORTING
    result = DATA(result)
)->second_method(
  EXPORTING
    input  = 42
  IMPORTING
    result = DATA(result)
).
```

## Inline VALUE

Inline declarations lead to strong differences.
While same-line produces horizontally long statements, new-line produces vertically long statements: 

```ABAP
DATA(result) = method( input = VALUE #( from = 23
                                        to   = 42 ) ).
                       
DATA(result) = method(
  input = VALUE #(
    from = 23
    to   = 42
  )
).
```

## Multiple VALUEs

With multiple inline VALUEs, the block layout of same-line vs. JSON layout of new-line becomes even more apparent: 

```ABAP
DATA(result) = method( input      = VALUE #( from = 23
                                             to   = 42 )
                       more_input = VALUE type( param = sub_method( ) ) ).

DATA(result) = method(
  input = VALUE #(
    from = 23
    to   = 42
  )
  more_input = VALUE type(
    param = sub_method( )
  )
).
```

## IFs

Same-line condenses methods inlined in IFs, while new-line expands them:

```ABAP
IF is_true( input      = 42
            more_input = 23 ).
  " do something
ENDIF.

IF is_true(
     input      = 42
     more_input = 23
   ).
  " do something
ENDIF.
```

## XSDBOOL

```ABAP
DATA(is_true) = xsdbool( method( input      = 42
                                 more_input = 23 ) = abap_true ).

DATA(is_true) = xsdbool(
  method(
    input      = 42
    more_input = 23
  ) = abap_true
).
```