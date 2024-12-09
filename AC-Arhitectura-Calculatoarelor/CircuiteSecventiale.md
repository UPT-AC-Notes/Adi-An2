```verilog
// flip flop
module d_ff (
    input clk,       // intrare tact
    input rst_b,     // intrare reset, activeaza iesirea la 0
    input set_b,     // intrare set, activeaza iesirea la 1
    input d,         // intrare sincrona de date
    output reg q     // iesire bistabil
);

always @ (posedge clk or negedge rst_b or negedge set_b) begin
    if (!set_b) 
        q <= 1; 
    else if (!rst_b) 
        q <= 0;  
    else 
        q <= d; 
end

endmodule
```

```verilog
// Latch SR
module sr_latch (
    input rst_b,     // intrare reset, activeaza iesirea la 0
    input set_b,     // intrare set, activeaza iesirea la 1
    output reg q     // iesire latch
);

always @(*) begin
    if (!set_b)
        q = 1;       // Activeaza iesirea la 1
    else if (!rst_b)
        q = 0;       // Activeaza iesirea la 0
    // altfel iesirea ramane neschimbata
end

endmodule
```

```verilog
module shift_register (
    input clk,
    input rst_b,
    input d,
    output reg [3:0] q // iesire cu 4 biti
);

always @(posedge clk or negedge rst_b) begin
    if (!rst_b)
        q <= 4'b0000;  // Reset la 0
    else
        q <= {q[2:0], d};  // Deplasare la dreapta
end

endmodule

```

```verilog
module binary_counter (
    input clk,
    input rst_b,
    output reg [3:0] count // contor pe 4 biti
);

always @(posedge clk or negedge rst_b) begin
    if (!rst_b)
        count <= 4'b0000; // Reset la 0
    else
        count <= count + 1; // Incrementare
end

endmodule

```

```verilog
// multiplexor
module mux_d_ff (
    input clk,
    input rst_b,
    input sel,       // Selector
    input d1,        // Intrare 1
    input d2,        // Intrare 2
    output reg q     // Iesire
);

always @(posedge clk or negedge rst_b) begin
    if (!rst_b)
        q <= 0;     // Reset la 0
    else
        q <= sel ? d1 : d2;  // Selecteaza intre d1 si d2
end

endmodule

```

```verilog
// finite state machine
module fsm_example (
    input clk,
    input rst_b,
    input in,           // Intrare FSM
    output reg state    // Starea curentă
);

parameter S0 = 1'b0, S1 = 1'b1;

always @(posedge clk or negedge rst_b) begin
    if (!rst_b)
        state <= S0;    // Stare inițială
    else begin
        case (state)
            S0: state <= in ? S1 : S0; // Trecere la S1 dacă `in` este 1
            S1: state <= in ? S1 : S0; // Trecere la S0 dacă `in` este 0
        endcase
    end
end

endmodule

```
