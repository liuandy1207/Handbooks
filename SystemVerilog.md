# SystemVerilog

## Finite State Machine
- synchronous sequential circuit with combination next state and output logic

```systemverilog
module FSM(input logic clk),
           input logic reset, // optional
           output logic out);
  typedef enum logic [1:0] {S0, S1, S2} statetype;
  // defines a two-bit logic value w/ 3 possibilities: S0, S1, S2
  // note: enum. encodings default to increasing numerical in binary
  statetype state, nexstate;    // defines two variables of the custom type statetype

  // state register
  always_ff @(posedge clk, posedge reset)  // asynchronous active-high reset
    if (reset) state <= S0;          // default to S0 on reset
    else       state <= nextstate;   // set to nextstate

  // next state logic
  always_comb
    case (state)
      S0: ...
      S1: ...
      S2: ...
      default: ...
    endcase

  // output logic
  assign ...
endmodule

```
