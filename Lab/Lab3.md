<<<<<<< HEAD
1. 
![](Images/Lab3Ex1.png)
- ``msd.v``
```verilog
module msd (
  input [4:0] i,
  output reg [3:0] o
);
  always @(*) begin
    o = i/10;
  end
endmodule


module msd_tb;
	reg [4:0] i;
	wire [3:0] o;
	
	msd msd_i (.i(i), .o(o));
	
	integer k;
	initial begin
	$display("Time\ti\t\to");
	$monitor("%0t\t%b(%2d)\t%b(%0d)", $time, i, i, o, o);
	i = 0;
	for (k = 1; k < 32; k = k + 1)
	  #10 i = k;
	end
endmodule
```


- ``run_msd.txt`` (run with ``do run_msd.txt`` inside ``modelsim`` console)
```tcl
# add all Verilog source files, separated by spaces
set sourcefiles {msd.v}

# set name of the top module
set topmodule msd_tb

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

2. 
![](Images/Lab3Ex2.png)
- ``div3.v``
```verilog
module div3 (
  input [3:0] i,
  output reg [2:0] o
);

	always @(*) begin
	o = (i == 0) ? 0 :
			 (i == 1) ? 0 :
			 (i == 2) ? 0 :
			 (i == 3) ? 1 :
			 (i == 4) ? 1 :
			 (i == 5) ? 1 :
			 (i == 6) ? 2 :
			 (i == 7) ? 2 :
			 (i == 8) ? 2 :
			 (i == 9) ? 3 :
			 (i == 10) ? 3 :
			 (i == 11) ? 3 :
			 (i == 12) ? 4 :
			 (i == 13) ? 4 :
			 (i == 14) ? 4 :
						 5;
	end
endmodule

  
module div3_tb;
	reg [3:0] i;
	wire [2:0] o;
	
	div3 div3_i (.i(i), .o(o));
	
	integer k;
	initial begin
	$display("Time\ti\t\to");
	$monitor("%0t\t%b(%2d)\t%b(%0d)", $time, i, i, o, o);
	i = 0;
	for (k = 1; k < 16; k = k + 1)
	  #10 i = k;
	end
endmodule
```

- ``run_div3.txt``
```tcl
# add all Verilog source files, separated by spaces
set sourcefiles {div3.v}

# set name of the top module
set topmodule div3_tb

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

3. 
![](Images/Lab3Ex3.png)
- ``cnt1s.v``
```verilog
module cnt1s (
  input [5:0] i,
  output reg [2:0] o
);
	integer k;
	integer tmp;
	always @(*) begin
	  tmp = i;
	  o=0;
	  for(k=1;k<7;k=k+1) begin
	    if(tmp%2==1)
	      o = o+1;
	    tmp = tmp/2;
	  end
	end
endmodule

module cnt1s_tb;
	reg [5:0] i;
	wire [2:0] o;
	
	cnt1s cnt1s_i (.i(i), .o(o));
	
	integer k;
	initial begin
	$display("Time\ti\t\to");
	$monitor("%0t\t%b(%2d)\t%b(%0d)", $time, i, i, o, o);
	i = 0;
	for (k = 1; k < 64; k = k + 1)
	  #10 i = k;
	end
endmodule
```

4. 
![](Images/Lab3Ex4.png)
- ``seq3b.v``
```verilog
module seq3b (
  input [3:0] i,
  output reg o
);
	always @(*) begin
	  o = (i[3:1] == 3'b111) || (i[3:1] == 3'b000) || (i[2:0] == 3'b111) || (i[2:0] == 3'b000);
	end
endmodule

module seq3b_tb;
	reg [3:0] i;
	wire o;
	
	seq3b seq3b_i (.i(i), .o(o));
	
	integer k;
	initial begin
	$display("Time\ti\t\to");
	$monitor("%0t\t%b(%2d)\t%b", $time, i, i, o);
	i = 0;
	for (k = 1; k < 16; k = k + 1)
	  #10 i = k;
	end
endmodule
```

- ``run_seq3b.v``
```tcl

# add all Verilog source files, separated by spaces
set sourcefiles {seq3b.v}

# set name of the top module
set topmodule seq3b_tb

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

5. 
![](Images/Lab3Ex5.png)

- ``mul5bcd.v``
```verilog
module mul5bcd (
  input [3:0] i,
  output reg [3:0] d, u
);
	always @(*) begin 
		d = (i*5)/10;
		u = (i*5)%10;
	end
endmodule

module mul5bcd_tb;
  reg [3:0] i;
  wire [3:0] d, u;

	mul5bcd mul5bcd_i (.i(i), .d(d), .u(u));
	
	integer k;
	initial begin
	$display("Time\ti\t\td\t\tu");
	$monitor("%0t\t%b(%4d)\t%b(%4d)\t%b(%4d)", $time, i, i, d, d, u, u);
	i = 0;
	for (k = 1; k < 10; k = k + 1)
	  #10 i = k;
	end
endmodule
```

- ``run_5bcd.txt``
```tcl
# add all Verilog source files, separated by spaces
set sourcefiles {mul5bcd.v}

# set name of the top module
set topmodule mul5bcd_tb

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

6. 
![](Images/Lab3Ex6.png)
- ``text2nibble.v``
```verilog
module text2nibble (
  input [7:0] i,
  output reg [3:0] o
);
  always @(*) begin
    o = (i >= 30 && i <= 39) ? i - 30 : 15;
  end
endmodule

module text2nibble_tb;
  reg [7:0] i;
  wire [3:0] o;

  text2nibble text2nibble_i (.i(i), .o(o));

  integer k;
  initial begin
    $display("Time\ti\ti_chr\to");
    $monitor("%0t\t%b\t%c\t%b(%d)", $time, i, i, o, o);
    i = 0;
    for (k = 1; k < 256; k = k + 1)
      #10 i = k;
  end
endmodule
```

- ``run_text2nibble.v``
```tcl

# add all Verilog source files, separated by spaces
set sourcefiles {text2nibble.v}

# set name of the top module
set topmodule text2nibble_tb

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
=======
![](../Images/Ex1Lab3.png)

- ``Lab3/Exercise.java``
```java
public interface Exercise {
    void solveExercise();
}

```

- ``Lab3/Exercise1.java``
```java
class Book{
    private final int noPages;

    public Book(int noPages){
        this.noPages = noPages;
    }

    public boolean isIdentical(Book b){
        return this.noPages == b.noPages;
    }

}
public class Exercise1 implements Exercise
{
    @Override
    public void solveExercise() {
        System.out.println("------Exercise 1------");
        System.out.println(new Book(12).isIdentical(new Book(12)));
        System.out.println("----------------------");
    }
}

```

- ``Lab3/Exercise2.java``
```java
class Square{
    private final double side;
    public Square(){
        this.side = 10;
    }

    public Square(double side){
        this.side = side;
    }

    public void printArea(){
        System.out.println("Square with side " + side + " has area "+ side * side);
    }

}
public class Exercise2 implements Exercise{
    @Override
    public void solveExercise() {
        System.out.println("------Exercise 2------");
        new Square().printArea();
        new Square(12).printArea();
        System.out.println("----------------------");
    }
}

```

- ``Lab3/Exercise3.java``
```java
class Pyramid{
    private final int n;
    public Pyramid(int n){
        this.n = n;
    }

    public void displayPyramid(){
        for(int i=1;i<=n;i++){
            for(int j=1;j<=n-i+1;j++){
                System.out.print(i);
            }
            System.out.println();
        }
    }
}
public class Exercise3 implements Exercise{
    @Override
    public void solveExercise() {
        System.out.println("------Exercise 3------");
        new Pyramid(4).displayPyramid();
        System.out.println("----------------------");
    }
}

```

- ``Lab3/Exercise4.java``
```java
class Sum{
    public static int sumOfNumbers(int... numbers){
        int sum = 0;
        for(int number : numbers){
            sum += number;
        }
        return sum;
    }
}
public class Exercise4 implements Exercise{
    @Override
    public void solveExercise() {
        System.out.println("------Exercise 4-----");
        System.out.println(Sum.sumOfNumbers(1,2,3,4,5,6,7,8,9,10));
        System.out.println("----------------------");
    }
}

```


![](../Images/Ex2Lab3.png)

- ``Lab3/ExerciseFisier.java``
```java
class Fisier {
    private static int nextId = 1;
    private int id;
    private String nume;
    private String continut;
    private Fisier versiuneAnterioara;
    private int numarConcatenari;

    public Fisier getVersiuneAnterioara(){
        return versiuneAnterioara;
    }

    public Fisier(String nume, String continut) {
        this.id = nextId++;
        this.nume = nume;
        this.continut = continut;
        this.versiuneAnterioara = null;
        this.numarConcatenari = 0;
    }

    public void salveazaVersiune() {
        Fisier versiuneNoua = new Fisier(this.nume + "bak", this.continut);
        versiuneNoua.versiuneAnterioara = this.versiuneAnterioara;
        this.versiuneAnterioara = versiuneNoua;
    }

    public void concateneaza(Fisier altFisier) {
        salveazaVersiune();

        this.continut += altFisier.continut;
        this.numarConcatenari++;
    }

    @Override
    public String toString() {
        StringBuilder sb = new StringBuilder();
        sb.append(id).append(" ").append(nume).append(" [").append(continut).append("]");

        if (versiuneAnterioara != null) {
            sb.append(" <").append(versiuneAnterioara).append(">");
        }

        return sb.toString();
    }

    public int numarConcatenari() {
        return numarConcatenari;
    }
}

public class ExerciseFisier implements Exercise{
    @Override
    public void solveExercise() {
        Fisier fisier1 = new Fisier("document1", "Acesta este primul document.");
        System.out.println("Fișier inițial: " + fisier1);

        Fisier fisier2 = new Fisier("document2", " Acesta este un alt document.");
        System.out.println("Fișier secundar: " + fisier2);

        fisier1.concateneaza(fisier2);
        System.out.println("După concatenare: " + fisier1);

        System.out.println("Număr concatenări fisier1: " + fisier1.numarConcatenari());

        fisier1.salveazaVersiune();
        System.out.println("După salvarea unei noi versiuni: " + fisier1);

        fisier1.concateneaza(fisier2);
        System.out.println("După a doua concatenare: " + fisier1);

        System.out.println("Număr concatenări fisier1: " + fisier1.numarConcatenari());

        System.out.println();
        fisier2.salveazaVersiune();
        fisier2.salveazaVersiune();
        fisier2.salveazaVersiune();
        fisier2.salveazaVersiune();
        var fisier = fisier2;
        while(fisier != null){
            System.out.println(fisier);
            fisier = fisier.getVersiuneAnterioara();
        }
    }
}

```


- ``Main.java``
```java
import java.util.ArrayList;
import java.util.List;

public class Main {
    public static void main(String[] args) {

        var exercises = new ArrayList<Exercise>() {{
            add(new Exercise1());
            add(new Exercise2());
            add(new Exercise3());
            add(new Exercise4());
            add(new ExerciseFisier());
        }};

        for (var exercise : exercises) {
            exercise.solveExercise();
        }

    }
}
>>>>>>> poo-master
```
