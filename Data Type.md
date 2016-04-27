# Data Type

## The new _logic_ type
* In Verilog, `reg` can be synthesized to either net or register.
* SystemVerilog re-defines `reg` as `logic`, a 4-state type. `reg` is replaced by `var logic`. `var` is optional.

|Verilog|SV(Full)|SV(Default)|
|:---:|:---:|:---:|
|`reg foo`|`var logic foo`|`logic foo`|
|`wire foo`|`wire logic foo`|`wire foo`|

* A new 2-state type is `bit`.

## Data type rules

### Verilog rules
* Variables (`integer`, `real`,`reg`,`time`) are assigned in procedural blocks while nets are assigned continuously.
* Module inputs are always nets, outputs are variables if they are manipulated in procedural blocks, otherwise are nets.
* Connections to the outputs are always nets, those to the inputs are variables  if they are manipulated in procedural blocks, otherwise are nets.
* Connections to inout ports are always nets.

### SV rules
* Variables can be assigned by all sorts of styles, thus `logic foo` can be used to replace `reg foo` and `wire foo`.
* Only nets can have multiple drivers. Variables cannot be driven by different types of drivers (procedural assignments, continuous assignments, and output ports).
* Variables cannot be driven by multiple continuous assignments or output ports. In procedural blocks, `always_comb` (an `always` block that should synthesize to combinational logic) does not allow multiple driver on variables either.

## 2-state vs 4-state
* 2-state `bit` inintilize to 0, while 4-state `logic` initilize to X.
* Assigning 4-state to 2-state converts X (not yet assigned) and Z (not driven, declared but never assigned) to 0.
* 4-state is recommended in RTL design, while 2-state can be useful in test bench. 

## Assignment issues

bookmark: p38