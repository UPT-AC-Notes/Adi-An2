### Java Exceptions Overview 
```java
class Ex1 extends Exception {}
class Ex2 extends Ex1 {}
class Ex3 extends Exception {}
class Ex4 extends RuntimeException {}
public class test{
    public void method() throws Ex1{
        // ERROR (we can only throw subclasses of Ex1) -> throw new Ex3();
        // ERROR (we can only throw subclasses of Ex1) -> throw new Exception();

        // OK -> throw new Ex1();
        // OK -> throw new Ex2();
        // Ok (because Ex4 is an unchecked exception) -> throw new Ex4();
            // checked exceptions must pe specified in the 'throws' clause while unchecked exceptions (RuntimeException and its sublcasses) can be thrown anywhere
        
    }
    public void method2(Integer option) throws Ex3, Ex1{ // everything works here
        if(option == 1){
            throw new Ex3(); 
        }else if(option==2){
            throw new Ex1();
        }
        throw new Ex4(); // ex4 is an unchecked exception (because it is a subclass of RuntimeException) and can be thrown without adding it tot the 'throws' clause
    }
    public static void method3(Boolean option){ // everything works here
        try{
            if(option){
                throw new Ex3(); // we're able to throw Ex3, which is not a subclass of Ex1, because we're in a try...catch block which is more flexible
                // this means that in a try...catch block we can throw any exception as long as we're catching it 
            }else{
                throw new Ex1();
            }
        }catch(Ex3 ex){
            System.out.println("method3: exception 3 thrown");
        }catch(Ex1 ex){
            System.out.println("method3: exception 1 thrown");
        }catch(Ex4 ex){ // we can catch unchecked exceptions even though they were not thrown
        }
        // if we catch an exception that was not thrown, the code won't compile
        /*catch(Ex2 ex){

        }*/
    }

    public static void main(String[] args){
        System.out.println("Hello World!");
        method3(false);
    }
}
```

```java
class E1 extends Exception {
}

class E2 extends E1 {
}

public class Main {
    public static void m(int x) throws E1 {
        if (x == 1) throw new E2();
    }

    public static void main(String[] args) {
        int k = 0, a = 1;
        while (k < 2) {
            try {
                k++;
                m(k);
                a++;
            } catch (E2 e) {
                a += 2; // it will enter here because at runtime the exception is treated as E2 even though m throws E1
            } catch (E1 e) {
                a += 3;
            } finally {
                a++;
            }
        }
        System.out.println(a);
    }
    // if we switch the catches around, we'll get a compile error saying 'exception E2 has already been caught'
}
```

### Exercitii 2023
- Ce valoare întreagă va fi afișată la linia  "//*" în urma execuției programului?
```java
class A {
    private static int x;
    private int y;

    public A(int x1, int y1) {
        x = x1;
        y = y1;
    }

    public void setxy(int x1, int y1) {
        x = x1;
        y = y1;
    }

    public int getx() {
        return x;
    }

    public int gety() {
        return y;
    }
}

class Main {
    public static void m(A z, A t) {
        z.setxy(3, 20);
        z = new A(2, 17);
    }

    public static void main(String[] args) {
        A a = new A(9, 50);
        A b = new A(7, 28);
        m(a, b);
        System.out.println(a.gety() + b.getx()); //*
    }
}
```

1. ``A a = new A(9,50)`` => $x = 9, y_a = 50;$
2. ``A b = new A(7,28)`` => $x = 7, y_b = 28;$
3. ``z.setxy(3,20) <=> a.setxy(3,20)`` => $x = 3, y_a = 20;$
4. ``z = new A(2,17)`` => $x = 2$ ($y_a$ nu isi schimba valoarea pentru ca spatiul de memorie referintat de variabila ``a`` nu este schimbat, doar referinta ``z`` nu mai pointeaza catre ``a``, ci catre un nou obiect care se va distruge dupa sfarsitul metodei ``m`` de catre garbage collector)
5. ``a.gety`` = 20; ``b.getx`` = 2
- Raspuns final: ``22``


---

- Ce valoare întreagă va fi afișată la linia  "//*" în urma execuției programului?

```java
class Ex extends RuntimeException {}

class Main {
    public static void m(int x) throws Ex {
        if (x == 2) throw new Ex();
    }

    public static void main(String[] args) {
        int a = 2;
        try {
            for (int i = 0; i < 4; i++) {
                m(i);
                a = a + 2;
            }
        } catch (Ex e) {
            a++;
        } finally {
            a++;
        }
        System.out.println(a); // *
    }
}
```

- Raspuns final: ``8``

---

- Considerând următorul cod Java, care din fragmentele de mai jos vor genera o eroare când sunt inserate la "/* AICI */"

```java
abstract class A {
    public void m(int p) {}

    public void r(int p) {}
}

class B extends A {
    public void m(int p) {}

    public void p(int p) {}

    public void q(int q) {}
}

class C extends A {
    public void m(int p) {}

    public void p(int p) {}

    public void r(int p, int t) {}
}

class Main {
    public static void main(String[] args) {
        A a = new B();
        C c = new C();
        /* AICI */
    }
}
```
- ``a)`` c.equals(a);
- ``b)`` c.r(1);
- ``c)`` a.q(1);
- ``d)`` a.p(1);
- ``e)`` a.m(1);
- Raspuns final: ``c, d``
---

- Considerând următorul cod Java, care din fragmentele de mai jos vor genera o eroare când sunt inserate la "/* AICI */"

```java
class A {
    private int a = 0;

    private static int b = 0;

    public int m(){
        return a;
    }

    public static int n(A x){
        /* AICI */
    }
}
```

- ``a)`` return m();
- ``b)`` return b;
- ``c)`` return x.a;
- ``d)`` return this.a;
- ``e)`` return a;
- Raspuns final: ``a, d, e``
---

- Ce valoare întreagă va fi afișată la linia  "//*" în urma execuției programului?

```java
class A {
    public int m(A p) {return 12;}
    public int n(A p) {return 38;}
}

class B extends A {
    public int m(B p) {return 3;}
    public int n(A p) {return 7;}
}

class C extends A {
    public int m(A p) {return 38;}
    public int n(A p) {return 4;}
}

class D extends A {
    public int m(A p) {return 1;}
    public int n(D p) {return 2;}
}

class Main {
    public static void main(String[] args){
        A x = new C();
        A y = new D();
        D z = new D();
        System.out.println(x.m(z) + y.n(z)); //*
    }
}
```
- Raspuns final: ``38 + 38 = 76``

---

- Considerând următorul cod Java, care din fragmentele de mai jos vor genera o eroare când sunt inserate la "/* AICI */"

```java
abstract class A {}

class B extends A {}

class C extends A {}

class D extends C {}

class Main{
    public static void main(String[] args){
        B b = new B();
        C c = new C();
        D d = new D();
        /* AICI */
    }
}
```

- ``a)`` c = b;
- ``b)`` A a = new A();
- ``c)`` c = d;
- ``d)`` A a = d;
- ``e)`` d = c;
- Raspuns final: ``a, b, e``

---

