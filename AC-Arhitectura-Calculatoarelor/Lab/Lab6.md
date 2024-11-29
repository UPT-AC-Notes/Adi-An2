![](../Images/Lab6Ex1.png)

- ``sadd.v``
```verilog
module sadd(
  input clk, rst_b,
  input x, y,
  output reg out
);
  localparam S0 = 1'b0;
  localparam S1 = 1'b1;
  
  reg st, st_nxt;
  
  always @(*) begin
    case(st)
      S0: 
        if(x & y) st_nxt = S1;
        else st_nxt = S0;
      S1: 
        if((~x) & (~y)) st_nxt = S0;
        else st_nxt = S1; 
    endcase
  end
  
  always @(*) begin
    case(st)
      S0: out = 1;
      S1: out = 0;
    endcase
  end
  
  always @(posedge clk, negedge rst_b)
    if(!rst_b) st <= S0;
    else st <= st_nxt;
  
endmodule

module sadd_tb;
  reg clk, rst_b, x, y;
  wire out;
  
  sadd uut(
    .clk(clk),
    .rst_b(rst_b),
    .x(x),
    .y(y),
    .out(out)
  );
  
  always begin
    #50 clk = ~clk;
  end
  
  initial begin
    clk = 0;
    rst_b = 0;
    x = 0;
    y=1;
    
    #25 rst_b = 1;
    
    
    #100 x = 1;
    #100 y = 0;
    #100 x = 0;
    
    
  end
  
endmodule
```