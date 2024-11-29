<<<<<<< HEAD
![](../Images/Lab4Ex1.png)
![](../Images/Lab4Ex2.png)

- ``fac.v``
```verilog
module fac (
    input x,    // Intrarea x
    input y,    // Intrarea y
    input ci,   // Carry in
    output z,   // Suma
    output co   // Carry out
);

    assign z = x ^ y ^ ci;

    assign co = (x & y) | (x & ci) | (y & ci);

endmodule

module fac_tb;
    reg x, y, ci;
    wire z, co;

    fac uut (
        .x(x),
        .y(y),
        .ci(ci),
        .z(z),
        .co(co)
    );

    initial begin
        $monitor("x=%b, y=%b, ci=%b -> z=%b, co=%b", x, y, ci, z, co);

        x = 0; y = 0; ci = 0;
        #10; 

        x = 0; y = 0; ci = 1;
        #10;

        x = 0; y = 1; ci = 0;
        #10;

        x = 0; y = 1; ci = 1;
        #10;

        x = 1; y = 0; ci = 0;
        #10;

        x = 1; y = 0; ci = 1;
        #10;

        x = 1; y = 1; ci = 0;
        #10;

        x = 1; y = 1; ci = 1;
        #10;

    end
endmodule

```

- ``run_fac.txt``
```txt
# add all Verilog source files, separated by spaces
set sourcefiles {fac.v}

# set name of the top module
set topmodule fac_tb

###################################################
#####DO NOT MODIFY THE SCRIPT BELLOW THIS LINE#####
###################################################

# quit current simulation if any
quit -sim

# empty the work library if present
if [file exists "work"] {vdel -all}
#create a new work library
vlib work

# run the compiler
if [catch "eval vlog $sourcefiles"] {
    puts "correct the compilation errors"
    return
}

vsim -voptargs=+acc $topmodule

run -all
quit -sim

```


![](../Images/Lab4Ex3.png)

- ``add2b.v``
```verilog
module add2b (
    input [1:0] x,
    input [1:0] y,
    input ci,
    output [1:0] o,
    output co
);

    wire c1;

    fac fa0 (
        .x(x[0]),
        .y(y[0]),
        .ci(ci),
        .z(o[0]),
        .co(c1)
    );

    fac fa1 (
        .x(x[1]),
        .y(y[1]),
        .ci(c1),
        .z(o[1]),
        .co(co)
    );

endmodule
module add2b_tb;

    reg [1:0] x, y;
    reg ci;
    wire [1:0] o;
    wire co;

    add2b uut (
        .x(x),
        .y(y),
        .ci(ci),
        .o(o),
        .co(co)
    );

    initial begin
        $monitor("x=%b, y=%b, ci=%b -> o=%b, co=%b", x, y, ci, o, co);

        // carry = 0
        x = 2'b00; y = 2'b00; ci = 1'b0; #10;
        x = 2'b00; y = 2'b01; ci = 1'b0; #10;
        x = 2'b00; y = 2'b10; ci = 1'b0; #10;
        x = 2'b00; y = 2'b11; ci = 1'b0; #10;
        x = 2'b01; y = 2'b00; ci = 1'b0; #10;
        x = 2'b01; y = 2'b01; ci = 1'b0; #10;
        x = 2'b01; y = 2'b10; ci = 1'b0; #10;
        x = 2'b01; y = 2'b11; ci = 1'b0; #10;
        x = 2'b10; y = 2'b00; ci = 1'b0; #10;
        x = 2'b10; y = 2'b01; ci = 1'b0; #10;
        x = 2'b10; y = 2'b10; ci = 1'b0; #10;
        x = 2'b10; y = 2'b11; ci = 1'b0; #10;
        x = 2'b11; y = 2'b00; ci = 1'b0; #10;
        x = 2'b11; y = 2'b01; ci = 1'b0; #10;
        x = 2'b11; y = 2'b10; ci = 1'b0; #10;
        x = 2'b11; y = 2'b11; ci = 1'b0; #10;

        // carry = 1
        x = 2'b00; y = 2'b00; ci = 1'b1; #10;
        x = 2'b00; y = 2'b01; ci = 1'b1; #10;
        x = 2'b00; y = 2'b10; ci = 1'b1; #10;
        x = 2'b00; y = 2'b11; ci = 1'b1; #10;
        x = 2'b01; y = 2'b00; ci = 1'b1; #10;
        x = 2'b01; y = 2'b01; ci = 1'b1; #10;
        x = 2'b01; y = 2'b10; ci = 1'b1; #10;
        x = 2'b01; y = 2'b11; ci = 1'b1; #10;
        x = 2'b10; y = 2'b00; ci = 1'b1; #10;
        x = 2'b10; y = 2'b01; ci = 1'b1; #10;
        x = 2'b10; y = 2'b10; ci = 1'b1; #10;
        x = 2'b10; y = 2'b11; ci = 1'b1; #10;
        x = 2'b11; y = 2'b00; ci = 1'b1; #10;
        x = 2'b11; y = 2'b01; ci = 1'b1; #10;
        x = 2'b11; y = 2'b10; ci = 1'b1; #10;
        x = 2'b11; y = 2'b11; ci = 1'b1; #10;

    end

endmodule
```

- ``run_add2b.txt``
```txt

# add all Verilog source files, separated by spaces
set sourcefiles {add2b.v fac.v}

# set name of the top module
set topmodule add2b_tb

###################################################
#####DO NOT MODIFY THE SCRIPT BELLOW THIS LINE#####
###################################################

# quit current simulation if any
quit -sim

# empty the work library if present
if [file exists "work"] {vdel -all}
#create a new work library
vlib work

# run the compiler
if [catch "eval vlog $sourcefiles"] {
    puts "correct the compilation errors"
    return
}

vsim -voptargs=+acc $topmodule

run -all
quit -sim

```


![](../Images/Lab4Ex4.png)

- ``cmp2b.v``
```verilog
module cmp2b(
  input [1:0] x,
  input [1:0] y,
  output eq,
  output lt,
  output gt
);
  assign eq = x == y;
  assign lt = x < y;
  assign gt = x > y;
  
endmodule

module cmp2b_tb;
  reg [1:0] x, y;
  wire eq, lt, gt;
  
  cmp2b uut(
    .x(x),
    .y(y),
    .eq(eq),
    .lt(lt),
    .gt(gt)
  );
  
  initial begin
    $monitor("x=%b, y=%b -> lt=%b, eq=%b, gt=%b", x, y, lt, eq, gt);
    x=2'b00; y=2'b00; #10;
    x=2'b01; y=2'b00; #10;
    x=2'b01; y=2'b01; #10;
    x=2'b01; y=2'b10; #10;
  end
endmodule
```

- ``run_cmp2.txt``
```txt

# add all Verilog source files, separated by spaces
set sourcefiles {cmp2b.v}

# set name of the top module
set topmodule cmp2b_tb

###################################################
#####DO NOT MODIFY THE SCRIPT BELLOW THIS LINE#####
###################################################

# quit current simulation if any
quit -sim

# empty the work library if present
if [file exists "work"] {vdel -all}
#create a new work library
vlib work

# run the compiler
if [catch "eval vlog $sourcefiles"] {
    puts "correct the compilation errors"
    return
}

vsim -voptargs=+acc $topmodule

run -all
quit -sim

```

![](../Images/Lab4Ex5.png)

- ``cmp4b.v``
```verilog
module cmp4b(
    input [3:0] x,
    input [3:0] y,
    output reg eq, 
    output reg lt, 
    output reg gt
);
    wire eq1, lt1, gt1, eq2, lt2, gt2;

    cmp2b cmp0(
        .x(x[3:2]), 
        .y(y[3:2]), 
        .eq(eq1), 
        .lt(lt1), 
        .gt(gt1)
    );
    cmp2b cmp1(
        .x(x[1:0]), 
        .y(y[1:0]), 
        .eq(eq2), 
        .lt(lt2), 
        .gt(gt2)
    );

    always @(*) begin
        if (eq1 && eq2) begin
            eq = 1;
            lt = 0;
            gt = 0;
        end else begin
            eq = 0;
            if (eq1 && lt2) begin
                lt = 1;
                gt = 0;
            end else if (eq1 && gt2) begin
                lt = 0;
                gt = 1;
            end else if (lt1) begin
                lt = 1;
                gt = 0;
            end else if (gt1) begin
                lt = 0;
                gt = 1;
            end
        end
    end

endmodule
```

- ``run_cmp4b.txt``
```txt

# add all Verilog source files, separated by spaces
set sourcefiles {cmp4b.v cmp2b.v}

# set name of the top module
set topmodule cmp4b_tb

###################################################
#####DO NOT MODIFY THE SCRIPT BELLOW THIS LINE#####
###################################################

# quit current simulation if any
quit -sim

# empty the work library if present
if [file exists "work"] {vdel -all}
#create a new work library
vlib work

# run the compiler
if [catch "eval vlog $sourcefiles"] {
    puts "correct the compilation errors"
    return
}

vsim -voptargs=+acc $topmodule

run -all
quit -sim

```
=======
![](../Images/ExLab4.png)

- ``Lab4/Remorca.java``
```java
package Lab4;
public class Remorca{
    private int nrCutii;
    private static int nrCutiiAnterioare = 0;
    private String nrInmatriculare;

    public int getNrCutii(){
		return nrCutii;
    }

    public String getNrInmatriculare(){
		return nrInmatriculare;
    }
    
    public Remorca(int nrCutii, String nrInmatriculare){
		this.nrCutii = nrCutii;
		nrCutiiAnterioare = nrCutii;
		this.nrInmatriculare = nrInmatriculare;
    }

    public Remorca(String nrInmatriculare){
		this.nrInmatriculare = nrInmatriculare;
		nrCutii = nrCutiiAnterioare == 0 ? 10 : nrCutiiAnterioare + 1;
		nrCutiiAnterioare = nrCutii;
    }
}

```

- ``Lab4/Tir.java``
```java
package Lab4;
public class Tir{
    private Remorca[] remorci;
    private int nrRemorci;
    private final int NR_MAX_REMORCI = 5;

    public int getNrRemorci(){
		return nrRemorci;
    }

    public Remorca[] getRemorci(){
		return remorci;
    }
    
    public Tir(){
		nrRemorci = 0;
		remorci = new Remorca[NR_MAX_REMORCI];
    }

    public boolean adaugaRemorca(int nrCutii, String nrInmatriculare){
		if(nrRemorci < NR_MAX_REMORCI){
		    remorci[nrRemorci++] = new Remorca(nrCutii, nrInmatriculare);
		    return true;
		}
		return false;
    }

    public boolean adaugaRemorca(Remorca remorca){
		if(nrRemorci < NR_MAX_REMORCI){
		    remorci[nrRemorci++] = remorca;
		    return true;
		}
		return false;
    }

    public Remorca stergeRemorca(String nrInmatriculare){
		for(int i=0; i < nrRemorci; i++){
		    if(remorci[i].getNrInmatriculare().equals(nrInmatriculare)){
			Remorca tmp = remorci[i];
			for(int j=i+1; j < nrRemorci; j++){
			    remorci[j-1] = remorci[j];
			}
			nrRemorci--;
			return tmp;
		    }
		}
		return null;
    }

    @Override
    public boolean equals(Object tirObj){
		if(tirObj instanceof Tir){
		    return false;
		}
		
		Tir tir = (Tir)tirObj;
		
		int s1 = 0, s2 = 0;
		for(int i=0; i<nrRemorci; i++){
		    s1 += remorci[i].getNrCutii();
		}
		Remorca[] remorciTir2 = tir.getRemorci();
		for(int i=0; i<tir.getNrRemorci(); i++){
		    s2 += remorciTir2[i].getNrCutii();
		}
	
		return s1 == s2;
    }

    @Override
    public String toString(){
		String result = "T -> ";
		for(int i=0; i<nrRemorci; i++){
		    result += "R(" + remorci[i].getNrInmatriculare() +
			", " + remorci[i].getNrCutii() + ") ";
		    if(i != nrRemorci-1){
				result += "-> ";
		    }
		}
		return result;
    }
};

```

- ``Lab4/Main.java``
```java
package Lab4;
public class Main{
    public static void main(String[] args){
		Tir t1 = new Tir();
		t1.adaugaRemorca(12, "DJ04AAI");
		t1.adaugaRemorca(12, "DJ05AAI");
	
		Tir t2 = new Tir();
		Remorca r = new Remorca(15, "TM05ABA");
		t1.adaugaRemorca(r);
		t2.adaugaRemorca(r);
		
		System.out.println(t1);
		t1.stergeRemorca("DJ05AAI");
		System.out.println(t1);
		
		System.out.println(t2);
    }
}

```

- To run, use the following commands when inside the ``Lab4`` folder:
	- ``cd ..``
	- ``javac Lab4/Remorca.java Lab4/Tir.java Lab4/Main.java``
	- ``java Lab4/Main``
>>>>>>> poo-master
